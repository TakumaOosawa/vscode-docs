---
ContentId: 8f2c9a1b-3d4e-5f6a-7b8c-9d0e1f2a3b4c
DateApproved: 12/10/2025
MetaDescription: VS Codeの様々なタイプのエージェントを使って、ローカル、バックグラウンド、またはクラウドでタスクを実行する方法を学びます。エージェント間で作業を引き継ぎ、ワークフローに最適なものを使用します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- background agent
- cloud agent
- copilot coding agent
- copilot cli
- tutorial
---

# チュートリアル: VS Codeでエージェントを使用する

このチュートリアルでは、Visual Studio Codeで様々なタイプのエージェントを使用する方法を説明します。Todoアプリをゼロから構築し、テーマの切り替えを追加し、ローカル、プラン、バックグラウンド、およびクラウドエージェントに作業を委任することでレイアウトを再設計します。

> [!TIP]
> まだCopilotサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で利用でき、毎月のインライン提案とチャット対話の制限を取得できます。

## 前提条件

このチュートリアルを完了するには、以下が必要です:

* [コンピュータにインストールされたVisual Studio Code](/download)
* [GitHubアカウント](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github) (クラウドエージェントワークフロー用)
* [GitHub Copilotサブスクリプション](/docs/copilot/setup.md)

## ステップ1: ローカルエージェントを使用してアプリをスキャフォールドする

このステップでは、ローカルエージェントを使用して初期のTodoアプリ構造を作成します。ローカルエージェントは、新しいプロジェクトのスキャフォールドや新機能の反復など、即時のフィードバックと結果が必要な対話型タスクに最適です。

1. 新しいプロジェクトフォルダを作成し、Gitバージョン管理下にあることを確認します。

    ```bash
    mkdir todo-app
    cd todo-app
    git init
    ```

1. VS Codeでプロジェクトフォルダを開きます。

1. チャットビュー (`kb(workbench.action.chat.open)`) を開き、エージェントドロップダウンから**Agent**を選択します。

    必要に応じて、特定の言語モデルを選択することもできます。

1. チャット入力フィールドに次のプロンプトを入力してTodoアプリをスキャフォールドし、**Send**を選択します。

    ```prompt
    Create a simple todo app with HTML, CSS, and JavaScript. Include an input field to add todos, a list to display them, and a delete button for each item.
    ```

    <video src="../images/agents-tutorial/local-agent-todo-app-scaffold.mp4" alt="Video showing a local agent scaffolding a todo app in VS Code." muted autoplay loop></video>

1. エージェントがアプリのさまざまなファイルを生成するのを確認します。必要に応じて**Keep**または**Undo**を使用して変更を受け入れるか拒否します。

1. 開発中に編集をライブでプレビューするには、[Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)拡張機能をまだ持っていない場合はインストールします。

1. 生成されたHTMLファイルを開き、**Show Preview**を選択してVS Codeで直接アプリをプレビューおよび操作します。

    <video src="../images/agents-tutorial/local-agent-todo-app-live-preview.mp4" alt="Video showing a local agent enhancing a todo app in VS Code with live preview." muted autoplay loop></video>

1. 追加のプロンプトを送信して、アプリをさらに強化します。変更を加えるとプレビューがライブで更新されることに注目してください。

    例えば、次のように質問できます:

    ```prompt
    Mark todos as completed with a strikethrough effect.
    ```

これで、追加機能で拡張できる動作するTodoアプリができました。ローカルエージェントを使用することで、リアルタイムでコードを対話的に生成および調整できます。

## ステップ2: バックグラウンドエージェントを使用して機能プランを実装する

このステップでは、プランエージェントを使用してテーマ切り替えの実装プランを作成し、実装をバックグラウンドエージェントに引き渡します。バックグラウンドエージェントは、即時の対話を必要としないタスクを委任するのに最適です。これらはGitワークツリーを使用してファイル変更をメインワークスペースから分離し、競合を防ぎます。

1. まず、ソース管理ビューで現在の変更をコミットしてクリーンな状態にします。

1. チャットビューで、**New Chat (+)** > **New Chat**を選択して新しいローカルエージェントセッションを開始します。以前のチャットセッションはセッションリストに保持されることに注目してください。

1. エージェントドロップダウンから**Plan**を選択してプランエージェントに切り替え、次のプロンプトを入力します:

    ```text
    Create a plan to add a dark/light theme toggle to the app. The toggle should switch between themes and persist the user's preference.
    ```

1. 提案された実装プランを確認し、必要に応じて調整します。

1. 準備ができたら、**Start Implementation** > **Continue in Background**を選択してプランをバックグラウンドエージェントに引き渡します。

    ![Screenshot showing the Start Implementation button in the Chat view.](../images/agents-tutorial/start-implementation-button.png)

1. バックグラウンドエージェントはGitワークツリーを作成し、機能の実装を開始します。**Sessions**ビューでバックグラウンドエージェントを追跡できます。セッションを選択すると、その進行状況の詳細が表示されます。

    <video src="../images/agents-tutorial/background-agent-theme-switcher.mp4" alt="Video showing a background agent implementing a theme switcher feature in VS Code." muted autoplay loop></video>

    > [!TIP]
    > バックグラウンドエージェントが動作している間、競合することなくメインワークスペースの編集を続けることができます。

1. バックグラウンドエージェントが終了したら、セッションの詳細から変更を確認します。または、ソース管理ビューに切り替えてGitワークツリーの変更を確認します。

1. 変更に満足したら、チャットビューで**Keep**を選択し、次に**Apply**を選択して変更をメインワークスペースに適用します。

    ![Screenshot showing the HTML preview of the app, which now has a theme switcher button.](../images/agents-tutorial/todo-app-theme-switcher.png)

バックグラウンドで自律的にタスクを実行するためにバックグラウンドエージェントを正常に使用しました。メインワークフローを中断することなく、さまざまなタスクのために複数のバックグラウンドエージェントを開始できます。

## ステップ3: クラウドエージェントを使用して機能でコラボレーションする

このステップでは、クラウドエージェント (Copilot coding agent) を使用してアプリのレイアウトを再設計し、GitHubのプルリクエストとコラボレーション機能を使用します。Copilot coding agentはリモートインフラストラクチャ上で実行され、即時のフィードバックを必要としないタスク、ローカルで実行する必要がないタスク、またはGitHubを通じたコラボレーションを含むタスクに最適です。

1. まず、プロジェクトをGitHubリポジトリに公開し、リモートとして追加してプロジェクトでCopilot coding agentを使用します。

    1. コマンドパレット (`kb(workbench.action.showCommands)`) から**Publish to GitHub**コマンドを実行し、プロンプトに従って新しいリポジトリを作成します。

    1. コマンドパレットから**Git: Add Remote**コマンドを実行し、プロンプトに従ってGitHubリポジトリをリモートとして追加します。

1. チャットビューで、**New Chat (+)** > **New Cloud Agent**を選択し、次のプロンプトを入力します:

    ```text
    Redesign the todo app layout to improve user experience. Update colors, spacing, typography, and add animations to give it a modern look.
    ```

1. クラウドエージェントはリクエストに取り組むために新しいセッションを開始します。GitHubリポジトリにブランチとプルリクエストを作成します。

    <video src="../images/agents-tutorial/cloud-agent-redesign-todo-app.mp4" alt="Video showing a cloud agent redesigning a todo app in VS Code." muted autoplay loop></video>

1. チャットビュー内の**Sessions**ビューでクラウドエージェントを追跡でき、進行中のすべてのエージェントセッションとそのステータスを確認できます。

    > [!TIP]
    > GitHub Pull Requests拡張機能がインストールされている場合、GitHub Pull Requestsビューの**Copilot on my Behalf**ビューでプルリクエストの進行状況を追跡することもできます。

1. 完了すると、クラウドエージェントはレビューのためにプルリクエストをあなたに割り当てます。

    ![Screenshot showing the cloud agent session details, with the file change details.](../images/agents-tutorial/cloud-agent-pull-request.png)

1. **Sessions**ビューでクラウドエージェントセッションを右クリックすると、プルリクエストをローカルでチェックアウトしたり、GitHubで表示したりするなど、追加のオプションを表示できます。

    <video src="../images/agents-tutorial/cloud-agent-checkout-pr.mp4" alt="Video showing checking out a pull request created by a cloud agent in VS Code." muted autoplay loop></video>

1. チームとの標準的なGitHubコードレビューワークフローを使用して、プルリクエストをレビュー、コメント、およびマージできます。

GitHubを使用して機能でコラボレーションするためにクラウドエージェントを正常に使用しました。クラウドエージェントを使用すると、リモートリソースを使用し、GitHubを通じてシームレスにコラボレーションできます。

## 次のステップ

様々なタイプのエージェントを使用して、Todoアプリを構築、強化、および再設計することに成功しました。エージェントの探索を続けてください:

* [エージェントの種類と使用時期について学ぶ](/docs/copilot/agents/overview.md)
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)を探索する
