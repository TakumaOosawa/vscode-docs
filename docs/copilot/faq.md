---
ContentId: e02ded07-6e5a-4f94-b618-434a2c3e8f09
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用する際のよくある質問。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilotよくある質問

この記事では、Visual Studio CodeでGitHub Copilotを使用する際のよくある質問に答えます。

## GitHub Copilotサブスクリプション

### Copilotサブスクリプションを取得するにはどうすればよいですか?

GitHub Copilotにアクセスする方法はいくつかあります：

| ユーザーの種類                   | 説明 |
|--------------------------------|-------------|
| 個人                     | <ul><li>GitHub Copilot Freeを設定して、基本機能を無料で試し、毎月のインライン提案とチャットインタラクションに制限があります。</li><li>有料GitHub Copilotプランにサインアップして、より大きな柔軟性とプレミアム機能へのアクセスを取得します。</li><li>[自分用GitHub Copilotの設定](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-yourself)で、すべてのオプションをご覧ください。</li></ul> |
| 組織/エンタープライズメンバー | <ul><li>GitHub Copilotのサブスクリプションを持つ組織またはエンタープライズのメンバーの場合、<https://github.com/settings/copilot>に移動し、「組織からCopilotを取得」でアクセスをリクエストできます。</li><li>[組織用GitHub Copilotの設定](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-your-organization)で、組織のCopilotを有効にする方法をご覧ください。</li></ul> |

### GitHubアカウントでサインインすることの利点は何ですか?

GitHub Copilotにアクセス可能なGitHubアカウントでサインインすると、以下の利点があります：

*[チャットインタラクションの毎月の制限が増加](https://docs.github.com/en/copilot/get-started/plans#comparing-copilot-plans)
*[チャットのプレミアム言語モデルへのアクセス](https://docs.github.com/en/copilot/reference/ai-models/supported-models#supported-ai-models-per-copilot-plan)（自動モデル選択以外）
*[独自のモデルキーを持ち込む](/docs/copilot/customization/language-models.md#bring-your-own-language-model-key)（BYOK）でより多くのモデルにアクセス
*[リモートリポジトリインデックスとセマンティックコード検索](/docs/copilot/reference/workspace-context.md#remote-index)
*[Copilotコードレビュー](https://docs.github.com/en/copilot/concepts/agents/code-review)
*[Copilotコンテンツ除外](https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot)
*[Copilotコーディングエージェントにタスクをデリゲート](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent)してバックグラウンド実行

Copilotプランによって、異なるレベルのアクセスと制限がある場合があります。詳細は[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)をご覧ください。

### Copilot使用状況を監視するにはどうすればよいですか?

VS CodeステータスバーのCopilotステータスダッシュボードで現在のCopilot使用状況を表示できます。ダッシュボードには以下の情報が表示されます：

-**インライン提案**：現在の月に使用したインライン提案クォータのパーセンテージ。
-**チャットメッセージ**：現在の月に使用したチャットリクエストクォータのパーセンテージ。
-**プレミアムリクエスト**：現在の月に使用したプレミアムリクエストクォータのパーセンテージ。
-**プレミアムリクエスト超過**：現在の月に使用した超過プレミアムリクエストの数。

GitHub Copilotドキュメントで[使用状況とエンタイトルメント監視](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/monitoring-your-copilot-usage-and-entitlements)について詳しく知ることができます。

### インライン提案またはチャットインタラクションの制限に達しました

インライン提案とチャットインタラクションの制限は毎月リセットされます。チャットインタラクションの制限に達した場合でも、引き続きインライン提案を使用できます。同様に、インライン提案の制限に達した場合でも、引き続きチャットを使用できます。

Copilot Freeのユーザーの場合、より多くのインライン提案とチャットインタラクションにアクセスするには、VS Codeから直接[有料プラン](https://docs.github.com/en/copilot/concepts/billing/individual-plans)にサインアップできます。別の方法として、次の月まで待つことで、無料でCopilotを引き続き使用できます。

![Copilotチャットメッセージの制限に達したことを示すChat表示、ステータスバー、およびタイトルバーの視覚的なインジケーター。](images/faq/copilot-chat-limit-reached.png)

有料プランをご利用で、すべてのプレミアムリクエストを使い切った場合、その月の残りの期間は、含まれるモデルの1つでCopilotを引き続き使用できます。プランの制限を超える追加のプレミアムリクエストをリクエストすることもできます。GitHub Copilotドキュメントで[追加のプレミアムリクエスト取得](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#what-if-i-run-out-of-premium-requests)について詳しく知ることができます。

### VS CodeでCopilotサブスクリプションが検出されません

Visual Studio Codeでチャットをするるには、GitHub Copilotにアクセス可能なGitHubアカウントでVS Codeにサインインする必要があります。

-Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、GitHubアカウントからサインアウトし、別のアカウントでサインインしてください。アクティビティバーの**アカウント**メニューを使用して、現在のGitHubアカウントからサインアウトしてください。詳細は[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)をご覧ください。

-[GitHub Copilot設定](https://github.com/settings/copilot)でCopilotサブスクリプションがまだアクティブであることを確認してください。

-GHE.comの管理ユーザーアカウント用Copilotプランを使用している場合、サインインする前にいくつかの設定を更新する必要があります。[GHE.comのアカウントでGitHub Copilotを使用する](https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/using-github-copilot-with-an-account-on-ghecom)をご覧ください。

### Copilotのアカウントを切り替えるにはどうすればよいですか?

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、VS CodeでGitHubアカウントからサインアウトし、別のアカウントでサインインしてください。

詳細は[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)をご覧ください。

## 一般的なCopilot質問

### VS CodeからCopilotを削除するにはどうすればよいですか?

`setting(chat.disableAIFeatures)`設定を使用してVS Codeの組み込みAI機能を無効にできます。これはVS Codeでの他の機能の設定方法と似ています。これにより、チャットやインライン提案などのVS Code機能が無効になり、非表示になり、Copilot拡張機能が無効になります。ワークスペースまたはユーザーレベルで設定を構成できます。

別の方法として、タイトルバーのチャットメニューから**AI機能を非表示にする方法を学ぶ**アクションを使用して、設定にアクセスしてください。

>[!NOTE]
>以前に組み込みAI機能を無効にした場合、新しいバージョンのVS Codeに更新すると、その選択が尊重されます。

### Copilotのネットワークとファイアウォール設定

-ユーザーまたは組織がファイアウォールやプロキシサーバーなどのセキュリティ対策を実装している場合、特定のドメインURLを「許可リスト」に含め、特定のポートとプロトコルを開くと便利です。GitHub Copilot用の[ファイアウォール設定のトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-firewall-settings-for-github-copilot)の詳細をご覧ください。

-会社のコンピューターで作業していて、企業ネットワークに接続している場合、VPNまたはHTTPプロキシサーバー経由でインターネットに接続している可能性があります。場合によっては、これらのタイプのネットワーク設定により、GitHub CopilotがGitHubのサーバーに接続できない可能性があります。GitHub Copilotの[ネットワークエラーのトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-network-errors-for-github-copilot)の詳細をご覧ください。

### リクエストがレート制限されています

このエラーは、Copilotリクエストのレート制限を超えていることを示唆しています。GitHubはレート制限を使用して、すべてのユーザーがCopilotサービスに公平にアクセスでき、不正使用から保護しています。

GitHubレート制限と、レート制限されている場合の対応について詳しく知ることができます[GitHub Copilotのレート制限](https://docs.github.com/en/copilot/troubleshooting-github-copilot/rate-limits-for-github-copilot)。

### Copilot拡張機能のプリリリースビルドはありますか?

はい。Copilot拡張機能のプリリリース（ナイトリー）バージョンに切り替えて、最新の機能と修正を試すことができます。拡張機能表示から、右クリックするか、歯車アイコンを選択してコンテキストメニューを表示してから、**プリリリースバージョンに切り替える**を選択します：

![プリリリースバージョンに切り替えるオプション付きの拡張機能表示コンテキストメニュー](images/faq/switch-to-pre-release.png)

拡張機能の詳細で「プリリリース」バッジを確認して、プリリリースバージョンを実行しているかどうかを判断できます：

![GitHub Copilot拡張機能のプリリリースバージョン](images/faq/copilot-ext-pre-release.png)

## インライン提案

### インライン提案を有効または無効にするにはどうすればよいですか?

VS CodeステータスバーのCopilotステータスダッシュボードのチェックボックスを使用して、VS Codeのインライン提案を有効または無効にできます。インライン提案をグローバルに、またはアクティブなエディターのファイルタイプに対して有効または無効にできます。

![Copilotアイコンが強調表示されているVS CodeステータスバーとCopilotがアクティブであることを示すスクリーンショット。](./images/faq/copilot-disable-completions.png)

別の方法として、`setting(github.copilot.enable)`および`setting(github.copilot.nextEditSuggestions.enabled)`設定を使用して、それぞれインライン提案と次の編集提案を有効または無効にします。ワークスペースまたはユーザーレベルで設定を構成できます。

### エディターでインライン提案が機能していません

-[GitHub Copilotが無効になっていない](#how-do-i-enable-or-disable-inline-suggestions)ことをグローバルまたはこの言語に対して確認してください
-[GitHub Copilotサブスクリプションがアクティブで検出されている](#my-copilot-subscription-is-not-detected-in-vs-code)ことを確認してください
-[ネットワーク設定](#network-and-firewall-configuration-for-copilot)がGitHub Copilotへの接続を許可するように構成されていることを確認してください。
-[Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free)でその月のインライン提案の制限に達していないことを確認してください。

## チャット

### チャット機能が機能していません

チャット機能がVisual Studio Codeで機能することを確認するには、以下の要件を確認します：

-最新バージョンのVisual Studio Code（**Code：アップデートを確認**を実行）を使用していることを確認します。
-[GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)および[GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)拡張機能の最新バージョンを持っていることを確認します。
-VS Codeにサインインしているアカウントが有効なCopilotサブスクリプションを持っている必要があります。[Copilotサブスクリプション](https://github.com/settings/copilot)を確認してください。
-[Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free)でその月のチャットインタラクション制限に達していないことを確認してください。

### エージェントはチャットで利用できません

VS Code設定でエージェントが有効になっていることを確認します：`setting(chat.agent.enabled)`。組織がこの機能を無効にしている可能性があります。管理者に確認して、エージェントを有効にしてください。

### VS Codeのエージェントにはどのようなことができますか?

エージェントは完全なコーディングタスクを自律的に処理します。マルチステップ実装を計画し、複数のファイルにわたって調整された変更を実行し、ターミナルコマンドを実行し、ツールを呼び出し、エラーが発生したときに自己修正します。エージェントは、機能実装、アーキテクチャレベルのリファクタリング、フレームワークマイグレーション、デバッグ、テスト生成に使用します。[エージェント使用](/docs/copilot/agents/overview.md)について詳しく知ることができます。

### Copilotは大規模なコードベースとモノレポで機能しますか?

はい。VS Codeはセマンティック検索、言語インテリジェンス（LSP）、およびGitHubのコード検索を使用してワークスペースを自動的にインデックス化し、リポジトリ全体で深い理解を提供します。大規模なリポジトリの場合、[リモートインデックス](/docs/copilot/reference/workspace-context.md#remote-index)はGitHubのインデックスを使用して、関連リポジトリ全体で高速で包括的な結果を提供します。[マルチルートワークスペース](/docs/editing/workspaces/multi-root-workspaces.md)を使用してモノレポのコンテキストをスコープし、[カスタム命令](/docs/copilot/customization/custom-instructions.md)を使用してプロジェクトのアーキテクチャを説明します。[大規模コードベースのベストプラクティス](/docs/copilot/best-practices.md#work-with-large-codebases)を参照してください。

### 組織はAI機能とエージェントアクセスを制御できますか?

はい。組織の管理者は、[エンタープライズAI設定](/docs/enterprise/ai-settings.md)および[ポリシー](/docs/enterprise/policies.md)を通じてCopilotを管理できます。これには、エージェントの有効化または無効化、モデルアクセスの制御、コンテンツ除外の構成、信頼境界の実装が含まれます。コンプライアンスの詳細は[GitHub Copilot Trust Center](https://resources.github.com/copilot-trust-center/)をご覧ください。

### エージェントは使用量制限されていますか?

エージェントはCopilotプランのプレミアムリクエストを使用します。有料プランには毎月のプレミアムリクエスト割り当てが含まれており、追加の容量をリクエストできます。ローカル、バックグラウンド、クラウド環境全体で複数のエージェントセッションを並行して実行できます。無料プランのユーザーは毎月のチャットインタラクション制限があります。詳細は[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)をご覧ください。

### 言語モデルピッカーで利用可能なモデルがすべて表示されていません

言語モデルピッカーで利用可能なモデルを選択できます。[言語モデルピッカーをカスタマイズ](/docs/copilot/customization/language-models.md#customize-the-model-picker)する方法をご覧ください。

組織は特定のモデルへのアクセスを制限できます。モデルが利用可能であると思われる場合は、組織の管理者に連絡してください。

### チャット表示が自動的に開くのを防ぐにはどうすればよいですか?

デフォルトでは、チャット表示はセカンダリサイドバーで開きます。ワークスペースでチャット表示を閉じると、VS Codeはこの設定を記憶し、次回そのワークスペースを開いたときにチャット表示を自動的に開きません。

チャット表示から直接デフォルトの表示を変更できます：

1. チャット表示を開きます（`kb(workbench.action.chat.open)`）。
1. チャット表示の右上隅にある`...`アイコンを選択します。
1. **デフォルトで表示**を選択して、チャト表示の自動開閉をオンまたはオフにします。

`setting(workbench.secondarySideBar.defaultVisibility)`設定でセカンダリサイドバーのデフォルト表示を制御することもできます。`hidden`に設定して、チャット表示が自動的に開くのを防いでください。

## トラブルシューティングとフィードバック

### Copilotについてフィードバックを提供するにはどうすればよいですか?

VS Codeの問題とGitHub Copilotの機能リクエストを[microsoft/vscode](https://github.com/microsoft/vscode)GitHubリポジトリで追跡します。このリポジトリで問題を作成するか、VS Codeで以下のフィードバックメカニズムを使用できます：

-**ゴーストテキスト提案**

エディターのゴーストテキスト提案にホバーするときに、**Copilot補完フィードバック送信**アクションを使用します。Issue Reporterで、問題の明確で詳細な説明（再現手順を含む）を提供します。

![エディターでCopilotGhost TextFeedbackアクションを送信するスクリーンショット。](images/faq/code-completions-feedback.png)

-**次の編集提案**

エディターの溝にある次の編集提案メニューで**フィードバック**アクションを選択します。Issue Reporterで、問題の明確で詳細な説明（再現手順を含む）を提供します。

![エディターの溝にある次の編集提案メニューのスクリーンショット。](images/faq/nes-feedback.png)

-**一般的な問題**

VS Code Issue Reporter（**ヘルプメニュー**>**問題を報告**）を開き、**VS Code拡張機能**ソースを選択し、**GitHub Copilot Chat**拡張機能を選択します。問題の明確で詳細な説明（再現手順を含む）を提供します。

![GitHub Copilot Chatが選択されたVS Code Issue Reporterのスクリーンショット。](images/faq/issue-reporter.png)

問題を報告するときは、[wiki](https://github.com/microsoft/vscode/wiki/Copilot-Issues)のガイドラインに従って、問題が実行可能であることを確認します。

問題を報告する際、Copilotログから情報を含めるのに役立つ場合があります。[ログを表示して診断を収集](/docs/copilot/troubleshooting.md)する方法をご覧ください。

## 追加リソース

-[GitHub Copilot Trust Center](https://resources.github.com/copilot-trust-center/)
-[VS CodeのAIのセキュリティに関する考慮事項](/docs/copilot/security.md)
-GitHubドキュメントの[GitHub Copilot FAQ](https://github.com/features/copilot#faq)

