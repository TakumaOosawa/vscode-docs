---
ContentId: f8b9e2a4-7c1d-4f5e-9a8b-3d2e1f0c6789
DateApproved: 3/9/2026
MetaDescription: VS CodeでGitHub Copilot coding agentを使い、バックグラウンドで自律的に機能実装やバグ修正を進める方法を説明します。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot coding agent

[GitHub Copilot coding agent](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent)は、開発タスクを完了するためにバックグラウンドで独立して動く、GitHubホストの自律型AI開発者です。coding agentを呼び出すには、GitHub issueをCopilotに割り当てるか、チャットからタスクを委任します。すると、エージェントは専用の分離された開発環境を使って、自律的に機能実装やバグ修正、リポジトリ全体にまたがる変更を進めます。

これは、エディター内で対話しながら開発を進め、コーディングセッション中にあなたの積極的な参加が必要な、VS Codeでの[エージェントの利用](/docs/copilot/agents/local-agents.md)とは異なります。

![VS Code内からissueをCopilot coding agentに割り当てる方法を示すGIF。](images/copilot-coding-agent/assign-to-copilot-gif.gif)

## 仕組み

Copilot coding agentの流れは次のとおりです。

1. **割り当て**: [GitHub issueを`@copilot`に割り当てる](#method-1-assign-issues-to-copilot)、[VS Codeチャットからタスクを委任する](#method-2-delegate-from-chat)、または[TODOのコードアクションを使う](#method-3-fix-todos-with-coding-agent)
1. **分析**: エージェントがタスクとリポジトリ構成を分析する
1. **開発**: Copilotは専用の分離されたGitHub Actions環境で作業し、次のことを行えます。
   * コードベースを調べる
   * 複数のファイルにまたがって変更する
   * ビルドとテストを実行する
   * linterやほかの自動チェックを実行する
1. **プルリクエスト**: 実装内容を含むプルリクエストをエージェントが作成する
1. **レビュー**: あなたが変更をレビューし、PRコメントで修正を依頼できる
1. **反復**: エージェントがフィードバックに応答し、実装を更新する

## 前提条件

Copilot coding agentを使うには、次の条件が必要です。

* **GitHub Copilotサブスクリプション**: Copilot Pro、Pro+、Business、Enterpriseプランで利用できます。
* **書き込みアクセス**: リポジトリへの書き込み権限が必要です。
* **エージェントの有効化**: アカウントまたは組織で、[Copilot coding agentを有効にしておく](https://docs.github.com/copilot/concepts/coding-agent/enable-coding-agent)必要があります。
* **VS Codeのセットアップ**: [GitHub Pull Requests拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)をインストールします。

GitHub Pull Requests拡張機能に、正しいGitHubアカウントでサインインしていることを確認してください。

![アカウントメニューでGitHub Pull Requestへのサインイン操作を強調表示したスクリーンショット。](images/copilot-coding-agent/sign-in-github-pull-requests.png)

**任意**: 実験的な設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にすると、Copilot Chatに**Delegate to coding agent**ボタンが表示され、タスクをより簡単に委任できます。

実験的な設定`setting(chat.agentSessionsViewLocation)`を有効にすると、専用のチャットエディターからcoding agentのセッションを管理したり、**Chat Sessions**ビューを表示したりすることもできます。

> [!TIP]
> まだCopilotを使えない場合は、[Copilot Freeプラン](https://github.com/features/copilot/plans)に登録すると、月ごとの上限付きで利用できます。

## VS CodeでCopilot coding agentに作業を割り当てる

### Method 1: Assign issues to Copilot

GitHub issueをチームメンバーに割り当てるのと同じように、Copilotに割り当てることでCopilot coding agentを開始できます。Copilot coding agentはissueを自動で分析し、作業を始めます。

1. **GitHub Pull Requests**ビューで、**Issues**セクションに移動します。

1. Copilotに割り当てるissueを見つけます。

1. issueを右クリックして**Assign to Copilot**を選ぶか、**Assign**を選んでから`@copilot`を選びます。

   > [!TIP]
   > GitHub.comでissueを直接`@copilot`に割り当てることもできます。その場合もcoding agentは同じように動作し、あとでVS CodeまたはGitHubでレビューできるプルリクエストを作成します。

1. エージェントがバックグラウンドでissueへの作業を始めます。

1. VS CodeでChatビューを開きます(`kb(workbench.action.chat.open)`)。
   ![GitHub Pull RequestsビューでAssign to Copilot操作と、Copilotに割り当てた作業用のPRクエリを強調表示したスクリーンショット。](images/copilot-coding-agent/github-pull-request-coding-agent.png)

### Method 2: Delegate from chat

チャットの会話から直接、作業をCopilot coding agentに引き継ぐこともできます。エージェントにその場でエディター内の変更を実装させる代わりに、タスクをcoding agentへ委任して、バックグラウンドで自律的に進めてもらえます。

1. VS CodeでChatビューを開きます(`kb(workbench.action.chat.open)`)。

1. 実装したい機能や変更について会話します。

1. 準備ができたら、次のいずれかの方法でエージェントに委任します。

   **委任ボタンを使う(実験的機能)**

   実験的な設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にすると、エージェントが有効なリポジトリではChatビューに**Delegate to coding agent**ボタンが表示されます。このボタンを選ぶと、現在のチャットコンテキストをcoding agentに引き継げます。

   タスクを委任すると、ファイル参照を含む追加のコンテキストがcoding agentに渡されるため、完了してほしい作業をより正確に計画できます。新しいチャットエディターが開き、coding agentの進行状況がリアルタイムで表示されます。

   <video src="images/copilot-coding-agent/delegate-to-coding-agent.mp4" title="VS Codeチャットからcoding agentに委任する方法を示す動画。" controls poster="images/copilot-coding-agent/delegate-to-coding-agent-poster.png"></video>

   **#copilotCodingAgentツールを使う**

   プロンプトで`#copilotCodingAgent`ツールを直接参照して、ローカルの変更の続き作業をバックグラウンドでCopilotに依頼することもできます。このツールは保留中の変更を自動的にリモートブランチへpushし、coding agentセッションを開始します。

   ![セッションをCopilot coding agentに引き継ぐ様子を示すスクリーンショット。](images/copilot-coding-agent/coding-agent-start.png)

1. エージェントがプルリクエストを作成し、話し合った変更の実装を始めます。coding agentセッションを開始すると(`#copilotCodingAgent`または**Delegate to coding agent**操作)、そのプルリクエストはChatビューでカードとして表示されます。

   ![Chatビューに表示されたcoding agentのPRカードのスクリーンショット。](images/copilot-coding-agent/pr-card-in-chat.png)

### Method 3: Fix TODOs with coding agent

コード内で`TODO`から始まるコメントには、coding agentセッションをすばやく始められるコードアクションが表示されるようになりました。これにより、コード上から特定のタスクを直接委任しやすくなります。

> [!TIP]
> `TODO`キーワードは`setting(githubIssues.createIssueTriggers)`設定で変更できます。どのコメントキーワードでcoding agentのコードアクションを表示するかをカスタマイズできます。

1. コード内の`TODO`コメントに移動します。

1. 電球アイコンを探すか、`kb(editor.action.quickFix)`を使ってQuick Fixメニューを開きます。

1. 表示されたコードアクションから**Delegate to coding agent**を選びます。

   ![TODOコメントの上に表示されたDelegate to coding agentというコードアクションのスクリーンショット。](images/copilot-coding-agent/coding-agent-todo.png)

1. coding agentがTODOコメントを分析し、求められている変更を新しいプルリクエストで実装します。

## エージェントの進行状況を追跡する

### coding agentの流れを理解する

Copilot coding agentに作業を割り当てると、次のような流れで進みます。想定と少し違って見える場合があります。

1. **最初のプルリクエスト作成**: エージェントはまず、空の初期コミットを含むプルリクエストをすぐに作成します。これで、以降の変更を行うワークスペースとブランチが用意されます。

2. **バックグラウンド処理**: coding agentはローカルマシンではなく、GitHubのクラウド基盤(GitHub Actions環境)で動作します。つまり、次のことを意味します。
   * すべての開発作業はGitHubのサーバー上でリモート実行される
   * エージェントはリポジトリ全体のコンテキストにアクセスできる
   * VS Codeを閉じても作業は続く

3. **段階的な更新**: 初期コミットのあと、エージェントは解決策を実装しながら実際のコード変更を含む追加コミットをpushします。

> [!NOTE]
> 変更のない初期コミットが見えても、それは想定どおりの動作です。エージェントはタスクを進めながら、そのあとに実際のコード変更を含むコミットを続けてpushします。

### VS Codeで作業を確認する

GitHub Pull Requests拡張機能には、次の情報を表示する専用の**Copilot on My Behalf**セクションがあります。

* アクティブなCopilot coding agentセッションの一覧
* エージェントが作成したプルリクエスト
* 各タスクの進行状況
* 新しい変更や更新を示す数値バッジ

![複数のcoding agentプルリクエストの状態を示すスクリーンショット。](images/copilot-coding-agent/coding-agent-status.png)

> [!TIP]
> GitHub.comから`@copilot`に割り当てた作業も確認できます。どこから開始したかに関係なく、アクティブなセッションとプルリクエストはすべてこのセクションに表示されます。

### 詳細なセッションログを表示する

1. Pull Requestsビューで、**Copilot on My Behalf**の下にあるエージェントの作業を見つけます。

1. **View Session**を選ぶと、エージェントが行ったすべての内容を詳しいログで確認できます。
   * 実行したコマンド
   * 変更したファイル
   * 実行したテスト
   * 判断の流れ

   ![coding agentセッションのログを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-session-log.png)

### 専用のチャットエディターでセッションを管理する(実験的機能)

専用のチャットエディターを使うと、coding agentのセッションを管理できます。次のことが可能です。

* coding agentの進行状況をリアルタイムで追う
* 追加の指示をチャットから直接送る
* エージェントの応答を専用の環境で確認する
* コード変更を表示または適用したり、プルリクエストを直接チェックアウトしたりする
* ローカルチャットからGitHub上のエージェントタスクへ、より自然に移行する
* より見やすいセッション表示を利用する
* セッションの読み込みが速くなり、より応答性の高い体験を得る

この機能を試すには、実験的な設定`setting(chat.agentSessionsViewLocation)`を有効にします。

* `view`に設定すると、VS Codeのサイドバーに**Chat Sessions**ビューが表示され、ローカルセッションとcoding agentセッションを管理できます。このビューには詳しいコンテキストを含む説明が表示されるため、必要な情報をすばやく見つけやすくなります。

   ![Coding Agentsビューを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-view.png)

* `showChatsMenu`に設定すると、coding agentセッションがローカルのチャット履歴と並んで表示されます。

   ![Coding Agent SessionsのQuick Pickを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-quick-pick.png)

coding agentが作成したプルリクエストは、セッション開始時にChatビューでもカードとして表示され、より自然に確認できます。

<!-- <video src="images/copilot-coding-agent/chat-sessions-view.mp4" title="Chat SessionsビューとGitHub coding agentの連携を示す動画。" autoplay loop controls muted></video> -->

### 委任体験の改善

最近の更新により、VS CodeからGitHub coding agentへ委任する体験が大きく改善されました。

* **より良いコンテキスト転送**: チャットからタスクを委任すると、ファイル参照を含む追加コンテキストが自動的にGitHub coding agentへ渡される
* **リアルタイムの進行表示**: 新しいチャットエディターが開き、coding agentの進行状況をリアルタイムで表示する
* **自然な移行**: ローカルチャットからGitHub上のエージェントタスクへ移るときのつながりが改善された
* **視覚的な統合の強化**: プルリクエストがChatビューで操作できるカードとして表示され、移動しやすくなった

これらの改善により、VS Codeを離れずにcoding agent向けのタスクをより正確に計画し、進行状況も確認しやすくなりました。

### 実行中のセッションをキャンセルする

エージェントを停止したい場合は、VS Codeを離れずにPRの概要ページで**Cancel coding agent**ボタンを使えます。

GitHub.comからセッションをキャンセルすることもできます。

1. GitHub.comで対象のGitHubリポジトリを開きます。
1. **Actions**タブに移動します。
1. 実行中のCopilot Coding Agentワークフローを見つけます。
1. **Cancel workflow**を選びます。

## レビューして改善を重ねる

### 作業の完了

Copilot coding agentはコードを分析し、タスク達成に必要な変更を判断すると、次の手順を実行します。

* すべての変更を含むプルリクエストを作成する
* レビューのためにPRをあなたへ割り当てる
* あなたをレビュアーとして追加する
* 実装内容を説明する詳しい説明を含める
* 必要に応じてスクリーンショットを追加する(UI変更の場合)

![VS Codeに表示されたCopilot coding agentのプルリクエストと、実装した機能のスクリーンショットを含む画面のスクリーンショット。](images/copilot-coding-agent/draft-with-screenshot.png)

### フィードバックを送る

プルリクエストのコメントを使ってエージェントの作業を導けます。エージェントが応答できるように、コメントには`@copilot`を含めてください。

1. **変更を依頼する**: 修正してほしい内容を具体的に書きます。

   ```text
   @copilot Please update the login form to include password strength validation
   ```

1. **改善を依頼する**: 機能追加や調整を依頼します。

   ```text
   @copilot Can you add error handling for network timeouts?
   ```

エージェントはフィードバックに応答し、求められた変更を行ってプルリクエストを更新します。

> [!TIP]
> coding agentが作成したプルリクエストを扱うときは、チャットセッションで`#activePullRequest`ツールが自動的に有効になります。これにより、変更されたファイル、割り当て先、状態(ドラフトかレビュー準備完了か)など、PRに関するコンテキストがチャットに渡されます。そのため、このPRについて質問したり、チャットでさらに改善を重ねたりできます。

## よくある質問

### Copilot coding agentとエージェントの利用は何が違いますか。

VS Codeには、自律的なコーディング体験が二つあります。VS Codeでエージェントを使う場合は、エディター内で直接やり取りしながら開発します。一方、Copilot coding agentはGitHub上で独立して動作し、バックグラウンドで機能を実装します。

| 機能 | Copilot coding agent | エージェントの利用 |
|---------|---------------------|------------------|
| **動作場所** | GitHubクラウド | あなたのVS Codeエディター |
| **自律性** | 完全に自律的 | ユーザーとのやり取りや反復がある |
| **成果物** | プルリクエストを作成する | ファイルを直接編集する |
| **向いている場面** | 要件が明確なタスク、バックグラウンド作業 | 対話しながらの開発、すぐに欲しいフィードバック |

[VS Codeでエージェントを使う方法](/docs/copilot/agents/local-agents.md)も参照してください。

### エージェントが始まらないのはなぜですか。

* GitHubアカウントでCopilotを利用できるか確認してください。
* リポジトリへの書き込み権限があることを確認してください。
* 組織でCopilot coding agentが有効になっているか確認してください。

### 最初のコミットが空に見えるのはなぜですか。

Copilot coding agentは作業を始めると、プルリクエストと作業ブランチを用意するために、最初に空のコミットを作成します。これは想定どおりの動作です。エージェントはGitHubのクラウド環境で作業を進めながら、そのあとに実際のコード変更を含むコミットをpushします。

進行状況は、プルリクエストから開けるセッションログ、GitHub Pull Requests拡張機能の**Copilot on My Behalf**セクション、またはChat Sessionsビューで確認できます。

### 実装が不完全なのはなぜですか。

* セッションログを見て、途中でエラーが起きていないか確認してください。
* エージェントの作業中にテストが失敗していないか確認してください。
* issueの説明に、より詳しい要件を書いてください。

### Copilot coding agentにはどのようなセキュリティ保護がありますか。

Copilot coding agentには組み込みのセキュリティ保護があり、GitHubのセキュリティフレームワーク内で動作します。セキュリティ対策、権限、ブランチ保護との互換性について詳しくは、[GitHub Copilot coding agentのセキュリティドキュメント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent#built-in-security-protections)を参照してください。

### Copilot coding agentを外部ツールで拡張できますか。

より高度なシナリオでは、Model Context Protocol(MCP)サーバーでCopilot coding agentを拡張し、次のものにアクセスさせることができます。

* 外部データベース
* クラウドサービス
* APIやサードパーティ統合
* カスタム開発ツール

[MCPでCopilot coding agentを拡張する方法](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/extending-copilot-coding-agent-with-mcp)も参照してください。

### 現在の制限事項は何ですか。

* **リポジトリをまたぐ変更**: issueを割り当てたリポジトリ内でしか作業できません。
* **タスクごとの複数PR**: 割り当てたタスクごとに、作成されるプルリクエストは一つだけです。
* **既存PRの変更**: 自分で作成していないプルリクエストでは作業できません。

制限事項、互換性、利用コストについて詳しくは、[GitHub Copilot Coding Agentのドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)を参照してください。

## 次のステップ

* [GitHubのセットアップガイド](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/enabling-copilot-coding-agent)に従ってCopilot coding agentを有効にする
* すぐに対話しながらコーディング支援を受けたい場合は、[VS Codeチャットのエージェント](/docs/copilot/chat/copilot-chat.md)を試す

## 関連情報

* [GitHub Copilot coding agentのドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)
* [GitHub Pull Requests拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
* [チャットセッションを管理する](/docs/copilot/chat/chat-sessions.md)
