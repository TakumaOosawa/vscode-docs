---
ContentId: f8b9e2a4-7c1d-4f5e-9a8b-3d2e1f0c6789
DateApproved: 12/10/2025
MetaDescription: VS CodeでGitHub Copilot coding agentとやり取りし、バックグラウンドで自律的に機能を実装し、バグを修正する方法について説明します。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot coding agent

[GitHub Copilot coding agent](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent)は、GitHubでホストされる自律型AI開発者で、バックグラウンドで独立して動作し、開発タスクを完了します。coding agentを呼び出すには、GitHub issueをCopilotに割り当てるか、チャットからタスクを委任します。すると、エージェントは自律的に機能の実装、バグの修正、独自の分離された開発環境を使用したリポジトリ全体にわたる変更を行います。

これはVS Codeでの[エージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents)とは異なります。VS Codeのエージェントはエディター内で対話的な開発を提供し、コーディング セッション中の積極的な参加が必要です。

![VS Code内からissueをCopilot coding agentに割り当てる方法を示すGIF。](images/copilot-coding-agent/assign-to-copilot-gif.gif)

## 仕組み

Copilot coding agentのワークフロー:

1. **割り当て**: [GitHub issueを`@copilot`に割り当てる](#method-1-assign-issues-to-copilot)、[VS Codeチャットからタスクを委任する](#method-2-delegate-from-chat)、または[TODOコード アクションを使用する](#method-3-fix-todos-with-coding-agent)
1. **分析**: エージェントがタスクとリポジトリ構造を分析します
1. **開発**: Copilotは、独自の分離されたGitHub Actions環境で作業します。ここでは次のことが可能です:
   * Explore your codebase
   * Make changes across multiple files
   * Run builds and tests
   * Execute linters and other automated checks
1. **プル リクエスト**: エージェントが実装を含むプル リクエストを作成します
1. **レビュー**: 変更をレビューし、PRコメントで修正を依頼できます
1. **反復**: エージェントがフィードバックに応答し、実装を更新します

## 前提条件

Copilot coding agentを使用する前に、次が必要です:

* **GitHub Copilotサブスクリプション**: Copilot Pro、Pro+、Business、またはEnterpriseプランで利用できます
* **書き込みアクセス**: リポジトリへの書き込み権限が必要です
* **エージェントの有効化**: アカウントまたは組織でCopilot coding agentを[有効にする必要があります](https://docs.github.com/copilot/concepts/coding-agent/enable-coding-agent)
* **VS Codeのセットアップ**: [GitHub Pull Requests拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)をインストールします

GitHub Pull Requests拡張機能に、正しいGitHubアカウントでサインインしていることを確認してください。

![アカウント メニューのスクリーンショット。GitHub Pull Requestへのサインイン アクションが強調表示されています。](images/copilot-coding-agent/sign-in-github-pull-requests.png)

**任意**: 実験的な設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にすると、Copilot Chatに**Delegate to coding agent**ボタンが表示され、タスクの委任がより簡単になります。

また、実験的な設定`setting(chat.agentSessionsViewLocation)`を有効にすると、専用のチャット エディターからcoding agentセッションを管理でき、**Chat Sessions**ビューを表示できます。

> [!TIP]
> まだCopilotにアクセスできない場合は、[Copilot Freeプラン](https://github.com/features/copilot/plans)に登録して、月ごとの対話回数の上限を利用できます。

## VS CodeでCopilot coding agentに作業を割り当てる

### Method 1: Assign issues to Copilot

チーム メンバーにissueを割り当てるのと同様に、GitHub issueをCopilotに割り当てることでCopilot coding agentをトリガーできます。Copilot coding agentはissueを自動的に分析し、作業を開始します。

1. **GitHub Pull Requests**ビューで、**Issues**セクションに移動します

1. Copilotに割り当てたいissueを見つけます

1. issueを右クリックして**Assign to Copilot**を選択するか、**Assign**を選択してから`@copilot`を選択します

   > [!TIP]
   > GitHub.com上でissueを直接`@copilot`に割り当てることもできます。coding agentは同じように動作し、プル リクエストを作成します。その後、そのプル リクエストをVS CodeまたはGitHubでレビューできます。

1. エージェントがバックグラウンドでissueの作業を開始します

1. VS Codeでチャット ビューを開きます(`kb(workbench.action.chat.open)`)
   ![GitHub Pull Requestsビューのスクリーンショット。Copilotへの割り当てアクションと、Copilotに割り当てられた作業のPRクエリが強調表示されています。](images/copilot-coding-agent/github-pull-request-coding-agent.png)

### Method 2: Delegate from chat

チャットの会話から直接Copilot coding agentに作業を引き継ぐこともできます。エージェントがエディターですぐに変更を実装するのではなく、タスクをcoding agentに委任し、バックグラウンドで自律的に作業させることができます。

1. VS Codeでチャット ビューを開きます(`kb(workbench.action.chat.open)`)

1. 実装したい機能や変更について会話します

1. 準備ができたら、次のいずれかの方法でエージェントに委任します:

   **Use the delegate button (Experimental)**

   実験的な設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にすると、エージェントが有効になっているリポジトリのチャット ビューに**Delegate to coding agent**ボタンが表示されます。このボタンを選択すると、現在のチャット コンテキストをcoding agentに引き継げます。

   タスクを委任すると、ファイル参照などの追加コンテキストがcoding agentに転送されるため、coding agentが完了すべきタスクを正確に計画できます。coding agentの進捗がリアルタイムで表示される新しいチャット エディターが開きます。

   <video src="images/copilot-coding-agent/delegate-to-coding-agent.mp4" title="VS Codeチャットからcoding agentに委任する方法を示す動画。" controls poster="images/copilot-coding-agent/delegate-to-coding-agent-poster.png"></video>

   **Use the #copilotCodingAgent tool**

   プロンプト内で`#copilotCodingAgent`ツールを直接参照して、Copilotにローカルの変更をバックグラウンドで継続するよう依頼することもできます。このツールは、保留中の変更をリモート ブランチに自動的にプッシュし、coding agentセッションを開始します:

   ![Copilot coding agentにセッションを引き継ぐ様子を示すスクリーンショット](images/copilot-coding-agent/coding-agent-start.png)

1. エージェントがプル リクエストを作成し、話し合った変更の実装を開始します。(`#copilotCodingAgent`または**Delegate to coding agent**アクションで)coding agentセッションを開始すると、プル リクエストがチャット ビューにカードとしてレンダリングされます。

   ![チャット ビューに表示されたcoding agentのPRカードのスクリーンショット。](images/copilot-coding-agent/pr-card-in-chat.png)

### Method 3: Fix TODOs with coding agent

コード内の`TODO`で始まるコメントに、coding agentセッションをすばやく開始するためのコード アクションが表示されるようになりました。これにより、コードから直接、特定のタスクを便利に委任できます。

> [!TIP]
> `TODO`キーワードは`setting(githubIssues.createIssueTriggers)`設定で構成できます。coding agentのコード アクションをトリガーするコメント キーワードをカスタマイズできます。

1. コード内の`TODO`コメントに移動します

1. 電球アイコンを探すか、`kb(editor.action.quickFix)`を使用してクイック フィックス メニューを開きます

1. 利用可能なコード アクションから**Delegate to coding agent**を選択します

   !['TODO'コメントの上に表示された'有限なコード アクション'のうち、'Delegate to coding agent'という項目のスクリーンショット](images/copilot-coding-agent/coding-agent-todo.png)

1. coding agentがTODOコメントを分析し、依頼された変更を新しいプル リクエストで実装します

## エージェントの進捗を追跡する

### coding agentのワークフローを理解する

Copilot coding agentに作業を割り当てると、想定と異なる可能性のある特定のワークフローに従います:

1. **初期プル リクエストの作成**: エージェントは、最初に空のコミットを含むプル リクエストを即座に作成します。これにより、以降の変更がすべて行われるワークスペースとブランチが確立されます。

2. **バックグラウンド処理**: coding agentはローカル マシンではなく、GitHubのクラウド インフラストラクチャ(GitHub Actions環境)で動作します。つまり:
   * All development happens remotely on GitHub's servers
   * The agent has access to the full repository context
   * Work continues even when you close VS Code

3. **段階的な更新**: 初期コミットの後、エージェントはソリューションを開発しながら、実際のコード変更を含む追加のコミットをプッシュします。

> [!NOTE]
> 変更のない初期コミットが表示されても、これは想定どおりの動作です。エージェントはタスクに取り組む中で、後続のコミットで実際のコード変更をプッシュし続けます。

### VS Codeで作業を監視する

GitHub Pull Requests拡張機能には、次を表示する専用の**Copilot on My Behalf**セクションがあります:

* All active Copilot coding agent sessions
* Pull requests created by the agent
* Progress status for each task
* Numeric badges indicating new changes or updates

![複数のcoding agentプル リクエストの状態を示すスクリーンショット](images/copilot-coding-agent/coding-agent-status.png)

> [!TIP]
> GitHub.comを通じて`@copilot`に割り当てた作業も監視できます。開始場所に関係なく、アクティブなセッションとプル リクエストはすべてこのセクションに表示されます。

### 詳細なセッション ログを表示する

1. Pull Requestsビューで、**Copilot on My Behalf**の下にあるエージェントの作業を見つけます

1. **View Session**を選択して、エージェントが行ったすべての詳細ログを表示します:
   * Commands executed
   * Files modified
   * Tests run
   * Decision-making process

   ![coding agentセッションのセッション ログを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-session-log.png)

### 専用のチャット エディターでセッションを管理する(実験的)

専用のチャット エディターからcoding agentセッションを管理すると、次のことができます:

* Follow the progress of the coding agent in real-time
* Provide follow-up instructions directly from chat
* See the agent's responses in a dedicated environment
* View or apply code changes and check out pull requests directly from the chat editor
* Experience seamless transitions from local chats to GitHub agent tasks with improved continuity
* Benefit from better session rendering with improved visual clarity
* Enjoy faster session loading for a more responsive experience

この機能を試すには、実験的な設定`setting(chat.agentSessionsViewLocation)`を有効にします:

* `view`に設定すると、VS Codeのサイド バーに**Chat Sessions**ビューが表示され、ローカル セッションとcoding agentセッションを管理できます。このビューには、関連情報をすばやく見つけるのに役立つ詳細なコンテキストを含むリッチな説明が含まれるようになりました。

   ![Coding Agentsビューを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-view.png)

* `showChatsMenu`に設定すると、coding agentセッションがローカルのチャット履歴と並んで表示されます

   ![Coding Agent Sessionsのクイック ピックを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-quick-pick.png)

coding agentが作成したプル リクエストは、セッション開始時にチャット ビューにカードとしてレンダリングされ、視覚的な統合が改善されます。

<!-- <video src="images/copilot-coding-agent/chat-sessions-view.mp4" title="Video showing Chat Sessions view and integration with GitHub coding agents." autoplay loop controls muted></video> -->

### Improved delegation experience

VS CodeからGitHub coding agentへの委任エクスペリエンスは、最近の更新で大幅に改善されました:

* **Better context forwarding**: When you delegate a task from chat, additional context including file references are automatically forwarded to the GitHub coding agent
* **Real-time progress**: New chat editor opens showing the coding agent's progress in real-time
* **Seamless transitions**: Improved continuity when moving from local chats to GitHub agent tasks
* **Enhanced visual integration**: Pull requests are rendered as interactive cards in the Chat view for better navigation

これらの改善により、VS Codeを離れることなく、coding agentのタスクを正確に計画し、進捗を監視しやすくなります。

### 実行中のセッションをキャンセルする

エージェントを停止する必要がある場合は、VS CodeでPRの概要ページにある**Cancel coding agent**ボタンを使用できます。

GitHub.comからセッションをキャンセルすることもできます:

1. GitHub.comでGitHubリポジトリに移動します
1. **Actions**タブに移動します
1. 実行中のCopilot Coding Agentワークフローを見つけます
1. **Cancel workflow**を選択します

## レビューと反復

### 作業の完了

Copilot coding agentがコードを分析し、タスクを達成するために必要な変更を特定した後、次の手順を実行します:

* Create a pull request with all changes
* Assign the PR to you for review
* Request you as a reviewer
* Include a detailed description explaining the implementation
* Add screenshots when applicable (for UI changes)

![実装された機能のスクリーンショットが含まれたCopilot coding agentのプル リクエストがVS Codeに表示されている様子を示すスクリーンショット。](images/copilot-coding-agent/draft-with-screenshot.png)

### フィードバックを提供する

プル リクエストのコメントを通じて、エージェントの作業を誘導できます。コメントで`@copilot`をタグ付けして、エージェントが応答するようにしてください:

1. **変更の依頼**: 修正が必要な内容について具体的なフィードバックを残します

   ```text
   @copilot Please update the login form to include password strength validation
   ```

1. **改善の依頼**: 追加機能や改善を依頼します

   ```text
   @copilot Can you add error handling for network timeouts?
   ```

エージェントはフィードバックに応答し、依頼された変更を行い、プル リクエストを更新します。

> [!TIP]
> coding agentが作成したプル リクエストで作業している場合、チャット セッションでは`#activePullRequest`ツールが自動的に有効になります。これにより、変更されたファイル、担当者、状態(ドラフトまたはレビュー可能)など、PRに関するチャット コンテキストが得られます。その後、このPRについて質問し、チャットでさらに反復できます。

## よくある質問

### Copilot coding agentとエージェントの使用の違いは何ですか?

VS Codeには、2つの自律的なコーディング エクスペリエンスがあります。VS Codeでのエージェントの使用はエディター内で直接対話的な開発を提供しますが、Copilot coding agentはGitHub上で独立して動作し、バックグラウンドで機能を実装します。

| Feature | Copilot coding agent | Using agents |
|---------|---------------------|------------------|
| **Where it runs** | GitHub cloud | Your VS Code editor |
| **Independence** | Fully autonomous | Involves user interaction and iteration |
| **Output** | Creates pull requests | Edits files directly |
| **Best for** | Well-defined tasks, background work | Interactive development, immediate feedback |

詳しくは、[VS Codeでのエージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents)をご覧ください。

### エージェントが開始しないのはなぜですか?

* Verify Copilot access on your GitHub account
* Ensure you have write permissions to the repository
* Check that Copilot coding agent is enabled for your organization

### 初期コミットが空に見えるのはなぜですか?

Copilot coding agentが作業を開始すると、プル リクエストと作業ブランチを確立するために、初期の空のコミットを作成します。これは想定どおりの動作です。エージェントはGitHubのクラウド環境で作業しながら、後続のコミットで実際のコード変更をプッシュします。

進捗は、プル リクエストからアクセスできるセッション ログ、GitHub Pull Requests拡張機能の**Copilot on My Behalf**セクション、またはChat Sessionsビューで監視できます。

### 実装が不完全なのはなぜですか?

* Review the session logs for any errors encountered
* Check if tests failed during the agent's work
* Provide more detailed requirements in your issue description

### Copilot coding agentにはどのようなセキュリティ保護がありますか?

Copilot coding agentには組み込みのセキュリティ保護が含まれ、GitHubのセキュリティ フレームワーク内で動作します。セキュリティ対策、アクセス許可、ブランチ保護との互換性の詳細については、[GitHub Copilot coding agentのセキュリティ ドキュメント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent#built-in-security-protections)をご覧ください。

### Copilot coding agentを外部ツールで拡張できますか?

高度なシナリオでは、Model Context Protocol(MCP)サーバーでCopilot coding agentを拡張し、次へのアクセスを付与できます:

* External databases
* Cloud services
* APIs and third-party integrations
* Custom development tools

詳しくは、[MCPでCopilot coding agentを拡張する](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/extending-copilot-coding-agent-with-mcp)をご覧ください。

### 現在の制限事項は何ですか?

* **Cross-repository changes**: Can only work within the repository where the issue is assigned
* **Multiple PRs per task**: Opens exactly one pull request per assigned task
* **Existing PR modifications**: Cannot work on pull requests it didn't create

制限事項、互換性、使用コストの詳細については、[GitHub Copilot Coding Agentドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)をご覧ください。

## 次の手順

* [GitHubセットアップ ガイド](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/enabling-copilot-coding-agent)に従ってCopilot coding agentを有効にします
* すぐに使える対話的なコーディング支援として、[VS Codeチャットのエージェント](/docs/copilot/chat/copilot-chat.md)を試します

## 関連リソース

* [GitHub Copilot coding agentドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)
* [GitHub Pull Requests拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
* [チャット セッションの管理](/docs/copilot/chat/chat-sessions.md)
