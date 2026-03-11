---
ContentId: f8e4b2c1-9d3a-4e5f-b6c7-8a9d0e1f2b3c
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでGitHub Copilotの問題をログ、診断、デバッグツールで解決します。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords:
- ai
- copilot
- troubleshooting
- diagnostics
- logs
- debugging
---
# Visual Studio CodeのAIのトラブルシューティング

この記事では、VS CodeのAI関連の問題をトラブルシューティングするための診断ツールとテクニックについて説明します。これらのツールを使用して、ネットワーク接続、カスタマイズファイル、およびAI応答の問題を特定してください。

## GitHub Copilotのログを表示する

GitHub Copilot拡張機能のログファイルは、Visual Studio Code拡張機能の標準的なログ場所に保存されます。これらのログを使用して、接続の問題、拡張機能のエラー、および予期しない動作を診断してください。

詳細なログを表示するには：

1. コマンドパレットを開きます（`kb(workbench.action.showCommands)`）。
1. **Developer: Set Log Level**を実行し、GitHub CopilotおよびGitHub Copilot Chat拡張機能の値を**Trace**に設定します。
1. **Output: Show Output Channels**を実行し、リストから**GitHub Copilot**または**GitHub Copilot Chat**を選択します。
1. 出力パネルで、選択した拡張機能のログを表示します。

出力チャネルを切り替えるには、出力パネルの右側のドロップダウンメニューから**GitHub Copilot**または**GitHub Copilot Chat**を選択します。

## ネットワーク診断を収集する

GitHub Copilotへの接続に問題が発生した場合は、ネットワーク接続診断を収集して、ファイアウォール、プロキシ、またはVPNの問題を特定してください。

1. コマンドパレットを開きます（`kb(workbench.action.showCommands)`）。
1. **GitHub Copilot: Collect Diagnostics**を実行します。
1. エディタータブが開き、問題を報告する際にレビューして共有できる診断情報が表示されます。

ネットワーク設定の詳細については、「[Copilotのネットワークおよびファイアウォール構成](/docs/copilot/faq.md#network-and-firewall-configuration-for-copilot)」を参照してください。

## チャット操作をデバッグする

VS Codeは、プロンプトをAIに送信するときに何が起こるかを検査するためのツールを提供します。

* **Agent Debugパネル（プレビュー）:**

    チャットセッション中のエージェント操作の時系列イベントログを表示します。ツール呼び出しシーケンス、LLMリクエスト、トークン使用量、プロンプトファイルディスカバリ、およびエラーが含まれます。これはチャット操作を理解およびデバッグするための主要なツールです。

    Agent Debugパネルを開くには：

    1. チャットビューでギアアイコンを選択します。
    1. **Show Agent Logs**を選択します。

    Agent Debugパネルから、エージェントデバッグイベントのスナップショットをチャット会話に添付して、AIにセッションについての質問をし、特定の操作をトラブルシューティングできます。ログビューのスパークルアイコンを選択して、[デバッグイベントをチャットに添付](/docs/copilot/chat/chat-debug-view.md#attach-debug-events-to-chat)します。

* **チャットデバッグビュー:**

    完全なシステムプロンプト、ユーザープロンプト、コンテキスト、およびツール呼び出しペイロードを含む、各LLMリクエストとレスポンスの詳細を表示します。このビューを使用して、各操作の言語モデルに送信および受信された正確なデータを検査してください。

    チャットデバッグビューを開くには：

    1. チャットビューのオーバーフローメニュー（`...`）を選択します。
    1. **Show Chat Debug View**を選択します。

[チャット操作のデバッグ](/docs/copilot/chat/chat-debug-view.md)の詳細をご覧ください。

## チャットカスタマイズ診断

チャットカスタマイズ診断ビューは、現在読み込まれているすべてのカスタムエージェント、プロンプトファイル、命令ファイル、およびスキルを表示します。このビューを使用して、適用されていないか、エラーを引き起こしているカスタマイズファイルの問題をトラブルシューティングしてください。

診断ビューを開くには：

1. チャットビューを右クリックします。
1. **Diagnostics**を選択します。

これにより、以下を一覧表示するマークダウンドキュメントが開きます：

* すべてのアクティブなカスタマイズファイルとその場所
* 各ファイルの読み込み状態（読み込み済み、失敗、またはスキップ）
* 読み込みに失敗したファイルのエラーメッセージ
* 命令が適用される順序

> [!TIP]
> カスタマイズファイルが適用されていない場合は、診断ビューを確認して、正常に読み込まれたことを確認し、エラーメッセージを確認してください。

## MCPサーバーのトラブルシューティング

MCPサーバーは外部サービスに接続することでチャット機能を拡張します。MCPサーバーが正常に動作していない場合は、そのログを表示して再起動できます。

MCPサーバーをトラブルシューティングするには：

1. コマンドパレットを開き、**MCP: List Servers**を実行します。
1. サーバーを選択して、そのステータスと利用可能なアクションを表示します。
1. **Show Output**を選択して、サーバーのログを表示します。
1. **Restart Server**を選択して、動作していないサーバーを再起動します。

[MCPサーバーの設定とデバッグ](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

## フィードバックを提供する

解決できない問題が発生した場合は、GitHub Copilotの改善に役立つように報告してください：

* **ゴーストテキスト提案**：エディター内のゴーストテキスト提案にカーソルを合わせ、**Send Copilot Completion Feedback**を選択します。
* **次の編集提案**：エディターのガターにある次の編集提案メニューの**Feedback**アクションを選択します。
* **一般的な問題**：**Help**>**Report Issue**を開き、**VS Code Extension**を選択して、**GitHub Copilot Chat**を選択します。

問題を報告する場合は、[Copilotログ](#github-copilotのログを表示する)から関連情報を含めて、問題の診断に役立つようにしてください。

## 関連リソース

* [チャット操作をデバッグする](/docs/copilot/chat/chat-debug-view.md)
* [カスタム命令](/docs/copilot/customization/custom-instructions.md)
* [MCPサーバー](/docs/copilot/customization/mcp-servers.md)
* [GitHub Copilot FAQ](/docs/copilot/faq.md)

