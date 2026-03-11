---
ContentId: 9f1a2b3c-4e5f-6d7c-8a9b-1c2d3e4f5a6b
DateApproved: 3/9/2026
MetaDescription: VS Code内でGitHub Copilot CLIを使用して自律的なコーディングタスク、ターミナル統合、隔離された開発ワークフローを実行する方法を学習します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- background
- copilot cli
- autonomous
- worktree
- parallel
---

# Visual Studio CodeのCopilot CLIセッション

Visual Studio CodeはGitHub Copilot CLIを使用してバックグラウンドでエージェントセッションを実行できます。VS Codeの統合Chat ビューから Copilot CLI セッションを開始、監視、管理できます。一方、エージェントは、エディター内で他の作業を続けながら、ローカルマシンで自律的に実行されます。複数のCopilot CLIセッションを並行して実行し、独立したタスクに同時に取り組むことができます。

Copilot CLIセッションを開始するには、[新しいセッションを作成](#create-a-copilot-cli-session)するか、[ローカルエージェントセッションをCopilot CLIにハンドオフ](#hand-off-a-local-session-to-copilot-cli)して、既存のコンテキストを渡します。

この記事では、Copilot CLIエージェントの主な機能、およびCopilot CLIからバックグラウンドセッションを開始および管理する方法について説明します。

![VS CodeのChat エディターとしてのCopilot CLIセッションのスクリーンショット。](../images/background-agents/copilot-cli-session.png)

> [!TIP]
> OpenAI Codexのようなサードパーティプロバイダーもバックグラウンド機能を提供しています。[サードパーティエージェント](/docs/copilot/agents/third-party-agents.md)の詳細を確認してください。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントの概要">
ローカル、バックグラウンド、クラウドエージェントをVS Codeで体験するための実践的なチュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## Copilot CLIセッションとは?

Copilot CLIセッションはローカルマシン上でバックグラウンドで独立して実行され、Copilot CLIエージェントハーネスを使用します。VS CodeはCopilot SDKを使用してこれらのエージェントと統合し、バックグラウンドセッションの開始、停止、進捗監視を行います。VS CodeはCopilot CLIを自動的にインストールして構成します。

Copilot SDKセッションはVS Codeの外で実行され、VS Codeウィンドウを閉じた後もバックグラウンドで実行を続けます。この動作は、エディター内でVS Codeエージェントハーネスを使用するローカルエージェント（VS Codeが停止すると実行が停止するもの）とは異なります。

統合Chat ビューからCopilot CLIセッションと対話できます。バックグラウンドセッションが入力や権限を必要とする場合、チャット内から実行できます。エージェント状態インジケーターもセッションが入力を必要とする場合のヒントを提供します。

Copilot CLIセッションはバックグラウンドで実行されるため、スコープが明確に定義されており、必要なコンテキストをすべて備えており、頻繁なユーザー対話を必要としないタスクに適しています。例として、計画からの機能実装、プルーフオブコンセプトの複数バリアントの作成、または明確に定義された修正または機能の実装が挙げられます。

Copilot CLIはチャットでスラッシュコマンド([再利用可能なプロンプト](/docs/copilot/customization/prompt-files.md)、[エージェントスキル](/docs/copilot/customization/agent-skills.md)、[フック](/docs/copilot/customization/hooks.md)、長い会話を管理するための`/compact`を含む)をサポートしています。Copilot CLIセッションのチャット入力で`/`を入力すると、利用可能なコマンドが表示されます。

### 隔離モード

Copilot CLIはエージェントからの変更がコードベースに適用される方法を管理するための2つのタイプの隔離モードをサポートしています: **Worktree**と**Workspace**隔離。Copilot CLIセッションを作成するときに、隔離モードを選択できます。

Copilot CLIエージェントからの変更を隔離し、アクティブな作業との干渉を防ぐには、**Worktree**隔離を使用します。このモードでは、VS CodeはCopilot CLIセッション用の別フォルダーに[Git worktree](/docs/sourcecontrol/branches-worktrees.md#understanding-worktrees)を作成します。エージェントによって作成されたすべての変更は worktree に適用され、メインワークスペースから分離されて、レビューして適用する準備ができるまで保たれます。

Copilot CLIセッションからの変更が現在のワークスペースに直接適用されるようにしたい場合は、**Workspace**隔離を選択できます。このモードでは、エージェントは現在のワークスペースで直接操作し、変更は直ちに適用されます。

> [!NOTE]
> Git worktreeと worktree 隔離を使用するには、ワークスペースがGitリポジトリである必要があります。

### Copilot CLIセッションの制限

* Copilot CLIセッションはVS Codeの組み込みツールすべてにアクセスできません。チャット入力で明示的に[コンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)できます。

* 拡張機能提供ツールへのアクセスがなく、CLIツール経由で利用可能なモデルに限定されます。

* 現在、認証を必要としないローカルMCPサーバーのみにアクセスできます。

## Copilot CLIセッションの作成

VS CodeでCopilot CLIセッションを新規作成するには:

1. 次のいずれかのオプションを使用して、新しいセッションを作成します

    * Chat ビューを開き(`kb(workbench.action.chat.open)`)、Session Targetドロップダウンから**Copilot CLI**を選択します

    * 上部の**新しいChat**アイコンを選択し、**新しいCopilot CLIセッション**を選択します

    * Command Palette(`kb(workbench.action.showCommands)`)から**Chat: New Copilot CLI**コマンドを実行します

1. ワークスペースまたはworktree [隔離モード](#isolation-modes)から選択します

    worktree隔離を使用した場合、エージェントは各ターンの終わりにworktreeへの変更を自動的にコミットし、セッション履歴がコミット履歴と一致したままになります。

    > [!TIP]
    > セッションリストで右クリックして**Open Worktree in New Window**を選択することで、セッションのworktreeを開くことができます。Source Control ビューリポジトリエクスプローラー(`scm.repositories.explorer`)でworktreeを表示することもできます。

1. プロンプトを送信してエージェントを開始します。オプションで、追加のコンテキストを追加するか、特定の言語モデルやカスタムエージェントを選択します。

1. Chat ビューでセッションステータスを追跡します。

> [!TIP]
> 複数のCopilot CLIセッションを作成して、異なるタスクに並行して取り組むことができます。

## ローカルセッションをCopilot CLIにハンドオフ

複雑なタスクの場合、最初にVS Code内のローカルエージェントと対話して要件を明確にしてから、タスクをCopilot CLIにハンドオフしてバックグラウンドで自律的に実行させることが有効な場合があります。これは[計画エージェント](/docs/copilot/agents/planning.md)を使用して計画を作成してから、その計画の実装をCopilot CLIにハンドオフするときに有効です。

ローカルエージェントの会話をCopilot CLIセッションにハンドオフすると、完全な会話履歴とコンテキストがバックグラウンドセッションに渡されます。

ローカルエージェントセッションをCopilot CLIにハンドオフするには:

1. Chat ビューを開きます(`kb(workbench.action.chat.open)`)

1. タスクをハンドオフする準備ができるまでローカルエージェントと対話します

1. Copilot CLIにハンドオフするには、次のオプションがあります:

    * **Session Target**ドロップダウンを開き、**Copilot CLI**を選択します

        ![VS CodeのChat インターフェースでSession Targetドロップダウンを表示しているスクリーンショット。](../images/background-agents/continue-in-cli.png)

    * [計画エージェント](/docs/copilot/agents/planning.md)を使用している場合は、**Start Implementation**ドロップダウンを選択し、**Continue in Copilot CLI**を選択してCopilot CLIセッションで実装を実行します

        ![VS CodeのChat インターフェースで「Start Implementation」ボタンを表示しているスクリーンショット。](../images/background-agents/plan-agent-start-implementation-cli.png)

Copilot CLIセッションが自動的に開始され、完全な会話履歴とコンテキストが引き継がれます。

## ターミナルからCopilot CLIを使用

Chat ビューからCopilot CLIセッションを開始することに加えて、VS Codeターミナルから直接Copilot CLIを使用できます。

![VS Code内のCopilot CLIセッションを表示しているスクリーンショット。](../images/background-agents/copilot-cli-in-terminal.png)

### Copilot CLIターミナルを開く

VS CodeはGitHub Copilot CLIターミナルプロファイルを登録しており、これを使用して専用のCopilot CLIターミナルを開くことができます。Copilot CLIターミナルは複数の方法で開くことができます:

* Terminal パネルの**+**ボタンの横のドロップダウンを選択し、**GitHub Copilot CLI**を選択します

* Command Palette から**Chat: New Copilot CLI Session**コマンドを実行してパネルでCopilot CLIターミナルを開くか、**Chat: New CLI Session to the Side**を実行して現在のエディターの横のエディタータブで開きます

* Command Palette(`kb(workbench.action.showCommands)`)から**Terminal: Create New Terminal (With Profile)**コマンドを実行し、**GitHub Copilot CLI**を選択します

* 任意のVS Code統合ターミナルで`copilot`を入力してCopilot CLIを直接開始します

Copilot CLIターミナルは以下のシェルをサポートしています:

* macOSおよびLinuxで**bash**と**zsh**
* Windows上で**PowerShell**と**Command Prompt**

### ターミナルからセッションを開始および再開

Copilot CLIターミナルから新しいセッションを開始すると、VS Codeは自動的にセッションを検出し、Chat ビューセッションリストに表示します。その後、ターミナルまたはChat ビューのいずれからでも進捗を追跡、フォローアッププロンプトを送信、または変更を確認できます。

ターミナルで既存のCopilot CLIセッションを再開するには、セッションリストでセッションを右クリックして**Resume in Terminal**を選択します。

VS CodeはCopilot CLIターミナルの認証を自動的に処理するため、別途サインインする必要はありません。

## 複数リポジトリワークスペース

ワークスペースに複数のGitリポジトリが含まれている場合、Copilot CLIセッションを開始するとVS CodeがChat 入力にリポジトリピッカーを表示します。このピッカーを使用して、worktreeを作成するリポジトリを選択します。

セッションが開始したら、リポジトリピッカーはそのセッションで無効になります。worktreeはSource Control リポジトリビューの**Worktrees**ノードの下の選択されたリポジトリの下に表示されます。

> [!TIP]
> ワークスペース内のすべてのリポジトリを表示するには、`setting(scm.repositories.explorer)`設定を有効にしてSource Control ビューを開きます。

## Copilot CLIでカスタムエージェントを使用(実験的)

[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を使用すると、VS Codeのエージェント用のカスタムペルソナとロールを定義できます。例えば、コードレビューを実行するためのカスタムエージェントを作成できます。カスタムエージェントは特定の指示と動作を定義できます。

Copilot CLIセッションを作成すると、カスタムエージェントを選択してタスクを処理させることができます。カスタムエージェントは定義された動作に従って操作します。

Copilot CLIでカスタムエージェントを使用するには:

1. `setting(github.copilot.chat.cli.customAgents.enabled)`設定でCopilot CLI用のカスタムエージェントを有効にします

1. Command Palette(`kb(workbench.action.showCommands)`)から**Chat: New Custom Agent**コマンドを使用して、ワークスペースにカスタムエージェントを作成します

1. 新しいCopilot CLIセッションを作成し、Agentsドロップダウンからカスタムエージェントを選択します

    ![VS CodeのChat インターフェースでカスタムエージェント選択を表示しているスクリーンショット。](../images/background-agents/custom-agent-selection-v2.png)

1. プロンプトを入力して、カスタムエージェントがタスクを処理するために使用されることに注意してください

> [!NOTE]
> 現在、ワークスペースで定義されたカスタムエージェントのみがCopilot CLIセッションで使用可能です。[カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md#create-a-custom-agent)の詳細を確認してください。

## 関連リソース

* [エージェント概要](/docs/copilot/agents/overview.md): さまざまなエージェントタイプとエージェント間でタスクをハンドオフする方法を理解します
* [カスタムエージェント](/docs/copilot/customization/custom-agents.md): カスタムエージェントのロールとペルソナを作成します
* [GitHub Copilot CLIドキュメント](https://cli.github.com/manual/gh_copilot)

