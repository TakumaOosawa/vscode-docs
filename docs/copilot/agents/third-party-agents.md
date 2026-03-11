---
ContentId: 8b3c4d5e-6f7a-8b9c-0d1e-2f3a4b5c6d7e
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでClaude AgentやOpenAI Codexなどのサードパーティエージェントを使用して、GitHub Copilot購読で自律的なコーディングタスクを実行する方法を学習します。
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

Visual Studio Codeのサードパーティエージェントは、AnthropicやOpenAIなどの外部プロバイダーが開発したAIエージェントです。サードパーティエージェントにより、これらのAIプロバイダーの独自機能を使用しながら、VS Codeの統一されたエージェントセッション管理と、コーディング、デバッグ、テストなどの充実したエディター体験の恩恵を受けることができます。さらに、既存のGitHub Copilot購読でこれらのプロバイダーを使用できます。

VS Codeはプロバイダーの SDK とエージェントハーネスを使用して、エージェントの独自機能にアクセスします。VS Codeではローカルおよびクラウドベースの両方のサードパーティエージェントを使用できます。クラウドベースのサードパーティエージェントとの統合は、GitHub Copilot プランを通じてが有効になります。

> [!NOTE]
> クラウド内のサードパーティコーディングエージェントは現在プレビュー段階です。

## サードパーティエージェントを使用する理由

VS Codeでサードパーティエージェントを使用する利点は次のとおりです。

* **独自機能の使用**: 各サードパーティエージェントには独自の強みと特殊機能があります。VS Codeはプロバイダーの SDK とエージェントハーネスを使用してこれらの機能にアクセスし、コーディングタスクに最適なエージェントを選択できます。
* **統一された体験**: サードパーティエージェントを含むすべてのエージェントセッションを、同じVS Code エージェント体験から管理します。
* **充実したエディター統合**: VS Codeのコーディング機能（リッチデバッグやテストなど）をエージェント機能と組み合わせて使用します。
* **課金**: 追加のセットアップなしに、既存のGitHub Copilot購読を通じて認証と課金を管理します。

## サードパーティクラウドエージェントを有効にする

VS Codeで使用する前に、Copilotアカウント設定でクラウド内のサードパーティエージェントサポートを有効にする必要があります。GitHub ドキュメントの[リポジトリでのサードパーティコーディングエージェントの有効化または無効化](https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies#enabling-or-disabling-third-party-coding-agents-in-your-repositories)の手順に従ってください。

VS Codeでクラウドエージェントを使用するために、プロバイダーのVS Code拡張機能をインストールする必要はありません。

## Claude Agent（プレビュー）

Claude エージェントセッションは、Anthropic の Claude Agent SDK によって直接VS Code にもたらされる自律的コーディング機能を提供します。Claude エージェントは、独自のツールと機能のセットを使用して、ワークスペース上で自律的に計画、実行、コーディングタスクの反復処理を行います。

`setting(github.copilot.chat.claudeAgent.enabled)` 設定で Claude エージェントセッションのサポートを有効または無効にします。

### Claude エージェントセッションを開始する

新しいClaude エージェントセッションを開始するには、以下の操作を行います。

1. Chat ビュー（`kb(workbench.action.chat.open)`）を開き、**新規チャット**（`+`）を選択します。

1. ローカルまたはクラウドエージェントセッションの間で選択します。

    * ローカルセッションの場合、**セッションタイプ**ドロップダウンから**Claude**を選択します。

        ![セッションタイプドロップダウンにClaude エージェントオプションが選択されている状態のスクリーンショット。](../images/third-party-agents/claude-agent-new-chat.png)

    * クラウドセッションの場合、**セッションタイプ**ドロップダウンから**クラウド**を選択します。次に、**パートナーエージェント**ドロップダウンから**Claude**を選択します。

        ![チャット入力でクラウドエージェントパートナー選択ピッカーを示すスクリーンショット。](../images/third-party-agents/partner-agent-cloud-chat.png)

1. プロンプトを入力し、エージェントにタスクを実行させます。

    Claude エージェントは、使用するツールを自律的に決定し、ワークスペースに変更を加えます。

### Claude エージェントスラッシュコマンド

Claude エージェントは、高度なワークフロー用の特殊なスラッシュコマンドを提供します。チャット入力ボックスで`/`を入力して、利用可能なコマンドを確認します。

| スラッシュコマンド | 説明 |
|---------------|-------------|
| `/agents` | 特定のタスク用の専門的なClaude エージェントを作成および管理します。ウィザードを通じてカスタムエージェント動作を定義します。[Claude sub-agents](https://code.claude.com/docs/en/sub-agents)について詳しく学びます。 |
| `/hooks` | Claude エージェントセッション中の主要な時点（ツール実行の前後など）で実行されるライフサイクルフックを設定します。[Claude hooks](https://code.claude.com/docs/en/hooks)について詳しく学びます。 |
| `/memory` | Claude エージェントセッション全体で永続的なコンテキストを提供する`CLAUDE.md`メモリファイルを開いて編集します。 |
| `/init` | プロジェクト用の新しい`CLAUDE.md`メモリファイルを初期化します。 |
| `/pr-comments` | プルリクエストからコメントを取得します。 |
| `/review` | プルリクエストのコード変更を確認します。 |
| `/security-review` | 現在のブランチの保留中コード変更のセキュリティレビューを実行します。 |

### 権限モード

Claude エージェントは、特定の操作を実行する前に権限をリクエストします。デフォルトでは、ワークスペース内のファイル編集は自動承認されますが、ターミナルコマンドの実行などの他の操作には確認が必要な場合があります。

エージェントがワークスペースに変更を適用する方法を選択できます。

* **自動的に編集**: Claude エージェントがタスクに取り組む際、ワークスペースに変更を自律的に加えます。
* **承認をリクエスト**: Claude エージェントがワークスペースに変更を加える前に、レビュー対象になります。
* **計画**: Claude エージェントがタスクの作業を開始する前に、意図したアプローチの概要を示します。

![Claude エージェント権限モードオプションを示すスクリーンショット。](../images/third-party-agents/claude-agent-permission-modes.png)

> [!CAUTION]
> `setting(github.copilot.chat.claudeAgent.allowDangerouslySkipPermissions)`設定はすべての権限チェックをバイパスします。インターネットアクセスのない隔離されたサンドボックス環境でのみこれを有効にしてください。

## OpenAI Codex

OpenAI Codex エージェントは、OpenAI の Codex を使用してコーディングタスクを自律的に実行します。Codex は VS Code で対話的に実行することも、バックグラウンドで無人実行することもできます。

OpenAI Codex エージェントを無効にするには、VS Code で[OpenAI Codex](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt)拡張機能を無効にするかアンインストールします。

### 前提条件

* 認証用の Copilot Pro+ 購読
* ローカルセッションの場合、[OpenAI Codex](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt)拡張機能

VS Code の OpenAI Codex では、Copilot Pro+ 購読を使用して、追加のセットアップなしで Codex に認証してアクセスできます。GitHub ドキュメントの[GitHub Copilot の課金と premium リクエスト](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)について詳しく知ります。

### Codex セッションを開始する

新しい OpenAI Codex エージェントセッションを開始するには、以下の操作を行います。

1. Chat ビュー（`kb(workbench.action.chat.open)`）を開き、**新規チャット**（`+`）を選択します。

1. ローカルまたはクラウドエージェントセッションの間で選択します。

    * ローカルセッションの場合、**セッションタイプ**ドロップダウンから**Codex**を選択します。

        ![セッションタイプドロップダウンに Codex エージェントオプションが選択されている状態のスクリーンショット。](../images/third-party-agents/codex-agent-new-chat.png)

    * クラウドセッションの場合、**セッションタイプ**ドロップダウンから**クラウド**を選択します。次に、**パートナーエージェント**ドロップダウンから**Codex**を選択します。

        ![チャット入力でクラウドエージェントパートナー選択ピッカーを示すスクリーンショット。](../images/third-party-agents/partner-agent-cloud-chat.png)

1. チャットエディター入力にプロンプトを入力し、エージェントにタスクを実行させます。

## よくある質問

<details>
<summary>既存の Copilot 購読でサードパーティエージェントを使用できますか?</summary>

はい、VS Code のサードパーティエージェントは、既存のGitHub Copilot 購読を通じて認証と課金を管理します。クラウドベースのサードパーティエージェントの場合、エージェントを有効にする手順に従ってください。

クラウドベースのサードパーティエージェントの場合、Copilot 購読プランに基づいて可用性が制限される場合があります。GitHub ドキュメントの[サードパーティエージェントについて](https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents)で詳しく確認してください。

</details>

<details>
<summary>サードパーティエージェントとプロバイダーの VS Code 拡張機能の使用に違いはありますか?</summary>

プロバイダーの VS Code 拡張機能と VS Code のサードパーティエージェント統合の両方により、プロバイダーのAI機能とエージェントハーネスを使用できます。違いは課金です。VS Code でサードパーティエージェントを使用する場合、GitHub は Copilot 購読を通じて課金します。プロバイダーの拡張機能を使用する場合は、プロバイダーの購読を通じて課金されます。

</details>

<details>
<summary>なぜ 2 つのClaude/Codex エージェントがあるのですか?</summary>

VS Code では、プロバイダーの可用性に応じて、ローカルまたはクラウドベースのサードパーティエージェントのいずれかを選択できます。**セッションタイプ**ドロップダウンからサードパーティエージェントを選択すると、そのプロバイダーのローカルエージェントセッションが作成されます。

クラウドベースのサードパーティエージェントを選択するには、まず**セッションタイプ**ドロップダウンから**クラウド**オプションを選択し、次に**パートナーエージェント**ドロップダウンからプロバイダーを選択します。

</details>

## 関連するリソース

* [エージェント概要](/docs/copilot/agents/overview.md): さまざまなエージェントタイプを理解し、エージェント間でのタスクのハンドオフ方法を学びます。
* [サードパーティエージェントについて](https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents): GitHub ドキュメントでサードパーティエージェントについて詳しく知ります。

