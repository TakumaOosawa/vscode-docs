---
ContentId: e02ded07-6e5a-4f94-b618-434a2c3e8f09
DateApproved: 01/08/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用するためのよくある質問。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot に関するよくある質問

この記事では、Visual Studio CodeでGitHub Copilotを使用することに関するよくある質問に回答します。

## GitHub Copilot サブスクリプション

### Copilotサブスクリプションを入手するにはどうすればよいですか？

GitHub Copilotにアクセスするには、さまざまな方法があります：

| ユーザーの種類                   | 説明 |
|--------------------------------|-------------|
| 個人                     | <ul><li>基本的な機能を無料で試すには、インライン提案とチャットの月間制限があるGitHub Copilot Freeを設定します。</li><li>より柔軟で高度な機能にアクセスするには、有料のGitHub Copilotプランにサインアップします。</li><li>すべてのオプションについては、[自分用にGitHub Copilotを設定する](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-yourself)を参照してください。 </li></ul> |
| 組織/エンタープライズメンバー | <ul><li>GitHub Copilotのサブスクリプションを持つ組織またはエンタープライズのメンバーである場合、<https://github.com/settings/copilot>にアクセスし、「組織からCopilotを取得」でアクセスをリクエストできます。</li><li>組織でCopilotを有効にするには、[組織用にGitHub Copilotを設定する](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-your-organization)を参照してください。</li></ul> |

### GitHubアカウントでサインインする利点は何ですか？

GitHub Copilotへのアクセス権を持つGitHubアカウントでサインインすると、次の利点があります：

* [チャットインタラクションの月間制限の増加](https://docs.github.com/en/copilot/get-started/plans#comparing-copilot-plans)
* 自動モデル選択を超えた[チャットでのプレミアム言語モデルへのアクセス](https://docs.github.com/en/copilot/reference/ai-models/supported-models#supported-ai-models-per-copilot-plan)
* より多くのモデルにアクセスするための[独自のモデルキーの持ち込み](/docs/copilot/customization/language-models.md#bring-your-own-language-model-key) (BYOK)
* [リモートリポジトリのインデックス作成とセマンティックコード検索](/docs/copilot/reference/workspace-context.md#remote-index)
* [Copilotコードレビュー](https://docs.github.com/en/copilot/concepts/agents/code-review)
* [Copilotコンテンツの除外](https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot)
* バックグラウンド実行のための[Copilotコーディングエージェントへのタスク委任](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent)

Copilotプランによっては、アクセスレベルと制限が異なる場合があります。詳細については、[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)を参照してください。

### Copilotの使用状況を確認するにはどうすればよいですか？

現在のCopilotの使用状況は、VS Codeステータスバーから利用できるCopilotステータスダッシュボードで確認できます。ダッシュボードには、次の情報が表示されます：

- **インライン提案**: 当月に使用したインライン提案の割り当ての割合。
- **チャットメッセージ**: 当月に使用したチャットリクエストの割り当ての割合。
- **プレミアムリクエスト**: 当月に使用したプレミアムリクエストの割り当ての割合。
- **プレミアムリクエストの超過**: 当月に使用した超過プレミアムリクエストの数。

[使用状況と権利の監視](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/monitoring-your-copilot-usage-and-entitlements)の詳細については、GitHub Copilotのドキュメントを参照してください。

### インライン提案またはチャットインタラクションの制限に達しました

インライン提案とチャットインタラクションの制限は、毎月リセットされます。チャットインタラクションの制限にのみ達した場合でも、インライン提案は引き続き使用できます。同様に、インライン提案の制限に達した場合でも、チャットは引き続き使用できます。

Copilot Freeのユーザーの場合、より多くのインライン提案とチャットインタラクションにアクセスするには、VS Codeから直接[有料プラン](https://docs.github.com/en/copilot/concepts/billing/individual-plans)にサインアップできます。あるいは、翌月まで待ってCopilotを無料で使い続けることもできます。

![Copilotチャットメッセージの制限に達したことを示すチャットビュー、ステータスバー、タイトルバーの視覚的なインジケーター。](images/faq/copilot-chat-limit-reached.png)

有料プランを利用していてプレミアムリクエストをすべて使い切った場合でも、その月の残りの期間は、含まれているモデルのいずれかでCopilotを引き続き使用できます。また、プランの制限を超えて追加のプレミアムリクエストをリクエストすることもできます。[追加のプレミアムリクエストを取得する](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#what-if-i-run-out-of-premium-requests)の詳細については、GitHub Copilotのドキュメントを参照してください。

### VS CodeでCopilotサブスクリプションが検出されません

Visual Studio Codeでチャットを使用するには、GitHub Copilotへのアクセス権を持つGitHubアカウントでVisual Studio Codeにサインインする必要があります。

- Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、GitHubアカウントからサインアウトして、別のアカウントでサインインしてください。現在のGitHubアカウントからサインアウトするには、アクティビティバーの**アカウント**メニューを使用します。詳細については、[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)を参照してください。

- [GitHub Copilot設定](https://github.com/settings/copilot)でCopilotサブスクリプションがまだ有効であることを確認してください。

- GHE.comの管理対象ユーザーアカウントでCopilotプランを使用している場合は、サインインする前にいくつかの設定を更新する必要があります。[GHE.comのアカウントでGitHub Copilotを使用する](https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/using-github-copilot-with-an-account-on-ghecom)を参照してください。

### Copilotのアカウントを切り替えるにはどうすればよいですか

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、VS CodeでGitHubアカウントからサインアウトし、別のアカウントでサインインしてください。

詳細については、[Copilotで別のGitHubアカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)を参照してください。

## 一般的なCopilotの質問

### VS CodeからCopilotを削除するにはどうすればよいですか？

他の機能を構成するのと同様に、`setting(chat.disableAIFeatures)`設定を使用して、VS Codeの組み込みAI機能を無効にできます。これにより、VS Codeのチャットやインライン提案などの機能が無効になり非表示になり、Copilot拡張機能が無効になります。この設定は、ワークスペースまたはユーザーレベルで構成できます。

あるいは、タイトルバーのチャットメニューから**AI機能を非表示にする方法**アクションを使用して設定にアクセスします。

> [!NOTE]
> 以前に組み込みのAI機能を無効にしていた場合、その選択はVS Codeの新しいバージョンへの更新時に尊重されます。

### Copilotのネットワークとファイアウォールの構成

- あなたやあなたの組織がファイアウォールやプロキシサーバーなどのセキュリティ対策を採用している場合、特定のドメインURLを「許可リスト」に含め、特定のポートとプロトコルを開くことが有益な場合があります。[GitHub Copilotのファイアウォール設定のトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-firewall-settings-for-github-copilot)について詳しく学びます。

- 会社の機器で作業し、企業ネットワークに接続している場合は、VPNまたはHTTPプロキシサーバー経由でインターネットに接続している可能性があります。場合によっては、これらの種類のネットワーク設定により、GitHub CopilotがGitHubのサーバーに接続できないことがあります。[GitHub Copilotのネットワークエラーのトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-network-errors-for-github-copilot)について詳しく学びます。

### リクエストがレート制限されています

このエラーは、Copilotリクエストのレート制限を超えたことを示唆しています。GitHubは、全員が公平にCopilotサービスにアクセスできるようにし、悪用を防ぐためにレート制限を使用しています。

レート制限とレート制限された場合の対処方法の詳細については、[GitHub Copilotのレート制限](https://docs.github.com/en/copilot/troubleshooting-github-copilot/rate-limits-for-github-copilot)を参照してください。

### Copilot拡張機能のプレリリースビルドはありますか？

はい、Copilot拡張機能のプレリリース（ナイトリー）バージョンに切り替えて、最新の機能や修正を試すことができます。拡張機能ビューから、右クリックするか歯車のアイコンを選択してコンテキストメニューを表示し、**プレリリースバージョンへの切り替え**を選択します：

![プレリリースバージョンへの切り替えオプションがある拡張機能ビューのコンテキストメニュー](images/faq/switch-to-pre-release.png)

プレリリースバージョンを実行しているかどうかは、拡張機能の詳細にある「プレリリース」バッジで確認できます：

![GitHub Copilot拡張機能のプレリリースバージョン](images/faq/copilot-ext-pre-release.png)

## インライン提案

### インライン提案を有効または無効にするにはどうすればよいですか？

VS CodeステータスバーのCopilotステータスダッシュボードにあるチェックボックスを使用して、VS Codeでのインライン提案を有効または無効にできます。インライン提案は、グローバルに、またはアクティブなエディターのファイルタイプに対して有効または無効にできます。

![Copilotがアクティブであることを示すCopilotアイコンを強調表示したVS Codeステータスバーを示すスクリーンショット。](./images/faq/copilot-disable-completions.png)

あるいは、`setting(github.copilot.enable)`および`setting(github.copilot.nextEditSuggestions.enabled)`設定を使用して、それぞれインライン提案と次の編集提案を有効または無効にします。これらの設定は、ワークスペースまたはユーザーレベルで構成できます。

### エディターでインライン提案が機能しない

- [GitHub Copilotが無効になっていない](#how-do-i-enable-or-disable-inline-suggestions)こと（グローバルまたはこの言語に対して）を確認してください。
- [GitHub Copilotサブスクリプションがアクティブで検出されている](#my-copilot-subscription-is-not-detected-in-vs-code)ことを確認してください。
- [ネットワーク設定](#network-and-firewall-configuration-for-copilot)がGitHub Copilotへの接続を許可するように構成されていることを確認してください。
- [Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free)での当月のインライン提案の制限に達していないことを確認してください。

## チャット

### チャット機能が機能しない

Visual Studio Codeでチャット機能が機能することを確認するには、次の要件を確認してください：

- Visual Studio Codeの最新バージョンを使用していることを確認してください（**Code: 更新の確認**を実行）。
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)と[GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)の両方の拡張機能の最新バージョンを使用していることを確認してください。
- VS CodeにサインインしているGitHubアカウントに、アクティブなCopilotサブスクリプションが必要です。[Copilotサブスクリプション](https://github.com/settings/copilot)を確認してください。
- [Copilot Freeプラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free)での当月のチャットインタラクションの制限に達していないことを確認してください。

### エージェントがチャットで利用できない

VS Codeの設定でエージェントが有効になっていることを確認してください：`setting(chat.agent.enabled)`。組織がこの機能を無効にしている可能性があります。管理者に確認してエージェントを有効にしてもらってください。

### 言語モデルピッカーですべてのモデルが利用できるわけではない

言語モデルピッカーで利用可能なモデルを選択できます。[言語モデルピッカーをカスタマイズする](/docs/copilot/customization/language-models.md#customize-the-model-picker)方法について詳しく学びます。

組織は特定のモデルへのアクセスを制限できます。モデルを利用できるようにする必要があると思われる場合は、組織の管理者に連絡してください。

### チャットビューが自動的に開かないようにするにはどうすればよいですか？

デフォルトでは、チャットビューはセカンダリサイドバーで開きます。ワークスペースのチャットビューを閉じると、VS Codeはこの設定を記憶し、次回そのワークスペースを開いたときにチャットビューを自動的に開きません。

チャットビューから直接デフォルトの可視性を変更できます：

1. チャットビューを開きます（`kb(workbench.action.chat.open)`）。
1. チャットビューの右上隅にある`...`アイコンを選択します。
1. **ビューをデフォルトで表示**を選択して、チャットビューの自動オープンを有効または無効にします。

`setting(workbench.secondarySideBar.defaultVisibility)`設定を使用して、セカンダリサイドバーのデフォルトの可視性を制御することもできます。チャットビューが自動的に開かないようにするには、`hidden`に設定します。

## トラブルシューティングとフィードバック

### Copilotに関するフィードバックを提供するにはどうすればよいですか？

VS CodeでのGitHub Copilotに関する問題と機能リクエストは、[microsoft/vscode](https://github.com/microsoft/vscode) GitHubリポジトリで追跡しています。このリポジトリで問題を作成するか、VS Codeで次のフィードバックメカニズムを使用できます：

- **ゴーストテキストの提案**

    エディターでゴーストテキストの提案にカーソルを合わせるときに、**Copilot完了フィードバックを送信**アクションを使用します。問題レポーターで、再現手順を含む問題の明確で詳細な説明を提供してください。

    ![エディターでのCopilotゴーストテキストフィードバックの送信アクションを示すスクリーンショット。](images/faq/code-completions-feedback.png)

- **次の編集提案**

    エディターのガターにある次の編集提案メニューで**フィードバック**アクションを選択します。問題レポーターで、再現手順を含む問題の明確で詳細な説明を提供してください。

    ![エディターのガターにある次の編集提案メニューを示すスクリーンショット。](images/faq/nes-feedback.png)

- **一般的な問題**

    VS Code問題レポーター（**ヘルプメニュー** > **問題を報告**）を開き、**VS Code拡張機能**ソースを選択してから、**GitHub Copilot Chat**拡張機能を選択します。再現手順を含む問題の明確で詳細な説明を提供してください。

    ![GitHub Copilot Chatが選択されたVS Code問題レポーターを示すスクリーンショット。](images/faq/issue-reporter.png)

問題を報告するときは、問題が実行可能であることを確認するために、[wiki](https://github.com/microsoft/vscode/wiki/Copilot-Issues)のガイドラインに従ってください。

問題を報告する場合は、[VS CodeのGitHub Copilotログを表示する](#view-logs-for-github-copilot-in-vs-code)からの情報を含めると役立つ場合があります。

### VS CodeのGitHub Copilotログを表示する

GitHub Copilot拡張機能のログファイルは、Visual Studio Code拡張機能の標準ログ場所に保存されます。

VS CodeでCopilotの詳細なログを取得するには、次の手順に従います：

1. コマンドパレット（`kb(workbench.action.showCommands)`）で、**Developer: Set Log Level**コマンドを実行し、値を**Trace**に設定します（これは、GitHub CopilotおよびGitHub Copilot Chat拡張機能に対してのみ実行できます）。
1. コマンドパレット（`kb(workbench.action.showCommands)`）で、**Output: Show Output Channels**コマンドを実行し、リストからGitHub CopilotまたはGitHub Copilot Chatを選択します。
1. 出力パネルで、選択した拡張機能のログを確認できます。
1. 別の出力チャネルに切り替えるには、出力パネルの右側にあるドロップダウンメニューから**GitHub Copilot**または**GitHub Copilot Chat**を選択します。

GitHub Copilotへの接続に問題が発生した場合は、ネットワーク接続診断ログを表示できます：

1. コマンドパレット（`kb(workbench.action.showCommands)`）を開きます。
1. **GitHub Copilot: Collect Diagnostics**コマンドを実行します。
1. 診断情報を検査できるエディタータブが開きます。

### チャットデバッグビューを使用する

チャットデバッグビューを使用して、使用されているプロンプトや言語モデルに送信されるコンテキストなど、AIのリクエストとレスポンスの詳細を確認できます。このビューは、AIがリクエストをどのように解釈しているか、レスポンスを生成するためにどのようなコンテキストを使用しているかを理解するのに役立ちます。

[チャットデバッグビュー](/docs/copilot/chat/chat-debug-view.md)について詳しく学びます。

## その他のリソース

- [GitHub Copilotトラストセンター](https://resources.github.com/copilot-trust-center/)
- GitHubドキュメントの[GitHub Copilot FAQ](https://github.com/features/copilot#faq)
