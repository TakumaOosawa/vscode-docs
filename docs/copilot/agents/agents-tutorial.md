---
ContentId: 8f2c9a1b-3d4e-5f6a-7b8c-9d0e1f2a3b4c
DateApproved: 3/9/2026
MetaDescription: VS Codeのさまざまなタイプのエージェントを使い始めて、ローカル、バックグラウンド、またはクラウドでタスクを実行します。エージェント間で作業を移行して、ワークフローに最適なものを使用します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- background
- cloud agent
- copilot coding agent
- copilot cli
- tutorial
---

# チュートリアル: VS Codeでエージェントを使用する

このチュートリアルでは、Visual Studio Codeのさまざまなタイプのエージェントを使用する方法をご説明します。Todoアプリをスクラッチから構築し、テーマトグルを追加し、ローカル、プラン、バックグラウンド、クラウドエージェント全体に作業を委任してレイアウトを再設計します。

> [!TIP]
> Copilotのサブスクリプションがまだない場合は、[Copilot無料プラン](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で使用でき、インラインサジェッションとチャットインタラクションの月間制限が得られます。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="ブラウザエージェントツールでWebアプリをテストする">
ブラウザエージェントツールを使用してWebアプリケーションを構築し、自動的にテストします。

* [ブラウザエージェント テストガイド](/docs/copilot/guides/browser-agent-testing-guide.md)

</div>

## 前提条件

このチュートリアルを完了するには、以下が必要です:

* [コンピューターにVisual Studio Codeをインストール](/download)
* [GitHubアカウント](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github)(クラウドエージェントワークフロー用)
* [GitHub Copilotサブスクリプション](/docs/copilot/setup.md)

## ステップ1: ローカルエージェントを使用してアプリをスキャフォールドする

このステップでは、ローカルエージェントを使用して初期のTodoアプリ構造を作成します。ローカルエージェントは、新しいプロジェクトのスキャフォールドや新しい機能での反復など、即座のフィードバックと結果が必要な対話的なタスクに最適です。

1. 新しいプロジェクトフォルダを作成し、Gitバージョン管理下にあることを確認します。

    ```bash
    mkdir todo-app
    cd todo-app
    git init
    ```

1. VS Codeでプロジェクトフォルダを開きます。

1. チャットビュー(`kb(workbench.action.chat.open)`)を開き、エージェントドロップダウンから**エージェント**を選択します。

    プリファレンスがある場合は、オプションで特定の言語モデルを選択します。

    > [!IMPORTANT]
    > エージェントオプションが表示されない場合は、VS Code設定でエージェントが有効になっていることを確認してください(`setting(chat.agent.enabled)`)。組織によってはエージェントが無効になっている可能性があります。このファンクショナリティを有効にするには管理者にお問い合わせください。

1. チャット入力フィールドに以下のプロンプトを入力し、**送信**を選択してTodoアプリをスキャフォールドします。

    ```prompt
    Create a simple todo app with HTML, CSS, and JavaScript. Include an input field to add todos, a list to display them, and a delete button for each item.
    ```

    <video src="../images/agents-tutorial/local-agent-todo-app-scaffold-v2.mp4" alt="ローカルエージェントがVS Codeでtodoアプリをスキャフォールドしている動画。" muted loop controls></video>

1. エージェントがアプリの異なるファイルを生成するときにレビューします。**保持**または**元に戻す**を使用して、必要に応じて変更を受け入れるか拒否します。

1. 統合ブラウザで変更をプレビューできます。

    * `localhostURL`の統合ブラウザを有効にするには、`setting(workbench.browser.openLocalhostLinks)`を構成します

    * `index.html`ファイルを開き、**プレビュー**ボタンを選択します。

1. さらなるプロンプトを送信してアプリをさらに強化します。プレビューが変更に伴ってライブで更新されることに注意してください。

    たとえば、以下を段聞くことができます:

    ```prompt
    Mark todos as completed with a strikethrough effect.
    ```

これでさらなる機能で拡張できる機能的なTodoアプリができました。ローカルエージェントを使用することで、リアルタイムでコードを対話的に生成および改善できます。

## ステップ2: Copilot CLIを使用して機能プランを実装する

このステップでは、プランエージェントを使用してテーマトグルの実装プランを作成し、その後Copilot CLIへの実装をバックグラウンドで移行します。Copilot CLIは、即座のインタラクションを必要としないタスクを委任するのに最適です。Git worktreesを使用してメインワークスペースからファイル変更を分離し、競合を防ぎます。

1. まず、ソース管理ビューで現在の変更をコミットして関連する状態にします。

1. チャットビューで、**新規チャット(+)** > **新規チャット**を選択して新しいローカルエージェントセッションを開始します。前のチャットセッションがセッションリストに保持されていることに注意してください。

1. エージェントドロップダウンから**プラン**を選択してプランエージェントに切り替え、以下のプロンプトを入力します:

    ```prompt-plan
    Create a plan to add a dark/light theme toggle to the app. The toggle should switch between themes and persist the user's preference.
    ```

1. プランエージェントは、プランを改善するために明確化する質問を行う可能性があります。必要に応じて応答します。

1. 準備ができたら、**実装を開始** > **Copilot CLIで続行**を選択してプランをCopilot CLIに移行します。

    ![チャットビューの[実装を開始]ボタンを示すスクリーンショット。](../images/agents-tutorial/plan-agent-start-implementation-cli.png)

1. Copilot CLIはGit worktreeを作成し、機能の実装を開始します。求められたら、**変更をコピー**を選択して現在のすべての変更がCopilot CLIで利用可能であることを確認します。

1. **セッション**ビューでCopilot CLIセッションを追跡できます。セッションを選択してその進捗の詳細を表示します。

    <video src="../images/agents-tutorial/background-agent-theme-switcher-v2.mp4" alt="Copilot CLIがVS Codeでテーマスイッチャー機能を実装している動画。" muted loop controls></video>

    > [!TIP]
    > Copilot CLIがバックグラウンドで動作している間、競合なくメインワークスペースを引き続き編集できます。

1. エージェントが終了した後、変更されたファイルを選択してその変更をレビューするか、**すべての変更を表示**を選択してすべての変更を含む複数ファイル差分エディタを開きます。

    > [!TIP]
    > Copilot CLIにフォローアッププロンプトを送信して、機能に調整または改善を行うことができます。

1. チャットビューで、**適用**を選択してメインワークスペースに変更を適用します。

Copilot CLIを使用してバックグラウンドでタスクを自律的に実行しました。メインワークフローを中断することなく、異なるタスク用の複数のCopilot CLIセッションを開始できます。

## ステップ3: クラウドエージェントを使用して機能に協業する

このステップでは、クラウドエージェント(Copilot Codingエージェント)を使用してアプリレイアウトを再設計し、GitHubのプルリクエストと協業機能を使用します。Copilot Codingエージェントはリモートインフラストラクチャで実行され、即座のフィードバックが不要なタスク、ローカルで実行する必要がないタスク、またはGitHubを通じた協業を伴うタスクに最適です。

1. まず、プロジェクトをGitHubリポジトリに公開し、プロジェクトにレモートとしてクラウドエージェント上で追加します。

    1. コマンドパレット(`kb(workbench.action.showCommands)`)から**GitHubに公開**コマンドを実行し、プロンプターに従って新しいリポジトリを作成します。

    1. コマンドパレットから**Git: リモートを追加**コマンドを実行し、プロンプターに従ってGitHubリポジトリをレモートとして追加します。

1. チャットビューで、**新規チャット(+)** > **新規チャット**を選択します。

1. セッションタイプドロップダウンから**クラウド**を選択してクラウドエージェントに切り替え、以下のプロンプトを入力します:

    ```text
    Redesign the todo app layout to improve user experience. Update colors, spacing, typography, and add animations to give it a modern look.
    ```

1. クラウドエージェントがリクエストで作業するための新しいセッションを開始します。GitHubリポジトリにブランチとプルリクエストを作成します。

    <video src="../images/agents-tutorial/cloud-agent-redesign-todo-app-v2.mp4" alt="クラウドエージェントがVS Codeでtodoアプリを再設計している動画。" muted loop controls></video>

1. チャットビューの**セッション**ビューでクラウドエージェントを追跡するか、リンクを選択してプルリクエストの詳細を表示します。

    > [!TIP]
    > GitHub Pull Requests拡張機能がインストールされている場合は、GitHub Pull Requestsビューの**自分の代わりにCopilot**ビューでプルリクエスト進捗を追跡することもできます。

1. 完了した後、クラウドエージェントがレビュー用のプルリクエストを割り当てます。

    ![クラウドエージェントセッションの詳細(ファイル変更の詳細付き)を示すスクリーンショット。](../images/agents-tutorial/cloud-agent-pull-request.png)

1. **セッション**ビューのクラウドエージェントセッションを右クリックして追加オプションを表示するか、セッションを選択して**チェックアウト**または**適用**を選択します。

GitHubを使用して機能に協業するためのクラウドエージェントを正常に使用しました。クラウドエージェントを使用すると、リモートリソースを使用し、GitHubの課題とプルリクエストを通じて変更に協業できます。

## 次のステップ

Todoアプリを構築、強化、再設計するためのさまざまなタイプのエージェントを正常に使用しました。エージェントの探索を続けてください:

* [エージェントタイプとそれらを使用する時期](/docs/copilot/agents/overview.md)について学習する
* [プランエージェントでタスクの計画と調査](/docs/copilot/agents/planning.md)
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)の探索

