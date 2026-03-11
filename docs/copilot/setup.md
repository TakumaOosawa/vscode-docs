---
ContentId: 37fd3bd2-4209-49f6-bec5-c544d6b1b289
DateApproved: 3/9/2026
MetaDescription: GitHubCopilotサブスクリプションにアクセスし、VisualStudioでGitHubCopilotを設定します。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VSCodeでGitHubCopilotを設定する

このガイドでは、VisualStudioCodeでGitHubCopilotを設定する手順について説明します。VSCodeでCopilotを使用するには、GitHubアカウントでGitHubCopilotにアクセスできる必要があります。

<video src="./images/setup/vscode-copilot-setup.mp4" poster="./images/setup/setup-copilot-sign-in.png" title="VisualStudioCodeでGitHubCopilotを設定する" loop controls muted></video>

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIを使い始める">
VSCodeでAIを使用して最初のアプリを構築するためのハンズオンチュートリアルに従います。

* [チュートリアルを開始](/docs/copilot/getting-started.md)

</div>

VSCodeでCopilotを始めるには、以下の手順に従います：

1. ステータスバーのCopilotアイコンにマウスを合わせ、**AIフィーチャーを使用**を選択します。

1. サインイン方法を選択し、プロンプトに従います。

    * アカウントにCopilotサブスクリプションが既にある場合、VSCodeはそのサブスクリプションを使用します。

    * まだCopilotサブスクリプションがない場合は、[CopilotFreeプラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップされ、インラインサジェストとチャットインタラクションの月間制限を取得します。異なる[GitHubCopilotプラン](https://docs.github.com/en/copilot/get-started/plans)の詳細をご覧ください。

1. VSCodeでCopilotの使用を開始します。

    [Copilotクイックスタート](/docs/copilot/getting-started.md)で基本を学習します。

1. チャットセッションで `/init` と入力して、プロジェクトをAI用に設定します。

    `/init` コマンドはコードベースを分析し、[カスタム指示](/docs/copilot/customization/custom-instructions.md)を作成して、AIがコーディング慣行に一致するコードを生成するのに役立ちます。

> [!IMPORTANT]
> GitHubCopilotの無料版のテレメトリは現在有効です。デフォルトでは、パブリックコードと一致するコードサジェスト（VSCodeと[github.com](http://github.com/copilot)エクスペリエンス内のコード参照を含む）が許可されます。VSCodeでテレメトリを無効化して `setting(telemetry.telemetryLevel)` を `off` に設定するか、[CopilotSettings](https://github.com/settings/copilot)でテレメトリとコードサジェスト設定の両方を調整することで、テレメトリデータ収集からオプトアウトできます。

## GHEアカウントでCopilotを使用する

CopilotサブスクリプションがGitHubEnterprise（GHE）アカウントに関連付けられている場合は、GHE認証情報を使用してVSCodeのCopilotにサインインできます。

1. まだの場合は、ステータスバーのCopilotアイコンにマウスを合わせ、**AIフィーチャーを使用**を選択します。

1. サインインダイアログで、**GHE.comで続行**を選択し、GHEインスタンスのURLと認証情報を入力します。

GitHubアカウントとGHEアカウントを切り替える必要がある場合は、[ワークスペースまたはプロフィールごとに異なるGitHubアカウントを使用](#ワークスペースまたはプロフィールごとに異なるgithubアカウントを使用)を参照して、手順を確認してください。

## Copilotで異なるGitHubアカウントを使用する

Copilotサブスクリプションが別のGitHubアカウントに関連付けられている場合は、以下の手順に従って、VSCodeから現在のGitHubアカウントをサインアウトし、別のアカウントでサインインします。

1. アクティビティバーの**アカウント**メニューを選択し、現在サインインしているアカウントの**サインアウト**を選択します。

    ![VSCodeのアカウントメニュー。現在のGitHubアカウントからサインアウトするオプションが表示されています。](images/setup/vscode-accounts-menu-signout.png)

1. 以下のいずれかの方法を使用してGitHubアカウントにサインインします：

    * ステータスバーのCopilotメニューから**Copilotを使用するためにサインイン**を選択します。

        ![Copilotステータスメニューから、Copilotを使用するためにサインインします。](images/setup/copilot-signedout-sign-in.png)

    * アクティビティバーの**アカウント**メニューを選択し、**GitHubでサインインしてGitHubCopilotを使用**を選択します。

        ![VSCodeのアカウントメニュー。GitHubでサインインしてGitHubCopilotを使用するオプションが表示されています。](images/setup/vscode-accounts-menu.png)

    * コマンドパレット（`kb(workbench.action.showCommands)`）で**GitHubCopilot：サインイン**コマンドを実行します。

## ワークスペースまたはプロフィールごとに異なるGitHubアカウントを使用する

VSCodeのワークスペースまたはプロフィールごとに、Copilotに異なるGitHubアカウントを使用できます。これは、仕事と個人プロジェクトに異なるアカウントでCopilotを使用する場合や、GitHub認証を使用する異なる拡張機能に異なるアカウントを使用する場合に役立ちます。

Copilotに使用するGitHubアカウントを設定するには、以下の手順に従います。この設定はワークスペースごと、およびプロフィールごとに保存されます。

* GitHub.comアカウントの場合：

    1. アクティビティバーの[アカウント]メニューで、**拡張機能アカウント設定の管理**を選択します
    1. 拡張機能のリストから**GitHubCopilotChat**を選択します
    1. 現在のワークスペースとプロフィールでCopilotに使用するGitHubアカウントを選択します

* GHE.comアカウントの場合：

    > [!TIP]
    > CopilotにGHEアカウントのみを使用する場合は、[GHEアカウントでCopilotを使用](#gheアカウントでcopilotを使用する)の手順に従ってGHEアカウントでサインインしてください。

    1. コマンドパレット（`kb(workbench.action.showCommands)`）から**環境設定：ユーザー設定を開く（JSON）**または**環境設定：ワークスペース設定を開く（JSON）**を実行します

    1. 次の設定を追加して、Copilotの認証プロバイダーとしてGitHubEnterpriseを指定します：

        ```json
        "github.copilot.advanced": {
            "authProvider": "github-enterprise"
        }
        ```

    1. まだサインインしていない場合は、GitHubEnterpriseアカウントに再度サインインします

## VSCodeからAIフィーチャーを削除する

VSCodeの他のフィーチャーを設定する方法と同様に、`setting(chat.disableAIFeatures)` 設定を使用して、VSCodeの組み込みAIフィーチャーを無効化できます。これにより、VSCode内のチャットやインラインサジェストなどのフィーチャーが無効になり、表示されなくなり、Copilot拡張機能が無効になります。ワークスペースまたはユーザーレベルで設定を設定できます。

または、タイトルバーのチャットメニューから**AIフィーチャーを非表示にする方法を学ぶ**アクションを使用して、設定にアクセスします。

> [!NOTE]
> 以前に組み込みAIフィーチャーを無効化している場合、VSCodeの新しいバージョンに更新すると、その選択が尊重されます。

## ワークスペースのAIフィーチャーを無効化する

特定のワークスペースのAIフィーチャーを無効化するには、ワークスペース設定で `setting(chat.disableAIFeatures)` 設定を設定します。この設定は、設定エディター（`kb(workbench.action.openSettings)`）で利用可能です。またはワークスペースの `settings.json` ファイルを編集できます。

## 次のステップ

* [AIを使用するためのクイックスタート](/docs/copilot/getting-started.md)を続けて、VSCodeでのAI駆動開発の主要なフィーチャーを発見します。

