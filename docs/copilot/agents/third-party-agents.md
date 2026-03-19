---
ContentId: 8b3c4d5e-6f7a-8b9c-0d1e-2f3a4b5c6d7e
DateApproved: 3/9/2026
MetaDescription: Visual Studio Codeで、GitHub CopilotサブスクリプションでサポートされているClaude AgentやOpenAI Codexなどのサードパーティエージェントを使用して、自動コーディングタスクを実行する方法を学習します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- agents
- third-party agent
- claude
- codex
- anthropic
- openai
- copilot
---

# Visual Studio Codeのサードパーティエージェント

Visual Studio Codeのサードパーティエージェントは、AnthropicやOpenAIなどの外部プロバイダーによって開発されたAIエージェントです。サードパーティエージェントを使用すると、これらのAIプロバイダーのユニークな機能を活用しながら、VS Codeの統一されたエージェントセッション管理とコーディング、デバッグ、テストなどの充実したエディタ体験を得ることができます。さらに、既存のGitHub Copilotサブスクリプションでこれらのプロバイダーを利用できます。

VS CodeはプロバイダーのSDKとエージェントハーネスを使用して、エージェントのユニークな機能にアクセスします。VS Codeではローカルとクラウドベースの両方のサードパーティエージェントを使用できます。クラウドベースのサードパーティエージェントとの統合は、GitHub Copilotプランを通じて有効になります。

> [!NOTE]
> クラウド内のサードパーティコーディングエージェントは現在プレビュー段階です。

## サードパーティエージェントを使用する理由

VS Codeでサードパーティエージェントを使用する利点は以下の通りです:

* **ユニークな機能を使用**: 各サードパーティエージェントは独自の強みと特化した機能を持っています。VS CodeはプロバイダーのSDKとエージェントハーネスを使用してこれらの機能にアクセスしており、コーディングタスクに最適なエージェントを選択できます。
* **統一された体験**: サードパーティエージェントを含むすべてのエージェントセッションを、同じVS Codeエージェント体験から管理できます。
* **充実したエディタ統合**: 豊富なデバッグやテストなどのVS Codeのコーディング機能を、エージェントの機能と組み合わせて使用できます。
* **請求**: 既存のGitHub Copilotサブスクリプションを通じて認証と請求を管理できるため、追加のセットアップは不要です。

## サードパーティクラウドエージェントを有効にする

VS Codeでサードパーティエージェントを使用する前に、Copilotアカウント設定でクラウド内のサードパーティエージェントのサポートを有効にする必要があります。GitHubドキュメントの[リポジトリでのサードパーティコーディングエージェントの有効化または無効化](https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies#enabling-or-disabling-third-party-coding-agents-in-your-repositories)の手順に従ってください。

VS Codeでプロバイダーのクラウドエージェントを使用するために、プロバイダーのVS Code拡張機能をインストールする必要はありません。

## Claude Agent(プレビュー)

Claude Agentセッションは、Anthropic Claude Agent SDKで実現されたエージェント的なコーディング機能を直接VS Codeで提供します。Claude Agentはワークスペースをしっかりと操作して、独自のツールと機能を使用してコーディングタスクを計画、実行、反復処理します。

`setting(github.copilot.chat.claudeAgent.enabled)`設定でClaude Agentセッションのサポートを有効または無効にします。

### Claude Agentセッションを開始する

新しいClaude Agentセッションを開始するには以下の手順に従います:

1. チャットビュー(`kb(workbench.action.chat.open)`)を開いて、**新しいチャット**(`+`)を選択します。

1. ローカルまたはクラウドエージェントセッションを選択します:

    * ローカルセッションの場合は、**セッションタイプ**ドロップダウンから**Claude**を選択します

        ![Claude Agentオプションが選択されたセッションタイプドロップダウンを示すスクリーンショット。](../images/third-party-agents/claude-agent-new-chat.png)

    * クラウドセッションの場合は、**セッションタイプ**ドロップダウンから**クラウド**を選択します。その後、**パートナーエージェント**ドロップダウンから**Claude**を選択します。

        ![チャット入力のクラウドエージェントパートナー選択ピッカーを示すスクリーンショット。](../images/third-party-agents/partner-agent-cloud-chat.png)

1. プロンプトを入力して、エージェントがタスクを処理するのを待ちます

    Claude Agentは自動的に使用するツールを決定し、ワークスペースに変更を加えます。

### Claude Agentスラッシュコマンド

Claude Agentは高度なワークフローのための特別なスラッシュコマンドを提供します。チャット入力ボックスで`/`を入力して、利用可能なコマンドを確認します。

| スラッシュコマンド | 説明 |
|---------------|-------------|
| `/agents` | 特定のタスク用の特化したClaude Agentを作成・管理します。ウィザード通じてカスタムエージェント動作を定義します。[Claude sub-agents](https://code.claude.com/docs/en/sub-agents)の詳細をご覧ください。 |
| `/hooks` | ツール実行の前後など、Claude Agentセッション中の重要なポイントで実行されるライフサイクルフックを設定します。[Claude hooks](https://code.claude.com/docs/en/hooks)の詳細をご覧ください。 |
| `/memory` | Claude AgentがセッションをまたいでCLAUDE.mdメモリファイルを開いて編集し、永続的なコンテキストを提供します。 |
| `/init` | プロジェクト用の新しいCLAUDE.mdメモリファイルを初期化します。 |
| `/pr-comments` | プルリクエストからコメントを取得します。 |
| `/review` | プルリクエストのコード変更をレビューします。 |
| `/security-review` | 現在のブランチの保留中コード変更のセキュリティレビューを実行します。 |

### 権限モード

Claude Agentは特定の操作を実行する前に権限をリクエストします。デフォルトでは、ワークスペース内のファイル編集は自動承認され、ターミナルコマンド実行などの他の操作には確認が必要な場合があります。

エージェントがワークスペースに変更を適用する方法を選択できます:

* **自動編集**: Claude Agentはタスクに取り組むときにワークスペースを自動的に変更します。
* **承認をリクエスト**: Claude Agentはワークスペースに変更を加える前にレビューを求めます。
* **計画**: Claude Agentはタスクの作業を開始する前に意図したアプローチの概要を説明します。

![Claude Agent権限モードオプションを示すスクリーンショット。](../images/third-party-agents/claude-agent-permission-modes.png)

> [!CAUTION]
> `setting(github.copilot.chat.claudeAgent.allowDangerouslySkipPermissions)`設定はすべての権限チェックをバイパスします。インターネットアクセスのない分離されたサンドボックス環境においてのみこの設定を有効にしてください。

## OpenAI Codex

OpenAI Codexエージェントは、OpenAIのCodexを使用してコーディングタスクを自動的に実行します。Codexはそれぞれの実行がVS Codeで対話的に、またはバックグラウンドで無人で実行できます。

OpenAI Codexエージェントを無効にするには、VS Codeで[OpenAI Codex](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt)拡張機能を無効化またはアンインストールします。

### 前提条件

* 認証用のCopilot Pro+サブスクリプション
* ローカルセッションの場合は、[OpenAI Codex](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt)拡張機能

VS CodeのOpenAI Codexによって、Copilot Pro+サブスクリプションを使用して認証し、追加のセットアップなくCodexにアクセスできます。GitHubドキュメントの[GitHub Copilot請求と高度なリクエスト](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)をご覧ください。

### Codexセッションを開始する

新しいOpenAI Codexエージェントセッションを開始するには以下の手順に従います:

1. チャットビュー(`kb(workbench.action.chat.open)`)を開いて、**新しいチャット**(`+`)を選択します。

1. ローカルまたはクラウドエージェントセッションを選択します:

    * ローカルセッションの場合は、**セッションタイプ**ドロップダウンから**Codex**を選択します

        ![Codexエージェントオプションが選択されたセッションタイプドロップダウンを示すスクリーンショット。](../images/third-party-agents/codex-agent-new-chat.png)

    * クラウドセッションの場合は、**セッションタイプ**ドロップダウンから**クラウド**を選択します。その後、**パートナーエージェント**ドロップダウンから**Codex**を選択します。

        ![チャット入力のクラウドエージェントパートナー選択ピッカーを示すスクリーンショット。](../images/third-party-agents/partner-agent-cloud-chat.png)

1. チャットエディタ入力にプロンプトを入力して、エージェントがタスクを処理するのを待ちます

## よくある質問

<details>
<summary>既存のCopilotサブスクリプションでサードパーティエージェントを使用できますか?</summary>

はい、VS CodeのサードパーティエージェントはGitHub Copilotサブスクリプション経由で認証と請求を管理します。クラウドベースのサードパーティエージェントの場合は、エージェントを有効にするための手順に従ってください。

クラウドベースのサードパーティエージェントの場合、利用可能性はCopilotサブスクリプションプランに基づいて制限される場合があります。詳細についてはGitHubドキュメントの[サードパーティエージェントについて](https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents)をご覧ください。

</details>

<details>
<summary>サードパーティエージェントはプロバイダーのVS Code拡張機能の使用とどのように異なりますか?</summary>

プロバイダーのVS Code拡張機能とVS Codeのサードパーティエージェント統合の両方により、プロバイダーのAI機能とエージェントハーネスを使用できます。違いは請求にあります。VS Codeのサードパーティエージェントをしたがああらった場合は、GitHubはCopilotサブスクリプション経由で請求します。プロバイダーの拡張機能を使用する場合は、プロバイダーのサブスクリプション経由で請求されます。

</details>

<details>
<summary>Claude/Codexエージェントが2つあるのはなぜですか?</summary>

VS Codeではプロバイダーの利用可能性に応じて、ローカルまたはクラウドベースのサードパーティエージェントから選択できます。**セッションタイプ**ドロップダウンからサードパーティエージェントを選択する場合、そのプロバイダーのローカルエージェントセッションが作成されます。

クラウドベースのサードパーティエージェントを選択するには、まず**セッションタイプ**ドロップダウンから**クラウド**オプションを選択し、次に**パートナーエージェント**ドロップダウンからプロバイダーを選択します。

</details>

## 関連リソース

* [エージェントの概要](/docs/copilot/agents/overview.md): 異なるエージェント類型とエージェント間のタスク移行方法を理解する
* [サードパーティエージェントについて](https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents): GitHubドキュメントでサードパーティエージェントの詳細を確認する

