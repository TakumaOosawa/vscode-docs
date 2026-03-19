---
ContentId: e02ded07-6e5a-4f94-b618-434a2c3e8f09
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用するための頻繁に寄せられる質問。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot よくある質問

この記事では、Visual Studio CodeでGitHub Copilotを使用する際についてよく寄せられる質問に答えます。

## GitHub Copilotサブスクリプション

### Copilotサブスクリプションを取得するには?

GitHub Copilotにアクセスする方法はいくつかあります:

| ユーザータイプ | 説明 |
|--------------------------------|-------------|
| 個人 | <ul><li>GitHub Copilot Freeを設定して、月単位のインライン提案とチャットインタラクションの制限の範囲内で、基本機能を無料で試してください。</li><li>GitHub Copilotの有料プランにサインアップして、より多くの柔軟性とプレミアム機能にアクセスしてください。</li><li>すべてのオプションについては、[自分用にGitHub Copilotをセットアップする](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-yourself) を参照してください。</li></ul> |
| 組織/エンタープライズメンバー | <ul><li>GitHub Copilotのサブスクリプションを持つ組織またはエンタープライズのメンバーである場合は、<https://github.com/settings/copilot> にアクセスして、「Get Copilot from an organization」下でアクセスをリクエストできます。</li><li>組織用にCopilotを有効にするには、[組織用にGitHub Copilotをセットアップする](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-your-organization) を参照してください。</li></ul> |

### GitHubアカウントでサインインする利点は何ですか?

GitHub Copilotへのアクセス権を持つGitHubアカウントでサインインすると、以下の利点があります:

* [チャットインタラクションの月単位の制限の増加](https://docs.github.com/en/copilot/get-started/plans#comparing-copilot-plans)
* [オートモデル選択を超えるチャットのプレミアムスピーチモデルへのアクセス](https://docs.github.com/en/copilot/reference/ai-models/supported-models#supported-ai-models-per-copilot-plan)
* [独自のモデルキーを持参](/docs/copilot/customization/language-models.md#bring-your-own-language-model-key) (BYOK) して、より多くのモデルにアクセスする
* [リポジトリのリモートインデックスセマンティックコード検索](/docs/copilot/reference/workspace-context.md#remote-index)
* [Copilotコード確認](https://docs.github.com/en/copilot/concepts/agents/code-review)
* [Copilotコンテンツ除外](https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot)
* [Copilotコーディングエージェントにタスクをデリゲート](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent) バックグラウンド実行の場合

Copilotプランに応じて、アクセスレベルと制限が異なります。詳しくは、[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans) を参照してください。

### Copilotの使用状況を監視するにはどうすればよいですか?

VS CodeのStatus BarからアクセスできるCopilot Status Dashboardで現在のCopilot使用状況を確認できます。ダッシュボードには、以下の情報が表示されます:

- **インライン提案**: 当月に使用したインライン提案クォータの割合。
- **チャットメッセージ**: 当月に使用したチャットリクエストクォータの割合。
- **プレミアムリクエスト**: 当月に使用したプレミアムリクエストクォータの割合。
- **プレミアムリクエスト超過**: 当月に使用したプレミアムリクエスト超過分の数。

GitHub Copilotドキュメントにアクセスして、[使用状況とエンタイトルメントの監視](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/monitoring-your-copilot-usage-and-entitlements) についての詳細情報を参照してください。

### インライン提案またはチャットインタラクションの制限に達しました

インライン提案とチャットインタラクションの制限は毎月リセットされます。チャットインタラクションの制限のみに達した場合は、引き続きインライン提案を使用できます。同様に、インライン提案の制限に達した場合は、チャットを引き続き使用できます。

Copilot Freeプランのユーザーの場合、より多くのインライン提案とチャットインタラクションにアクセスするには、VS Codeから直接[有料プラン](https://docs.github.com/en/copilot/concepts/billing/individual-plans) にサインアップできます。または、次の月まで待つと、Copilotを無料で引き続き使用できます。

![チャットビュー、Status Bar、およびタイトルバーの視覚インジケーターで、Copilotチャットメッセージの制限に達したことを示します。](images/faq/copilot-chat-limit-reached.png)

有料プランを使用していて、すべてのプレミアムリクエストを使い果たした場合でも、当月の残りの期間は含まれているモデルの1つでCopilotを使用できます。プランの制限を超えた追加のプレミアムリクエストをリクエストすることもできます。GitHub Copilotドキュメントで[追加プレミアムリクエストの取得](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#what-if-i-run-out-of-premium-requests) について詳しく学んでください。

### Copilotサブスクリプションが VS Codeで検出されません

Visual Studio Codeでチャットを使用するには、GitHub Copilotへのアクセス権を持つGitHubアカウントを使用してVisual Studio Codeにサインインする必要があります。

- Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、GitHubアカウントからサインアウトし、別のアカウントでサインインしてください。Activity BarのAccounts メニューを使用して、現在のGitHubアカウントからサインアウトしてください。詳細情報については、[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot) を参照してください。

- [GitHub Copilot設定](https://github.com/settings/copilot) でCopilotサブスクリプションがまだアクティブであることを確認してください。

- GHE.comでマネージユーザーアカウント用のCopilotプランを使用している場合は、サインインする前にいくつかの設定を更新する必要があります。詳細については、[GHE.comのアカウントでGitHub Copilotを使用する](https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/using-github-copilot-with-an-account-on-ghecom) を参照してください。

### Copilotのアカウントを切り替えるにはどうするのですか?

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、VS CodeでGitHubアカウントからサインアウトし、別のアカウントでサインインしてください。

詳細情報については、[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot) を参照してください。

## 一般的なCopilot質問

### VS CodeからCopilotを削除するにはどうするのですか?

`setting(chat.disableAIFeatures)` 設定を使用して、VS Codeの組み込みAI機能を無効にできます。これは、VS Codeで他の機能を構成する方法と同じです。これにより、チャットやインライン提案などの機能がVS Codeで無効化および非表示になり、Copilot拡張機能が無効になります。ワークスペースまたはユーザーレベルで設定を構成できます。

または、タイトルバーのチャットメニューの**AI機能を非表示にする方法を学ぶ** アクションを使用して、設定にアクセスしてください。

> [!NOTE]
> 以前に組み込みAI機能を無効にした場合、VS Codeの新しいバージョンに更新した後も、その選択は保持されます。

### Copilotのネットワークとファイアウォール構成

- ファイアウォールやプロキシサーバーなどのセキュリティ対策を採用している場合、特定のドメインURLを「許可リスト」に含め、特定のポートとプロトコルを開くことが有益な場合があります。GitHub Copilotの[ファイアウォール設定のトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-firewall-settings-for-github-copilot) について詳しく学んでください。

- 会社の機器を使用していて企業ネットワークに接続している場合は、VPNまたはHTTPプロキシサーバー経由でインターネットに接続している可能性があります。場合によっては、これらのタイプのネットワークセットアップにより、GitHub CopilotがGitHubのサーバーに接続することが妨げられることがあります。GitHub Copilotの[ネットワークエラーのトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-network-errors-for-github-copilot) について詳しく学んでください。

### リクエストがレート制限されています

このエラーは、Copilotリクエストのレート制限を超えたことを示唆しています。GitHubはレート制限を使用して、すべてのユーザーがCopilotサービスに公平にアクセスできることと、不正使用から保護することを確認しています。

レート制限とレート制限を受けた場合の対応方法の詳細については、[GitHub Copilotのレート制限](https://docs.github.com/en/copilot/troubleshooting-github-copilot/rate-limits-for-github-copilot) を参照してください。

### Copilot拡張機能のプレリリースビルドはありますか?

はい、Copilot拡張機能のプレリリース(夜間)バージョンに切り替えて、最新の機能と修正を試すことができます。拡張機能ビューから、歯車アイコンを右クリックまたは選択してコンテキストメニューを表示し、**プレリリースバージョンに切り替える** を選択します:

![プレリリースバージョンに切り替えるオプション付きの拡張機能ビューコンテキストメニュー](images/faq/switch-to-pre-release.png)

拡張機能の詳細でプレリリースバッジによってプレリリースバージョンを実行していることがわかります:

![GitHub Copilot拡張機能のプレリリースバージョン](images/faq/copilot-ext-pre-release.png)

## インライン提案

### インライン提案を有効または無効にするにはどうするのですか?

VS CodeのStatus BarのCopilot Status Dashboardのチェックボックスを使用して、VS Codeでインライン提案を有効または無効にできます。インライン提案をグローバルに、またはアクティブなエディターのファイルタイプ単位で有効または無効にできます。

![VS Code Status Barのスクリーンショット。Copilotがアクティブであることを示すCopilotアイコンをハイライトしています。](./images/faq/copilot-disable-completions.png)

または、`setting(github.copilot.enable)` と`setting(github.copilot.nextEditSuggestions.enabled)` 設定を使用して、インライン提案と次の編集提案をそれぞれ有効または無効にしてください。ワークスペースまたはユーザーレベルで設定を構成できます。

### エディターでインライン提案が機能していません

- [GitHub Copilotがグローバルまたはこの言語で無効になっていない](#how-do-i-enable-or-disable-inline-suggestions) ことを確認してください
- [GitHub Copilotサブスクリプションがアクティブであり、検出されている](#my-copilot-subscription-is-not-detected-in-vs-code) ことを確認してください
- [ネットワーク設定](#network-and-firewall-configuration-for-copilot) がGitHub Copilotへの接続を許可するように構成されていることを確認してください。
- [Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free) で当月のインライン提案の制限に達していないことを確認してください。

## チャット

### チャット機能が機能していません

Visual Studio Codeでチャット機能が機能することを確認するには、以下の要件を確認してください:

- Visual Studio Codeの最新バージョンがインストールされていることを確認してください。(**Code: Check for Updates** を実行してください)。
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) と[GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) 拡張機能の両方の最新バージョンがインストールされていることを確認してください。
- VS Codeにサインインしている GitHubアカウントには、アクティブなCopilotサブスクリプションが必要です。[Copilotサブスクリプション](https://github.com/settings/copilot) を確認してください。
- [Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free) で当月のチャットインタラクションの制限に達していないことを確認してください。

### エージェントがチャットで利用できません

VS Code設定: `setting(chat.agent.enabled)` でエージェントが有効になっていることを確認してください。組織がこの機能を無効にしている可能性があります。エージェントを有効にするために管理者に確認してください。

### VS Codeのエージェントは何ができますか?

エージェントは、コーディングタスク全体を自律的に処理します。多段階の実装を計画し、複数のファイル全体で調整された変更を実行し、ターミナルコマンドを実行し、ツールを起動し、エラーが発生した場合に自己修正します。機能実装、アーキテクチャレベルのリファクタリング、フレームワークマイグレーション、デバッグ、テスト生成にエージェントを使用してください。[エージェントの使用](/docs/copilot/agents/overview.md) について詳しく学んでください。

### Copilotは大規模なコードベースとモノレポに対応しますか?

はい。VS Codeはセマンティック検索、言語インテリジェンス(LSP)、GitHubのコード検索を使用してワークスペースを自動的にインデックス付けし、リポジトリ全体で深い理解を提供します。大規模なリポジトリの場合、[リモートインデックス](/docs/copilot/reference/workspace-context.md#remote-index) はGitHubのインデックスを使用して、関連リポジトリ全体で高速で包括的な結果を提供します。[マルチルートワークスペース](/docs/editing/workspaces/multi-root-workspaces.md) を使用してモノレポのコンテキストをスコープし、[カスタム指示](/docs/copilot/customization/custom-instructions.md) で プロジェクトのアーキテクチャを説明してください。[大規模なコードベースのベストプラクティス](/docs/copilot/best-practices.md#work-with-large-codebases) を参照してください。

### 組織はAI機能とエージェントアクセスを制御できますか?

はい。組織の管理者は、[エンタープライズAI設定](/docs/enterprise/ai-settings.md) と[ポリシー](/docs/enterprise/policies.md) を通じてCopilotを管理できます。エージェントの有効化と無効化、モデルアクセスの制御、コンテンツの除外の構成、信頼境界の実装が含まれます。詳細については、[GitHub Copilot Trust Center](https://resources.github.com/copilot-trust-center/) を参照してください。

### エージェント使用には制限がありますか?

エージェントはCopilotプランからプレミアムリクエストを使用します。有料プランには月単位のプレミアムリクエスト配分が含まれており、追加の容量をリクエストできます。ローカル、バックグラウンド、クラウド環境全体で複数のエージェントセッションを並行して実行できます。無料プランのユーザーは、月単位のチャットインタラクション制限があります。詳細については、[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans) を参照してください。

### 言語モデルピッカーで すべてのモデルが使用できるわけではありません

言語モデルピッカーで利用可能なモデルを選択できます。[言語モデルピッカーをカスタマイズ](/docs/copilot/customization/language-models.md#customize-the-model-picker) する方法を学んでください。

組織は特定のモデルへのアクセスを制限できます。モデルが利用可能になるべきだと思われる場合は、組織の管理者に連絡してください。

### チャットビューが自動的に開かないようにするにはどうするのですか?

デフォルトでは、チャットビューはセカンダリサイドバーで開き ます。ワークスペースのチャットビューを閉じると、VS Codeはこの設定を記憶し、次回ワークスペースを開いた時点ではチャットビューが自動的に開きません。

チャットビューから直接デフォルトの表示を変更できます:

1. チャットビューを開きます(`kb(workbench.action.chat.open)`)。
1. チャットビューの右上隅の`...` アイコンを選択します。
1. **Show View by Default** を選択して、チャットビューの自動開放を有効または無効にします。

`setting(workbench.secondarySideBar.defaultVisibility)` 設定を使用してセカンダリサイドバーのデフォルトの表示を制御することもできます。`hidden` に設定して、チャットビューが自動的に開かないようにしてください。

## トラブルシューティングとフィードバック

### Copilotについてどのようにフィードバックを提供できますか?

VS CodeのGitHub Copilotの問題と機能リクエストは、[microsoft/vscode](https://github.com/microsoft/vscode) GitHubリポジトリで追跡します。このリポジトリで問題を作成することも、VS Codeで以下のフィードバックメカニズムを使用することもできます:

- **ゴーストテキスト提案**

    エディターのゴーストテキスト提案にカーソルを合わせるときに、**Send Copilot Completion Feedback** アクションを使用してください。Issue Reporterで、問題を再現する手順を含めた、明確で詳細な説明を提供してください。

    ![エディターで Copilot Ghost Text Feedbackアクションを送信するスクリーンショット。](images/faq/code-completions-feedback.png)

- **次の編集提案**

    エディターのガターの次の編集提案メニューの**Feedback** アクションを選択してください。Issue Reporterで、問題を再現する手順を含めた、明確で詳細な説明を提供してください。

    ![エディターのガターの次の編集提案メニューのスクリーンショット。](images/faq/nes-feedback.png)

- **一般的な問題**

    VS Code Issue Reporter (**Help menu** > **Report Issue**) を開き、**VS Code Extension** ソースを選択してから、**GitHub Copilot Chat** 拡張機能を選択します。問題を再現する手順を含めた、明確で詳細な説明を提供してください。

    ![GitHub Copilot Chatが選択されたVS Code Issue Reporterのスクリーンショット。](images/faq/issue-reporter.png)

問題を報告するときは、[wiki](https://github.com/microsoft/vscode/wiki/Copilot-Issues) のガイドラインに従って、問題が対応可能であることを確認してください。

問題を報告する場合は、Copilotログからの情報を含めることが役に立つことがあります。[ログを表示して診断を収集する](/docs/copilot/troubleshooting.md) 方法を学んでください。

## その他のリソース

- [GitHub Copilot Trust Center](https://resources.github.com/copilot-trust-center/)
- [VS CodeのAIについてのセキュリティに関する考慮事項](/docs/copilot/security.md)
- GitHubドキュメントの[GitHub Copilot FAQ](https://github.com/features/copilot#faq)

