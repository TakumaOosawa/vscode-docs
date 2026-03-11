---
ContentId: 3a6e8c1d-5f2b-4d9a-b7e1-9c4f2a8d6b3e
DateApproved: 3/9/2026
MetaDescription: VS Codeでローカルエージェントを使用して、ワークスペース、ツール、モデルへのフルアクセスで対話型コーディングタスクを実行する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- local agent
- chat
- copilot
---

# Visual Studio Codeのローカルエージェント

ローカルエージェントはVisual Studio Code内のマシン上で対話的に実行されます。これらは現在のワークスペースで動作し、拡張機能提供ツールやMCPサーバーを含むVS Codeで利用可能なツールとモデルの完全な範囲にアクセスできます。[カスタムエージェントを作成](/docs/copilot/customization/custom-agents.md)することで、エージェントにコードレビュアー、テスター、ドキュメンテーションライターなどの特定のロールやペルソナを引き受けさせることができます。

ローカルエージェントはVS Codeのチャットインターフェイスで動作します。チャットセッションを閉じるとローカルエージェントはアクティブのままで、セッションビューで追跡できます。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントの使用を開始する">
ローカル、バックグラウンド、クラウドエージェントをVS Codeで体験するハンズオンチュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## ローカルエージェントを使用する理由

* ブレーンストーミング、計画、またはまだ完全に定義されていないタスクなど、即座フィードバックが必要な対話型の会話
* リント エラー、スタックトレース、単体テスト結果など、開発者環境からのコンテキストが必要なタスク
* VS Code拡張機能またはMCPサーバーからの特定のツールへのアクセスが必要なタスク、またはBYOKモデルのような特定のモデルを使用する必要があるタスク
* 他のチームメンバーからのコラボレーションが不要なタスク

## 主な特徴

* ローカルマシン上のVS Code内で実行され、現在のワークスペースで動作
* 対話的なチャットベースのインターフェイスでリアルタイムフィードバックと反復処理が可能
* ワークスペース、ファイル、コンテキストへの完全なアクセス
* 組み込みツール、MCPツール、拡張機能提供ツールなど、VS Codeで構成されたすべてのエージェントツールにアクセス可能
* BYOKモデルや他のプロバイダーからのモデルを含む、VS Codeで利用可能なすべてのモデルを使用可能

## 組み込みエージェント

ローカルエージェントセッションは、異なるタイプのタスクに最適化された3つの組み込みエージェントのいずれかを使用します。チャットセッション中はいつでもチャットビューのエージェントピッカーから別のエージェントを選択してエージェントを切り替えられます。より専門的なワークフローについては、独自の[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成できます。

### エージェント

エージェントは、ターミナルコマンドとツールの実行が必要になる可能性のある高レベルの要件に基づく複雑なコーディングタスクに最適化されています。AIは自律的に動作し、関連するコンテキストとファイルを決定し、実行が必要な作業を計画し、発生する問題を解決するために反復します。

VS Codeはコード変更をエディターに直接適用し、エディターオーバーレイコントロールで提案されたエディットを移動して確認できます。エージェントは異なるタスクを実行するために複数の[ツール](/docs/copilot/agents/agent-tools.md)を呼び出す可能性があります。

[ツールを追加](/docs/copilot/agents/agent-tools.md)してMCPサーバーを追加するか、ツールを投稿する拡張機能をインストールすることで、チャットをカスタマイズできます。

エージェントで開く: [安定版](vscode://GitHub.Copilot-Chat/chat?mode=agent) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=agent)

> [!IMPORTANT]
> エージェントオプションが表示されない場合は、VS Code設定でエージェントが有効になっていることを確認してください（`setting(chat.agent.enabled)`）。組織がエージェントを無効にしている可能性もあります。この機能を有効にするには管理者に問い合わせてください。

### 計画

計画エージェントはコーディングタスクの構造化された実装計画を作成するために最適化されています。複雑な機能または変更を実装前に小さく管理しやすいステップに分割したい場合は計画エージェントを使用してください。

計画エージェントは、必要なステップの概要を示す詳細な計画を生成し、タスクの包括的な理解を確保するために明確化する質問をします。その後計画を実装エージェントに引き渡すか、ガイドとして使用できます。

計画で開く: [安定版](vscode://GitHub.Copilot-Chat/chat?mode=plan) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=plan)

[エージェントによる計画](/docs/copilot/agents/planning.md)についてさらに詳しく学習します。

### 質問

質問機能は、コードベース、コーディング、一般的なテクノロジーの概念に関する質問に答えるのに最も適しています。何かがどのように機能するか理解したい場合、アイデアを探索したい場合、またはコーディングタスクでヘルプが必要な場合は質問を使用してください。

質問はエージェント機能を使用してコードベースを調査し、関連するコンテキストを収集します。レスポンスにはコードベースに個別に適用できるコードブロックが含まれることがあります。コードブロックを適用するには、コードブロックの上にマウスを移動して**エディターで適用**ボタンを選択します。

質問で開く: [安定版](vscode://GitHub.Copilot-Chat/chat?mode=ask) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=ask)

### 編集モード（非推奨）

編集モードは非推奨です。複数ファイルコード編集にはエージェントモードを使用してください。`setting(chat.editMode.hidden)`設定を有効にすることで編集モードを復元できます。

## 使用を開始する

> [!TIP]
> バックグラウンドおよびクラウドエージェントを含む異なるエージェントタイプの操作を実演するハンズオンチュートリアルについては、[エージェントのチュートリアル](/docs/copilot/agents/agents-tutorial.md)を参照してください。

ローカルエージェントセッションを開始するには:

1. チャットビューのエージェントピッカーから**エージェント**を選択します。

1. チャット入力フィールドに高レベルのプロンプトを入力します。例えば以下のように尋ねることができます:

    ```prompt-agent
    Implement a user authentication system with OAuth2 and JWT.
    ```

    または

    ```prompt-agent
    Set up a CI/CD pipeline for this project.
    ```

1. ツールピッカーを使用して[ツールを有効にして](/docs/copilot/agents/agent-tools.md)エージェントにより多くの機能を与えます。

1. **送信**を選択するか、`kb(workbench.action.chat.submit)`を押してプロンプトを送信します。

1. エージェントがリクエストを処理する際にコード変更とツール呼び出しを確認して承認します。

    エージェントが動作している間にフォローアップのプロンプトを送信できます。後で送信するメッセージをキューに入れるか、エージェントを新しい方向に導くか、停止してすぐに送信します。[実行中のリクエスト中のメッセージ送信](/docs/copilot/chat/chat-sessions.md#send-messages-while-a-request-is-running)についてさらに詳しく学習します。

    > [!TIP]
    > VS Codeはワークスペース構成設定や環境設定などの機密ファイルへの不用意な編集から保護するのに役立ちます。[機密ファイルの編集](/docs/copilot/chat/review-code-edits.md#edit-sensitive-files)についてさらに詳しく学習します。

質問で開始するには:

1. チャット入力フィールドにプロンプトを入力します。例えば以下のように尋ねることができます:

    ```prompt-ask
    Provide 3 ways to implement a search feature in React.
    ```

    または

    ```prompt-ask
    Where is the db connection configured in this project? #codebase
    ```

1. チャットビューのエージェントピッカーから**質問**を選択します。

1. オプションで、[プロンプトにコンテキストを追加して](/docs/copilot/chat/copilot-chat-context.md)より正確なレスポンスを取得します。

1. **送信**を選択するか、`kb(workbench.action.chat.submit)`を押してプロンプトを送信します。

## 関連リソース

* [エージェント概要](/docs/copilot/agents/overview.md): エージェントタイプとセッション管理の概要。
* [エージェントチュートリアル](/docs/copilot/agents/agents-tutorial.md): 異なるエージェントタイプを操作するためのハンズオンチュートリアル。
* [ツール](/docs/copilot/agents/agent-tools.md): 組み込み、MCP、拡張ツールでエージェントを拡張します。
* [カスタムエージェント](/docs/copilot/customization/custom-agents.md): 独自のAIエージェントと拡張機能を作成します。
* [チャット](/docs/copilot/chat/copilot-chat.md): チャットインターフェイスと相互作用機能について学習します。

