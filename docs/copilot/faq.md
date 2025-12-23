---
ContentId: e02ded07-6e5a-4f94-b618-434a2c3e8f09
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotを使用する際のよくある質問です。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilotのよくある質問

この記事では、Visual Studio CodeでGitHub Copilotを使用する際のよくある質問に回答します。

## GitHub Copilotのサブスクリプション

### Copilotのサブスクリプションを取得するにはどうすればよいですか？

GitHub Copilotにアクセスする方法はいくつかあります:

| ユーザーの種類                 | 説明 |
|--------------------------------|-------------|
| 個人                           | <ul><li>インライン候補とチャットのやり取りに月ごとの上限がある、無償のGitHub Copilot Freeを設定して、基本的な機能を試すことができます。</li><li>より柔軟に利用でき、プレミアム機能にもアクセスできる有料のGitHub Copilotプランに申し込みます。</li><li>すべての選択肢については、[自分用にGitHub Copilotをセットアップする](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-yourself)を参照してください。</li></ul> |
| 組織/Enterpriseのメンバー      | <ul><li>GitHub Copilotのサブスクリプションを持つ組織またはEnterpriseのメンバーであれば、<https://github.com/settings/copilot>にアクセスし、「Get Copilot from an organization」の下でアクセスを要求することで、Copilotへのアクセスをリクエストできます。</li><li>組織でCopilotを有効にする方法については、[組織用にGitHub Copilotをセットアップする](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-your-organization)を参照してください。</li></ul> |

### GitHubアカウントでサインインする利点は何ですか？

GitHub CopilotにアクセスできるGitHubアカウントでサインインすると、次の利点があります:

* [チャットのやり取りの月ごとの上限の増加](https://docs.github.com/en/copilot/get-started/plans#comparing-copilot-plans)
* [チャットでプレミアム言語モデルにアクセス](https://docs.github.com/en/copilot/reference/ai-models/supported-models#supported-ai-models-per-copilot-plan)（自動モデル選択以外）
* [独自のモデルキーを持ち込む](/docs/copilot/customization/language-models.md#bring-your-own-language-model-key)（BYOK）ことで、より多くのモデルにアクセス
* [リモートリポジトリのインデックス作成とセマンティックコード検索](/docs/copilot/reference/workspace-context.md#remote-index)
* [Copilotのコードレビュー](https://docs.github.com/en/copilot/concepts/agents/code-review)
* [Copilotのコンテンツ除外](https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot)
* [バックグラウンド実行のためにCopilotコーディングエージェントにタスクを委任](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent)

Copilotプランによって、アクセスできる内容や制限は異なる場合があります。詳細については、[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)を参照してください。

### Copilotの使用状況を監視するにはどうすればよいですか？

現在のCopilot使用状況は、VS Codeのステータスバーから利用できるCopilotステータスダッシュボードで確認できます。ダッシュボードには次の情報が表示されます:

- **インライン候補**: 今月使用したインライン候補のクォータの割合。
- **チャットメッセージ**: 今月使用したチャット要求のクォータの割合。
- **プレミアム要求**: 今月使用したプレミアム要求のクォータの割合。
- **プレミアム要求の超過**: 今月使用した超過プレミアム要求の回数。

[使用状況と権利の監視](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/monitoring-your-copilot-usage-and-entitlements)の詳細については、GitHub Copilotドキュメントを参照してください。

### インライン候補またはチャットのやり取りの上限に達しました

インライン候補とチャットのやり取りの上限は毎月リセットされます。チャットのやり取りの上限にのみ達した場合でも、インライン候補は引き続き使用できます。同様に、インライン候補の上限に達した場合でも、チャットは引き続き使用できます。

Copilot Freeのユーザーがより多くのインライン候補とチャットのやり取りにアクセスするには、VS Codeから直接[有料プラン](https://docs.github.com/en/copilot/concepts/billing/individual-plans)に申し込むことができます。あるいは、翌月まで待って、Copilotを引き続き無料で使用することもできます。

![チャットビュー、ステータスバー、タイトルバーに表示される、Copilotチャットメッセージの上限に達したことを示す視覚的なインジケーター。](images/faq/copilot-chat-limit-reached.png)

有料プランを利用していてプレミアム要求をすべて使い切った場合でも、その月の残りの期間は同梱のモデルのいずれかでCopilotを引き続き使用できます。また、プランの上限を超えて追加のプレミアム要求をリクエストすることもできます。[追加のプレミアム要求を取得する](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#what-if-i-run-out-of-premium-requests)方法については、GitHub Copilotドキュメントを参照してください。

### VS CodeでCopilotサブスクリプションが検出されません

Visual Studio Codeでチャットを使用するには、GitHub CopilotにアクセスできるGitHubアカウントでVisual Studio Codeにサインインしている必要があります。

- Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、GitHubアカウントからサインアウトして、別のアカウントでサインインしてください。現在のGitHubアカウントからサインアウトするには、アクティビティバーの**Accounts**メニューを使用します。詳細については、[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)を参照してください。

- [GitHub Copilot settings](https://github.com/settings/copilot)でCopilotサブスクリプションが引き続き有効であることを確認してください。

- GHE.comのマネージドユーザーアカウント向けのCopilotプランを使用している場合は、サインインする前にいくつかの設定を更新する必要があります。[GHE.comのアカウントでGitHub Copilotを使用する](https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/using-github-copilot-with-an-account-on-ghecom)を参照してください。

### Copilotでアカウントを切り替えるにはどうすればよいですか？

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、VS CodeでGitHubアカウントからサインアウトし、別のアカウントでサインインしてください。

詳細については、[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)を参照してください。

## Copilotに関する一般的な質問

### VS CodeからCopilotを削除するにはどうすればよいですか？

VS Codeの他の機能と同様に、`setting(chat.disableAIFeatures)`設定でVS Codeに組み込まれたAI機能を無効にできます。これにより、VS Codeのチャットやインライン候補などの機能が無効化されて非表示になり、Copilot拡張機能も無効になります。この設定は、ワークスペースレベルまたはユーザーレベルで構成できます。

または、タイトルバーのチャットメニューから**Learn How to Hide AI Features**アクションを使用して設定にアクセスします。

> [!NOTE]
> 以前に組み込みのAI機能を無効にしている場合、その選択はVS Codeの新しいバージョンに更新しても尊重されます。

### Copilotのネットワークとファイアウォールの構成

- あなたや組織がファイアウォールやプロキシサーバーなどのセキュリティ対策を採用している場合、特定のドメインURLを「allowlist」に追加し、特定のポートとプロトコルを開放すると有益な場合があります。トラブルシューティングの詳細については、[GitHub Copilotのファイアウォール設定](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-firewall-settings-for-github-copilot)を参照してください。

- 会社の機器で作業し、社内ネットワークに接続している場合、VPNまたはHTTPプロキシサーバー経由でインターネットに接続していることがあります。場合によっては、この種のネットワーク構成によりGitHub CopilotがGitHubのサーバーに接続できないことがあります。詳細については、[GitHub Copilotのネットワークエラーのトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-network-errors-for-github-copilot)を参照してください。

### リクエストがレート制限されました

このエラーは、Copilotリクエストのレート制限を超えたことを示しています。GitHubは、誰もが公平にCopilotサービスへアクセスできるようにし、悪用から保護するためにレート制限を使用しています。

レート制限の詳細と、レート制限された場合の対処方法については、[GitHub Copilotのレート制限](https://docs.github.com/en/copilot/troubleshooting-github-copilot/rate-limits-for-github-copilot)を参照してください。

### Copilot拡張機能のプレリリースビルドはありますか？

はい。Copilot拡張機能をプレリリース（nightly）バージョンに切り替えて、最新の機能や修正を試すことができます。拡張機能ビューから右クリックするか、歯車アイコンを選択してコンテキストメニューを表示し、**Switch to Pre-Release Version**を選択します:

![Extensions view context menu with Switch to Pre-Release Version option](images/faq/switch-to-pre-release.png)

拡張機能の詳細にある「Pre-release」バッジで、プレリリースバージョンを実行しているかどうかを確認できます:

![Pre-release version of the GitHub Copilot extension](images/faq/copilot-ext-pre-release.png)

## インライン候補

### インライン候補を有効または無効にするにはどうすればよいですか？

VS CodeのステータスバーからCopilotステータスダッシュボードを開き、チェックボックスを使用してVS Codeのインライン候補を有効または無効にできます。インライン候補は、グローバルに、またはアクティブなエディターのファイルの種類ごとに有効/無効を切り替えられます。

![Screenshot showing the VS Code status bar, highlighting the Copilot icon that indicates Copilot is active.](./images/faq/copilot-disable-completions.png)

または、`setting(github.copilot.enable)`と`setting(github.copilot.nextEditSuggestions.enabled)`設定を使用して、それぞれインライン候補と次の編集候補を有効または無効にできます。これらの設定は、ワークスペースレベルまたはユーザーレベルで構成できます。

### エディターでインライン候補が動作しません

- Verify that [GitHub Copilot is not disabled](#how-do-i-enable-or-disable-inline-suggestions) globally or for this language
- Verify that your [GitHub Copilot subscription is active and detected](#my-copilot-subscription-is-not-detected-in-vs-code)
- Verify that your [network settings](#network-and-firewall-configuration-for-copilot) are configured to allow connectivity to GitHub Copilot.
- Verify that you have not reached the limit of inline suggestions for the month with the [Copilot Free plan](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free).

## チャット

### チャット機能が動作しません

Visual Studio Codeでチャット機能が動作することを確認するため、次の要件を確認してください:

- Visual Studio Codeが最新バージョンであることを確認してください（**Code: Check for Updates**を実行します）。
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)拡張機能と[GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)拡張機能の両方が最新バージョンであることを確認してください。
- VS CodeにサインインしているGitHubアカウントに、有効なCopilotサブスクリプションが必要です。[Copilotサブスクリプション](https://github.com/settings/copilot)を確認してください。
- [Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free)で今月のチャットのやり取りの上限に達していないことを確認してください。

### チャットでエージェントを利用できません

VS Code設定でエージェントが有効になっていることを確認してください:`setting(chat.agent.enabled)`。組織がこの機能を無効にしている可能性があります。エージェントを有効にするには、管理者に確認してください。

### 言語モデルピッカーで利用できないモデルがあります

言語モデルピッカーで利用できるモデルは選択できます。[言語モデルピッカーをカスタマイズする](/docs/copilot/customization/language-models.md#customize-the-model-picker)方法を確認してください。

組織は特定のモデルへのアクセスを制限できます。利用できるべきモデルが利用できないと考えられる場合は、組織の管理者に連絡してください。

### チャットビューが自動的に開かないようにするにはどうすればよいですか？

既定では、チャットビューはセカンダリサイドバーで開きます。ワークスペースでチャットビューを閉じると、VS Codeはこの設定を記憶し、次回そのワークスペースを開いたときにチャットビューを自動的に開きません。

既定の表示/非表示は、チャットビューから直接変更できます:

1. Open the Chat view (`kb(workbench.action.chat.open)`).
1. Select the `...` icon in the top-right corner of the Chat view.
1. Select **Show View by Default** to enable or disable the automatic opening of the Chat view.

`setting(workbench.secondarySideBar.defaultVisibility)`設定を使用して、セカンダリサイドバーの既定の表示/非表示も制御できます。`hidden`に設定すると、チャットビューが自動的に開かないようにできます。

## トラブルシューティングとフィードバック

### Copilotにフィードバックを送るにはどうすればよいですか？

VS CodeのGitHub Copilotに関する問題と機能要望は、[microsoft/vscode](https://github.com/microsoft/vscode) GitHubリポジトリで追跡しています。このリポジトリでIssueを作成するか、VS Codeで次のフィードバック手段を使用できます:

- **ゴーストテキストの候補**

    エディターでゴーストテキストの候補にカーソルを合わせたときに、**Send Copilot Completion Feedback**アクションを使用します。Issue Reporterで、再現手順を含め、問題の明確で詳細な説明を記載してください。

    ![Screenshot that shows sending Copilot Ghost Text Feedback action in the editor.](images/faq/code-completions-feedback.png)

- **次の編集候補**

    エディターのガターにある次の編集候補メニューで**Feedback**アクションを選択します。Issue Reporterで、再現手順を含め、問題の明確で詳細な説明を記載してください。

    ![Screenshot that shows next edit suggestions menu in the editor gutter.](images/faq/nes-feedback.png)

- **一般的な問題**

    VS Code Issue reporter（**Help menu** > **Report Issue**）を開き、**VS Code Extension**ソースを選択してから、**GitHub Copilot Chat**拡張機能を選択します。再現手順を含め、問題の明確で詳細な説明を記載してください。

    ![Screenshot that shows VS Code Issue Reporter with GitHub Copilot Chat selected.](images/faq/issue-reporter.png)

Issueを報告するときは、報告内容が対応可能なものになるように、[wiki](https://github.com/microsoft/vscode/wiki/Copilot-Issues)のガイドラインに従ってください。

Issueを報告する場合、[GitHub Copilotログ](#view-logs-for-github-copilot-in-vs-code)の情報を含めると役立つことがあります。

### VS CodeでGitHub Copilotのログを表示する

GitHub Copilot拡張機能のログファイルは、Visual Studio Code拡張機能の標準のログ保存場所に格納されます。

VS CodeでCopilotの詳細ログを取得するには、次の手順に従います:

1. In the Command Palette (`kb(workbench.action.showCommands)`), run the **Developer: Set Log Level** command and set the value to **Trace** (you can do this only for the GitHub Copilot and GitHub Copilot Chat extensions).
1. In the Command Palette (`kb(workbench.action.showCommands)`), run the **Output: Show Output Channels** command and select either GitHub Copilot or GitHub Copilot Chat from the list.
1. In the Output panel, you can see the logs for the selected extension.
1. To switch to another output channel, on the right of the Output panel, select **GitHub Copilot** or **GitHub Copilot Chat** from the dropdown menu.

GitHub Copilotへの接続で問題が発生した場合は、ネットワーク接続診断ログを表示できます:

1. Open the Command Palette (`kb(workbench.action.showCommands)`).
1. Run the **GitHub Copilot: Collect Diagnostics** command.
1. An editor tab opens where you can inspect the diagnostics information.

### Chat Debug viewを使用する

Chat Debug viewを使用すると、使用中のプロンプトや言語モデルに送信されるコンテキストなど、AIリクエストと応答の詳細を確認できます。このビューは、AIがリクエストをどのように解釈し、どのコンテキストを使って応答を生成しているかを理解するのに役立ちます。

[Chat Debug view](/docs/copilot/chat/chat-debug-view.md)の詳細を確認してください。

## 追加リソース

- [GitHub Copilot Trust Center](https://resources.github.com/copilot-trust-center/)
- GitHubドキュメントの[GitHub Copilot FAQ](https://github.com/features/copilot#faq)
