---
ContentId: 9f1a2b3c-4e5f-6d7c-8a9b-1c2d3e4f5a6b
DateApproved: 01/08/2026
MetaDescription: Visual Studio Code での自律的なコーディングタスク、ターミナル統合、および分離された開発ワークフローのための Copilot CLI などのバックグラウンドエージェントの使用方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- background agent
- copilot cli
---

# Visual Studio Code のバックグラウンドエージェント

Visual Studio Code のバックグラウンドエージェントは、Copilot CLI などの CLI ベースのエージェントであり、ローカルマシンのバックグラウンドで実行されます。エディターで他の作業を続けている間、それらは自律的に動作します。バックグラウンドエージェントは、Git worktree を使用してメインワークスペースから分離して作業し、アクティブな作業との競合を防ぐことができます。

この記事では、バックグラウンドエージェントの主な機能、および Copilot CLI または OpenAI Codex からバックグラウンドセッションを開始および管理する方法について説明します。

![VS Code のチャットエディターとしてのバックグラウンドエージェントセッションのスクリーンショット。](../images/background-agents/background-agent-session.png)

## バックグラウンドエージェントとは?

VS Code のエディターコンテキスト内で動作し、それを認識しているローカルエージェントとは異なり、バックグラウンドエージェントはローカルマシンのコマンドラインインターフェイス (CLI) を介して独立して実行されます。VS Code の統合されたチャットビューからすべてのバックグラウンドエージェントセッションを表示および管理できます。このビューでは、VS Code から直接新しいバックグラウンドエージェントセッションを作成したり、ローカルエージェントの会話をバックグラウンドエージェントに引き継いだりすることもできます。

バックグラウンドエージェントはユーザーの操作なしにバックグラウンドで実行されるため、よく定義されたスコープと必要なすべてのコンテキストを持つタスクに適しています。例としては、計画からの機能の実装、概念実証の複数のバリエーションの作成、明確に定義された修正または機能の実装などがあります。

バックグラウンドエージェントは、コードベースに変更を自律的に適用します。エディターでのアクティブな作業への干渉を防ぐために、バックグラウンドエージェントは Git worktree を使用して[分離された環境](#create-an-isolated-background-agent-session-experimental)で実行でき、メインワークスペースに影響を与えることなく変更を加えることができます。worktree 分離を使用してバックグラウンドエージェントセッションを開始すると、VS Code はそのセッション用に別のフォルダーを自動的に作成します。メインワークスペースでバックグラウンドエージェントを実行することもできますが、競合が発生する可能性があります。

バックグラウンドエージェントは CLI 経由で実行され、VS Code の組み込みツールやランタイムコンテキスト (失敗したテストやテキスト選択など) に直接アクセスすることはできません。また、MCP サーバーや拡張機能が提供するツールにもアクセスできません。これらは、CLI ツールで使用可能なモデルに制限されます。バックグラウンドエージェントはターミナルコマンドを実行でき、必要に応じて承認を求める場合があります。

タスクをバックグラウンドエージェントに割り当てるには、チャットビューから直接新しいバックグラウンドセッションを作成するか、エージェントの専用 CLI を使用するか、VS Code からのローカルチャット会話をバックグラウンドエージェントセッションとして引き継ぐことができます。

### Copilot CLI

**Copilot CLI** は、VS Code の主要なバックグラウンドエージェントです。Copilot CLI をターミナルから直接使用したり、VS Code 内からセッションを開始および管理したりできます。

開始するには、Copilot CLI をインストールしてセットアップしてください。VS Code がこれを処理しますが、次のコマンドを使用して CLI を手動でインストールすることもできます:

```bash
npm install -g @github/copilot
```

GitHub ドキュメントの [Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli) の詳細をご確認ください。

### OpenAI Codex

**OpenAI Codex** バックグラウンドエージェントは、OpenAI の Codex を使用してコーディングタスクを自律的に実行します。OpenAI Codex エージェントを使用するには、Visual Studio Marketplace から [OpenAI Codex](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt) 拡張機能をインストールしてください。

VS Code の OpenAI Codex を使用すると、Copilot Pro+ サブスクリプションを使用して、追加のセットアップなしで Codex を認証およびアクセスできます。GitHub ドキュメントの [GitHub Copilot の課金とプレミアムリクエスト](https://docs.github.com/en/copilot/concepts/billing/copilot-requests) の詳細をご確認ください。

## バックグラウンドエージェントセッションの表示と管理

VS Code のチャットビューから、すべてのバックグラウンドエージェントセッションを表示および管理できます。フィルターオプションから **Background Agents** (バックグラウンドエージェント) を選択して、セッションリストをフィルター処理し、バックグラウンドエージェントセッションのみを表示します。

![VS Code チャットビューのバックグラウンドエージェントフィルターのスクリーンショット。](../images/background-agents/background-agent-filter.png)

リストからバックグラウンドエージェントセッションを選択して、チャットビューでセッションの詳細を開きます。セッションをエディタータブ (チャットエディター) で表示したい場合は、セッションを右クリックして **Open as Editor** (エディターとして開く) を選択します。

VS Code のチャット会話ではなくターミナルでバックグラウンドセッションを表示したい場合は、チャットビューでセッションを右クリックして **Resume Agent Session in Terminal** (ターミナルでエージェントセッションを再開) を選択します。VS Code 内で直接 Copilot CLI と対話できます。

![VS Code 内の Copilot CLI セッションを示すスクリーンショット。](../images/background-agents/copilot-cli-in-terminal.png)

## バックグラウンドエージェントセッションの開始

ワークフローに応じて、いくつかの方法でバックグラウンドエージェントセッションを開始できます。CLI を使用して新しいセッションを作成し、タスクの詳細を直接提供するか、VS Code の[チャットビュー](/docs/copilot/agents/overview.md#agent-sessions-list)から新しいセッションを開始できます。

もう1つのアプローチ (特に複雑なタスクの場合) は、最初に VS Code のチャットでローカルエージェントと対話し、スコープと詳細が明確になったら、タスクをバックグラウンドエージェントセッションに引き継ぐことです。たとえば、[Plan エージェント](/docs/copilot/chat/chat-planning.md)を使用してマルチステップの機能実装の概要を説明し、実際のコーディングをバックグラウンドエージェントに委任することができます。

### Copilot CLI バックグラウンドエージェントセッションの作成

VS Code で新しい Copilot CLI バックグラウンドエージェントセッションを作成するには、いくつかの方法があります:

* チャットビューから:

    1. チャットビューを開きます (`kb(workbench.action.chat.open)`)

    1. **New Chat** (新しいチャット) ドロップダウン > **New Background Agent** (新しいバックグラウンドエージェント) を選択します

* ローカルチャットセッション中に:

    * チャット入力に `@cli <task description>` と入力してメッセージを送信します

    * プロンプトを入力し、**Continue In** (続行) > **Background Agent** (バックグラウンドエージェント) を選択します

* コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: New Background Agent** (チャット: 新しいバックグラウンドエージェント) コマンドを実行します

新しいバックグラウンドエージェントセッションが開き、追加のタスク詳細を提供したり、Copilot CLI セッションの進行状況を追跡したりできます。

> [!TIP]
> ターミナルで GitHub Copilot CLI を使用してセッションを開始すると、VS Code のチャットビューがこのバックグラウンドセッションを自動的に検出して表示します。このバックグラウンドセッションと VS Code 内からさらにやり取りできます。

### OpenAI Codex バックグラウンドエージェントセッションの作成

チャットビューから新しい OpenAI Codex バックグラウンドエージェントセッションを作成するには:

* チャットビューから:

    1. チャットビューを開きます (`kb(workbench.action.chat.open)`)

    1. **New Chat** (新しいチャット) ドロップダウン > **New Codex Agent** (新しい Codex エージェント) を選択します

* コマンドパレット (`kb(workbench.action.showCommands)`) から **Codex: New Codex Agent** (Codex: 新しい Codex エージェント) コマンドを実行します

新しい Codex バックグラウンドエージェントセッションが開き、追加のタスク詳細を提供したり、Codex セッションの進行状況を追跡したりできます。

### エージェントセッションをバックグラウンドエージェントに引き継ぐ

複雑なタスクの場合、最初に VS Code チャットでローカルエージェントと対話して要件を明確にし、その後、自律的な実行のためにタスクをバックグラウンドエージェントに引き継ぐと役立つ場合があります。ローカルエージェントの会話をバックグラウンドエージェントセッションに引き継ぐと、完全な会話履歴とコンテキストがバックグラウンドエージェントに渡されます。

バックグラウンドエージェントセッションでローカルエージェントセッションを続行するには:

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)

1. タスクをバックグラウンドエージェントに引き継ぐ準備ができるまで、ローカルエージェントと対話します

1. バックグラウンドエージェントに引き継ぐには、次のオプションがあります:

    * **Continue In** (続行) を選択し、次に **Background** (バックグラウンド) を選択します

        ![VS Code チャットインターフェイスの「チャットで続行」ボタンを示すスクリーンショット。](../images/background-agents/continue-in-chat-background.png)

    * [Plan エージェント](/docs/copilot/chat/chat-planning.md)を使用している場合は、**Start Implementation** (実装を開始) ドロップダウンを選択し、**Continue in Background** (バックグラウンドで続行) を選択して、バックグラウンドエージェントセッションで実装を実行します

        ![VS Code チャットインターフェイスの「実装を開始」ボタンを示すスクリーンショット。](../images/background-agents/plan-agent-start-implementation-background.png)

    * チャット入力に `@cli` と入力して、タスクをバックグラウンドエージェントに引き継ぎます

バックグラウンドエージェントセッションが自動的に開始され、完全な会話履歴とコンテキストが引き継がれます。チャットビューでバックグラウンドエージェントの進行状況を監視できます。

## 分離されたバックグラウンドエージェントセッションの作成 (実験的)

バックグラウンドエージェントの変更をメインワークスペースから分離するには、[Git worktree](/docs/sourcecontrol/branches-worktrees.md#understanding-worktrees) を使用するバックグラウンドエージェントセッションを作成できます。worktree を作成すると、VS Code はセッション用の別のフォルダーを作成します。バックグラウンドエージェントはこの分離されたフォルダーで動作し、アクティブな作業との競合を防ぎます。

バックグラウンドエージェントセッションで Git worktree を使用するには:

1. VS Code で新しい Copilot CLI バックグラウンドエージェントセッションを開始します。

1. チャット入力ボックスで、分離モードとして **Worktree** を選択します。

    ![VS Code チャットインターフェイスの「Worktree」分離モードオプションを示すスクリーンショット。](../images/background-agents/isolated-run-mode.png)

    **Workspace** (ワークスペース) を選択すると、バックグラウンドエージェントは変更をメインワークスペースに直接適用します。

1. プロンプトを入力してエージェントセッションを開始します。VS Code は自動的に新しい Git worktree を作成します。

    バックグラウンドエージェントによって行われたすべての変更は worktree フォルダーに適用され、メインワークスペースから分離されます。

1. ソース管理ビューの **Repositories** (リポジトリ) ビューで、Git worktree を表示できます

    ![VS Code ソース管理ビューの Git worktree を示すスクリーンショット。](../images/background-agents/git-worktree-source-control.png)

    Agents (エージェント) ビューには、バックグラウンドエージェントセッションの worktree パスも表示されます。

1. Agents (エージェント) ビューでバックグラウンドエージェントの進行状況を監視します

1. バックグラウンドエージェントがタスクを完了した後、worktree からの変更を確認し、メインワークスペースにマージできます。

    バックグラウンドセッション出力の下部に、このバックグラウンドエージェントセッションから変更されたファイルの概要が表示され、その後にこの worktree からのすべての未処理の変更 (バックグラウンドエージェントからのもの、または worktree への独自の編集である可能性があります) が続きます。

    ![worktree の変更を保持する機能を示すスクリーンショット。](../images/background-agents/filechanges.png)

    次のことを選択できます:
    * 個々のファイル名をクリックするか、`View All Edits` (すべての編集を表示) diff ボタンを使用して、ファイルの変更を調査します
    * `Keep` (保持) ボタンを使用して、エージェントセッションからの保留中の変更を保持するか、`Undo` (元に戻す) を使用して削除します
    * `Apply` (適用) ボタンを使用して、worktree で保持されたすべての変更をローカルリポジトリに適用します

[VS Code ソース管理での Git worktree の使用](/docs/sourcecontrol/branches-worktrees.md)の詳細をご確認ください。

## バックグラウンドエージェントでのカスタムエージェントの使用 (実験的)

[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を使用すると、VS Code のエージェントのカスタムペルソナと役割を定義できます。たとえば、コードレビューを実行するためのカスタムエージェントを作成できます。カスタムエージェントは、特定の指示と動作を定義できます。

バックグラウンドエージェントセッションを作成するときに、タスクを処理するカスタムエージェントを選択できます。バックグラウンドエージェントは、カスタムエージェントの定義された動作に従って動作します。

バックグラウンドエージェントでカスタムエージェントを有効にするには:

1. `setting(github.copilot.chat.cli.customAgents.enabled)` 設定でバックグラウンドエージェントのカスタムエージェントを有効にします

1. コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: New Custom Agent** (チャット: 新しいカスタムエージェント) コマンドを使用して、ワークスペースにカスタムエージェントを作成します

    > [!NOTE]
    > 現在、ワークスペースで定義されたカスタムエージェントのみがバックグラウンドエージェントセッションで使用できます。[カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md#create-a-custom-agent)について詳しくは、こちらをご覧ください。

1. 新しいバックグラウンドエージェントセッションを作成し、Agents (エージェント) ドロップダウンからカスタムエージェントを選択します

    ![VS Code チャットインターフェイスでのカスタムエージェントの選択を示すスクリーンショット。](../images/background-agents/custom-agent-selection.png)

1. プロンプトを入力すると、カスタムエージェントがタスクの処理に使用されることがわかります

## 関連リソース

* [エージェントの概要](/docs/copilot/agents/overview.md): さまざまなエージェントの種類と、エージェント間でタスクを引き継ぐ方法を理解します
* [クラウドエージェント](/docs/copilot/agents/cloud-agents.md): GitHub統合が必要なタスクのためのクラウドエージェントについて学びます
* [カスタムエージェント](/docs/copilot/customization/custom-agents.md): カスタムエージェントの役割とペルソナを作成します
* [GitHub Copilot CLI ドキュメント](https://cli.github.com/manual/gh_copilot)
