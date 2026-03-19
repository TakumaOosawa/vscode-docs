---
ContentId: f8e4b2c1-9d3a-4e5f-b6c7-8a9d0e1f2b3c
DateApproved: 3/9/2026
MetaDescription: Visual Studio Code で GitHub Copilot の問題をログ、診断、デバッグツールでトラブルシューティングします。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords:
- ai
- copilot
- troubleshooting
- diagnostics
- logs
- debugging
---
# Visual Studio Code の AI のトラブルシューティング

この記事では、VS Code における AI関連の問題をトラブルシューティングするための診断ツールとテクニックについて説明します。これらのツールを使用して、ネットワーク接続、カスタマイズファイル、AI応答に関する問題を特定できます。

## GitHub Copilot のログを表示する

GitHub Copilot拡張機能のログファイルは、Visual Studio Code拡張機能の標準的なログの場所に保存されています。これらのログを使用して、接続の問題、拡張機能のエラー、予期しない動作を診断できます。

詳細なログを表示するには:

1. コマンドパレット(`kb(workbench.action.showCommands)`)を開きます。
1. **Developer: Set Log Level** を実行し、GitHub Copilot と GitHub Copilot Chat 拡張機能の値を **Trace** に設定します。
1. **Output: Show Output Channels** を実行し、リストから **GitHub Copilot** または **GitHub Copilot Chat** を選択します。
1. [出力]パネルで、選択した拡張機能のログを表示します。

出力チャネルを切り替えるには、[出力]パネルの右側のドロップダウンメニューから **GitHub Copilot** または **GitHub Copilot Chat** を選択します。

## ネットワーク診断を収集する

GitHub Copilot への接続に問題が発生した場合、ネットワーク接続診断を収集して、ファイアウォール、プロキシ、VPN の問題を特定してください。

1. コマンドパレット(`kb(workbench.action.showCommands)`)を開きます。
1. **GitHub Copilot: Collect Diagnostics** を実行します。
1. エディタタブが開き、レビューして、問題を報告するときに共有できる診断情報が表示されます。

ネットワーク設定の詳細については、「[Copilot のネットワークとファイアウォール設定](/docs/copilot/faq.md#network-and-firewall-configuration-for-copilot)」を参照してください。

## チャットインタラクションのデバッグ

VS Code は、AI にプロンプトを送信したときの動作を検査するツールを提供しています。

* **Agent Debug panel (プレビュー):**

    チャットセッション中のエージェントインタラクションの時系列イベントログを表示します。ツールコールシーケンス、LLMリクエスト、トークン使用量、プロンプトファイル検出、エラーが含まれます。これはチャットインタラクションを理解してデバッグするための主要なツールです。

    Agent Debug panel を開くには:

    1. Chat ビューのギアアイコンを選択します。
    1. **Show Agent Logs** を選択します。

    Agent Debug panel から、エージェントデバッグイベントのスナップショットをチャット会話にアタッチして、AI にセッションについて質問し、特定のインタラクションをトラブルシューティングできます。Logs ビューのスパークルアイコンを選択して、[デバッグイベントをチャットにアタッチ](/docs/copilot/chat/chat-debug-view.md#attach-debug-events-to-chat)してください。

* **Chat Debug view:**

    完全なシステムプロンプト、ユーザープロンプト、コンテキスト、ツール呼び出しペイロードを含む、各LLMリクエストとレスポンスの生詳細を表示します。このビューを使用して、各インタラクションの言語モデルに送受信される正確なデータを検査してください。

    Chat Debug view を開くには:

    1. Chat ビューのオーバーフローメニュー(`...`)を選択します。
    1. **Show Chat Debug View** を選択します。

[チャットインタラクションのデバッグ](/docs/copilot/chat/chat-debug-view.md)の詳細をご覧ください。

## チャットカスタマイズ診断

チャットカスタマイズ診断ビューは、現在読み込まれているカスタムエージェント、プロンプトファイル、命令ファイル、スキルをすべて表示します。このビューを使用して、カスタマイズファイルが適用されていない、またはエラーを引き起こしている問題をトラブルシューティングしてください。

診断ビューを開くには:

1. Chat ビューで右クリックします。
1. **Diagnostics** を選択します。

これにより、以下がリストされたマークダウンドキュメントが開きます:

* すべてのアクティブなカスタマイズファイルとそれらの場所
* 各ファイルの読み込み状態(読み込み済み、失敗、またはスキップ)
* 読み込みに失敗したファイルのエラーメッセージ
* 命令が適用される順序

> [!TIP]
> カスタマイズファイルが適用されていない場合、診断ビューで確認して、正常に読み込まれたこと、およびエラーメッセージを確認してください。

## MCP サーバーのトラブルシューティング

MCP サーバーは外部サービスに接続することで、チャット機能を拡張します。MCP サーバーが正常に機能していない場合、そのログを表示して再度開始できます。

MCP サーバーをトラブルシューティングするには:

1. コマンドパレットを開き、**MCP: List Servers** を実行します。
1. サーバーを選択して、その状態と利用可能なアクションを表示します。
1. **Show Output** を選択して、サーバーのログを表示します。
1. **Restart Server** を選択して、動作不良のサーバーを再起動します。

[MCP サーバーの設定とデバッグ](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

## フィードバックを提供する

解決できない問題が発生した場合、GitHub Copilot の改善に役立てるために、それらを報告してください:

* **ゴーストテーキスト候補**: エディターのゴーストテキスト候補にマウスを置き、**Send Copilot Completion Feedback** を選択します。
* **次の編集候補**: エディターガターの次の編集候補メニューの **Feedback** アクションを選択します。
* **一般的な問題**: **Help** > **Report Issue** を開き、**VS Code Extension** を選択して、**GitHub Copilot Chat** を選択します。

問題を報告するときは、[Copilot ログ](#github-copilot-のログを表示する)から関連情報を含めて、問題の診断に役立ててください。

## 関連リソース

* [チャットインタラクションのデバッグ](/docs/copilot/chat/chat-debug-view.md)
* [カスタム命令](/docs/copilot/customization/custom-instructions.md)
* [MCP サーバー](/docs/copilot/customization/mcp-servers.md)
* [GitHub Copilot FAQ](/docs/copilot/faq.md)

