---
ContentId: 4e7a2c91-b8d3-4f6e-a1c5-9d0e3f7b2a84
DateApproved: 03/09/2026
MetaDescription: OpenTelemetryトレース、メトリクス、イベントを使用してVS CodeでGitHub Copilotエージェントインタラクションを監視する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- monitoring
- telemetry
- OpenTelemetry
- OTel
- traces
- metrics
- agents
---

# OpenTelemetryを使用したエージェント使用状況の監視

この記事では、VS CodeでCopilot Chatエージェントインタラクション用のOpenTelemetry監視を有効にして構成する方法について説明しています。

CopilotChatは、[OpenTelemetry](https://opentelemetry.io/)(OTel)経由でトレース、メトリクス、イベントをエクスポートでき、エージェントインタラクション、LLM呼び出し、ツール実行、トークン使用量を可視化できます。すべてのシグナル名と属性は[OTelGenAIセマンティック規約](https://github.com/open-telemetry/semantic-conventions/blob/main/docs/gen-ai/)に従っているため、データはOTel互換のバックエンドで動作します。

## 収集される内容

CopilotChatは3つのタイプのOTelシグナル(トレース、メトリクス、イベント)を出力します。

### トレース

各エージェントインタラクションは、完全な実行フローをキャプチャする階層的なスパンツリーを生成します。

```text
invoke_agent copilot                           [~15s]
  ├── chat gpt-4o                              [~3s]  (LLM requests tool calls)
  ├── execute_tool readFile                    [~50ms]
  ├── execute_tool runCommand                  [~2s]
  ├── chat gpt-4o                              [~4s]  (LLM generates final response)
  └── (span ends)
```

トレースを構成する3つのスパンタイプがあります。

| スパン | 説明 | 主な属性 |
|---|---|---|
| `invoke_agent` | LLM呼び出しとツール実行を含むエージェント全体のオーケストレーションをラップします | エージェント名、会話ID、ターンカウント、総トークン使用量 |
| `chat` | 単一のLLM APIコール | モデル、トークンカウント、応答時間、終了理由 |
| `execute_tool` | 単一のツール呼び出し | ツール名、ツールタイプ、期間、成功ステータス |

エージェントがサブエージェント(例えば`runSubagent`ツール経由)を呼び出すと、トレースコンテキストが自動的に伝播されます。サブエージェントの`invoke_agent`スパンは親エージェントの`execute_tool`スパンの子として表示され、非同期の境界を越えた接続されたトレースツリーが生成されます。

### メトリクス

| メトリクス | タイプ | 説明 |
|---|---|---|
| `gen_ai.client.operation.duration` | ヒストグラム | LLM APIコール期間(秒) |
| `gen_ai.client.token.usage` | ヒストグラム | トークンカウント(入力と出力) |
| `copilot_chat.tool.call.count` | カウンター | 名前と成功別のツール呼び出し数 |
| `copilot_chat.tool.call.duration` | ヒストグラム | ツール実行レイテンシ(ミリ秒) |
| `copilot_chat.agent.invocation.duration` | ヒストグラム | エージェント全体の期間(秒) |
| `copilot_chat.agent.turn.count` | ヒストグラム | エージェント呼び出しあたりのLLM往復 |
| `copilot_chat.session.count` | カウンター | 開始されたチャットセッション |
| `copilot_chat.time_to_first_token` | ヒストグラム | 最初のSSEトークンまでの時間(秒) |

メトリクスには`gen_ai.request.model`、`gen_ai.provider.name`、`gen_ai.tool.name`、`error.type`などのフィルター用の属性が含まれています。

### イベント

| イベント | 説明 |
|---|---|
| `gen_ai.client.inference.operation.details` | モデル、トークン、終了理由を含むLLM呼び出しの完全なメタデータ |
| `copilot_chat.session.start` | 新しいチャットセッションが開始されるときに出力 |
| `copilot_chat.tool.call` | タイミングとエラー詳細を含むツール呼び出しごと |
| `copilot_chat.agent.turn` | トークンカウントを含むターンごとのLLM往復 |

### リソース属性

すべてのシグナルは以下のリソース属性を含みます。

| 属性 | 値 |
|---|---|
| `service.name` | `copilot-chat`(`OTEL_SERVICE_NAME`で構成可能) |
| `service.version` | 拡張機能バージョン |
| `session.id` | VSCodeウィンドウあたり一意 |

`OTEL_RESOURCE_ATTRIBUTES`を使用してカスタムリソース属性を追加し、チーム、部門、または他の組織的な境界でフィルタリングします。

```bash
export OTEL_RESOURCE_ATTRIBUTES="team.id=platform,department=engineering"
```

### コンテンツキャプチャ

デフォルトでは、プロンプトコンテンツ、応答、またはツール引数は取得されません。モデル名、トークンカウント、期間などのメタデータのみが含まれます。

完全なコンテンツをキャプチャするには、`setting(github.copilot.chat.otel.captureContent)`設定を有効にするか、`COPILOT_OTEL_CAPTURE_CONTENT=true`を設定してください。これにより、スパン属性が完全なプロンプトメッセージ、応答メッセージ、システムプロンプト、ツールスキーマ、ツール引数、ツール結果で入力されます。

> [!CAUTION]
> コンテンツキャプチャには、コード、ファイルコンテンツ、ユーザープロンプトなどの機密情報が含まれる可能性があります。信頼できる環境でのみこれを有効にしてください。

## OTel監視を有効にする

以下のいずれかの条件が真の場合、OTelがアクティブになります。

* `setting(github.copilot.chat.otel.enabled)`が`true`
* `COPILOT_OTEL_ENABLED=true`
* `OTEL_EXPORTER_OTLP_ENDPOINT`が設定されている

### VS Code設定

**設定**(`kb(workbench.action.openSettings)`)を開き、`copilot otel`を検索します。

| 設定 | タイプ | デフォルト | 説明 |
|---|---|---|---|
| `setting(github.copilot.chat.otel.enabled)` | ブール値 | `false` | OTelエミッションを有効にする |
| `setting(github.copilot.chat.otel.exporterType)` | 文字列 | `"otlp-http"` | `otlp-http`、`otlp-grpc`、`console`、または`file` |
| `setting(github.copilot.chat.otel.otlpEndpoint)` | 文字列 | `"http://localhost:4318"` | OTLPコレクターエンドポイント |
| `setting(github.copilot.chat.otel.captureContent)` | ブール値 | `false` | 完全なプロンプトと応答コンテンツをキャプチャ |
| `setting(github.copilot.chat.otel.outfile)` | 文字列 | `""` | JSONLines出力のファイルパス |

### 環境変数

環境変数は常にVSCode設定よりも優先されます。

| 変数 | デフォルト | 説明 |
|---|---|---|
| `COPILOT_OTEL_ENABLED` | `false` | OTelを有効にします。`OTEL_EXPORTER_OTLP_ENDPOINT`が設定されている場合も有効になります。 |
| `COPILOT_OTEL_ENDPOINT` | | OTLPエンドポイントURL(`OTEL_EXPORTER_OTLP_ENDPOINT`よりも優先) |
| `OTEL_EXPORTER_OTLP_ENDPOINT` | | 標準OTelOTLPエンドポイントURL |
| `OTEL_EXPORTER_OTLP_PROTOCOL` | `http/protobuf` | OTLPプロトコル。`grpc`のみが動作を変更します。 |
| `OTEL_SERVICE_NAME` | `copilot-chat` | リソース属性のサービス名 |
| `OTEL_RESOURCE_ATTRIBUTES` | | 追加リソース属性(`key1=val1,key2=val2`) |
| `COPILOT_OTEL_CAPTURE_CONTENT` | `false` | 完全なプロンプトと応答コンテンツをキャプチャ |
| `OTEL_EXPORTER_OTLP_HEADERS` | | 認証ヘッダー(例えば`Authorization=Bearer token`) |

## 可観測性バックエンドで使用する

CopilotChatのOTel出力は、OTLPプロトコルをサポートするバックエンドで動作します。`setting(github.copilot.chat.otel.otlpEndpoint)`設定または`OTEL_EXPORTER_OTLP_ENDPOINT`環境変数をバックエンドのOTLPインジェスチョンURLに向け、エクスポーターの種類をバックエンドのプロトコル(`otlp-http`または`otlp-grpc`)と一致するように構成します。

### AspireDashboard

[AspireDashboard](https://aspire.dev/dashboard/standalone/)はローカル開発に最もシンプルなオプションです。組み込みのOTLPエンドポイントとトレースビューアを備えた単一のDockerコンテナで、クラウドアカウントは必要ありません。

```bash
docker run --rm -d \
  -p 18888:18888 \
  -p 4317:18889 \
  --name aspire-dashboard \
  mcr.microsoft.com/dotnet/aspire-dashboard:latest
```

```json
{
  "github.copilot.chat.otel.enabled": true,
  "github.copilot.chat.otel.exporterType": "otlp-grpc",
  "github.copilot.chat.otel.otlpEndpoint": "http://localhost:4317"
}
```

`http://localhost:18888`を開き、**トレース**に移動してエージェントインタラクションスパンを表示します。

### Jaeger

[Jaeger](https://www.jaegertracing.io/)はOTLPを直接受け入れるオープンソースの分散トレーシングプラットフォームです。

```bash
docker run -d --name jaeger -p 16686:16686 -p 4318:4318 jaegertracing/jaeger:latest
```

```json
{
  "github.copilot.chat.otel.enabled": true,
  "github.copilot.chat.otel.otlpEndpoint": "http://localhost:4318"
}
```

`http://localhost:16686`を開き、サービス`copilot-chat`を選択し、**トレースを検索**を選択します。

### AzureApplicationInsights

[OTelCollector](https://opentelemetry.io/docs/collector/)と[AzureMonitorエクスポーター](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/exporter/azuremonitorexporter)を使用して、CopilotChatテレメトリをApplicationInsightsに転送します。VSCode`setting(github.copilot.chat.otel.otlpEndpoint)`設定をコレクターのOTLPエンドポイントに向け、コレクターをApplicationInsights接続文字列にエクスポートするように構成します。

### Langfuse

[Langfuse](https://langfuse.com/)はネイティブOTLPインジェスチョンとOTelGenAIセマンティック規約のサポートを備えたオープンソースのLLM可観測性プラットフォームです。

```json
{
  "github.copilot.chat.otel.enabled": true,
  "github.copilot.chat.otel.otlpEndpoint": "http://localhost:3000/api/public/otel",
  "github.copilot.chat.otel.captureContent": true
}
```

`OTEL_EXPORTER_OTLP_HEADERS`環境変数で認証ヘッダーを設定します。詳細は[LangfuseOTelドキュメント](https://langfuse.com/docs/opentelemetry/introduction)を参照してください。

### その他のバックエンド

[GrafanaTempo](https://grafana.com/oss/tempo/)、[Honeycomb](https://www.honeycomb.io/)、[Datadog](https://www.datadoghq.com/)など、OTLP互換のバックエンドが動作します。各バックエンドのOTLPインジェスチョン設定のドキュメントを参照してください。

## セキュリティとプライバシー

OTel監視はデフォルトでオフになっており、明示的に有効にするまでデータは出力されません。収集内容と保存先を制御できます。

| 側面 | 詳細 |
|---|---|
| **デフォルトでオフ** | 明示的に有効にしない限り、OTelデータは出力されません。無効になっている場合、OTelSDKは読み込まれず、ランタイムオーバーヘッドはゼロになります。 |
| **デフォルトでコンテンツなし** | プロンプト、応答、ツール引数には`captureContent`でのオプトインが必要です。 |
| **デフォルト属性にPIIなし** | セッションID、モデル名、トークンカウントは個人を特定できる情報ではありません。 |
| **ユーザー構成エンドポイント** | データは指定した場所にのみ移動します。フォンホーム動作はありません。 |

## 関連コンテンツ

- [Copilot設定リファレンス](/docs/copilot/reference/copilot-settings.md)
- [VS CodeでのAIのトラブルシューティング](/docs/copilot/troubleshooting.md)
- [OTelGenAIセマンティック規約](https://github.com/open-telemetry/semantic-conventions/blob/main/docs/gen-ai/)
- [AspireDashboardスタンドアロンドキュメント](https://aspire.dev/dashboard/standalone/)

