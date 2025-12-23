---
ContentId: 8f2c9a1b-3d4e-5f6a-7b8c-9d0e1f2a3b4c
DateApproved: 12/10/2025
MetaDescription: VS Codeのさまざまな種類のエージェントを使って、ローカル、バックグラウンド、またはクラウドでタスクを実行する方法を開始します。エージェント間で作業を引き継ぎ、ワークフローに最適なものを活用します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- エージェント
- バックグラウンドエージェント
- クラウドエージェント
- copilot coding agent
- copilot cli
- チュートリアル
---

# チュートリアル: VS Codeでエージェントを活用する

このチュートリアルでは、Visual Studio Codeでさまざまな種類のエージェントを使用する方法を説明します。todoアプリをゼロから作成し、テーマの切り替えを追加し、ローカル、プラン、バックグラウンド、クラウドエージェントに作業を委任してレイアウトを再設計します。

> [!TIP]
> まだCopilotサブスクリプションがない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップすることでCopilotを無料で利用でき、インライン提案とチャットインタラクションの月間上限が適用されます。

## 前提条件

このチュートリアルを完了するには、次が必要です:

* [コンピューターにインストールされたVisual Studio Code](/download)
* [GitHubアカウント](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github) (クラウドエージェントのワークフロー用)
* [GitHub Copilotサブスクリプション](/docs/copilot/setup.md)

## 手順1: ローカルエージェントを使ってアプリをスキャフォールドする

この手順では、ローカルエージェントを使用してtodoアプリの初期構造を作成します。ローカルエージェントは、新しいプロジェクトのスキャフォールドや新機能の反復など、すぐにフィードバックと結果が欲しいインタラクティブなタスクに最適です。

1. Create a new project folder and ensure it's under Git version control.

    ```bash
    mkdir todo-app
    cd todo-app
    git init
    ```

1. Open the project folder in VS Code.

1. チャットビュー(`kb(workbench.action.chat.open)`)を開き、エージェントドロップダウンから**Agent**を選択します。

    必要に応じて、好みがあれば特定の言語モデルを選択します。

1. チャット入力フィールドに次のプロンプトを入力してtodoアプリをスキャフォールドし、**Send**を選択します。

    ```prompt
    HTML、CSS、JavaScriptでシンプルなtodoアプリを作成してください。todoを追加するための入力フィールド、表示用のリスト、各項目に削除ボタンを含めてください。
    ```

    <video src="../images/agents-tutorial/local-agent-todo-app-scaffold.mp4" alt="Video showing a local agent scaffolding a todo app in VS Code." muted autoplay loop></video>

1. エージェントがアプリのさまざまなファイルを生成する様子を確認します。必要に応じて**Keep**または**Undo**を使用して変更を承認または拒否します。

1. 開発しながら編集内容をライブでプレビューするには、まだインストールしていない場合は[Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)拡張機能をインストールします。

1. 生成されたHTMLファイルを開き、**Show Preview**を選択してVS Code内で直接アプリをプレビューし、操作します。

    <video src="../images/agents-tutorial/local-agent-todo-app-live-preview.mp4" alt="Video showing a local agent enhancing a todo app in VS Code with live preview." muted autoplay loop></video>

1. 追加のプロンプトを送信して、アプリをさらに強化します。変更を加えるたびにプレビューがライブで更新されることを確認します。

    たとえば、次のように依頼できます:

    ```prompt
    完了したtodoに取り消し線の効果を付けてマークしてください。
    ```

これで、追加機能で拡張できる動作するtodoアプリができました。ローカルエージェントを使用することで、リアルタイムにコードを対話的に生成し、洗練できます。

## 手順2: バックグラウンドエージェントを使って機能プランを実装する

この手順では、プランエージェントを使用してテーマ切り替えの実装プランを作成し、その実装をバックグラウンドエージェントに引き継ぎます。バックグラウンドエージェントは、即時のやり取りを必要としないタスクの委任に最適です。Git worktreeを使用して、メインワークスペースからファイル変更を分離し、競合を防ぎます。

1. まず、ソース管理ビューで現在の変更をコミットして、クリーンな状態にします。

1. チャットビューで**New Chat (+)** > **New Chat**を選択して、新しいローカルエージェントセッションを開始します。以前のチャットセッションがセッションリストに保持されていることを確認します。

1. エージェントドロップダウンから**Plan**を選択してプランエージェントに切り替え、次のプロンプトを入力します:

    ```text
    アプリにダーク/ライトテーマの切り替えを追加するためのプランを作成してください。この切り替えはテーマ間を切り替え、ユーザーの設定を永続化する必要があります。
    ```

1. 提案された実装プランを確認し、必要に応じて調整します。

1. 準備ができたら、**Start Implementation** > **Continue in Background**を選択して、プランをバックグラウンドエージェントに引き継ぎます。

    ![Screenshot showing the Start Implementation button in the Chat view.](../images/agents-tutorial/start-implementation-button.png)

1. バックグラウンドエージェントは、機能の実装を開始するためのGit worktreeを作成します。**Sessions**ビューでバックグラウンドエージェントを追跡できます。セッションを選択して進行状況の詳細を確認します。

    <video src="../images/agents-tutorial/background-agent-theme-switcher.mp4" alt="Video showing a background agent implementing a theme switcher feature in VS Code." muted autoplay loop></video>

    > [!TIP]
    > バックグラウンドエージェントが作業している間も、競合なくメインワークスペースの編集を続けられます。

1. バックグラウンドエージェントが完了したら、セッションの詳細から変更を確認します。あるいは、ソース管理ビューに切り替えてGit worktree内の変更を確認します。

1. 変更内容に問題がなければ、チャットビューで**Keep**を選択し、次に**Apply**を選択して変更をメインワークスペースに適用します。

    ![Screenshot showing the HTML preview of the app, which now has a theme switcher button.](../images/agents-tutorial/todo-app-theme-switcher.png)

バックグラウンドエージェントを使用して、バックグラウンドでタスクを自律的に実行できました。メインのワークフローを中断することなく、異なるタスク向けに複数のバックグラウンドエージェントを開始できます。

## 手順3: クラウドエージェントを使って機能を共同作業する

この手順では、クラウドエージェント(Copilot coding agent)を使用してアプリのレイアウトを再設計し、GitHubのプルリクエストとコラボレーション機能を使用します。Copilot coding agentはリモートインフラストラクチャで実行され、即時のフィードバックを必要としないタスク、ローカルで実行する必要がないタスク、またはGitHubを通じた共同作業を伴うタスクに最適です。

1. まず、プロジェクトをGitHubリポジトリに公開し、リモートとして追加してプロジェクトでCopilot coding agentを使用できるようにします。

    1. コマンドパレット(`kb(workbench.action.showCommands)`)から**Publish to GitHub**コマンドを実行し、プロンプトに従って新しいリポジトリを作成します。

    1. コマンドパレットから**Git: Add Remote**コマンドを実行し、プロンプトに従ってGitHubリポジトリをリモートとして追加します。

1. チャットビューで**New Chat (+)** > **New Cloud Agent**を選択し、次のプロンプトを入力します:

    ```text
    ユーザーエクスペリエンスを向上させるためにtodoアプリのレイアウトを再設計してください。色、余白、タイポグラフィを更新し、アニメーションを追加してモダンな見た目にしてください。
    ```

1. クラウドエージェントはリクエストに対応するための新しいセッションを開始します。GitHubリポジトリにブランチとプルリクエストを作成します。

    <video src="../images/agents-tutorial/cloud-agent-redesign-todo-app.mp4" alt="Video showing a cloud agent redesigning a todo app in VS Code." muted autoplay loop></video>

1. チャットビューの**Sessions**ビューでクラウドエージェントを追跡できます。進行中のすべてのエージェントセッションとその状態を確認できます。

    > [!TIP]
    > GitHub Pull Requests拡張機能がインストールされている場合は、GitHub Pull Requestsビューの**Copilot on my Behalf**ビューでプルリクエストの進行状況も追跡できます。

1. 完了すると、クラウドエージェントはレビューのためにプルリクエストをあなたに割り当てます。

    ![Screenshot showing the cloud agent session details, with the file change details.](../images/agents-tutorial/cloud-agent-pull-request.png)

1. **Sessions**ビューでクラウドエージェントセッションを右クリックして、プルリクエストをローカルにチェックアウトする、GitHubで表示するなどの追加オプションを表示します。

    <video src="../images/agents-tutorial/cloud-agent-checkout-pr.mp4" alt="Video showing checking out a pull request created by a cloud agent in VS Code." muted autoplay loop></video>

1. チームで標準のGitHubコードレビューのワークフローを使用して、プルリクエストをレビュー、コメント、マージできます。

クラウドエージェントを使用して、GitHubで機能の共同作業を行えました。クラウドエージェントにより、リモートリソースを利用し、GitHubを通じてシームレスに共同作業できます。

## 次のステップ

さまざまな種類のエージェントを使用して、todoアプリの構築、強化、再設計を行えました。引き続きエージェントを探索しましょう:

* [エージェントの種類と使いどころ](/docs/copilot/agents/overview.md)について学ぶ
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)を探索する
