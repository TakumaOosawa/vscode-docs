---
ContentId: 557a7e74-f77e-488d-90ea-fd2cfecfffda
DateApproved: 12/10/2025
MetaDescription: VS CodeでGitHub Copilot chatを使い始めましょう。chatへのアクセス方法や、自然言語でコーディングを始めてコードベースを理解し、問題を解決する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでchatを使い始める

Visual Studio CodeのChatを使うと、自然言語でAIによるコーディング支援を受けられます。コードについて質問したり、複雑なロジックの理解を助けてもらったり、新機能を生成したり、バグを修正したりできます。これらはすべて会話形式のインターフェイスで行えます。

この記事では、VS Codeで利用できるさまざまなchat体験へのアクセス方法、最初のプロンプトの送信、より良い結果を得るための効果的なプロンプトの書き方、ワークフローに合わせたchatのカスタマイズ方法を学びます。

## VS Codeでchatにアクセスする

VS CodeにはAIチャット会話を開始する3つの方法があり、それぞれ異なるワークフローやタスクに最適化されています。各chat体験にアクセスするには、VS CodeのタイトルバーにあるChatメニュー、または対応するキーボードショートカットを使用します。

![Screenshot of the Copilot Chat menu in the VS Code Command Center](images/copilot-chat/copilot-chat-menu-command-center.png)

<details>
<summary>Chatビュー</summary>

`kb(workbench.action.chat.open)`を押すと、専用のサイドパネルでChatビューを開きます。chat用により広い作業領域が必要な場合は、chatメニューから**New Chat Editor**を選択してエディタタブとして開くか、**New Chat Window**を選択して別ウィンドウとして開くこともできます。

**Chatビューの用途:**

* 継続的なマルチターンのチャット会話
* 複数の[agents](#switch-between-agents)を切り替えて、質問したり、複数ファイルにまたがるコード編集を行ったり、自律的なコーディングワークフローを開始したりする
* 複数ファイルにまたがる機能に取り組む
* 複雑な変更の計画と実装

![Screenshot of the Chat view](images/copilot-chat/chat-view.png)

</details>

<details>
<summary>Inline chat</summary>

`kb(inlineChat.start)`を押すと、エディタまたはターミナル上で直接チャット会話を開始できます。

**Inline chatの用途:**

* 作業中の場所でそのまま提案を受け取る
* 現在のコンテキストでコードを理解する
* ターミナルコマンドや出力について支援を受ける

![Screenshot of Inline chat](images/copilot-chat/inline-chat.png)

</details>

<details>
<summary>Quick chat</summary>

`kb(workbench.action.quickchat.toggle)`を押すと、軽量なチャットオーバーレイを開きます。

**Quick chatの用途:**

* 長い会話が不要な簡単な質問
* 現在の表示を変えずに回答を得る
* 作業への集中を保ちながら情報を調べる

![Screenshot of Quick Chat](images/copilot-chat/quick-chat.png)

</details>

> [!TIP]
> `code chat`コマンドを使うと、コマンドラインから直接chatを開始できます。詳細は、[VS Codeコマンドラインのドキュメント](/docs/configure/command-line.md#start-chat-from-the-command-line)を参照してください。

## 最初のchatプロンプトを送信する

まずは基本的な電卓アプリを作成して、VS Codeでchatがどのように動作するかを確認しましょう。

1. Open the Chat view by pressing `kb(workbench.action.chat.open)` or selecting **Chat** from the VS Code title bar.
1. `kb(workbench.action.chat.open)`を押すか、VS Codeのタイトルバーから**Chat**を選択してChatビューを開きます。

1. Select **Agent** from the agent picker.
1. agent pickerから**Agent**を選択します。

    agentを使用すると、chatが必要な作業を自律的に判断し、ワークスペースに必要な変更を加えます。

1. Type the following prompt in the chat input field and press `kb(workbench.action.chat.submit)` to submit it:
1. chat入力欄に次のプロンプトを入力し、`kb(workbench.action.chat.submit)`を押して送信します。

    ```prompt
    HTML、CSS、JavaScriptで基本的な電卓アプリを作成してください
    ```

    agentは変更をワークスペースに直接適用します。また、依存関係のインストールやビルドスクリプトの実行などのために、ターミナルコマンドを実行することもあります。

1. In the editor, [review the suggested changes](/docs/copilot/chat/review-code-edits.md) and choose to keep or discard them.
1. エディタで、[提案された変更を確認](/docs/copilot/chat/review-code-edits.md)し、保持するか破棄するかを選択します。

1. Ask follow-up questions to enhance the app. For example, you might ask:
1. 追加の質問をしてアプリを改善します。たとえば、次のように依頼できます。

    ```prompt
    ダークモードの切り替えを追加してください
    ```

    or
    または

    ```prompt
    モダンなデザインでスタイルを整えてください
    ```

    会話を続けると、VS Codeはchatのプロンプトと応答の履歴をコンテキストとして使用します。このコンテキストにより、chatとマルチターンの会話を行い、結果を洗練させて改善できます。

> [!TIP]
> 音声入力を使用して、VS Codeでchatと対話できます。詳しくは、[chatで音声入力を使用する](/docs/configure/accessibility/voice.md)を参照してください。

## さまざまな言語モデルを試す

VS Codeでは、さまざまな言語モデルを選択でき、それぞれ異なるタスクに最適化されています。素早いコーディング作業向けのモデルもあれば、複雑な推論や計画に優れたモデルもあります。

言語モデルを変更するには、chat入力欄のmodel pickerを使用し、目的に最も合うモデルを選択します。

![Screenshot of the language model picker in the Chat view, showing a dropdown list of available models.](images/copilot-chat/chat-model-picker.png)

他のモデルプロバイダーのモデルを追加して、chatで使用することもできます。詳しくは、[他のプロバイダーのモデルを使用する](/docs/copilot/customization/language-models.md)を参照してください。

> [!NOTE]
> 利用できるモデルの一覧は、Copilotのサブスクリプションによって異なる場合があり、時間とともに変化する可能性があります。詳細は、GitHub Copilotのドキュメントの[利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)を参照してください。

## agentsを切り替える

Agentsを使うと、chatが特定のタスクに最適化された別の役割やペルソナを担えます。chatセッション中はいつでもagentsを切り替えられます。

1. Open the Chat view (`kb(workbench.action.chat.open)`).
1. Chatビューを開きます（`kb(workbench.action.chat.open)`）。

1. Select the desired agent from the agent picker.
1. agent pickerから目的のagentを選択します。

    ![Screenshot showing the Chat view with the agent picker expanded, displaying different agent options.](../images/customization/chat-mode-dropdown.png)

### 組み込みagents

VS Codeには、4つの組み込みagents（**Agent**、**Plan**、**Ask**、**Edit**）が用意されています。より特化したワークフローのために、独自の[custom agents](/docs/copilot/customization/custom-agents.md)を作成することもできます。

<details>
<summary>Agent</summary>

Agentは、ターミナルコマンドやツールの実行が必要になる可能性のある、高レベル要件に基づく複雑なコーディングタスクに最適化されています。AIは自律的に動作し、関連するコンテキストと編集対象ファイルを判断し、必要な作業を計画し、問題が発生したら反復して解決します。

VS Codeはエディタ内でコード変更を直接適用し、エディタのオーバーレイコントロールで提案された編集間を移動して確認できます。agentは、さまざまなタスクを実行するために複数の[tools](/docs/copilot/chat/chat-tools.md)を呼び出すことがあります。

MCPサーバーを追加するか、toolsを提供する拡張機能をインストールすることで、[追加のtoolsでchatをカスタマイズ](/docs/copilot/chat/chat-tools.md)できます。

Open chat with Agent: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=agent) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=agent)

### agentsを使い始める

> [!TIP]
> background agentやcloud agentなど、さまざまなagentタイプの使い方を実演するハンズオンチュートリアルについては、[agentsチュートリアル](/docs/copilot/agents/agents-tutorial.md)を参照してください。

To start a local agent session:

1. Select **Agent** from the agent picker in the Chat view.
1. Chatビューのagent pickerから**Agent**を選択します。

1. Type a high-level prompt in the chat input field. For example, you might ask:
1. chat入力欄に高レベルのプロンプトを入力します。たとえば、次のように依頼できます。

    ```prompt
    Implement a user authentication system with OAuth2 and JWT.
    ```

    or
    または

    ```prompt
    Set up a CI/CD pipeline for this project.
    ```

1. Use the tools picker to [enable tools](/docs/copilot/chat/chat-tools.md) and give the agent more capabilities.
1. tools pickerを使用して[toolsを有効化](/docs/copilot/chat/chat-tools.md)し、agentにより多くの機能を付与します。

1. Select **Send** or press `kb(workbench.action.chat.submit)` to submit your prompt.
1. **Send**を選択するか`kb(workbench.action.chat.submit)`を押してプロンプトを送信します。

1. Review and confirm code changes and tool invocations as the agent works through your request.
1. agentがリクエストを進める間、コード変更とツール呼び出しを確認して承認します。

    > [!TIP]
    > VS Codeは、ワークスペース構成設定や環境設定などの機密性の高いファイルへの意図しない編集から保護するのに役立ちます。詳しくは、[機密性の高いファイルを編集する](/docs/copilot/chat/review-code-edits.md#edit-sensitive-files)を参照してください。

</details>

<details>
<summary>Plan</summary>

plan agentは、コーディングタスクに対する構造化された実装計画の作成に最適化されています。複雑な機能や変更を実装前に小さく管理しやすい手順へ分解したい場合は、plan agentを使用します。

plan agentは、必要な手順を示す詳細な計画を生成し、タスクを包括的に理解するために確認の質問をします。その後、計画をimplementation agentに引き継ぐか、ガイドとして使用できます。

Open chat with Plan: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=plan) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=plan)

### plan agentを使い始める

1. Type a high-level prompt in the chat input field. For example, you might ask:
1. chat入力欄に高レベルのプロンプトを入力します。たとえば、次のように依頼できます。

    ```prompt
    Update the application to support multi-language localization.
    ```

    or
    または

    ```prompt
    Add a search feature to the application.
    ```

1. Select **Plan** from the agent picker in the Chat view.
1. Chatビューのagent pickerから**Plan**を選択します。

1. Select **Send** or press `kb(workbench.action.chat.submit)` to submit your prompt.
1. **Send**を選択するか`kb(workbench.action.chat.submit)`を押してプロンプトを送信します。

1. Answer any clarifying questions or refine the plan as needed.
1. 確認の質問に回答するか、必要に応じて計画を洗練します。

1. Select **Start Implementation** to hand off the plan to an implementation agent.
1. **Start Implementation**を選択して、計画をimplementation agentに引き継ぎます。

</details>

<details>
<summary>Ask</summary>

Askは、コードベース、コーディング、一般的な技術概念に関する質問への回答に最適化されています。仕組みを理解したい、アイデアを検討したい、コーディングタスクの助けが欲しい場合はAskを使用します。複数ファイルにまたがる大きな変更や、より複雑なコーディングタスクには、agentsの使用を検討してください。

応答には、個別にコードベースへ適用できるコードブロックが含まれる場合があります。これは単一ファイル内の小さな編集に適しています。コードブロックをコードベースに適用するには、コードブロックにカーソルを合わせて**Apply in Editor**ボタンを選択します。

Open chat with Ask: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=ask) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=ask)

### Askを使い始める

1. Type your prompt in the chat input field. For example, you might ask:
1. chat入力欄にプロンプトを入力します。たとえば、次のように依頼できます。

    ```prompt
    Provide 3 ways to implement a search feature in React.
    ```

    or
    または

    ```prompt
    Where is the db connection configured in this project? #codebase
    ```

1. Select **Ask** from the agent picker in the Chat view.
1. Chatビューのagent pickerから**Ask**を選択します。

1. Optionally, [add context to your prompt](/docs/copilot/chat/copilot-chat-context.md) to get more accurate responses.
1. 必要に応じて、[プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)して、より正確な応答を得ます。

1. Select **Send** or press `kb(workbench.action.chat.submit)` to submit your prompt.
1. **Send**を選択するか`kb(workbench.action.chat.submit)`を押してプロンプトを送信します。

</details>

<details>
<summary>Edit</summary>

Editは、プロジェクト内の複数ファイルにまたがるコード編集に最適化されています。Editは、行いたい変更内容と編集したいファイルが明確な場合のコーディングタスクに便利です。

VS Codeはエディタ内でコード変更を直接適用し、そこで確認できます。エディタのオーバーレイコントロールで`kbstyle(Up)`と`kbstyle(Down)`を使用して編集間を移動し、変更を保持または取り消します。

Open chat with Edit: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=edit) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=edit)

### Editを使い始める

1. Type your request in the chat input field. For example, you might ask:
1. chat入力欄に依頼内容を入力します。たとえば、次のように依頼できます。

    ```prompt
    Refactor the authentication logic to use OAuth2.
    ```

    or
    または

    ```prompt
    Add unit tests for the user service.
    ```

1. Select **Edit** from the agent picker in the Chat view.
1. Chatビューのagent pickerから**Edit**を選択します。

1. [Add context to your prompt](/docs/copilot/chat/copilot-chat-context.md) to guide the AI to make edits in the right files.
1. [プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)して、AIが適切なファイルに編集を行えるようにします。

1. Select **Send** or press `kb(workbench.action.chat.submit)` to submit your prompt.
1. **Send**を選択するか`kb(workbench.action.chat.submit)`を押してプロンプトを送信します。

1. Review the code changes in the editor by using the overlay controls.
1. オーバーレイコントロールを使用して、エディタでコード変更を確認します。

</details>

## ワークフローに合わせてchatをカスタマイズする

コンテキストを追加すると、chatからより関連性の高い応答を得られます。さらに、プロジェクト固有のガイドラインや開発プラクティスに合わせてchatを調整するために、VS Codeではいくつかの方法でchatをカスタマイズできます。

* [**Custom instructions**](/docs/copilot/customization/custom-instructions.md): コーディング規約、好みのフレームワーク、アーキテクチャガイドラインなど、すべての会話にわたってchatの振る舞いを導く永続的な指示を追加します。
* [**Prompt files**](/docs/copilot/customization/prompt-files.md): `/`コマンドで呼び出せる再利用可能なプロンプトテンプレートを定義し、チーム全体で共通ワークフローを標準化します。
* [**Custom agents**](/docs/copilot/customization/custom-agents.md): コードレビュー、計画、ドキュメント作成など、特定の開発ロールやタスクに合わせた別のペルソナ向けに特化したcustom agentsを作成します。
* [**MCP servers**](/docs/copilot/customization/mcp-servers.md): Model Context Protocolを通じて外部ツールやサービスを統合し、カスタム機能でchatを拡張します。

## 効果的なプロンプトを書く

chatから最良の結果を得るために、プロンプトを書くときは次のヒントを意識してください。

* **`#`メンションでコンテキストを追加する**: 特定のファイル（`#file`）、コードベース（`#codebase`）、ターミナル出力（`#terminalSelection`）を参照します。chat入力欄で`#`を入力すると、利用可能なコンテキスト項目を確認できます。詳しくは、[プロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)を参照してください。

* **`/`コマンドを使用する**: `/`を入力して、`/new`や`/explain`などの一般的なコマンドにアクセスします。また、独自の[custom prompts](/docs/copilot/customization/prompt-files.md)を作成できます。

* **toolsを参照する**: `#`に続けてtool名を入力すると、chatの機能を拡張できます。たとえば、`#fetch`はWebコンテンツを取得し、`#githubRepo`はGitHubリポジトリを検索します。詳しくは、[chatでtoolsを追加して使用する](/docs/copilot/chat/chat-tools.md)を参照してください。

## 次のステップ

基本を理解したら、さらにchatの機能を試してみましょう。

* [複数のchatセッションを作成する](/docs/copilot/chat/chat-sessions.md)
* [プロンプトにコンテキストを追加して、より関連性の高い応答を得る](/docs/copilot/chat/copilot-chat-context.md)
* [MCPサーバーや拡張機能が提供するtoolsでchatの機能を拡張する](/docs/copilot/chat/chat-tools.md)

## 追加リソース

* コードベースの理解、コード生成、デバッグ、ノートブックでの作業など、一般的なタスクを扱う[chatプロンプトの例](/docs/copilot/chat/prompt-examples.md)を参考にしてください。

* [GitHub Copilot](https://github.com/features/copilot)の詳細と、VS Codeでの使い方については、[GitHub Copilotのドキュメント](https://docs.github.com/copilot/getting-started-with-github-copilot?tool=vscode)を参照してください。

* YouTubeの[VS Code Copilot Series](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)もご覧ください。Copilotを[Python](https://www.youtube.com/watch?v=DSHfHT5qnGc)、[C#](https://www.youtube.com/watch?v=VsUQlSyQn1E)、[Java](https://www.youtube.com/watch?v=zhCB95cE0HY)、[PowerShell](https://www.youtube.com/watch?v=EwtRzAFiXEM)、[C++](https://www.youtube.com/watch?v=ZfT2CXY5-Dc)などで使用するための、より入門的なコンテンツや言語別の動画を見つけられます。
