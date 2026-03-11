---
ContentId: f8b9e2a4-7c1d-4f5e-9a8b-3d2e1f0c6789
DateApproved: 3/9/2026
MetaDescription: VS Codeで GitHub Copilot コーディングエージェントと相互作用して、バックグラウンドで機能を自律的に実装し、バグを修正する方法について説明します。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot コーディングエージェント

[GitHub Copilot コーディングエージェント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent)は、GitHub でホストされている自律的な AI 開発者で、バックグラウンドで独立して開発タスクを完了するために機能します。コーディングエージェントを起動するには、GitHub Issue を Copilot に割り当てるか、チャットからタスクを委任します。その後、エージェントは機能を実装し、バグを修正し、独立した開発環境を使用してリポジトリ全体で変更を行うために自律的に機能します。

これは、[VS Code でエージェントを使用する](/docs/copilot/agents/local-agents.md)場合と異なります。これはエディター内で対話的な開発を提供し、コーディングセッション中に積極的な参加が必要です。

![VS Code 内から Copilot コーディングエージェントに Issue を割り当てる方法を示す GIF。](images/copilot-coding-agent/assign-to-copilot-gif.gif)

## 仕組み

Copilot コーディングエージェントのワークフロー:

1. **割り当て**: [GitHub Issue を`@copilot`に割り当てるか](#method-1-assign-issues-to-copilot)、[VS Code チャットからタスクを委任するか](#method-2-delegate-from-chat)、[TODO コードアクションを使用します](#method-3-fix-todos-with-coding-agent)
1. **分析**: エージェントがタスクとリポジトリ構造を分析します
1. **開発**: Copilot は独立した GitHub Actions 環境で機能し、次のことができます:
   * コードベースを参照
   * 複数のファイル全体で変更を行う
   * ビルドとテストを実行
   * リンターと他の自動化チェックを実行
1. **Pull request**: エージェントが実装を含む pull request を作成します
1. **レビュー**: 変更をレビューし、PR コメントを通じて修正をリクエストできます
1. **イテレーション**: エージェントがフィードバックに応答し、実装を更新します

## 前提条件

Copilot コーディングエージェントを使用する前に、以下が必要です:

* **GitHub Copilot サブスクリプション**: Copilot Pro、Pro+、Business、または Enterprise プランで利用可能
* **書き込みアクセス**: リポジトリへの書き込み権限が必要です
* **エージェントを有効にする**: Copilot コーディングエージェントは、アカウントまたは組織の[有効にする必要があります](https://docs.github.com/copilot/concepts/coding-agent/enable-coding-agent)
* **VS Code セットアップ**: [GitHub Pull Requests 拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)をインストールします

GitHub Pull Request 拡張機能に正しい GitHub アカウントでサインインしていることを確認してください。

![アカウントメニューを表示するスクリーンショット。GitHub Pull Request アクションへのサインインを強調しています。](images/copilot-coding-agent/sign-in-github-pull-requests.png)

**オプション**: 実験的設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にして、Copilot Chat に**コーディングエージェントに委任する**ボタンを表示し、タスク委任を簡単にします。

また、実験的設定`setting(chat.agentSessionsViewLocation)`を有効にすることで、専用のチャットエディターからコーディングエージェントセッションを管理し、**Chat Sessions**ビューを表示できます。

> [!TIP]
> Copilot アクセスをまだお持ちでない場合は、[Copilot Free プラン](https://github.com/features/copilot/plans)にサインアップして、月間のインタラクション制限を受けることができます。

## VS Code で Copilot コーディングエージェントに作業を割り当てる

### 方法 1: Issue を Copilot に割り当てる

GitHub Issue をチームメンバーに割り当てるのと同じように、GitHub Issue を Copilot に割り当てることで Copilot コーディングエージェントをトリガーできます。Copilot コーディングエージェントは自動的に Issue を分析し、作業を開始します。

1. **GitHub Pull Requests**ビューで、**Issues**セクションに移動します

1. Copilot に割り当てる Issue を見つけます

1. Issue を右クリックして**Copilot に割り当てる**を選択するか、**割り当て**を選択してから`@copilot`を選択します

   > [!TIP]
   > GitHub.com で`@copilot`に Issue を直接割り当てることもできます。コーディングエージェントは同じ方法で機能し、VS Code または GitHub で確認できる pull request を作成します。

1. エージェントがバックグラウンドで Issue の処理を開始します

1. VS Code でチャットビューを開きます(`kb(workbench.action.chat.open)`)
   ![GitHub Pull Requests ビューを表示するスクリーンショット。Copilot アクションへの割り当てと、Copilot に割り当てられた作業の PR クエリを強調しています。](images/copilot-coding-agent/github-pull-request-coding-agent.png)

### 方法 2: チャットから委任する

チャット会話から直接 Copilot コーディングエージェントに作業を引き渡すこともができます。エージェントをエディターで変更をすぐに実装する代わりに、タスクをコーディングエージェントに委任して、バックグラウンドで自律的に処理してもらうことができます。

1. VS Code でチャットビューを開きます(`kb(workbench.action.chat.open)`)

1. 実装したい機能または変更について会話します

1. 準備ができたら、以下の方法のいずれかを使用してエージェントに委任します:

   **委任ボタンを使用する (実験的)**

   実験的設定`setting(githubPullRequests.codingAgent.uiIntegration)`を有効にして、エージェントが有効になっているリポジトリのチャットビューに**コーディングエージェントに委任する**ボタンを表示します。このボタンを選択して、現在のチャットコンテキストをコーディングエージェントに引き渡します。

   タスクを委任すると、ファイル参照を含む追加コンテキストがコーディングエージェントに転送され、エージェントが完了するタスクを正確に計画できるようになります。新しいチャットエディターが開き、コーディングエージェントの進行状況がリアルタイムで表示されます。

   <video src="images/copilot-coding-agent/delegate-to-coding-agent.mp4" title="VS Code チャットからコーディングエージェントに委任する方法を示すビデオ。" controls poster="images/copilot-coding-agent/delegate-to-coding-agent-poster.png"></video>

   **#copilotCodingAgent ツールを使用する**

   プロンプトで`#copilotCodingAgent`ツールを直接参照することで、Copilot にローカル変更をバックグラウンドで続行するよう依頼することもできます。このツールは、保留中の変更をリモートブランチに自動的にプッシュし、コーディングエージェントセッションを開始します:

   ![Copilot コーディングエージェントにセッションを引き渡すスクリーンショット](images/copilot-coding-agent/coding-agent-start.png)

1. エージェントが pull request を作成し、説明された変更の実装を開始します。コーディングエージェントセッションを開始する場合(`#copilotCodingAgent`または**コーディングエージェントに委任する**アクション経由)、pull request はチャットビューにカードとして表示されます。

   ![チャットビューでのコーディングエージェント PR カードのスクリーンショット。](images/copilot-coding-agent/pr-card-in-chat.png)

### 方法 3: TODO をコーディングエージェントで修正する

コード内の`TODO`で始まるコメントには、コーディングエージェントセッションを迅速に開始するコードアクションが表示されます。これにより、コードから特定のタスクを直接委任する便利な方法が提供されます。

> [!TIP]
> `TODO`キーワードは、`setting(githubIssues.createIssueTriggers)`設定を介して構成可能です。コーディングエージェントコードアクションをトリガーするコメントキーワードをカスタマイズできます。

1. コード内の`TODO`コメントに移動します

1. 電球アイコンを探すか、`kb(editor.action.quickFix)`を使用してクイックフィックメニューを開きます

1. 利用可能なコードアクションから**コーディングエージェントに委任する**を選択します

   ![「TODO」コメントの上のコードアクションのスクリーンショット。「コーディングエージェントに委任する」と呼ばれています。](images/copilot-coding-agent/coding-agent-todo.png)

1. コーディングエージェントが TODO コメントを分析し、新しい pull request でリクエストされた変更を実装します

## エージェントの進行状況を追跡する

### コーディングエージェントワークフローを理解する

作業を Copilot コーディングエージェントに割り当てると、期待と異なる場合がある特定のワークフローに従います:

1. **初期 pull request 作成**: エージェントは、pull request とワーキングブランチを確立する初期空コミットを直ちに作成します。これは、すべての変更が行われるワークスペースとブランチを確立します。

2. **バックグラウンド処理**: コーディングエージェントは、ローカルマシンではなく GitHub のクラウドインフラストラクチャ(GitHub Actions 環境)で機能します。これは以下を意味します:
   * すべての開発は GitHub のサーバーでリモートで行われます
   * エージェントは完全なリポジトリコンテキストにアクセスできます
   * VS Code を閉じている場合でも作業が継続されます

3. **段階的な更新**: 初期コミットの後、エージェントはソリューションを開発する際に、実際のコード変更を含む追加コミットをプッシュします。

> [!NOTE]
> 変更のない初期コミットが表示される場合、これは予期された動作です。エージェントは、タスクに対して作業を続ける際に、後続のコミットで実際のコード変更をプッシュし続けます。

### VS Code で作業を監視する

GitHub Pull Requests 拡張機能は、以下を表示する専用の**Copilot on My Behalf**セクションを提供します:

* すべてのアクティブな Copilot コーディングエージェントセッション
* エージェントによって作成された pull request
* 各タスクの進行状況
* 新しい変更または更新を示す数値バッジ

![複数のコーディングエージェント pull request のステータスを表示するスクリーンショット](images/copilot-coding-agent/coding-agent-status.png)

> [!TIP]
> GitHub.com を通じて`@copilot`に割り当てた作業を監視することもできます。すべてのアクティブなセッションと pull request は、それらをどこで開始したかに関わらず、このセクションに表示されます。

### 詳細なセッションログを表示する

1. Pull Requests ビューで、**Copilot on My Behalf**の下のエージェントの作業を探します

1. **View Session**を選択して、エージェントが行ったすべての詳細ログを表示します:
   * 実行されたコマンド
   * 変更されたファイル
   * 実行されたテスト
   * 意思決定プロセス

   ![コーディングエージェントセッションのセッションログを表示するスクリーンショット。](images/copilot-coding-agent/coding-agent-session-log.png)

### 専用チャットエディターでセッションを管理する (実験的)

専用のチャットエディターからコーディングエージェントセッションを管理して、以下を行うことができます:

* コーディングエージェントの進行状況をリアルタイムで追跡
* チャットから直接フォローアップ指示を提供
* 専用環境でエージェントの応答を表示
* チャットエディターからコード変更を表示または適用し、pull request をチェックアウト
* ローカルチャットから GitHub エージェントタスクへのシームレスな移行により、継続性を改善
* 改善されたビジュアルの明確性により、より良い セッションレンダリング
* より応答の速い経験のために高速なセッション読み込みをお楽しみください

実験的設定`setting(chat.agentSessionsViewLocation)`を有効にしてこの機能を試してください:

* `view`に設定されているときは、VS Code サイドバーの**Chat Sessions**ビューが表示され、ローカルおよびコーディングエージェントセッションを管理できます。ビューには、関連情報をすばやく見つけやすくするための詳細なコンテキストを含む豊富な説明が含まれています。

   ![コーディングエージェントビューを表示するスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-view.png)

* `showChatsMenu`に設定すると、コーディングエージェントセッションがローカルチャット履歴と一緒に表示されます

   ![「コーディングエージェントセッション」クイックピックを表示するスクリーンショット。](images/copilot-coding-agent/coding-agent-sessions-quick-pick.png)

コーディングエージェントが作成した pull request は、セッションを開始すると、チャットビューにカードとしても表示され、より良いビジュアル統合を提供します。

<!-- <video src="images/copilot-coding-agent/chat-sessions-view.mp4" title="Chat Sessions ビューと GitHub コーディングエージェントとの統合を示すビデオ。" autoplay loop controls muted></video> -->

### 委任エクスペリエンスの改善

VS Code から GitHub コーディングエージェントへの委任エクスペリエンスは、最近の更新で大幅に改善されています:

* **より良いコンテキスト転送**: チャットからタスクを委任すると、ファイル参照を含む追加コンテキストが自動的に GitHub コーディングエージェントに転送されます
* **リアルタイムの進行状況**: コーディングエージェントの進行状況を示す新しいチャットエディターが開きます
* **シームレスな移行**: ローカルチャットから GitHub エージェントタスクに移動するときの継続性を改善
* **強化されたビジュアル統合**: pull request がチャットビューでインタラクティブカードとしてレンダリングされ、より良いナビゲーションが実現します

これらの改善により、VS Code を離れることなく、コーディングエージェント用のタスクを正確に計画して進行状況を監視できるようになります。

### 実行中のセッションをキャンセルする

エージェントを停止する必要がある場合は、VS Code に留まって、PR 概要ページの**コーディングエージェントをキャンセル**ボタンを使用できます。

GitHub.com からセッションをキャンセルすることもできます:

1. GitHub.com で GitHub リポジトリに移動します
1. **Actions**タブに移動します
1. 実行中の Copilot Coding Agent ワークフローを探します
1. **ワークフローをキャンセル**を選択します

## レビューとイテレーション

### 作業完了

Copilot コーディングエージェントがコードを分析し、タスクを完了するために必要な変更を決定した後、次の手順を実行します:

* すべての変更を含む pull request を作成
* PR をレビュー用にあなたに割り当てます
* レビュー担当者としてリクエスト
* 実装説明の詳細な説明を含める
* 適用可能な場合は、スクリーンショットを追加します(UI の変更の場合)

![Copilot コーディングエージェントから VS Code に表示される pull request のスクリーンショット。実装された機能のスクリーンショットが含まれています。](images/copilot-coding-agent/draft-with-screenshot.png)

### フィードバックを提供する

pull request コメントを通じてエージェントの作業をガイドできます。エージェントが応答するようにコメントで`@copilot`をタグ付けしてください:

1. **リクエストの変更**: 変更する必要があるもの についての具体的なフィードバックを残します

   ```text
   @copilot ログインフォームを更新して、パスワード強度検証を含めてください
   ```

1. **改善をリクエスト**: 追加機能または改善をリクエスト

   ```text
   @copilot ネットワークタイムアウトのエラーハンドリングを追加できますか?
   ```

エージェントがフィードバックに応答し、リクエストされた変更を行い、pull request を更新します。

> [!TIP]
> コーディングエージェントによって作成された pull request で作業する場合、`#activePullRequest`ツールはチャットセッションで自動的に有効になります。これにより、チャットは PR についてのコンテキストを取得します。変更されたファイル、割り当てられたユーザー、状態(ドラフトまたはレビュー準備完了)を含みます。その後、この PR についてチャットで質問でき、チャットで詳細に反復処理できます。

## よくある質問

### Copilot コーディングエージェントとエージェントの使用の違いは何ですか?

VS Code は 2 つの自律的なコーディングエクスペリエンスを提供します。VS Code でのエージェントの使用はエディター内で対話的な開発を提供しますが、Copilot コーディングエージェントは GitHub で独立して、バックグラウンドで機能を実装します。

| 機能 | Copilot コーディングエージェント | エージェントの使用 |
|---------|---------------------|------------------|
| **実行場所** | GitHub クラウド | VS Code エディター |
| **独立性** | 完全に自律 | ユーザー の相互作用と反復を含む |
| **出力** | pull request を作成 | ファイルを直接編集 |
| **最適な用途** | よく定義されたタスク、バックグラウンド作業 | 対話的な開発、即座のフィードバック |

[VS Code でエージェントを使用する](/docs/copilot/agents/local-agents.md)について詳しく学びます。

### エージェントが開始しないのはなぜですか?

* GitHub アカウントで Copilot アクセスを確認します
* リポジトリへの書き込み権限があることを確認します
* Copilot コーディングエージェントが組織に対して有効になっていることを確認します

### 初期コミットが空に見えるのはなぜですか?

Copilot コーディングエージェントが動作を開始すると、pull request とワーキングブランチを確立するための初期空コミットを作成します。これは予期された動作です。エージェントは GitHub のクラウド環境で機能する際に、実際のコード変更を含む後続のコミットをプッシュします。

pull request からアクセス可能なセッションログ、GitHub Pull Request 拡張機能の**Copilot on My Behalf**セクション、またはチャットセッションビューを通じて進行状況を監視できます。

### 実装が不完全なのはなぜですか?

* エラーについてセッションログをレビュー
* エージェントの作業中にテストが失敗したかどうかを確認
* Issue の説明で、より詳細な要件を提供

### Copilot コーディングエージェントにはどのようなセキュリティ保護がありますか?

Copilot コーディングエージェントには組み込みのセキュリティ保護が含まれており、GitHub のセキュリティフレームワーク内で動作します。セキュリティ対策、権限、およびブランチ保護の互換性に関する詳細情報については、[GitHub Copilot コーディングエージェントのセキュリティドキュメント](https://docs.github.com/en/copilot/concepts/about-copilot-coding-agent#built-in-security-protections)を参照してください。

### Copilot コーディングエージェントを外部ツールで拡張できますか?

高度なシナリオでは、Model Context Protocol(MCP)サーバーを使用して Copilot コーディングエージェントを拡張して、以下へのアクセス権を付与できます:

* 外部データベース
* クラウドサービス
* API とサードパーティ統合
* カスタム開発ツール

[MCP を使用して Copilot コーディングエージェントを拡張する](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/extending-copilot-coding-agent-with-mcp)について詳しく学びます。

### 現在の制限事項は何ですか?

* **リポジトリ全体の変更**: Issue が割り当てられているリポジトリ内でのみ機能
* **タスクごとの複数の PR**: 割り当てられたタスクごとにちょうど 1 つの pull request を開く
* **既存の PR 修正**: 作成していない pull request で機能できない

制限事項、互換性、使用コストの詳細情報については、[GitHub Copilot Coding Agent ドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)を参照してください。

## 次のステップ

* [GitHub セットアップガイド](https://docs.github.com/en/copilot/using-github-copilot/coding-agent/enabling-copilot-coding-agent)に従って Copilot コーディングエージェントを有効にします
* [VS Code チャットでエージェント](/docs/copilot/chat/copilot-chat.md)を試して、即座の対話的なコーディング支援を提供します

## 関連リソース

* [GitHub Copilot コーディングエージェントドキュメント](https://docs.github.com/en/copilot/using-github-copilot/coding-agent)
* [GitHub Pull Requests 拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
* [チャットセッションを管理する](/docs/copilot/chat/chat-sessions.md)

