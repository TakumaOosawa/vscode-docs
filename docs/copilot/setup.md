---
ContentId: 37fd3bd2-4209-49f6-bec5-c544d6b1b289
DateApproved: 01/08/2026
MetaDescription: GitHub Copilotサブスクリプションにアクセスし、Visual StudioでGitHub Copilotをセットアップします。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeでのGitHub Copilotのセットアップ

このガイドでは、Visual Studio CodeでGitHub Copilotをセットアップする手順を説明します。VS CodeでCopilotを使用するには、GitHubアカウントでGitHub Copilotにアクセスできる必要があります。

<video src="./images/setup/vscode-copilot-setup.mp4" poster="./images/setup/setup-copilot-sign-in.png" title="Visual Studio CodeでのGitHub Copilotのセットアップ" autoplay loop controls muted></video>

VS CodeでCopilotの使用を開始するには、次の手順に従います。

1. ステータスバーのCopilotアイコンの上にマウスを置き、**AI機能を使用する**を選択します。

1. サインイン方法を選択し、プロンプトに従います。

    * アカウントにCopilotサブスクリプションが既にある場合、VS Codeはそのサブスクリプションを使用します。

    * まだCopilotサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップされ、インライン提案とチャット対話の月間制限が適用されます。さまざまな[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)の詳細については、こちらをご覧ください。

1. VS CodeでCopilotの使用を開始しましょう！

    [Copilotクイックスタート](/docs/copilot/getting-started.md)で基本を学びます。

> [!IMPORTANT]
> 無料版のGitHub Copilotでは、現在テレメトリが有効になっています。デフォルトでは、VS Codeおよび[github.com](http://github.com/copilot)エクスペリエンスでのコード参照を含む、パブリックコードと一致するコード提案が許可されています。`setting(telemetry.telemetryLevel)`を`off`に設定してVS Codeのテレメトリを無効にすることで、テレメトリデータの収集をオプトアウトできます。または、[Copilot設定](https://github.com/settings/copilot)でテレメトリとコード提案の設定の両方を調整することもできます。

## GHEアカウントでCopilotを使用する

CopilotサブスクリプションがGitHub Enterprise (GHE)アカウントに関連付けられている場合は、GHE資格情報を使用してVS CodeでCopilotにサインインできます。

1. まだ行っていない場合は、ステータスバーのCopilotアイコンの上にマウスを置き、**AI機能を使用する**を選択します。

1. サインインダイアログで、**GHE.comで続行**を選択し、GHEインスタンスのURLと資格情報を入力します。

GitHub.comアカウントとGHEアカウントを切り替える必要がある場合は、手順について[ワークスペースまたはプロファイルごとに異なるGitHubアカウントを使用する](#use-a-different-github-account-per-workspace-or-profile)を参照してください。

## Copilotで異なるGitHubアカウントを使用する

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、次の手順に従ってVS CodeでGitHubアカウントからサインアウトし、別のアカウントでサインインします。

1. アクティビティバーの**アカウント**メニューを選択し、現在サインインしているアカウントの**サインアウト**を選択します。

    ![現在のGitHubアカウントからサインアウトするオプションを表示しているVS Codeのアカウントメニュー。](images/setup/vscode-accounts-menu-signout.png)

1. 次のいずれかの方法を使用してGitHubアカウントにサインインします。

    * ステータスバーのCopilotメニューから**Copilotを使用するためにサインイン**を選択します。

        ![CopilotステータスメニューからCopilotを使用するためにサインインします。](images/setup/copilot-signedout-sign-in.png)

    * アクティビティバーの**アカウント**メニューを選択し、**GitHub Copilotを使用するためにGitHubでサインイン**を選択します。

        ![GitHub Copilotを使用するためにGitHubでサインインするオプションを表示しているVS Codeのアカウントメニュー。](images/setup/vscode-accounts-menu.png)

    * コマンドパレット（`kb(workbench.action.showCommands)`）で**GitHub Copilot: サインイン**コマンドを実行します。

## ワークスペースまたはプロファイルごとに異なるGitHubアカウントを使用する

VS Codeのワークスペースまたはプロファイルごとに、Copilot用に異なるGitHubアカウントを使用できます。これは、仕事用と個人用のプロジェクトで異なるアカウントを使用してCopilotを利用する場合や、GitHub認証を使用するさまざまな拡張機能で異なるアカウントを使用したい場合に便利です。

Copilotに使用するGitHubアカウントを構成するには、次の手順に従います。この構成は、ワークスペースごとおよびプロファイルごとに保存されます。

* GitHub.comアカウントの場合:

    1. アクティビティバーのアカウントメニューで、**拡張機能アカウント設定の管理**を選択します
    1. 拡張機能のリストから**GitHub Copilot Chat**を選択します
    1. 現在のワークスペースとプロファイルでCopilotに使用するGitHubアカウントを選択します

* GHE.comアカウントの場合:

    > [!TIP]
    > GHEアカウントのみをCopilotに使用したい場合は、[GHEアカウントでCopilotを使用する](#use-copilot-with-a-ghe-account)の手順に従ってGHEアカウントでサインインしてください。

    1. コマンドパレット（`kb(workbench.action.showCommands)`）から**基本設定: ユーザー設定を開く (JSON)** または**基本設定: ワークスペース設定を開く (JSON)** を実行します

    1. 次の設定を追加して、Copilotの認証プロバイダーとしてGitHub Enterpriseを指定します。

        ```json
        "github.copilot.advanced": {
            "authProvider": "github-enterprise"
        }
        ```

    1. まだサインインしていない場合は、GitHub Enterpriseアカウントに再サインインします

## VS CodeからAI機能を削除する

VS Codeの他の機能を構成するのと同様に、`setting(chat.disableAIFeatures)`設定を使用して、VS Codeの組み込みAI機能を無効にすることができます。これにより、VS Codeのチャットやインライン提案などの機能が無効化および非表示になり、Copilot拡張機能が無効になります。この設定は、ワークスペースまたはユーザーレベルで構成できます。

または、タイトルバーのチャットメニューから**AI機能を非表示にする方法**アクションを使用して設定にアクセスします。

> [!NOTE]
> 以前に組み込みAI機能を無効にしていた場合、新しいバージョンのVS Codeに更新しても選択内容は尊重されます。

## ワークスペースのAI機能を無効にする

特定のワークスペースのAI機能を無効にするには、ワークスペース設定で`setting(chat.disableAIFeatures)`設定を構成します。この設定は設定エディター（`kb(workbench.action.openSettings)`）で使用できます。または、ワークスペースの`settings.json`ファイルを編集することもできます。

## 次のステップ

* [AIを使用するためのクイックスタート](/docs/copilot/getting-started.md)に進み、VS CodeでのAI搭載開発の主要な機能を確認してください。
