---
ContentId: 9f1a2b3c-4e5f-6d7c-8a9b-1c2d3e4f5a6b
DateApproved: 12/10/2025
MetaDescription: VS Codeで、自律的なコーディング タスク、ターミナル統合、分離された開発ワークフローに利用できるCopilot CLIなどのバックグラウンド エージェントの使い方を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- background agent
- copilot cli
---

# Visual Studio Codeのバックグラウンド エージェント

Visual Studio Codeのバックグラウンド エージェントは、ローカル マシン上でバックグラウンドで実行されるCopilot CLIなどのCLIベースのエージェントです。エディターで別の作業を続けている間も、自律的に動作します。バックグラウンド エージェントはGit worktreeを使用してメイン ワークスペースから分離して作業し、進行中の作業との競合を防ぐことができます。

この記事では、バックグラウンド エージェントの主な機能と、Copilot CLIまたはOpenAI Codexからバックグラウンド セッションを開始および管理する方法について説明します。

![VS Codeで、バックグラウンド エージェント セッションをチャット エディターとして表示しているスクリーンショット。](../images/background-agents/background-agent-session.png)

## バックグラウンド エージェントとは

VS Codeのエディター コンテキスト内で動作し、その内容を認識できるローカル エージェントとは異なり、バックグラウンド エージェントはローカル マシン上でコマンドライン インターフェイス(CLI)を介して独立して実行されます。VS Codeの統合されたチャット ビューから、すべてのバックグラウンド エージェント セッションを表示して管理できます。このビューでは、VS Codeから直接新しいバックグラウンド エージェント セッションを作成したり、ローカル エージェントの会話をバックグラウンド エージェントに引き継いだりすることもできます。

バックグラウンド エージェントはユーザー操作なしでバックグラウンド実行されるため、スコープが明確で必要なコンテキストがそろっているタスクに適しています。たとえば、計画に基づく機能の実装、概念実証の複数バリエーションの作成、明確に定義された修正や機能の実装などがあります。

バックグラウンド エージェントは、コードベースへの変更を自律的に適用します。エディターでの進行中の作業への干渉を防ぐため、バックグラウンド エージェントはGit worktreeを使用して[分離された環境](#create-an-isolated-background-agent-session-experimental)で実行でき、メイン ワークスペースに影響を与えずに変更を行えます。worktreeの分離でバックグラウンド エージェント セッションを開始すると、VS Codeはそのセッション用に別のフォルダーを自動的に作成します。メイン ワークスペースでバックグラウンド エージェントを実行することもできますが、競合が発生する可能性があります。

バックグラウンド エージェントはCLI経由で実行され、VS Codeの組み込みツールや実行時コンテキスト(失敗したテストやテキスト選択など)に直接アクセスできません。また、MCPサーバーや拡張機能が提供するツールにもアクセスできません。CLIツール経由で利用可能なモデルに限定されます。バックグラウンド エージェントはターミナル コマンドを実行でき、必要に応じて承認を求めることがあります。

バックグラウンド エージェントにタスクを割り当てるには、チャット ビューから直接新しいバックグラウンド セッションを作成する、エージェント専用のCLIを使用する、またはVS Codeのローカル チャット会話をバックグラウンド エージェント セッションとして引き継ぐ方法があります。

### Copilot CLI

**Copilot CLI**は、VS Codeの主要なバックグラウンド エージェントです。ターミナルからCopilot CLIを直接使用するか、VS Codeからセッションを開始および管理できます。

開始するには、Copilot CLIをインストールしてセットアップしてください。VS Codeがこれを処理するはずですが、次のコマンドでCLIを手動でインストールすることもできます。

```bash
npm install -g @github/copilot
```

Learn more about [Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli) in the GitHub documentation.

### OpenAI Codex

**OpenAI Codex**バックグラウンド エージェントはOpenAIのCodexを使用して、自律的にコーディング タスクを実行します。OpenAI Codexエージェントを使用するには、Visual Studio Marketplaceから[OpenAI Codex](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt)拡張機能をインストールしてください。

VS CodeのOpenAI Codexでは、Copilot Pro+サブスクリプションを使用して認証し、追加のセットアップなしでCodexにアクセスできます。[GitHub Copilotの請求とプレミアム リクエスト](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)の詳細はGitHubドキュメントを参照してください。

## バックグラウンド エージェント セッションを表示して管理する

VS Codeのチャット ビューから、すべてのバックグラウンド エージェント セッションを表示して管理できます。フィルター オプションから**バックグラウンド エージェント**を選択すると、セッション一覧をバックグラウンド エージェント セッションのみに絞り込めます。

![VS Codeのチャット ビューにあるバックグラウンド エージェント フィルターのスクリーンショット。](../images/background-agents/background-agent-filter.png)

一覧からバックグラウンド エージェント セッションを選択すると、チャット ビューでセッションの詳細が開きます。エディター タブ(チャット エディター)でセッションを表示したい場合は、セッションを右クリックして**エディターとして開く**を選択します。

VS Code内のチャット会話ではなくターミナルでバックグラウンド セッションを表示したい場合は、チャット ビューでセッションを右クリックし、**ターミナルでエージェント セッションを再開**を選択します。VS CodeでCopilot CLIを直接操作できます。

![VS Code内でCopilot CLIセッションを表示しているスクリーンショット。](../images/background-agents/copilot-cli-in-terminal.png)

## バックグラウンド エージェント セッションを開始する

ワークフローに応じて、いくつかの方法でバックグラウンド エージェント セッションを開始できます。CLIを使用して新しいセッションを作成し、タスクの詳細を直接指定することも、VS Codeの[チャット ビュー](/docs/copilot/agents/overview.md#manage-agent-sessions)から新しいセッションを開始することもできます。

別の方法として(特に複雑なタスクの場合)、まずVS Codeのチャットでローカル エージェントとやり取りし、スコープと詳細が明確になったらタスクをバックグラウンド エージェント セッションに引き継ぐことができます。たとえば、[Plan agent](/docs/copilot/chat/chat-planning.md)を使用して複数ステップの機能実装を概略化し、その後の実際のコーディングをバックグラウンド エージェントに委任できます。

### Create a Copilot CLI background agent session

VS Codeでは、いくつかの方法で新しいCopilot CLIバックグラウンド エージェント セッションを作成できます。

* チャット ビューから:

    1. チャット ビューを開く(`kb(workbench.action.chat.open)`)

    1. **新しいチャット**のドロップダウン > **新しいバックグラウンド エージェント**を選択する

* ローカル チャット セッション中:

    * チャット入力に`@cli <task description>`と入力してメッセージを送信する

    * プロンプトを入力し、**続行先** > **バックグラウンド エージェント**を選択する

* コマンド パレット(`kb(workbench.action.showCommands)`)から**Chat: 新しいバックグラウンド エージェント**コマンドを実行する

新しいバックグラウンド エージェント セッションが開き、追加のタスク詳細を指定したり、Copilot CLIセッションの進行状況を追跡したりできます。

> [!TIP]
> ターミナルでGitHub Copilot CLIを使用してセッションを開始すると、VS Codeのチャット ビューがこのバックグラウンド セッションを自動的に検出して表示します。VS Code内からこのバックグラウンド セッションをさらに操作できます。

### Create an OpenAI Codex background agent session

チャット ビューから新しいOpenAI Codexバックグラウンド エージェント セッションを作成するには:

* チャット ビューから:

    1. チャット ビューを開く(`kb(workbench.action.chat.open)`)

    1. **新しいチャット**のドロップダウン > **新しいCodex エージェント**を選択する

* コマンド パレット(`kb(workbench.action.showCommands)`)から**Codex: 新しいCodex エージェント**コマンドを実行する

新しいCodexバックグラウンド エージェント セッションが開き、追加のタスク詳細を指定したり、Codexセッションの進行状況を追跡したりできます。

### Hand off an agent session to a background agent

複雑なタスクの場合、まずVS Codeのチャットでローカル エージェントとやり取りして要件を明確にし、その後、自律実行のためにタスクをバックグラウンド エージェントに引き継ぐと便利です。ローカル エージェントの会話をバックグラウンド エージェント セッションに引き継ぐと、会話履歴とコンテキストの全体がバックグラウンド エージェントに渡されます。

ローカル エージェント セッションをバックグラウンド エージェント セッションで続行するには:

1. チャット ビューを開く(`kb(workbench.action.chat.open)`)

1. タスクをバックグラウンド エージェントに引き継ぐ準備ができるまで、ローカル エージェントとやり取りする

1. バックグラウンド エージェントに引き継ぐには、次のオプションがあります。

    * **続行先**を選択し、**バックグラウンド**を選択する

        ![VS Codeのチャット インターフェイスにある「Continue in Chat」ボタンを示すスクリーンショット。](../images/background-agents/continue-in-chat-background.png)

    * [Plan agent](/docs/copilot/chat/chat-planning.md)を使用している場合は、**Start Implementation**のドロップダウンを選択し、**Continue in Background**を選択して、バックグラウンド エージェント セッションで実装を実行する

        ![VS Codeのチャット インターフェイスにある「Start Implementation」ボタンを示すスクリーンショット。](../images/background-agents/plan-agent-start-implementation-background.png)

    * チャット入力で`@cli`と入力し、タスクをバックグラウンド エージェントに引き継ぐ

バックグラウンド エージェント セッションは自動的に開始され、会話履歴とコンテキストの全体が引き継がれます。チャット ビューでバックグラウンド エージェントの進行状況を監視できます。

## 分離されたバックグラウンド エージェント セッションを作成する(試験段階)

バックグラウンド エージェントによる変更をメイン ワークスペースから分離するために、[Git worktree](/docs/sourcecontrol/branches-worktrees.md#understanding-worktrees)を使用するバックグラウンド エージェント セッションを作成できます。worktreeを作成すると、VS Codeはそのセッション用に別のフォルダーを作成します。バックグラウンド エージェントはこの分離フォルダー内で動作し、進行中の作業との競合を防ぎます。

バックグラウンド エージェント セッションでGit worktreeを使用するには:

1. VS Codeで新しいCopilot CLIバックグラウンド エージェント セッションを開始します。

1. チャット入力ボックスで、分離モードとして**Worktree**を選択します。

    ![VS Codeのチャット インターフェイスで「Worktree」分離モード オプションを表示しているスクリーンショット。](../images/background-agents/isolated-run-mode.png)

    **Workspace**を選択すると、バックグラウンド エージェントはメイン ワークスペースに直接変更を適用します。

1. プロンプトを入力してエージェント セッションを開始します。VS Codeは新しいGit worktreeを自動的に作成します。

    バックグラウンド エージェントが行ったすべての変更はworktreeフォルダーに適用され、メイン ワークスペースから分離されます。

1. ソース管理ビューの**リポジトリ**ビューで、Git worktreeを確認できます。

    ![VS Codeのソース管理ビューでGit worktreeを表示しているスクリーンショット。](../images/background-agents/git-worktree-source-control.png)

    エージェント ビューにも、バックグラウンド エージェント セッションのworktreeパスが表示されます。

1. エージェント ビューでバックグラウンド エージェントの進行状況を監視します。

1. バックグラウンド エージェントがタスクを完了したら、worktreeの変更をレビューし、メイン ワークスペースにマージできます。

    バックグラウンド セッション出力の下部には、このバックグラウンド エージェント セッションで変更されたファイルの概要が表示され、その後にこのworktreeの未処理の変更(バックグラウンド エージェントによるもの、またはworktreeに対する自分の編集によるもの)がすべて続きます。

    ![worktreeの変更を保持できることを示すスクリーンショット。](../images/background-agents/filechanges.png)

    次の操作を選択できます。
    * 個々のファイル名をクリックするか、`View All Edits`の差分ボタンを使用して、ファイルの変更を確認する
    * `Keep`ボタンを使用してエージェント セッションの保留中の変更を保持する、または`Undo`でそれらを削除する
    * `Apply`ボタンを使用して、worktree上で保持されたすべての変更をローカル リポジトリに適用する

[VS Codeのソース管理でGit worktreeを使用する](/docs/sourcecontrol/branches-worktrees.md)方法の詳細を参照してください。

## バックグラウンド エージェントでカスタム エージェントを使用する(試験段階)

[カスタム エージェント](/docs/copilot/customization/custom-agents.md)を使用すると、VS Codeのエージェント向けにカスタムのペルソナとロールを定義できます。たとえば、コード レビューを行うカスタム エージェントを作成できます。カスタム エージェントでは、特定の指示と動作を定義できます。

バックグラウンド エージェント セッションを作成するとき、タスクを処理するカスタム エージェントを選択できます。バックグラウンド エージェントは、カスタム エージェントで定義された動作に従って動作します。

バックグラウンド エージェントでカスタム エージェントを有効にするには:

1. `setting(github.copilot.chat.cli.customAgents.enabled)`設定で、バックグラウンド エージェントのカスタム エージェントを有効にします。

1. コマンド パレット(`kb(workbench.action.showCommands)`)から**Chat: 新しいカスタム エージェント**コマンドを実行して、ワークスペースにカスタム エージェントを作成します。

    > [!NOTE]
    > 現在、ワークスペースで定義されたカスタム エージェントのみがバックグラウンド エージェント セッションで利用できます。[カスタム エージェントの作成](/docs/copilot/customization/custom-agents.md#create-a-custom-agent)の詳細を参照してください。

1. 新しいバックグラウンド エージェント セッションを作成し、エージェントのドロップダウンからカスタム エージェントを選択します。

    ![VS Codeのチャット インターフェイスでカスタム エージェントの選択を表示しているスクリーンショット。](../images/background-agents/custom-agent-selection.png)

1. プロンプトを入力し、タスクの処理にカスタム エージェントが使用されていることを確認します。

## 関連リソース

* [エージェントの概要](/docs/copilot/agents/overview.md): さまざまなエージェントの種類と、エージェント間でタスクを引き継ぐ方法を理解する
* [クラウド エージェント](/docs/copilot/agents/cloud-agents.md): GitHub統合が必要なタスク向けのクラウド エージェントについて学ぶ
* [カスタム エージェント](/docs/copilot/customization/custom-agents.md): カスタム エージェントのロールとペルソナを作成する
* [GitHub Copilot CLIドキュメント](https://cli.github.com/manual/gh_copilot)
