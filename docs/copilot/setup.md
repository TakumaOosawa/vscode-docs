---
ContentId: 37fd3bd2-4209-49f6-bec5-c544d6b1b289
DateApproved: 3/9/2026
MetaDescription: GitHub Copilotサブスクリプションにアクセスし、Visual StudioでGitHub Copilotをセットアップします。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeでGitHub Copilotをセットアップする

このガイドでは、Visual Studio CodeでGitHub Copilotをセットアップする手順を説明します。VS CodeでCopilotを使用するには、GitHubアカウントでGitHub Copilotにアクセスできる必要があります。

<video src="./images/setup/vscode-copilot-setup.mp4" poster="./images/setup/setup-copilot-sign-in.png" title="Visual Studio CodeでGitHub Copilotをセットアップする" loop controls muted></video>

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIを使い始める">
VS CodeでAIを使用して最初のアプリを作成するためのハンズオンチュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/getting-started.md)

</div>

VS CodeでCopilotを使用するには、以下の手順に従ってください。

1. ステータスバーのCopilotアイコンにマウスポインターを置き、「AIフィーチャーを使用」を選択します。

1. サインイン方法を選択し、プロンプトに従います。

    * アカウントにCopilotサブスクリプションがある場合、VS CodeはそのサブスクリプションDを使用します。

    * まだCopilotサブスクリプションを持っていない場合は、[Copilot Free プラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップでき、インラインサジェスチョンとチャットインタラクションの月次制限を取得します。別の[GitHub Copilotプラン](https://docs.github.com/en/copilot/get-started/plans)について詳しく説明します。

1. VS CodeでCopilotの使用を開始してください！

    [Copilot クイックスタート](/docs/copilot/getting-started.md)で基本を学んでください。

1. チャットセッションで`/init`と入力して、プロジェクトをAI用にセットアップします。

    `/init`コマンドはコードベースを分析し、[カスタム指示](/docs/copilot/customization/custom-instructions.md)を作成して、AIがコーディング慣行に一致するコードを生成するのに役立ちます。

> [!IMPORTANT]
> GitHub Copilotの無料版でのテレメトリは現在有効になっています。デフォルトでは、VS Codeおよび[github.com](http://github.com/copilot)エクスペリエンスのコード参照を含むパブリックコードと一致するコードサジェスチョンが許可されます。VS Codeでテレメトリを無効にして`setting(telemetry.telemetryLevel)`を`off`に設定するか、[Copilot 設定](https://github.com/settings/copilot)でテレメトリとコードサジェスチョン設定の両方を調整することで、テレメトリデータの収集をオプトアウトできます。

## GHEアカウントでCopilotを使用する

Copilotサブスクリプションが GitHub Enterprise (GHE) アカウントに関連付けられている場合、GHE認証情報を使用してVS CodeのCopilotにサインインできます。

1. まだの場合は、ステータスバーのCopilotアイコンにマウスポインターを置き、「AIフィーチャーを使用」を選択します。

1. サインインダイアログで「GHE.comで続行」を選択し、GHEインスタンスURLと認証情報を入力します。

GitHub.comアカウントとGHEアカウントを切り替える必要がある場合は、[ワークスペースまたはプロファイルごとに異なるGitHubアカウントを使用する](#ワークスペースまたはプロファイルごとに異なるgithubアカウントを使用する)を参照して、手順をご確認ください。

## Copilotで別のGitHubアカウントを使用する

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、以下の手順に従ってVS Codeのサインアウト、別のアカウントでサインインしてください。

1. アクティビティバーの「アカウント」メニューを選択し、現在サインインしているアカウントの「サインアウト」を選択します。

    ![現在のGitHubアカウントからサインアウトするオプションを表示するVS Codeのアカウントメニュー。](images/setup/vscode-accounts-menu-signout.png)

1. 以下のいずれかの方法でGitHubアカウントにサインインします。

    * ステータスバーのCopilotメニューから「Copilotを使用するためにサインイン」を選択します。

        ![Copilotステータスメニューからサインインする。](images/setup/copilot-signedout-sign-in.png)

    * アクティビティバーの「アカウント」メニューを選択し、「GitHubでサインインしてGitHub Copilotを使用」を選択します。

        ![GitHub Copilotを使用するためにGitHubでサインインするオプションを表示するVS CodeのアカウントメニューD。](images/setup/vscode-accounts-menu.png)

    * コマンドパレット (`kb(workbench.action.showCommands)`) で「GitHub Copilot: Sign in」コマンドを実行します。

## ワークスペースまたはプロファイルごとに異なるGitHubアカウントを使用する

VS CodeのワークスペースごとまたはプロファイルごとにCopilotに対して異なるGitHubアカウントを使用できます。これは、仕事用と個人用のプロジェクトで異なるアカウントでCopilotを使用する場合や、GitHub認証を使用する異なる拡張機能に対して異なるアカウントを使用する場合に便利です。

Copilotに使用するGitHubアカウントを構成するには、以下の手順に従ってください。この構成は、ワークスペースごと、プロファイルごとに保存されます。

* GitHub.comアカウントの場合:

    1. アクティビティバーのアカウントメニューで「拡張機能アカウント設定を管理」を選択します。
    1. 拡張機能のリストから「GitHub Copilot Chat」を選択します。
    1. 現在のワークスペースとプロファイルでCopilotに使用するGitHubアカウントを選択します。

* GHE.comアカウントの場合:

    > [!TIP]
    > CopilotにGHEアカウントのみを使用する場合は、[GHEアカウントでCopilotを使用する](#gheアカウントでcopilotを使用する)の手順に従ってGHEアカウントでサインインしてください。

    1. コマンドパレット (`kb(workbench.action.showCommands)`) から「Preferences: Open User Settings (JSON)」または「Preferences: Open Workspace Settings (JSON)」を実行します。

    1. Copilotの認証プロバイダーとしてGitHub Enterpriseを指定するため、以下の設定を追加します。

        ```json
        "github.copilot.advanced": {
            "authProvider": "github-enterprise"
        }
        ```

    1. まだサインインしていない場合は、GitHubEnterpriseアカウントに再度サインインします。

## VS CodeからAIフィーチャーを削除する

VS Codeの他のフィーチャーを構成する方法と同様に、`setting(chat.disableAIFeatures)`設定を使用してVS Codeの組み込みAIフィーチャーを無効にできます。これにより、チャットやインラインサジェスチョンなどのVS CodeのフィーチャーD無効化/非表示になり、Copilot拡張機能が無効になります。ワークスペースレベルまたはユーザーレベルで設定を構成できます。

または、タイトルバーのチャットメニューから「AIフィーチャーを非表示にする方法を説明」アクションを使用して、設定にアクセスできます。

> [!NOTE]
> 以前に組み込みAIフィーチャーを無効にした場合、新しいバージョンのVS Codeに更新しても、その選択は尊重されます。

## ワークスペースのAIフィーチャーを無効にする

特定のワークスペースのAIフィーチャーを無効にするには、ワークスペース設定で`setting(chat.disableAIFeatures)`設定を構成します。この設定は設定エディター (`kb(workbench.action.openSettings)`) で利用できるか、ワークスペースの`settings.json`ファイルを編集できます。

## 次のステップ

* [AIを使用するためのクイックスタート](/docs/copilot/getting-started.md)を続行して、VS CodeでのAI駆動開発の主要フィーチャーを発見してください。

