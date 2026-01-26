---
ContentId: f8b9e2a4-7c1d-4f5e-9a8b-3d2e1f0c6789
DateApproved: 01/08/2026
MetaDescription: VS Code で GitHub Copilot coding agent と対話し、バックグラウンドで自律的に機能を実装したりバグを修正したりする方法について説明します。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot coding agent

[GitHub Copilot coding agent](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent)は、開発タスクを完了するためにバックグラウンドで独立して動作する、GitHub ホスト型の自律的な AI 開発者です。coding agent を呼び出すには、GitHub の issue を Copilot に割り当てるか、チャットからタスクを委任します。するとエージェントは自律的に機能の実装、バグの修正、独自に分離された開発環境を使用してリポジトリ全体の変更を行います。

これは、VS Code 内の[エージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents)とは異なります。VS Code 内のエージェントはエディター内で対話的な開発を提供し、コーディングセッション中にユーザーの積極的な参加を必要とします。

![VS Code 内から Copilot coding agent に issue を割り当てる方法を示す GIF。](images/copilot-coding-agent/assign-to-copilot-gif.gif)

## 仕組み

Copilot coding agent のワークフロー:

1. **割り当て**: [`@copilot` に GitHub issue を割り当てる](#method-1-assign-issues-to-copilot)、[VS Code チャットからタスクを委任する](#method-2-delegate-from-chat)、または [TODO コードアクションを使用する](#method-3-fix-todos-with-coding-agent)
1. **分析**: エージェントがタスクとリポジトリ構造を分析します
1. **開発**: Copilot は独自の分離された GitHub Actions 環境で動作し、以下のことが可能です:
   * コードベースの探索
   * 複数のファイルにわたる変更
   * ビルドとテストの実行
   * リンターやその他の自動チェックの実行
1. **プルリクエスト**: エージェントが実装を含むプルリクエストを作成します
1. **レビュー**: 変更をレビューし、PR コメントを通じて修正をリクエストできます
1. **反復**: エージェントはフィードバックに応答し、実装を更新します

## 前提条件

Copilot coding agent を使用する前に、以下が必要です:

* **GitHub Copilot サブスクリプション**: Copilot Pro、Pro+、Business、または Enterprise プランで利用可能
* **書き込みアクセス権**: リポジトリへの書き込み権限が必要です
* **エージェントの有効化**: アカウントまたは組織で Copilot coding agent が[有効になっている必要があります](https://docs.github.com/copilot/concepts/coding-agent/enable-coding-agent)
* **VS Code セットアップ**: [GitHub Pull Requests 拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)をインストールします

正しい GitHub アカウントで GitHub Pull Request 拡張機能にサインインしていることを確認してください。

![アカウントメニューを表示し、GitHub Pull Request へのサインインアクションを強調表示しているスクリーンショット。](images/copilot-coding-agent/sign-in-github-pull-requests.png)

**オプション**: 実験的な設定 `setting(githubPullRequests.codingAgent.uiIntegration)` を有効にすると、Copilot Chat に **Delegate to coding agent** ボタンが表示され、タスクの委任が容易になります。

また、実験的な設定 `setting(chat.agentSessionsViewLocation)` を有効にすると、専用のチャットエディターから coding agent セッションを管理し、**Chat Sessions** ビューを表示できます。

> [!TIP]
> まだ Copilot にアクセスできない場合は、[Copilot Free プラン](https://github.com/features/copilot/plans)にサインアップして、毎月の対話制限を得ることができます。

## VS Code で Copilot coding agent に作業を割り当てる

### 方法 1: Copilot に issue を割り当てる

チームメンバーに issue を割り当てるのと同じように、GitHub issue を Copilot に割り当てることで Copilot coding agent をトリガーできます。Copilot coding agent は自動的に issue を分析し、作業を開始します。

1. **GitHub Pull Requests** ビューで、**Issues** セクションに移動します

1. Copilot に割り当てたい issue を見つけます

1. issue を右クリックして **Assign to Copilot** を選択するか、**Assign** を選択してから `@copilot` を選択します

   > [!TIP]
   > GitHub.com で直接 `@copilot` に issue を割り当てることもできます。coding agent は同様に機能し、VS Code または GitHub 上でレビューできるプルリクエストを作成します。

1. エージェントはバックグラウンドで issue の作業を開始します

1. VS Code でチャットビューを開きます (`kb(workbench.action.chat.open)`)
   ![GitHub Pull Requests ビューを表示し、Copilot への割り当てアクションと、Copilot に割り当てられた作業の PR クエリを強調表示しているスクリーンショット。](images/copilot-coding-agent/github-pull-request-coding-agent.png)

### 方法 2: チャットから委任する

チャットの会話から直接 Copilot coding agent に作業を引き継ぐこともできます。エージェントにエディターですぐに変更を実装させるのではなく、coding agent にタスクを委任してバックグラウンドで自律的に作業させることができます。

1. VS Code でチャットビューを開きます (`kb(workbench.action.chat.open)`)

1. 実装したい機能や変更について会話します

1. 準備ができたら、以下のいずれかの方法を使用してエージェントに委任します:

   **委任ボタンを使用する (実験的)**

   実験的な設定 `setting(githubPullRequests.codingAgent.uiIntegration)` を有効にすると、エージェントが有効になっているリポジトリのチャットビューに **Delegate to coding agent** ボタンが表示されます。このボタンを選択して、現在のチャットコンテキストを coding agent に引き継ぎます。

   タスクを委任すると、ファイル参照を含む追加のコンテキストが coding agent に転送され、coding agent が完了すべきタスクを正確に計画できるようになります。新しいチャットエディターが開き、coding agent の進捗状況がリアルタイムで表示されます。

   <video src="images/copilot-coding-agent/delegate-to-coding-agent.mp4" title="Video showing how to delegate to coding agent from VS Code chat." controls poster="images/copilot-coding-agent/delegate-to-coding-agent-poster.png"></video>

   **#copilotCodingAgent ツールを使用する**

   プロンプトで `#copilotCodingAgent` ツールを直接参照して、ローカルの変更をバックグラウンドで継続するよう Copilot に依頼することもできます。このツールは、保留中の変更をリモートブランチに自動的にプッシュし、coding agent セッションを開始します:

   ![Copilot coding agent へのセッションの引き継ぎを示すスクリーンショット](images/copilot-coding-agent/coding-agent-start.png)

1. エージェントはプルリクエストを作成し、話し合った変更の実装を開始します。(`#copilotCodingAgent` または **Delegate to coding agent** アクションを使用して) coding agent セッションを開始すると、プルリクエストがチャットビューにカードとしてレンダリングされます。

   ![チャットビュー内の coding agent PR カードのスクリーンショット。](images/copilot-coding-agent/pr-card-in-chat.png)

### 方法 3: coding agent で TODO を修正する

コード内の `TODO` で始まるコメントに、コーディングエージェントセッションを素早く開始するためのコードアクションが表示されるようになりました。これは、特定のタスクをコードから直接委任する便利な方法を提供します。

> [!TIP]
> `TODO` キーワードは `setting(githubIssues.createIssueTriggers)` 設定で構成可能です。coding agent のコードアクションをトリガーするコメントキーワードをカスタマイズできます。

1. コード内の `TODO` コメントに移動します

1. 電球アイコンを探すか、`kb(editor.action.quickFix)` を使用してクイックフィックスメニューを開きます

1. 利用可能なコードアクションから **Delegate to coding agent** を選択します

   ![Delegate to coding agent という 'TODO' コメントの上のコードアクションのスクリーンショット](images/copilot-coding-agent/coding-agent-todo.png)

1. coding agent は TODO コメントを分析し、新しいプルリクエストで要求された変更を実装します

## エージェントの進捗状況を追跡する

### coding agent ワークフローを理解する

Copilot coding agent に作業を割り当てると、期待とは異なる可能性のある特定のワークフローに従います:

1. **初期プルリクエストの作成**: エージェントはすぐに初期の空のコミットを含むプルリクエストを作成します。これにより、すべての変更が行われるワークスペースとブランチが確立されます。

2. **バックグラウンド処理**: coding agent はローカルマシンではなく、GitHub のクラウドインフラストラクチャ (GitHub Actions 環境) で動作します。これは以下を意味します:
   * すべての開発は GitHub のサーバー上でリモートで行われます
   * エージェントは完全なリポジトリコンテキストにアクセスできます
   * VS Code を閉じても作業は継続します

3. **増分更新**: 初期コミットの後、エージェントはソリューションを開発するにつれて、実際のコード変更を含む追加のコミットをプッシュします。

> [!NOTE]
> 変更のない初期コミットが表示された場合、これは期待される動作です。エージェントはタスクに取り組むにつれて、実際のコード変更を後続のコミットでプッシュし続けます。

### VS Code での作業の監視

GitHub Pull Requests 拡張機能は、以下を表示する専用の **Copilot on My Behalf** セクションを提供します:

* すべてのアクティブな Copilot coding agent セッション
* エージェントによって作成されたプルリクエスト
* 各タスクの進捗状況
* 新しい変更や更新を示す数字バッジ

![複数の coding agent プルリクエストのステータスを示すスクリーンショット](images/copilot-coding-agent/coding-agent-status.png)

> [!TIP]
> GitHub.com を通じて `@copilot` に割り当てた作業も監視できます。アクティブなセッションとプルリクエストは、どこで開始したかに関係なく、すべてこのセクションに表示されます。

### 詳細なセッションログの表示

1. Pull Requests ビューで、**Copilot on My Behalf** の下にあるエージェントの作業を見つけます

1. **View Session** を選択して、エージェントが行ったすべての詳細なログを表示します:
   * 実行されたコマンド
   * 変更されたファイル
   * 実行されたテスト
   * 意思決定プロセス

   ![coding agent セッションのセッションログを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-session-log.png)

### 専用のチャットエディターによるセッションの管理 (実験的)

以下のことを可能にする専用のチャットエディターから coding agent セッションを管理できます:

* coding agent の進捗状況をリアルタイムで追跡する
* チャットから直接フォローアップの指示を提供する
* 専用環境でエージェントの応答を確認する
* チャットエディターから直接コード変更を表示または適用し、プルリクエストをチェックアウトする
* 継続性が向上し、ローカルチャットから GitHub エージェントタスクへのシームレスな移行を体験する
* 視覚的な明瞭さが向上した、より優れたセッションレンダリングの恩恵を受ける
* より応答性の高い体験のための高速なセッション読み込みを楽しむ

実験的な設定 `setting(chat.agentSessionsViewLocation)` を有効にして、この機能を試してください:

* `view` に設定すると、ローカルおよび coding agent セッションを管理するための **Chat Sessions** ビューが VS Code サイドバーに表示されます。ビューには、関連情報をすばやく見つけるのに役立つ詳細なコンテキストを含む豊富な説明が含まれるようになりました。

   ![Coding Agents ビューを示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-view.png)

* `showChatsMenu` に設定すると、coding agent セッションがローカルチャット履歴と一緒に表示されます

   ![Coding Agent Sessions Quick Pick を示すスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-quick-pick.png)

また、セッションを開始すると、coding agent によって作成されたプルリクエストがチャットビューにカードとしてレンダリングされ、視覚的な統合が向上します。

<!-- <video src="images/copilot-coding-agent/chat-sessions-view.mp4" title="Video showing Chat Sessions view and integration with GitHub coding agents." autoplay loop controls muted></video> -->

### 委任体験の向上

VS Code から GitHub coding agent への委任体験は、最近のアップデートで大幅に強化されました:

* **コンテキスト転送の改善**: チャットからタスクを委任すると、ファイル参照を含む追加のコンテキストが GitHub coding agent に自動的に転送されます
* **リアルタイムの進捗状況**: coding agent の進捗状況をリアルタイムで表示する新しいチャットエディターが開きます
* **シームレスな移行**: ローカルチャットから GitHub エージェントタスクへの移行時の継続性が向上しました
* **強化された視覚的統合**: プルリクエストがチャットビューに対話型カードとしてレンダリングされ、ナビゲーションが向上しました

これらの改善により、VS Code を離れることなく、coding agent のタスクを正確に計画し、その進捗状況を監視することが容易になります。

### 実行中のセッションのキャンセル

エージェントを停止する必要がある場合は、VS Code に留まり、PR 概要ページの **Cancel coding agent** ボタンを使用できます。

GitHub.com からセッションをキャンセルすることもできます:

1. GitHub.com の GitHub リポジトリに移動します
1. **Actions** タブに移動します
1. 実行中の Copilot Coding Agent ワークフローを見つけます
1. **Cancel workflow** を選択します

## レビューと反復

### 作業の完了

Copilot coding agent がコードを分析し、タスクを達成するために必要な変更を決定した後、以下の手順を実行します:

* すべての変更を含むプルリクエストを作成する
* レビューのために PR をあなたに割り当てる
* レビュアーとしてあなたをリクエストする
* 実装を説明する詳細な説明を含める
* 該当する場合 (UI の変更など)、スクリーンショットを追加する

![VS Code に表示された Copilot coding agent からのプルリクエストと、実装された機能のスクリーンショットを示すスクリーンショット。](images/copilot-coding-agent/draft-with-screenshot.png)

### フィードバックの提供

プルリクエストのコメントを通じてエージェントの作業をガイドできます。エージェントが応答するように、コメントで必ず `@copilot` をタグ付けしてください:

1. **変更のリクエスト**: 変更が必要な点について具体的なフィードバックを残します

   ```text
   @copilot Please update the login form to include password strength validation
   ```

1. **改善のリクエスト**: 追加の機能や改善を依頼します

   ```text
   @copilot Can you add error handling for network timeouts?
   ```

エージェントはフィードバックに応答し、リクエストされた変更を行い、プルリクエストを更新します。

> [!TIP]
> coding agent によって作成されたプルリクエストを操作する場合、`#activePullRequest` ツールがチャットセッションで自動的に有効になります。これにより、変更されたファイル、割り当てられた人、状態 (ドラフトまたはレビュー待ち) など、PR に関するチャットコンテキストが提供されます。その後、この PR について質問したり、チャットでさらに反復したりできます。

## よくある質問

### Copilot coding agent とエージェントの使用の違いは何ですか？

VS Code は 2 つの自律的なコーディング体験を提供します。VS Code でのエージェントの使用はエディター内で直接対話的な開発を提供するのに対し、Copilot coding agent は GitHub 上で独立して機能し、バックグラウンドで機能を実装します。

| 機能 | Copilot coding agent | エージェントの使用 |
|---------|---------------------|------------------|
| **実行場所** | GitHub クラウド | VS Code エディター |
| **独立性** | 完全に自律的 | ユーザーの対話と反復を含む |
| **出力** | プルリクエストを作成 | ファイルを直接編集 |
| **最適な用途** | 明確に定義されたタスク、バックグラウンド作業 | 対話的開発、即時フィードバック |

[VS Code でのエージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents)について詳しくはこちらをご覧ください。

### エージェントが開始しないのはなぜですか？

* GitHub アカウントでの Copilot アクセスを確認してください
* リポジトリへの書き込み権限があることを確認してください
* 組織で Copilot coding agent が有効になっていることを確認してください

### 初期コミットが空に見えるのはなぜですか？

Copilot coding agent が作業を開始すると、プルリクエストと作業ブランチを確立するために初期の空のコミットを作成します。これは期待される動作です。エージェントは GitHub のクラウド環境で作業するにつれて、実際のコード変更を含む後続のコミットをプッシュします。

進捗状況は、プルリクエスト、GitHub Pull Request 拡張機能の **Copilot on My Behalf** セクション、または Chat Sessions ビューからアクセスできるセッションログを通じて監視できます。

### 実装が不完全なのはなぜですか？

* 発生したエラーについてセッションログを確認してください
* エージェントの作業中にテストが失敗したかどうかを確認してください
* issue の説明でより詳細な要件を提供してください

### Copilot coding agent にはどのようなセキュリティ保護がありますか？

Copilot coding agent には組み込みのセキュリティ保護が含まれており、GitHub のセキュリティフレームワーク内で動作します。セキュリティ対策、権限、ブランチ保護の互換性の詳細については、[GitHub Copilot coding agent セキュリティドキュメント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent#built-in-security-protections)をご覧ください。

### Copilot coding agent を外部ツールで拡張できますか？

高度なシナリオでは、Model Context Protocol (MCP) サーバーを使用して Copilot coding agent を拡張し、以下へのアクセスを提供できます:

* 外部データベース
* クラウドサービス
* API およびサードパーティの統合
* カスタム開発ツール

[MCP を使用した Copilot coding agent の拡張](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/extending-copilot-coding-agent-with-mcp)について詳しくはこちらをご覧ください。

### 現在の制限は何ですか？

* **リポジトリ間の変更**: issue が割り当てられているリポジトリ内でのみ機能します
* **タスクごとの複数の PR**: 割り当てられたタスクごとに正確に 1 つのプルリクエストを開きます
* **既存の PR の修正**: 自身が作成していないプルリクエストでは作業できません

制限、互換性、使用コストの詳細については、[GitHub Copilot Coding Agent ドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)をご覧ください。

## 次のステップ

* [GitHub セットアップガイド](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/enabling-copilot-coding-agent)に従って Copilot coding agent を有効にする
* 即時の対話型コーディング支援のために [VS Code チャットのエージェント](/docs/copilot/chat/copilot-chat.md)を試す

## 関連リソース

* [GitHub Copilot coding agent ドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)
* [GitHub Pull Requests 拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
* [チャットセッションの管理](/docs/copilot/chat/chat-sessions.md)
