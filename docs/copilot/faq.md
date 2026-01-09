---
ContentId: e02ded07-6e5a-4f94-b618-434a2c3e8f09
DateApproved: 12/10/2025
MetaDescription: Visual Studio Code で GitHub Copilot を使用するためのよくある質問。
MetaSocialImage: images/shared/github-copilot-social.png
---
# GitHub Copilot よくある質問

この記事では、Visual Studio Code で GitHub Copilot を使用する際のよくある質問に回答します。

## GitHub Copilot サブスクリプション

### Copilot サブスクリプションを取得するにはどうすればよいですか？

GitHub Copilot にアクセスするには、いくつかの方法があります：

| ユーザーの種類                   | 説明 |
|--------------------------------|-------------|
| 個人                     | <ul><li>GitHub Copilot Free をセットアップすると、インライン提案やチャットインタラクションの月間制限内で基本的な機能を無料で試すことができます。</li><li>より柔軟性を高め、プレミアム機能にアクセスするには、有料の GitHub Copilot プランにサインアップしてください。</li><li>すべてのオプションについては、[個人用 GitHub Copilot の設定](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-yourself)を参照してください。</li></ul> |
| 組織/エンタープライズメンバー | <ul><li>GitHub Copilot のサブスクリプションを持つ組織またはエンタープライズのメンバーである場合、<https://github.com/settings/copilot> にアクセスし、「Get Copilot from an organization」の下でアクセスをリクエストすることで、Copilot へのアクセスをリクエストできます。</li><li>組織で Copilot を有効にするには、[組織での GitHub Copilot の設定](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-your-organization)を参照してください。</li></ul> |

### GitHub アカウントでサインインする利点は何ですか？

アクセス権を持つ GitHub アカウントでサインインすると、GitHub Copilot に以下の利点があります：

* [チャットインタラクションの月間制限の増加](https://docs.github.com/en/copilot/get-started/plans#comparing-copilot-plans)
* 自動モデル選択を超えた [チャットでのプレミアム言語モデルへのアクセス](https://docs.github.com/en/copilot/reference/ai-models/supported-models#supported-ai-models-per-copilot-plan)
* [独自のモデルキーの持ち込み](/docs/copilot/customization/language-models.md#bring-your-own-language-model-key) (BYOK) による追加モデルへのアクセス
* [リモートリポジトリのインデックス作成とセマンティックコード検索](/docs/copilot/reference/workspace-context.md#remote-index)
* [Copilot コードレビュー](https://docs.github.com/en/copilot/concepts/agents/code-review)
* [Copilot コンテンツ除外](https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot)
* バックグラウンド実行のための [Copilot コーディングエージェントへのタスク委任](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent)

Copilot プランによっては、アクセスレベルや制限が異なる場合があります。詳細については、[GitHub Copilot プラン](https://docs.github.com/en/copilot/get-started/plans)を参照してください。

### Copilot の使用状況を確認するにはどうすればよいですか？

現在の Copilot の使用状況は、VS Code ステータスバーから利用できる Copilot ステータスダッシュボードで確認できます。ダッシュボードには以下の情報が表示されます：

- **インライン提案**: 今月のインライン提案クォータの使用率。
- **チャットメッセージ**: 今月のチャットリクエストクォータの使用率。
- **プレミアムリクエスト**: 今月のプレミアムリクエストクォータの使用率。
- **プレミアムリクエスト超過分**: 今月既に使用した超過分のプレミアムリクエスト数。

[使用状況とエンタイトルメントの監視](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/monitoring-your-copilot-usage-and-entitlements)に関する詳細については、GitHub Copilot ドキュメントを参照してください。

### インライン提案またはチャットインタラクションの制限に達しました

インライン提案とチャットインタラクションの制限は毎月リセットされます。チャットインタラクションの制限にのみ達した場合でも、インライン提案は引き続き使用できます。同様に、インライン提案の制限に達した場合でも、チャットは引き続き使用できます。

Copilot Free のユーザーは、VS Code から直接 [有料プラン](https://docs.github.com/en/copilot/concepts/billing/individual-plans)にサインアップすることで、より多くのインライン提案やチャットインタラクションにアクセスできます。あるいは、翌月になるまで待ってから Copilot を無料で使い続けることもできます。

![Copilot チャットメッセージの制限に達したことを示す、チャットビュー、ステータスバー、タイトルバーの視覚的なインジケーター。](images/faq/copilot-chat-limit-reached.png)

有料プランを利用していてプレミアムリクエストをすべて使い切った場合でも、その月の残りの期間は含まれているモデルのいずれかで Copilot を引き続き使用できます。また、プランの制限を超えて追加のプレミアムリクエストをリクエストすることもできます。[追加のプレミアムリクエストの取得](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#what-if-i-run-out-of-premium-requests)に関する詳細は、GitHub Copilot ドキュメントを参照してください。

### VS Code で Copilot サブスクリプションが検出されません

Visual Studio Code でチャットを使用するには、GitHub Copilot にアクセスできる GitHub アカウントで Visual Studio Code にサインインする必要があります。

- Copilot サブスクリプションが別の GitHub アカウントに関連付けられている場合は、現在の GitHub アカウントからサインアウトし、別のアカウントでサインインしてください。現在のアカウントからサインアウトするには、アクティビティバーの **アカウント** メニューを使用してください。詳細については、[Copilot で別の GitHub アカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)を参照してください。

- [GitHub Copilot 設定](https://github.com/settings/copilot)で、Copilot サブスクリプションがまだ有効であることを確認してください。

- GHE.com 上の管理対象ユーザーアカウントで Copilot プランを使用している場合は、サインインする前にいくつかの設定を更新する必要があります。[GHE.com アカウントでの GitHub Copilot の使用](https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/using-github-copilot-with-an-account-on-ghecom)を参照してください。

### Copilot のアカウントを切り替えるにはどうすればよいですか？

Copilot サブスクリプションが別の GitHub アカウントに関連付けられている場合は、VS Code で GitHub アカウントからサインアウトし、別のアカウントでサインインしてください。

詳細については、[Copilot で別の GitHub アカウントを使用する](/docs/copilot/setup.md#use-a-different-github-account-with-copilot)を参照してください。

## 一般的な Copilot の質問

### VS Code から Copilot を削除するにはどうすればよいですか？

VS Code の他の機能を構成するのと同様に、`setting(chat.disableAIFeatures)` 設定を使用して VS Code の組み込み AI 機能を無効にすることができます。これにより、VS Code のチャットやインライン提案などの機能が無効化され非表示になり、Copilot 拡張機能も無効化されます。この設定はワークスペースまたはユーザーレベルで構成できます。

あるいは、タイトルバーのチャットメニューから **AI 機能を非表示にする方法** アクションを使用して設定にアクセスしてください。

> [!NOTE]
> 以前に組み込み AI 機能を無効にしていた場合、その選択は新しいバージョンの VS Code に更新しても尊重されます。

### Copilot のネットワークおよびファイアウォール構成

- あなたやあなたの組織がファイアウォールやプロキシサーバーなどのセキュリティ対策を採用している場合、特定のドメイン URL を「許可リスト」に追加し、特定のポートとプロトコルを開放することが有益な場合があります。[GitHub Copilot のファイアウォール設定](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-firewall-settings-for-github-copilot)のトラブルシューティングについて詳細をご覧ください。

- 会社の機器で作業し、企業ネットワークに接続している場合、VPN または HTTP プロキシサーバーを介してインターネットに接続している可能性があります。場合によっては、これらの種類のネットワークセットアップにより、GitHub Copilot が GitHub のサーバーに接続できなくなることがあります。[GitHub Copilot のネットワークエラーのトラブルシューティング](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-network-errors-for-github-copilot)について詳細をご覧ください。

### リクエストがレート制限されています

このエラーは、Copilot リクエストのレート制限を超えたことを示唆しています。GitHub は、誰もが Copilot サービスに公平にアクセスできるようにし、乱用を防ぐためにレート制限を使用しています。

レート制限と、レート制限された場合の対処方法については、[GitHub Copilot のレート制限](https://docs.github.com/en/copilot/troubleshooting-github-copilot/rate-limits-for-github-copilot)を参照してください。

### Copilot 拡張機能のプレリリースビルドはありますか？

はい、Copilot 拡張機能のプレリリース（ナイトリー）バージョンに切り替えて、最新の機能や修正を試すことができます。拡張機能ビューから、右クリックするか歯車アイコンを選択してコンテキストメニューを表示し、**プレリリースバージョンへの切り替え** を選択します：

![プレリリースバージョンへの切り替えオプションがある拡張機能ビューのコンテキストメニュー](images/faq/switch-to-pre-release.png)

拡張機能の詳細にある「プレリリース」バッジで、プレリリースバージョンを実行しているかどうかを確認できます：

![GitHub Copilot 拡張機能のプレリリースバージョン](images/faq/copilot-ext-pre-release.png)

## インライン提案

### インライン提案を有効または無効にするにはどうすればよいですか？

VS Code ステータスバーの Copilot ステータスダッシュボードにあるチェックボックスを使用して、VS Code でインライン提案を有効または無効にできます。インライン提案は、グローバルに、またはアクティブなエディターのファイルタイプに対して有効または無効にできます。

![Copilot がアクティブであることを示す Copilot アイコンを強調表示した VS Code ステータスバーのスクリーンショット。](./images/faq/copilot-disable-completions.png)

あるいは、`setting(github.copilot.enable)` および `setting(github.copilot.nextEditSuggestions.enabled)` 設定を使用して、それぞれインライン提案と次回の編集提案を有効または無効にします。これらの設定はワークスペースまたはユーザーレベルで構成できます。

### エディターでインライン提案が機能しない

- [GitHub Copilot が無効になっていない](#how-do-i-enable-or-disable-inline-suggestions) ことを、グローバルまたはこの言語に対して確認してください
- [GitHub Copilot サブスクリプションが有効で検出されている](#my-copilot-subscription-is-not-detected-in-vs-code) ことを確認してください
- [ネットワーク設定](#network-and-firewall-configuration-for-copilot) が GitHub Copilot への接続を許可するように構成されていることを確認してください。
- [Copilot Free プラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free) で今月のインライン提案の制限に達していないことを確認してください。

## チャット

### 私に対してチャット機能が動作しません

Visual Studio Code でチャット機能が動作することを確認するには、以下の要件を確認してください：

- Visual Studio Code の最新バージョンを使用していることを確認してください（**Code: 更新の確認** を実行）。
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) および [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) 拡張機能の両方の最新バージョンを使用していることを確認してください。
- VS Code にサインインしている GitHub アカウントに、有効な Copilot サブスクリプションがある必要があります。[Copilot サブスクリプション](https://github.com/settings/copilot) を確認してください。
- [Copilot Free プラン](https://docs.github.com/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/about-github-copilot-free) で今月のチャットインタラクションの制限に達していないことを確認してください。

### チャットでエージェントが利用できない

VS Code 設定: `setting(chat.agent.enabled)` でエージェントが有効になっていることを確認してください。組織がこの機能を無効にしている可能性があります。管理者に確認してエージェントを有効にしてもらってください。

### 言語モデルピッカーですべてのモデルが利用できるわけではない

言語モデルピッカーで利用可能なモデルを選択できます。[言語モデルピッカーのカスタマイズ](/docs/copilot/customization/language-models.md#customize-the-model-picker) 方法を学びましょう。

組織は特定のモデルへのアクセスを制限できます。モデルが利用可能であるべきだと考える場合は、組織の管理者に連絡してください。

### チャットビューが自動的に開かないようにするにはどうすればよいですか？

デフォルトでは、チャットビューはセカンダリサイドバーで開きます。ワークスペースのチャットビューを閉じると、VS Code はこの設定を記憶し、次回そのワークスペースを開いたときにチャットビューを自動的に開きません。

デフォルトの表示設定はチャットビューから直接変更できます：

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)。
1. チャットビューの右上隅にある `...` アイコンを選択します。
1. **ビューをデフォルトで表示** を選択して、チャットビューの自動オープンを有効または無効にします。

また、`setting(workbench.secondarySideBar.defaultVisibility)` 設定を使用して、セカンダリサイドバーのデフォルトの表示設定を制御することもできます。`hidden` に設定すると、チャットビューが自動的に開かなくなります。

## トラブルシューティングとフィードバック

### Copilot に関するフィードバックを提供するにはどうすればよいですか？

[microsoft/vscode](https://github.com/microsoft/vscode) GitHub リポジトリで VS Code の GitHub Copilot に関する課題と機能リクエストを追跡しています。このリポジトリで課題を作成するか、VS Code の以下のフィードバックメカニズムを使用できます：

- **ゴーストテキスト提案**

    エディターでゴーストテキスト提案にカーソルを合わせたときに、**Copilot 補完フィードバックを送信** アクションを使用します。課題レポーターで、再現手順を含めて課題の明確かつ詳細な説明を提供してください。

    ![エディターでの Copilot ゴーストテキストフィードバック送信アクションを示すスクリーンショット。](images/faq/code-completions-feedback.png)

- **次回の編集提案**

    エディターガターの次回の編集提案メニューで **フィードバック** アクションを選択します。課題レポーターで、再現手順を含めて課題の明確かつ詳細な説明を提供してください。

    ![エディターガターの次回の編集提案メニューを示すスクリーンショット。](images/faq/nes-feedback.png)

- **一般的な課題**

    VS Code 課題レポーター (**ヘルプ** > **問題を報告**) を開き、**VS Code 拡張機能** ソースを選択してから、**GitHub Copilot Chat** 拡張機能を選択します。再現手順を含めて課題の明確かつ詳細な説明を提供してください。

    ![GitHub Copilot Chat が選択された VS Code 課題レポーターを示すスクリーンショット。](images/faq/issue-reporter.png)

課題を報告する際は、課題が実行可能であることを確認するために、[wiki](https://github.com/microsoft/vscode/wiki/Copilot-Issues) のガイドラインに従ってください。

課題を報告する場合、[GitHub Copilot ログ](#view-logs-for-github-copilot-in-vs-code) からの情を含めると役立つ場合があります。

### VS Code で GitHub Copilot のログを表示する

GitHub Copilot 拡張機能のログファイルは、Visual Studio Code 拡張機能の標準ログ場所に保存されます。

VS Code で Copilot の詳細なログを取得するには、以下の手順に従ってください：

1. コマンドパレット (`kb(workbench.action.showCommands)`) で、**Developer: Set Log Level** コマンドを実行し、値を **Trace** に設定します（これは GitHub Copilot および GitHub Copilot Chat 拡張機能に対してのみ実行できます）。
1. コマンドパレット (`kb(workbench.action.showCommands)`) で、**出力: 出力チャネルを表示...** コマンドを実行し、リストから GitHub Copilot または GitHub Copilot Chat を選択します。
1. 出力パネルで、選択した拡張機能のログを確認できます。
1. 別の出力チャネルに切り替えるには、出力パネルの右側にあるドロップダウンメニューから **GitHub Copilot** または **GitHub Copilot Chat** を選択します。

GitHub Copilot への接続に問題が発生した場合は、ネットワーク接続診断ログを表示できます：

1. コマンドパレット (`kb(workbench.action.showCommands)`) を開きます。
1. **GitHub Copilot: Collect Diagnostics** コマンドを実行します。
1. 診断情報を検査できるエディタータブが開きます。

### チャットデバッグビューを使用する

チャットデバッグビューを使用して、使用されているプロンプトや言語モデルに送信されるコンテキストなど、AI リクエストとレスポンスの詳細を確認できます。このビューは、AI がリクエストをどのように解釈し、どのようなコンテキストを使用してレスポンスを生成しているかを理解するのに役立ちます。

[チャットデバッグビュー](/docs/copilot/chat/chat-debug-view.md)について詳細をご覧ください。

## 追加リソース

- [GitHub Copilot トラストセンター](https://resources.github.com/copilot-trust-center/)
- GitHub ドキュメント内の [GitHub Copilot FAQ](https://github.com/features/copilot#faq)
