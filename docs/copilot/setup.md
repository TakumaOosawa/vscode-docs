---
ContentId: 37fd3bd2-4209-49f6-bec5-c544d6b1b289
DateApproved: 12/10/2025
MetaDescription: GitHub Copilotサブスクリプションにアクセスし、Visual StudioでGitHub Copilotをセットアップします。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeでGitHub Copilotをセットアップする

このガイドでは、Visual Studio CodeでGitHub Copilotをセットアップする手順を説明します。VS CodeでCopilotを使用するには、GitHubアカウントでGitHub Copilotにアクセスできる必要があります。

<video src="./images/setup/vscode-copilot-setup.mp4" poster="./images/setup/setup-copilot-sign-in.png" title="Setting up GitHub Copilot in Visual Studio Code" autoplay loop controls muted></video>

次の手順に従って、VS CodeでCopilotを使い始めてください。

1. ステータスバーのCopilotアイコンにマウスを合わせ、**AI機能を使用する**を選択します。

1. サインイン方法を選択し、画面の指示に従います。

    * アカウントですでにCopilotサブスクリプションをお持ちの場合、VS Codeはそのサブスクリプションを使用します。

    * まだCopilotサブスクリプションをお持ちでない場合は、[Copilot無料プラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)に登録され、インラインの提案とチャットのやり取りに月次の上限が適用されます。異なる[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)の詳細をご覧ください。

1. VS CodeでCopilotを使い始めましょう。

    [Copilotクイックスタート](/docs/copilot/getting-started.md)で基本を学びましょう。

> [!IMPORTANT]
> GitHub Copilotの無料版では、現在テレメトリが有効になっています。既定では、公開コードに一致するコードの提案( VS Codeおよび[github.com](http://github.com/copilot)のエクスペリエンスにおけるコード参照を含む)が許可されています。VS Codeで`setting(telemetry.telemetryLevel)`を`off`に設定してテレメトリを無効にすることで、テレメトリデータ収集をオプトアウトできます。または、[Copilot設定](https://github.com/settings/copilot)でテレメトリとコード提案の設定の両方を調整できます。

## GHEアカウントでCopilotを使用する

CopilotサブスクリプションがGitHub Enterprise (GHE)アカウントに関連付けられている場合は、GHEの資格情報を使用してVS CodeでCopilotにサインインできます。

1. まだ実行していない場合は、ステータスバーのCopilotアイコンにマウスを合わせ、**AI機能を使用する**を選択します。

1. サインインダイアログで**GHE.comで続行**を選択し、GHEインスタンスのURLと資格情報を入力します。

GitHub.comアカウントとGHEアカウントを切り替える必要がある場合は、手順について「[ワークスペースまたはプロファイルごとに別のGitHubアカウントを使用する](#use-a-different-github-account-per-workspace-or-profile)」を参照してください。

## Copilotで別のGitHubアカウントを使用する

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、次の手順に従ってVS CodeでGitHubアカウントからサインアウトし、別のアカウントでサインインします。

1. アクティビティバーの**アカウント**メニューを選択し、現在サインインしているアカウントの**サインアウト**を選択します。

    ![VS Codeのアカウントメニュー。現在のGitHubアカウントからサインアウトするオプションを示しています。](images/setup/vscode-accounts-menu-signout.png)

1. 次のいずれかの方法でGitHubアカウントにサインインします。

    * ステータスバーのCopilotメニューから**サインインしてCopilotを使用する**を選択します。

        ![CopilotのステータスメニューからサインインしてCopilotを使用する。](images/setup/copilot-signedout-sign-in.png)

    * アクティビティバーの**アカウント**メニューを選択し、**GitHubにサインインしてGitHub Copilotを使用する**を選択します。

        ![VS Codeのアカウントメニュー。GitHubにサインインしてGitHub Copilotを使用するオプションを示しています。](images/setup/vscode-accounts-menu.png)

    * コマンドパレット(`kb(workbench.action.showCommands)`)で**GitHub Copilot: Sign in**コマンドを実行します。

## ワークスペースまたはプロファイルごとに別のGitHubアカウントを使用する

VS Codeのワークスペースまたはプロファイルごとに、Copilotに異なるGitHubアカウントを使用できます。これは、仕事用と個人用プロジェクトで異なるアカウントでCopilotを使用する場合や、GitHub認証を使用する拡張機能ごとに異なるアカウントを使用したい場合に便利です。

次の手順に従って、Copilotで使用するGitHubアカウントを構成します。この構成は、ワークスペースごとおよびプロファイルごとに保存されます。

* GitHub.comアカウントの場合:

    1. アクティビティバーのアカウントメニューで**拡張機能アカウントの設定を管理**を選択します
    1. 拡張機能の一覧から**GitHub Copilot Chat**を選択します
    1. 現在のワークスペースとプロファイルでCopilotに使用するGitHubアカウントを選択します

* GHE.comアカウントの場合:

    > [!TIP]
    > CopilotにGHEアカウントのみを使用する場合は、「[GHEアカウントでCopilotを使用する](#use-copilot-with-a-ghe-account)」の手順に従ってGHEアカウントでサインインしてください。

    1. コマンドパレット(`kb(workbench.action.showCommands)`)から**Preferences: Open User Settings (JSON)**または**Preferences: Open Workspace Settings (JSON)**を実行します

    1. 次の設定を追加して、Copilotの認証プロバイダーとしてGitHub Enterpriseを指定します。

        ```json
        "github.copilot.advanced": {
            "authProvider": "github-enterprise"
        }
        ```

    1. Re-sign in to your GitHub Enterprise account if you're not already signed in

## VS CodeからAI機能を削除する

VS Codeの他の機能を構成する方法と同様に、`setting(chat.disableAIFeatures)`設定を使用してVS Codeの組み込みAI機能を無効にできます。これにより、VS Codeのチャットやインラインの提案などの機能が無効化されて非表示になり、Copilot拡張機能も無効になります。この設定は、ワークスペースレベルまたはユーザーレベルで構成できます。

または、タイトルバーのチャットメニューから**AI機能を非表示にする方法を確認**アクションを使用して設定にアクセスします。

> [!NOTE]
> 以前に組み込みAI機能を無効にしている場合、その選択はVS Codeの新しいバージョンに更新しても尊重されます。

## ワークスペースのAI機能を無効にする

特定のワークスペースのAI機能を無効にするには、ワークスペース設定で`setting(chat.disableAIFeatures)`設定を構成します。この設定は設定エディター(`kb(workbench.action.openSettings)`)で使用できます。または、ワークスペース内の`settings.json`ファイルを編集できます。

## 次の手順

* [AIの使用クイックスタート](/docs/copilot/getting-started.md)に進み、VS CodeでAIを活用した開発の主な機能を確認してください。
