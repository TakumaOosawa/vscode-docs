---
ContentId: 4e7a2c91-b8d3-4f6e-a1c5-9d0e3f7b2a84
DateApproved: 03/09/2026
MetaDescription: VS CodeのOpenTelemetryトレース、メトリクス、イベントを使用してGitHub Copilotエージェントの相互作用を監視する方法を学びます。
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

# OpenTelemetryでエージェント使用状況を監視する

このアーティクルでは、VS CodeのCopilot Chatエージェント相互作用に対してOpenTelemetry監視を有効化および構成する方法について説明します。

Copilot Chatは、[OpenTelemetry](https://opentelemetry.io/)（OTel）を経由してトレース、メトリクス、イベントをエクスポートでき、エージェント相互作用、LLM呼び出し、ツール実行、トークン使用량に対する可視性を提供します。すべてのシグナル名と属性は[OTel GenAI Semantic Conventions](https://github.com/open-telemetry/semantic-conventions/blob/main/docs/gen-ai/)に従うため、データはあらゆるOTel互換バックエンドで機能します。

## 収集対象

Copilot Chatは3つのタイプのOTelシグナル（トレース、メトリクス、イベント）をエミットします。

### トレース

各エージェント相互作用は、完全な実行フローをキャプチャする階層スパンツリーを生成します。

```text
invoke_agent copilot                           [~15s]
  ├── chat gpt-4o                              [~3s]  (LLM requests tool calls)
  ├── execute_tool readFile                    [~50ms]
  ├── execute_tool runCommand                  [~2s]
  ├── chat gpt-4o                              [~4s]  (LLM generates final response)
  └── (span ends)
```

トレースを構成する3つのスパンタイプがあります。

| スパン | 説明 | キー属性 |
|---|---|---|
| `invoke_agent` | エージェントオーケストレーション全体（すべてのLLM呼び出しとツール実行を含む）をラップします | エージェント名、会話ID、ターン数、合計トークン使用量 |
| `chat` | 単一のLLM API呼び出し | モデル、トークン数、応答時間、終了理由 |
| `execute_tool` | 単一のツール呼び出し | ツール名、ツールタイプ、期間、成功ステータス |

エージェントがサブエージェントを呼び出す場合（たとえば、`runSubagent`ツール経由）、トレースコンテキストは自動的に伝播されます。サブエージェントの`invoke_agent`スパンは親エージェントの`execute_tool`スパンの子として表示され、非同期境界全体に接続されたトレースツリーが生成されます。

### メトリクス

| メトリクス | タイプ | 説明 |
|---|---|---|
| `gen_ai.client.operation.duration` | ヒストグラム | LLM API呼び出し期間（秒） |
| `gen_ai.client.token.usage` | ヒストグラム | トークン数（入力と出力） |
| `copilot_chat.tool.call.count` | カウンター | 名前と成功別のツール呼び出し |
| `copilot_chat.tool.call.duration` | ヒストグラム | ツール実行レイテンシ（ミリ秒） |
| `copilot_chat.agent.invocation.duration` | ヒストグラム | エージェントエンドツーエンド期間（秒） |
| `copilot_chat.agent.turn.count` | ヒストグラム | エージェント呼び出しごとのLLMラウンドトリップ |
| `copilot_chat.session.count` | カウンター | 開始したチャットセッション |
| `copilot_chat.time_to_first_token` | ヒストグラム | 最初のSSEトークンまでの時間（秒） |

メトリクスには、`gen_ai.request.model`、`gen_ai.provider.name`、`gen_ai.tool.name`、`error.type`など、フィルタリング用の属性が含まれます。

### イベント

| イベント | 説明 |
|---|---|
| `gen_ai.client.inference.operation.details` | モデル、トークン、終了理由を含む完全なLLM呼び出しメタデータ |
| `copilot_chat.session.start` | 新しいチャットセッションが開始されるときにエミットされます |
| `copilot_chat.tool.call` | タイミングとエラー詳細を含むツール呼び出しごと |
| `copilot_chat.agent.turn` | トークン数を含むターンごとのLLMラウンドトリップ |

### リソース属性

すべてのシグナルは以下のリソース属性を持ちます。

| 属性 | 値 |
|---|---|
| `service.name` | `copilot-chat`（`OTEL_SERVICE_NAME`で設定可能） |
| `service.version` | 拡張機能バージョン |
| `session.id` | VS Codeウィンドウごとに一意 |

カスタムリソース属性を`OTEL_RESOURCE_ATTRIBUTES`で追加して、チーム、部門、その他の組織的な境界でフィルタリングします。

```bash
export OTEL_RESOURCE_ATTRIBUTES="team.id=platform,department=engineering"
```

### コンテンツキャプチャ

デフォルトでは、プロンプトコンテンツ、応答、またはツール引数はキャプチャされません。モデル名、トークン数、期間などのメタデータのみが含まれます。

完全なコンテンツをキャプチャするには、`setting(github.copilot.chat.otel.captureContent)`設定を有効にするか、`COPILOT_OTEL_CAPTURE_CONTENT=true`を設定してください。これにより、スパン属性に完全なプロンプトメッセージ、応答メッセージ、システムプロンプト、ツールスキーマ、ツール引数、ツール結果が設定されます。

> [!CAUTION]
> コンテンツキャプチャには、コード、ファイルコンテンツ、ユーザープロンプトなど、機密情報が含まれる可能性があります。信頼できる環境でのみ有効にしてください。

## OTel監視を有効化する

次のいずれかの条件が当てはまる場合、OTelがアクティベートされます。

* `setting(github.copilot.chat.otel.enabled)`が`true`である
* `COPILOT_OTEL_ENABLED=true`である
* `OTEL_EXPORTER_OTLP_ENDPOINT`が設定されている

### VS Code設定

**設定**（`kb(workbench.action.openSettings)`）を開き、`copilot otel`を検索します。

| 設定 | タイプ | デフォルト | 説明 |
|---|---|---|---|
| `setting(github.copilot.chat.otel.enabled)` | ブール値 | `false` | OTelエミッションを有効化 |
| `setting(github.copilot.chat.otel.exporterType)` | 文字列 | `"otlp-http"` | `otlp-http`、`otlp-grpc`、`console`、または`file` |
| `setting(github.copilot.chat.otel.otlpEndpoint)` | 文字列 | `"http://localhost:4318"` | OTLPコレクターエンドポイント |
| `setting(github.copilot.chat.otel.captureContent)` | ブール値 | `false` | 完全なプロンプトと応答コンテンツをキャプチャ |
| `setting(github.copilot.chat.otel.outfile)` | 文字列 | `""` | JSON行出力用ファイルパス |

### 環境変数

環境変数は常にVS Code設定よりも優先されます。

| 変数 | デフォルト | 説明 |
|---|---|---|
| `COPILOT_OTEL_ENABLED` | `false` | OTelを有効化。`OTEL_EXPORTER_OTLP_ENDPOINT`が設定されている場合も有効化されます。 |
| `COPILOT_OTEL_ENDPOINT` | | OTLPエンドポイントURL（`OTEL_EXPORTER_OTLP_ENDPOINT`より優先） |
| `OTEL_EXPORTER_OTLP_ENDPOINT` | | 標準OTel OTLPエンドポイントURL |
| `OTEL_EXPORTER_OTLP_PROTOCOL` | `http/protobuf` | OTLPプロトコル。`grpc`のみ動作を変更します。 |
| `OTEL_SERVICE_NAME` | `copilot-chat` | リソース属性のサービス名 |
| `OTEL_RESOURCE_ATTRIBUTES` | | 追加のリソース属性（`key1=val1,key2=val2`） |
| `COPILOT_OTEL_CAPTURE_CONTENT` | `false` | 完全なプロンプトと応答コンテンツをキャプチャ |
| `OTEL_EXPORTER_OTLP_HEADERS` | | 認証ヘッダー（たとえば、`Authorization=Bearer token`） |

## 可視化バックエンドで使用する

Copilot ChatのOTel出力は、OTLPプロトコルをサポートするあらゆるバックエンドで機能します。`setting(github.copilot.chat.otel.otlpEndpoint)`設定または`OTEL_EXPORTER_OTLP_ENDPOINT`環境変数をバックエンドのOTLPインジェストURLにポイントし、エクスポーターの種類をバックエンドのプロトコル（`otlp-http`または`otlp-grpc`）に合わせて設定します。

### Aspire Dashboard

[Aspire Dashboard](https://aspire.dev/dashboard/standalone/)はローカル開発に最適なオプションです。これは単一のDockerコンテナで、組み込みのOTLPエンドポイントとトレース表示機能を備えており、クラウドアカウントは不要です。

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

`http://localhost:18888`を開き、**トレース**に移動してエージェント相互作用スパンを表示します。

### Jaeger

[Jaeger](https://www.jaegertracing.io/)はOTLPを直接受け入れるオープンソース分散トレースプラットフォームです。

```bash
docker run -d --name jaeger -p 16686:16686 -p 4318:4318 jaegertracing/jaeger:latest
```

```json
{
  "github.copilot.chat.otel.enabled": true,
  "github.copilot.chat.otel.otlpEndpoint": "http://localhost:4318"
}
```

`http://localhost:16686`を開き、サービス`copilot-chat`を選択して、**トレースを検索**を選択します。

### Azure Application Insights

[OTel Collector](https://opentelemetry.io/docs/collector/)と[Azure Monitor エクスポーター](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/exporter/azuremonitorexporter)を使用して、Copilot ChatテレメトリーをApplication Insightsに転送します。VS Codeの`setting(github.copilot.chat.otel.otlpEndpoint)`設定をコレクターのOTLPエンドポイントにポイントし、コレクターをApplication Insights接続文字列にエクスポートするように設定します。

### Langfuse

[Langfuse](https://langfuse.com/)はネイティブOTLPインジェストとOTel GenAI Semantic Conventionsサポートを備えたオープンソースLLM可視化プラットフォームです。

```json
{
  "github.copilot.chat.otel.enabled": true,
  "github.copilot.chat.otel.otlpEndpoint": "http://localhost:3000/api/public/otel",
  "github.copilot.chat.otel.captureContent": true
}
```

`OTEL_EXPORTER_OTLP_HEADERS`環境変数で認証ヘッダーを設定してください。詳細は[Langfuse OTelドキュメント](https://langfuse.com/docs/opentelemetry/introduction)を参照してください。

### その他のバックエンド

[Grafana Tempo](https://grafana.com/oss/tempo/)、[Honeycomb](https://www.honeycomb.io/)、[Datadog](https://www.datadoghq.com/)など、あらゆるOTLp互換バックエンドが機能します。各バックエンドのドキュメントを参照して、OTLPインジェストの設定を確認してください。

## セキュリティとプライバシー

OTel監視はデフォルトでオフになっており、明示的に有効化するまでデータはエミットされません。収集対象と送信先を制御できます。

| 側面 | 詳細 |
|---|---|
| **デフォルトでオフ** | 明示的に有効化しない限り、OTelデータはエミットされません。無効化された場合、OTel SDKはロードされず、ランタイムオーバーヘッドはゼロです。 |
| **デフォルトではコンテンツなし** | プロンプト、応答、ツール引数には`captureContent`でのオプトインが必要です。 |
| **デフォルト属性にPIIなし** | セッションID、モデル名、トークン数は個人識別情報ではありません。 |
| **ユーザー設定エンドポイント** | データはポイント先のみに送信されます。フォンホーム動作はありません。 |

## 関連コンテンツ

- [Copilot設定リファレンス](/docs/copilot/reference/copilot-settings.md)
- [VS CodeのAIをトラブルシューティングする](/docs/copilot/troubleshooting.md)
- [OTel GenAI Semantic Conventions](https://github.com/open-telemetry/semantic-conventions/blob/main/docs/gen-ai/)
- [Aspire Dashboard スタンドアロンドキュメント](https://aspire.dev/dashboard/standalone/)

