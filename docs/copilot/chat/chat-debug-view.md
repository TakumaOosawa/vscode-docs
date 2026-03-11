---
ContentId: 2f4a8e9d-3c5b-4f6e-a7d8-1c2b3e4f5a6b
DateApproved: 3/9/2026
MetaDescription: Agent LogsとChat Debug viewを使用して、Visual Studio CodeでAIリクエスト、ツール呼び出し、エージェント相互作用を検査します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# チャット相互作用のデバッグ

Visual Studio Codeは、AIにプロンプトを送信したときに何が起きるかを理解するためのツールを提供します。これらのツールを使用して、エージェントがプロンプトファイルをどのように発見し、ツールを呼び出し、言語モデルリクエストを行い、応答を生成するかを検査します。

VS Codeは、2つの相互補完的なデバッグツールを提供します：

* **Agent Debug panel**（Preview）は、チャットセッション中に発生するすべてのイベントの時系列ログを表示します。ツール呼び出し、LLMリクエスト、プロンプトファイル発見、エラーが含まれます。
* **Chat Debug view**は、各LLMリクエストとレスポンスの詳細を表示します。完全なシステムプロンプト、ユーザープロンプト、コンテキスト、ツール呼び出しペイロードが含まれます。

## Agent Debug panel

> [!NOTE]
> Agent Debug panelは現在プレビュー版です。

Agent Debug panelは、プロンプトを送信したときに何が起きるかを理解するための主要なツールです。チャットセッション中のエージェント相互作用の時系列イベントログを表示し、[カスタムエージェント](/docs/copilot/agents/local-agents.md)とオーケストレートされたサブエージェントワークフローのデバッグに特に役立ちます。

Agent Debug panelを開くには：

* Chat viewのギアアイコンを選択して、**Show Agent Logs**を選択します。

* Command Paletteから**Developer: Open Agent Debug Panel**を実行します。

Agent Debug panelで3つのビューを切り替えられます：

* **Logs**：セッション中のイベントの時系列リスト。特定のイベントタイプに焦点を当てるためのフィルタリングオプションがあります。

* **Agent Flow Chart**：セッション中のエージェントとサブエージェント間の相互作用を視覚化するフローチャート。

* **Summary**：総ツール呼び出し数、トークン使用量、エラー数、全体的な期間など、セッションの集計統計。

> [!NOTE]
> Agent Debug panelは現在、ローカルチャットセッションのみで利用可能です。ログデータは永続化されないため、現在のVS Codeセッションのチャットセッションのログのみを表示できます。

### Logs view

Logs viewは、チャットセッション中に発生したイベントの時系列リストを表示します。各イベントには、タイムスタンプ、イベントタイプ、概要情報が含まれます。各イベントを展開して、LLMリクエストの完全なシステムプロンプトやツール呼び出しの入力と出力など、詳細情報を確認できます。

![Agent Logsのイベントリストのスクリーンショット。](../images/chat-debug-view/agent-logs.png)

フラットリストとサブエージェント別にイベントをグループ化するツリービュー間で切り替えられます。フィルタリングオプションを使用して、特定のイベントまたはイベントタイプに焦点を当てます。

Logs viewは、Agent Debug panelを開いたときのデフォルトビューです。[Summary view](#summary-view)から**View Logs**を選択して、Logs viewに切り替えることもできます。

### Summary view

Summary viewは、総ツール呼び出し数、トークン使用量、エラー数、全体的な期間など、チャットセッションの集計統計を提供します。

![Agent Logsのsummary viewのスクリーンショット。チャットセッションの集計統計を表示しています。](../images/chat-debug-view/agent-logs-summary-v2.png)

Summary viewを開くには：

1. Chat viewのギアアイコンを選択して**Show Agent Logs**を選択し、Agent Debug panelを開きます。

1. パネルの上部にあるブレッドクラムのセッション説明を選択します。

### Agent Flow Chart view

Agent Flow Chart viewは、イベントと相互作用のシーケンスをエージェント間で視覚化し、複雑なオーケストレーションをより簡単に理解できるようにします。

![Agent Logsのフローチャートのスクリーンショット。エージェントとサブエージェント間の相互作用を表示しています。](../images/chat-debug-view/agent-flow-chart-v2.png)

フローチャートをパンおよびズームでき、フローチャート内のいずれかのノードを選択して、そのイベントについての詳細を確認できます。

フローチャートビューを開くには、[Summary view](#summary-view)から**Agent Flow Chart**を選択します。

1. Chat viewのギアアイコンを選択して**Show Agent Logs**を選択し、Agent Debug panelを開きます。

1. パネルの上部にあるブレッドクラムのセッション説明を選択します。

1. Summary viewから**Agent Flow Chart**を選択します。

### チャットに対するデバッグイベントをアタッチ

エージェントデバッグイベントのスナップショットをチャット会話にアタッチして、AIに現在のセッションについての質問をできます。これは、トークン使用量、どのカスタマイズが読み込まれたか、どのツール呼び出しが発生したか、リクエストにかかった時間を理解するのに役立ちます。

チャットに対するデバッグイベントをアタッチするには：

1. チャットセッションの[Agent Logs view](#logs-view)を開きます

1. Agent Debug panelの右上にあるスパークルアイコンを選択します。これにより、Chat viewが開き、デバッグイベントスナップショットがコンテキストとしてアタッチされます。

## Chat Debug view

Chat Debug viewは、各AIリクエストとレスポンスの詳細を表示します。正確なシステムプロンプト、ユーザープロンプト、コンテキスト、または言語モデルに送受信されたツールレスポンスペイロードを検査する必要があるときに使用します。

### Chat Debug viewを開く

Chat Debug viewを開くには：

* Chat viewのオーバーフローメニューを選択して、**Show Chat Debug View**を選択します。
* Command Paletteから**Developer: Show Chat Debug View**コマンドを実行します。

![Chat Debug viewのスクリーンショット。チャットリクエストとレスポンスの詳細を表示しています。](../images/chat-debug-view/chat-debug-view.png)

### デバッグ出力を読む

Chat Debug viewの各相互作用には、展開可能なセクションが含まれます：

| セクション | 表示内容 | 確認項目 |
|---|---|---|
| **System prompt** | AIの動作、機能、制約を定義する指示。 | カスタム指示またはエージェント説明が正しく表示されていることを確認します。 |
| **User prompt** | モデルに送信された正確なプロンプトテキスト。 | `#`-mentionsが解決された実際のコンテンツを含めて、プロンプトが期待どおりに送信されたことを確認します。 |
| **Context** | リクエストにアタッチされたファイル、シンボル、その他のコンテキストアイテム。 | 期待されたファイルとコンテキストが表示されていることを確認します。ファイルがない場合は、インデックスされていないか、コンテキストウィンドウがいっぱいの可能性があります。 |
| **Response** | 推論を含むモデルのレスポンスの完全なテキスト。 | モデルがリクエストをどのように解釈したかを理解するために、レスポンスを確認します。 |
| **Tool responses** | リクエスト中に呼び出されたツールの入力と出力。 | ツールが正しい入力を受け取り、期待される出力を返したことを確認します。MCPサーバーのデバッグに役立ちます。 |

各セクションを展開して完全な詳細を確認できます。これは、単一のリクエストの一部として複数のツールが呼び出される可能性がある[エージェントを使用する](/docs/copilot/agents/local-agents.md)場合に特に役立ちます。

## 一般的なトラブルシューティングシナリオ

### AIがワークスペースファイルを無視する

AIが汎用情報で応答して、コードベースを参照しない場合：

1. Agent Logsを開き、ワークスペースファイルがインデックスされたことを確認するために**Discovery**イベントを確認します。
1. Chat Debug viewを開き、**Context**セクションを確認して、ワークスペースファイルがコンテキストに表示されていることを確認します。表示されていない場合は、[ワークスペースインデックス](/docs/copilot/reference/workspace-context.md)がアクティブであることを確認します。
1. 明示的な`#`-mentionsを追加（`#file`または`#codebase`など）して、正しいファイルが含まれていることを確認します。[コンテキストの管理](/docs/copilot/chat/copilot-chat-context.md)の詳細を参照してください。

### MCPツールが呼び出されていない

AIが期待されるツールを呼び出さない場合：

1. Agent Logsを開き、**Tool calls**フィルタを確認して、ツールが呼び出されたか、スキップされたかを確認します。
1. Chat Debug viewを開き、**System prompt**セクションを確認して、ツールが利用可能なツールのリストに表示されていることを確認します。
1. ツールがない場合は、MCPサーバーが実行中で正しく設定されていることを確認します。
1. プロンプトで`#tool-name`を使用してツールを明示的に記述してみてください。

### AIレスポンスが不完全または途中で切れている

レスポンスがカットされているように見える場合：

1. Agent Logsで**LLM requests**イベントを確認してトークン使用量を確認します。
1. 完全なコンテキストウィンドウによりモデルがレスポンスを切り詰めることがあります。[新しいチャットセッション](/docs/copilot/chat/chat-sessions.md)を開始してコンテキストをリセットします。

### プロンプトファイルが適用されていない

カスタム指示またはプロンプトファイルが効果を持たないように見える場合：

1. Agent Logsを開き、**Discovery**イベントを確認して、ファイルが読み込まれたか、スキップされたか、検証に失敗したかを確認します。
1. ファイルの場所と`applyTo`パターンが現在のコンテキストと一致することを確認します。
1. [チャットカスタマイズ診断](/docs/copilot/troubleshooting.md#chat-customization-diagnostics)でエラー詳細を確認します。

## 関連リソース

* [チャット概要](/docs/copilot/chat/copilot-chat.md)
* [AIのコンテキストを管理](/docs/copilot/chat/copilot-chat-context.md)
* [VS CodeでのAIのトラブルシューティング](/docs/copilot/troubleshooting.md)
* [VS CodeでAIを使用するためのセキュリティに関する考慮事項](/docs/copilot/security.md)

