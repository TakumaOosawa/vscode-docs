---
ContentId: 9f1a2b3c-4e5f-6d7c-8a9b-1c2d3e4f5a6b
DateApproved: 3/9/2026
MetaDescription: VS Code内でGitHub Copilot CLIを使用して、自律的なコーディングタスク、ターミナル統合、分離された開発ワークフローを学びます。
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

Visual Studio CodeではGitHub Copilot CLIを使用してバックグラウンドでエージェントセッションを実行できます。VS Code内の統合Chat表示からCopilot CLIセッションを開始、監視、管理できます。エージェントはあなたのローカルマシン上で自律的に実行され、エディタで他の作業を継続できます。複数のCopilot CLIセッションを並行実行して、独立したタスクに同時に対応できます。

Copilot CLIセッションを開始するには、[新しいセッションを作成](#create-a-copilot-cli-session)するか、[ローカルエージェントセッションをCopilot CLIに引き継ぐ](#hand-off-a-local-session-to-copilot-cli)ことで、既存のコンテキストを渡せます。

この記事ではCopilot CLIエージェントの主な機能と、Copilot CLIからバックグラウンドセッションを開始・管理する方法について説明します。

![VS Code内のCopilot CLIセッションをチャットエディタで表示したスクリーンショット](../images/background-agents/copilot-cli-session.png)

> [!TIP]
> OpenAI Codexなどのサードパーティプロバイダーもバックグラウンド機能を提供しています。[サードパーティエージェント](/docs/copilot/agents/third-party-agents.md)について詳しく学びます。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントを始める">
ローカル、バックグラウンド、クラウドエージェントをVS Code内で体験するためのハンズオンチュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## Copilot CLIセッションとは

Copilot CLIセッションはローカルマシン上のバックグラウンドで独立して実行され、Copilot CLIエージェントハーネスを使用します。VS CodeはCopilot SDKを使用してこれらのエージェントと統合し、バックグラウンドセッションの開始、停止、進行状況の監視ができます。VS CodeはCopilot CLIを自動的にインストールして設定します。

Copilot SDKセッションはVS Code外で実行さ続け、VS Codeウィンドウを閉じた後もバックグラウンドで実行を続けます。これはエディタ内のVS Codeエージェントハーネスを使用するローカルエージェントと異なり、VS Codeが停止すると実行も停止します。

統合Chat表示からCopilot CLIセッションとやり取りできます。バックグラウンドセッションがあなたの入力を必要とするか、アクションを実行する権限が必要な場合、チャット内から実行できます。エージェントステータスインジケータはセッションが入力を必要とするときにもヒントを表示します。

Copilot CLIセッションはバックグラウンドで実行されるため、明確なスコープを持ち、必要なコンテキストがすべて揃っており、頻繁なユーザー操作を必要としないタスクに適しています。例としては、計画から機能を実装する、概念実証の複数のバリエーションを作成する、明確に定義された修正または機能を実装することが挙げられます。

Copilot CLIはチャット内のスラッシュコマンドをサポートしており、[再利用可能なプロンプト](/docs/copilot/customization/prompt-files.md)、[エージェントスキル](/docs/copilot/customization/agent-skills.md)、[フック](/docs/copilot/customization/hooks.md)、および長い会話を管理するための`/compact`が含まれています。Copilot CLIセッションのチャット入力で`/`と入力して、利用可能なコマンドを確認してください。

### 分離モード

Copilot CLIはエージェントの変更をコードベースに適用する方法を管理するための2種類の分離モードをサポートしています：**Worktree**と**Workspace**の分離です。新しいCopilot CLIセッションを作成するときに分離モードを選択できます。

Copilot CLIエージェントからの変更を分離し、アクティブな作業への干渉を防ぐには、**Worktree**の分離を使用してください。このモード内で、VS CodeはCopilot CLIセッション用に別のフォルダーに[Gitワークツリー](/docs/sourcecontrol/branches-worktrees.md#understanding-worktrees)を作成します。エージェントが行ったすべての変更はワークツリーに適用され、レビューして適用する準備ができるまでメインワークスペースから分離されたままになります。

Copilot CLIセッションからの変更を現在のワークスペースに直接適用する場合は、**Workspace**の分離を選択できます。このモード内では、エージェントは現在のワークスペースで直接動作し、変更がその場で適用されます。

> [!NOTE]
> Gitワークツリーとワークツリー分離を使用するには、ワークスペースがGitリポジトリである必要があります。

### Copilot CLIセッションの制限事項

* Copilot CLIセッションはすべてのVS Code組み込みツールにアクセスできません。チャット入力で明示的に[コンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)できます。

* 拡張機能が提供するツールにアクセスできず、CLIツール経由で利用可能なモデルに限定されます。

* 現在、認証を必要としないローカルMCPサーバーのみにアクセスできます。

## Copilot CLIセッションを作成する

VS Code内で新しいCopilot CLIセッションを作成するには：

1. 以下のいずれかのオプションを使用して新しいセッションを作成します

    * Chat表示を開く（`kb(workbench.action.chat.open)`）し、セッションターゲットドロップダウンから**Copilot CLI**を選択します

    * 上部の**新規チャット**アイコンを選択し、**新規Copilot CLIセッション**を選択します

    * コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: New Copilot CLI**コマンドを実行します

1. ワークスペースまたはワークツリーの[分離モード](#isolation-modes)を選択します

    ワークツリー分離を使用する場合、エージェントは各ターンの終了時に変更をワークツリーに自動的にコミットするため、セッション履歴はコミット履歴と一致したままになります。

    > [!TIP]
    > セッション一覧でセッションを右クリックし、**ワークツリーを新しいウィンドウで開く**を選択して、セッションのワークツリーを開くことができます。ソース管理表示リポジトリエクスプローラー（`scm.repositories.explorer`）でワークツリーを表示することもできます。

1. プロンプトを送信してエージェントを開始します。必要に応じて、追加のコンテキストを追加するか、特定の言語モデルとカスタムエージェントを選択してください。

1. Chat表示でセッションステータスを追跡します。

> [!TIP]
> 複数のCopilot CLIセッションを作成して、異なるタスクに並行して取り組むことができます。

## ローカルセッションをCopilot CLIに引き継ぐ

複雑なタスクの場合、まずVS Code内のローカルエージェントと対話して要件を明確にしてから、タスクをCopilot CLIに引き継いでバックグラウンドで自律的に実行したほうが役立つ場合があります。これは[計画エージェント](/docs/copilot/agents/planning.md)を使用して計画を作成してから、その計画の実装をCopilot CLIに引き継ぐ場合に役立ちます。

ローカルエージェント会話をCopilot CLIセッションに引き継ぐと、完全な会話履歴とコンテキストがバックグラウンドセッションに渡されます。

ローカルエージェントセッションをCopilot CLIに引き継ぐには：

1. Chat表示を開く（`kb(workbench.action.chat.open)`）

1. タスクを引き継ぐ準備ができるまでローカルエージェントと対話します

1. Copilot CLIに引き継ぐには、以下のオプションがあります：

    * **セッションターゲット**ドロップダウンを開き、**Copilot CLI**を選択します

        ![VS Codeのチャットインターフェースのセッションターゲットドロップダウンを表示したスクリーンショット](../images/background-agents/continue-in-cli.png)

    * [計画エージェント](/docs/copilot/agents/planning.md)を使用している場合は、**実装を開始**ドロップダウンを選択して、**Copilot CLIで続行**を選択し、Copilot CLIセッション内で実装を実行します

        ![VS Codeのチャットインターフェースの「実装を開始」ボタンを表示したスクリーンショット](../images/background-agents/plan-agent-start-implementation-cli.png)

Copilot CLIセッションが自動的に開始され、完全な会話履歴とコンテキストが引き継がれます。

## ターミナルからCopilot CLIを使用する

Chat表示からCopilot CLIセッションを開始するのに加えて、VS Codeターミナルから直接Copilot CLIを使用できます。

![VS Code内のCopilot CLIセッションを表示したスクリーンショット](../images/background-agents/copilot-cli-in-terminal.png)

### Copilot CLIターミナルを開く

VS CodeはCopilot CLIターミナルの専用ターミナルプロファイルを登録しており、これを使用できます。Copilot CLIターミナルを開く方法は複数あります：

* ターミナルパネルの**+**ボタンの横のドロップダウンを選択し、**GitHub Copilot CLI**を選択します

* コマンドパレットから**Chat: New Copilot CLI Session**コマンドを実行してパネル内にCopilot CLIターミナルを開くか、**Chat: New CLI Session to the Side**を実行して現在のエディタの横のエディタタブで開きます

* コマンドパレット（`kb(workbench.action.showCommands)`）から**Terminal: Create New Terminal (With Profile)**コマンドを実行し、**GitHub Copilot CLI**を選択します

* VS Code統合ターミナルで`copilot`と入力してCopilot CLIを直接開始します

Copilot CLIターミナルは以下のシェルをサポートしています：

* macOSとLinuxでは**bash**と**zsh**
* Windowsでは**PowerShell**と**Command Prompt**

### ターミナルからセッションを開始・再開する

Copilot CLIターミナルから新しいセッションを開始すると、VS Codeはセッションを自動的に検出し、Chat表示のセッション一覧に表示します。その後、ターミナルまたはChat表示のいずれからでも進行状況を追跡し、フォローアップのプロンプトを送信したり、変更を確認できます。

ターミナルで既存のCopilot CLIセッションを再開するには、セッション一覧内のセッションを右クリックし、**ターミナルで再開**を選択します。

VS CodeはCopilot CLIターミナルの認証を自動的に処理するため、別途サインインする必要はありません。

## マルチリポジトリワークスペース

ワークスペースに複数のGitリポジトリが含まれている場合、Copilot CLIセッションを開始するとVS Codeはチャット入力にリポジトリピッカーを表示します。このピッカーを使用して、ワークツリーを作成するリポジトリを選択してください。

セッションが開始された後、そのセッションではリポジトリピッカーは無効になります。ワークツリーはソース管理リポジトリ表示の選択したリポジトリの下の**ワークツリー**ノードの下に表示されます。

> [!TIP]
> ワークスペース内のすべてのリポジトリを表示するには、`setting(scm.repositories.explorer)`設定を有効にしてソース管理表示を開いてください。

## Copilot CLIでカスタムエージェントを使用する（実験的）

[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を使用して、VS Code内のエージェントのカスタムペルソナとロールを定義できます。例えば、コードレビューを実行するカスタムエージェントを作成できます。カスタムエージェントは特定の指示と動作を定義できます。

Copilot CLIセッションを作成するときに、タスクを処理するカスタムエージェントを選択できます。カスタムエージェントは定義された動作に従って動作します。

Copilot CLIでカスタムエージェントを使用するには：

1. `setting(github.copilot.chat.cli.customAgents.enabled)`設定でCopilot CLIのカスタムエージェントを有効にします

1. コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: New Custom Agent**コマンドでワークスペース内にカスタムエージェントを作成します

1. 新しいCopilot CLIセッションを作成し、エージェントドロップダウンからカスタムエージェントを選択します

    ![VS Codeのチャットインターフェースのカスタムエージェント選択を表示したスクリーンショット](../images/background-agents/custom-agent-selection-v2.png)

1. プロンプトを入力して、カスタムエージェントがタスクを処理することを確認してください

> [!NOTE]
> 現在、ワークスペース内で定義されたカスタムエージェントのみがCopilot CLIセッションで利用可能です。[カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md#create-a-custom-agent)について詳しく学びます。

## 関連リソース

* [エージェント概要](/docs/copilot/agents/overview.md)：異なるエージェントタイプを理解し、エージェント間でタスクを引き継ぐ方法を学ぶ
* [カスタムエージェント](/docs/copilot/customization/custom-agents.md)：カスタムエージェントのロールとペルソナを作成する
* [GitHub Copilot CLIドキュメント](https://cli.github.com/manual/gh_copilot)

