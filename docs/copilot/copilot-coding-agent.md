---
ContentId: f8b9e2a4-7c1d-4f5e-9a8b-3d2e1f0c6789
DateApproved: 12/10/2025
MetaDescription: VS CodeのGitHub Copilotコーディングエージェントと対話し、バックグラウンドでの自律的な機能の実装やバグ修正を行う方法について説明します。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilotコーディングエージェント

[GitHub Copilotコーディングエージェント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent)は、GitHubがホストする自律型AI開発者であり、バックグラウンドで独立して開発タスクを完遂します。コーディングエージェントを呼び出すには、GitHubのissueをCopilotに割り当てるか、チャットからタスクを委任します。すると、エージェントは自律的に機能の実装、バグの修正、独自の手順で分離された開発環境を使用してリポジトリ全体の変更を行います。

これはVS Codeの[エージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents)とは異なります。VS Codeのエージェントはエディター内でinteractiveな開発を提供するものであり、コーディングセッション中にユーザーの積極的な参加が必要です。

![VS Code内からCopilotコーディングエージェントにissueを割り当てる方法を示すGIF。](images/copilot-coding-agent/assign-to-copilot-gif.gif)

## 仕組み

Copilotコーディングエージェントのワークフロー：

1. **割り当て**: [`@copilot`にGitHubのissueを割り当てる](#method-1-assign-issues-to-copilot)、[VS Codeのチャットからタスクを委任する](#method-2-delegate-from-chat)、または[TODOコードアクションを使用する](#method-3-fix-todos-with-coding-agent)
1. **分析**: エージェントがタスクとリポジトリ構造を分析します
1. **開発**: Copilotは独自の分離されたGitHub Actions環境で動作し、以下を実行できます：
   * コードベースの探索
   * 複数のファイルにわたる変更
   * ビルドとテストの実行
   * リンターやその他の自動チェックの実行
1. **プルリクエスト**: エージェントは実装を含むプルリクエストを作成します
1. **レビュー**: 変更を確認し、PRのコメントを通じて修正を要求できます
1. **反復**: エージェントはフィードバックに応答し、実装を更新します

## 前提条件

Copilotコーディングエージェントを使用する前に、以下が必要です：

* **GitHub Copilotサブスクリプション**: Copilot Pro、Pro+、Business、またはEnterpriseプランで使用可能です
* **書き込みアクセス権**: リポジトリへの書き込み権限が必要です
* **エージェントの有効化**: Copilotコーディングエージェントがアカウントまたは組織で[有効になっている必要があります](https://docs.github.com/copilot/concepts/coding-agent/enable-coding-agent)
* **VS Codeのセットアップ**: [GitHub Pull Requests拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)をインストールします

正しいGitHubアカウントでGitHub Pull Request拡張機能にサインインしていることを確認してください。

![アカウントメニューのスクリーンショット、GitHub Pull Requestへのサインインアクションを強調表示。](images/copilot-coding-agent/sign-in-github-pull-requests.png)

**オプション**: 実験的な設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にして、Copilot Chatに**Delegate to coding agent**ボタンを表示し、タスクの委任を容易にします。

また、実験的な設定`setting(chat.agentSessionsViewLocation)`を有効にすることで、専用のチャットエディターからコーディングエージェントセッションを管理し、**Chat Sessions**ビューを表示することもできます。

> [!TIP]
> まだCopilotにアクセスできない場合は、[Copilotの無料プラン](https://github.com/features/copilot/plans)にサインアップして、月ごとのインタラクション制限を取得できます。

## VS CodeでCopilotコーディングエージェントに作業を割り当てる

### 方法1: Copilotにissueを割り当てる

チームメンバーにissueを割り当てるのと同様に、GitHubのissueをCopilotに割り当てることで、Copilotコーディングエージェントをトリガーできます。Copilotコーディングエージェントは自動的にissueを分析し、作業を開始します。

1. **GitHub Pull Requests**ビューで、**Issues**セクションに移動します

1. Copilotに割り当てたいissueを見つけます

1. issueを右クリックして**Assign to Copilot**を選択するか、**Assign**を選択してから`@copilot`を選択します

   > [!TIP]
   > GitHub.comで直接`@copilot`にissueを割り当てることもできます。コーディングエージェントは同様に機能し、VS CodeまたはGitHubでレビューできるプルリクエストを作成します。

1. エージェントはバックグラウンドでissueの作業を開始します

1. VS Codeでチャットビューを開きます(`kb(workbench.action.chat.open)`)
   ![GitHub Pull Requestsビューのスクリーンショット、Copilotへの割り当てアクションとCopilotに割り当てられた作業のPRクエリを強調表示。](images/copilot-coding-agent/github-pull-request-coding-agent.png)

### 方法2: チャットからの委任

また、チャットでの会話から直接Copilotコーディングエージェントに作業を引き渡すこともできます。エディターですぐに変更を実装させるのではなく、タスクをコーディングエージェントに委任して、バックグラウンドで自律的に作業させることができます。

1. VS Codeでチャットビューを開きます(`kb(workbench.action.chat.open)`)

1. 実装したい機能や変更について会話します

1. 準備ができたら、以下のいずれかの方法を使用してエージェントに委任します：

   **委任ボタンを使用する (実験的)**

   実験的な設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にすると、エージェントが有効になっているリポジトリのチャットビューに**Delegate to coding agent**ボタンが表示されます。このボタンを選択して、現在のチャットコンテキストをコーディングエージェントに引き渡します。

   タスクを委任すると、ファイル参照を含む追加のコンテキストがコーディングエージェントに転送され、完了すべきタスクを正確に計画できます。新しいチャットエディターが開き、コーディングエージェントの進行状況がリアルタイムで表示されます。

   <video src="images/copilot-coding-agent/delegate-to-coding-agent.mp4" title="VS Codeチャットからコーディングエージェントに委任する方法を示すビデオ。" controls poster="images/copilot-coding-agent/delegate-to-coding-agent-poster.png"></video>

   **#copilotCodingAgentツールを使用する**

   プロンプトで直接`#copilotCodingAgent`ツールを参照して、Copilotにローカルの変更をバックグラウンドで継続するように依頼することもできます。このツールは、保留中の変更をリモートブランチに自動的にプッシュし、コーディングエージェントセッションを開始します：

   ![Copilotコーディングエージェントへのセッション引き渡しを示すスクリーンショット](images/copilot-coding-agent/coding-agent-start.png)

1. エージェントはプルリクエストを作成し、話し合われた変更の実装を開始します。コーディングエージェントセッションを開始すると(``#copilotCodingAgent`を使用するか、**Delegate to coding agent**アクションを使用)、プルリクエストはチャットビューにカードとしてレンダリングされます。

   ![チャットビュー内のコーディングエージェントPRカードのスクリーンショット。](images/copilot-coding-agent/pr-card-in-chat.png)

### 方法3: コーディングエージェントを使用したTODOの修正

コード内の`TODO`で始まるコメントに、コーディングエージェントセッションを素早く開始するためのCode Actionが表示されるようになりました。これにより、コードから直接特定のタスクを委任する便利な方法が提供されます。

> [!TIP]
> `TODO`キーワードは`setting(githubIssues.createIssueTriggers)`設定で構成可能です。コーディングエージェントのCode Actionをトリガーするコメントキーワードをカスタマイズできます。

1. コード内の`TODO`コメントに移動します

1. 電球アイコンを探すか、`kb(editor.action.quickFix)`を使用してQuick Fixメニューを開きます

1. 利用可能なCode Actionから**Delegate to coding agent**を選択します

   !['Delegate to coding agent'という'TODO'コメントの上にあるコードアクションのスクリーンショット](images/copilot-coding-agent/coding-agent-todo.png)

1. コーディングエージェントはTODOコメントを分析し、新しいプルリクエストで要求された変更を実装します

## エージェントの進行状況の追跡

### コーディングエージェントのワークフローを理解する

Copilotコーディングエージェントに作業を割り当てると、期待とは異なる特定のワークフローに従う場合があります：

1. **初期プルリクエストの作成**: エージェントはすぐに初期の空のコミットでプルリクエストを作成します。これにより、すべての変更が行われるワークスペースとブランチが確立されます。

2. **バックグラウンド処理**: コーディングエージェントはローカルマシンではなく、GitHubのクラウドインフラストラクチャ（GitHub Actions環境）で動作します。つまり：
   * すべての開発はGitHubのサーバー上でリモートで行われます
   * エージェントは完全なリポジトリコンテキストにアクセスできます
   * VS Codeを閉じても作業は継続します

3. **増分更新**: 初期コミットの後、エージェントはソリューションを開発するにつれて、実際のコード変更を含む追加のコミットをプッシュします。

> [!NOTE]
> 変更のない初期コミットが表示される場合、これは期待される動作です。エージェントはタスクに取り組むにつれて、実際のコード変更を後続のコミットでプッシュし続けます。

### VS Codeでの作業の監視

GitHub Pull Requests拡張機能には、以下を表示する専用の**Copilot on My Behalf**セクションがあります：

* すべてのアクティブなCopilotコーディングエージェントセッション
* エージェントによって作成されたプルリクエスト
* 各タスクの進行状況ステータス
* 新しい変更または更新を示す数値バッジ

![複数のコーディングエージェントのプルリクエストのステータスを示すスクリーンショット](images/copilot-coding-agent/coding-agent-status.png)

> [!TIP]
> GitHub.comを通じて`@copilot`に割り当てた作業も監視できます。すべてのアクティブなセッションとプルリクエストは、開始場所に関係なく、このセクションに表示されます。

### 詳細なセッションログの表示

1. Pull Requestsビューで、**Copilot on My Behalf**の下にあるエージェントの作業を見つけます

1. **View Session**を選択して、エージェントが行ったすべての詳細なログを確認します：
   * 実行されたコマンド
   * 変更されたファイル
   * 実行されたテスト
   * 意思決定プロセス

   ![コーディングエージェントセッションのログを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-session-log.png)

### 専用チャットエディターによるセッションの管理（実験的）

専用のチャットエディターからコーディングエージェントセッションを管理できます。これにより、以下のことが可能になります：

* コーディングエージェントの進行状況をリアルタイムで追跡する
* チャットから直接フォローアップの指示を提供する
* 専用の環境でエージェントの応答を確認する
* チャットエディターから直接コード変更を表示または適用し、プルリクエストをチェックアウトする
* 継続性が向上したローカルチャットからGitHubエージェントタスクへのシームレスな移行を体験する
* Improved visual clarityによるより良いセッションレンダリングの恩恵を受ける
* より応答性の高い体験のための高速なセッション読み込みを楽しむ

この機能を試すには、実験的な設定`setting(chat.agentSessionsViewLocation)`を有効にします：

* `view`に設定すると、VS Codeのサイドバーにローカルおよびコーディングエージェントセッションを管理するための**Chat Sessions**ビューが表示されます。ビューには、関連情報をすばやく見つけるのに役立つ詳細なコンテキストを含むリッチな説明が含まれるようになりました。

   ![コーディングエージェントビューを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-view.png)

* `showChatsMenu`に設定すると、コーディングエージェントセッションがローカルチャット履歴と一緒に表示されます

   ![コーディングエージェントセッションクイックピックを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-quick-pick.png)

セッションを開始すると、コーディングエージェントによって作成されたプルリクエストもチャットビューにカードとしてレンダリングされ、視覚的な統合が向上します。

<!-- <video src="images/copilot-coding-agent/chat-sessions-view.mp4" title="Video showing Chat Sessions view and integration with GitHub coding agents." autoplay loop controls muted></video> -->

### 委任体験の向上

VS CodeからGitHubコーディングエージェントへの委任体験は、最近のアップデートで大幅に強化されました：

* **コンテキスト転送の改善**: チャットからタスクを委任すると、ファイル参照を含む追加のコンテキストが自動的にGitHubコーディングエージェントに転送されます
* **リアルタイムの進行状況**: 新しいチャットエディターが開き、コーディングエージェントの進行状況がリアルタイムで表示されます
* **シームレスな移行**: ローカルチャットからGitHubエージェントタスクへの移動時の継続性が向上しました
* **視覚的統合の強化**: プルリクエストは、より良いナビゲーションのためにチャットビューでインタラクティブなカードとしてレンダリングされます

これらの改善により、VS Codeを離れることなく、コーディングエージェントのタスクを正確に計画し、進行状況を監視することが容易になります。

### 実行中のセッションのキャンセル

エージェントを停止する必要がある場合は、VS Codeにとどまり、PR概要ページの**Cancel coding agent**ボタンを使用できます。

GitHub.comからセッションをキャンセルすることもできます：

1. GitHub.comのGitHubリポジトリに移動します
1. **Actions**タブに移動します
1. 実行中のCopilot Coding Agentワークフローを見つけます
1. **Cancel workflow**を選択します

## レビューと反復

### 作業完了

Copilotコーディングエージェントがコードを分析し、タスクを達成するために必要な変更を決定した後、次の手順を実行します：

* すべての変更を含むプルリクエストを作成する
* レビューのためにPRをあなたに割り当てる
* レビュアーとしてあなたをリクエストする
* 実装を説明する詳細な説明を含める
* 該当する場合、スクリーンショットを追加する（UIの変更の場合）

![実装された機能のスクリーンショットを含む、VS Codeに表示されたCopilotコーディングエージェントからのプルリクエストを示すスクリーンショット。](images/copilot-coding-agent/draft-with-screenshot.png)

### フィードバックの提供

プルリクエストのコメントを通じてエージェントの作業をガイドできます。エージェントが応答するように、コメントで`@copilot`をタグ付けしてください：

1. **変更のリクエスト**: 変更が必要な点について具体的なフィードバックを残します

   ```text
   @copilot ログインフォームを更新して、パスワードの強度検証を含めてください
   ```

1. **改善のリクエスト**: 追加の機能や改良を求めます

   ```text
   @copilot ネットワークタイムアウトのエラー処理を追加できますか？
   ```

エージェントはフィードバックに応答し、要求された変更を行い、プルリクエストを更新します。

> [!TIP]
> コーディングエージェントによって作成されたプルリクエストを操作する場合、`#activePullRequest`ツールがチャットセッションで自動的に有効になります。これにより、変更されたファイル、割り当てられたユーザー、ステータス（ドラフトまたはレビュー準備完了）など、PRに関するチャットコンテキストが得られます。その後、このPRについて質問し、チャットでさらに反復することができます。

## よくある質問

### Copilotコーディングエージェントとエージェントの使用の違いは何ですか？

VS Codeは2つの自律的なコーディング体験を提供します。VS Codeのエージェントの使用はエディター内で直接interactiveな開発を提供しますが、CopilotコーディングエージェントはGitHub上で独立して機能し、バックグラウンドで機能を実装します。

| 機能 | Copilotコーディングエージェント | エージェントの使用 |
|---------|---------------------|------------------|
| **実行場所** | GitHubクラウド | VS Codeエディター |
| **独立性** | 完全に自律的 | ユーザーの対話と反復が必要 |
| **出力** | プルリクエストを作成 | ファイルを直接編集 |
| **最適** | 定義されたタスク、バックグラウンド作業 | interactiveな開発、即時フィードバック |

[VS Codeでのエージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents)について詳しくはこちらをご覧ください。

### エージェントが開始されないのはなぜですか？

* GitHubアカウントのCopilotアクセス権を確認してください
* リポジトリへの書き込み権限があることを確認してください
* Copilotコーディングエージェントが組織で有効になっていることを確認してください

### 初期コミットが空に見えるのはなぜですか？

Copilotコーディングエージェントが作業を開始すると、プルリクエストと作業ブランチを確立するために初期の空のコミットを作成します。これは期待される動作です。エージェントはGitHubのクラウド環境で作業するため、実際のコード変更を含む後続のコミットをプッシュします。

進行状況は、プルリクエスト、GitHub Pull Request拡張機能の**Copilot on My Behalf**セクション、またはChat Sessionsビューからアクセスできるセッションログを通じて監視できます。

### 実装が不完全なのはなぜですか？

* 発生したエラーについてセッションログを確認してください
* エージェントの作業中にテストが失敗したかどうかを確認してください
* issueの説明により詳細な要件を提供してください

### Copilotコーディングエージェントにはどのようなセキュリティ保護がありますか？

Copilotコーディングエージェントには組み込みのセキュリティ保護が含まれており、GitHubのセキュリティフレームワーク内で動作します。セキュリティ対策、権限、およびブランチ保護の互換性の詳細については、[GitHub Copilotコーディングエージェントのセキュリティドキュメント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent#built-in-security-protections)を参照してください。

### 外部ツールを使用してCopilotコーディングエージェントを拡張できますか？

高度なシナリオの場合、Model Context Protocol (MCP)サーバーを使用してCopilotコーディングエージェントを拡張し、以下へのアクセスを許可できます：

* 外部データベース
* クラウドサービス
* APIおよびサードパーティ統合
* カスタム開発ツール

[MCPを使用したCopilotコーディングエージェントの拡張](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/extending-copilot-coding-agent-with-mcp)について詳しくはこちらをご覧ください。

### 現在の制限は何ですか？

* **クロスリポジトリの変更**: issueが割り当てられているリポジトリ内でのみ機能します
* **タスクごとの複数のPR**: 割り当てられたタスクごとに正確に1つのプルリクエストを開きます
* **既存のPRの変更**: 作成していないプルリクエストでは機能しません

制限、互換性、および使用コストの詳細については、[GitHub Copilotコーディングエージェントのドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)を参照してください。

## 次のステップ

* [GitHubセットアップガイド](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/enabling-copilot-coding-agent)に従ってCopilotコーディングエージェントを有効にする
* 即時かつinteractiveなコーディング支援のために[VS Codeチャットのエージェント](/docs/copilot/chat/copilot-chat.md)を試す

## 関連リソース

* [GitHub Copilotコーディングエージェントのドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)
* [GitHub Pull Requests拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
* [チャットセッションの管理](/docs/copilot/chat/chat-sessions.md)
