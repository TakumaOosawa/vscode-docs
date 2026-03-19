---
ContentId: 0aefcb70-7884-487f-953e-46c3e07f7cbe
DateApproved: 3/9/2026
MetaDescription: VS CodeのAIエージェントを使用して、プロジェクト全体でコードを自律的に計画、実装、テストします。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords:
- GitHub Copilot
- AI
- agents
- autonomous
- agentic
- multi-file editing
- architecture
- refactoring
- deep context
- semantic search
- codebase understanding
- enterprise
- large codebase
- inline suggestions
- chat
- MCP
- team
- background agents
- third-party agents
- introduction
- overview
- getting started
---
# VS CodeのGitHub Copilot

GitHub Copilotは、Visual Studio Codeで、AI搭載のエージェントとコーディングツールを提供します。コードベースの深い意味理解により、プロジェクト全体でコードの変更を計画、実装、検証する自律的なエージェントを使用します。複数のエージェントセッションをローカルで、バックグラウンドで、またはクラウドで並行実行できます。Copilot、ClaudeやCodexなどのサードパーティエージェント、またはカスタムエージェントから選択します。すべてを一元ビューから管理できます。インライン候補、インラインチャット、スマートアクションが、コーディングワークフロー全体の各段階でサポートします。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIを使い始める">
VS CodeでAIを使用して最初のアプリを構築するための実践的なチュートリアルに従います。

* [チュートリアルを始める](/docs/copilot/getting-started.md)

</div>

## エージェントとエージェントセッション

エージェントは、エンドツーエンドで完全なコーディングタスクを処理します。エージェントに高度なタスクを与えると、作業をステップに分割し、ファイルを編集し、ターミナルコマンドを実行し、ツールを呼び出し、エラーやテスト失敗が発生した場合は自己修正します。各タスクは**エージェントセッション**内で実行されます。これは追跡、一時停止、再開、または別のエージェントに引き継ぐことができる永続的な会話です。

<video src="images/overview/agents-intro.mp4" title="VS Codeで完全な機能を構築するエージェントセッションを示すビデオ。" loop controls muted></video>

> [!IMPORTANT]
> 組織がVS CodeでエージェントをDisabledにしている可能性があります。この機能を有効にするには、管理者に問い合わせてください。

### 一元ビューからセッションを管理する

複数のエージェントセッションを並行実行し、各セッションは異なるタスクに重点を置きます。**Chat**パネルの**Sessions**ビューでは、ローカルで実行されるもの、バックグラウンドで実行されるもの、またはクラウドで実行されるものなど、すべてのアクティブセッションを監視できるシングルプレイスが提供されます。各セッションの状態を確認し、セッション間を切り替え、ファイルの変更を確認し、中断したところから再開できます。

<video src="images/overview/agent-sessions-demo.mp4" title="エージェントセッションリストを示すビデオ(フィルタリング、表示、アーカイブ可能)。" loop controls muted></video>

[エージェントセッションの管理](/docs/copilot/chat/chat-sessions.md)についてさらに詳しく知ってください。

### エージェントは任意の場所で実行できます

エージェントは、対話的な作業用にVS Codeでローカルで実行でき、自律的なタスク用にマシンのバックグラウンドで実行でき、またはプルリクエストを介したチームコラボレーションのためにクラウドで実行できます。AnthropicやOpenAIなどの提供者からのサードパーティエージェントも使用できます。任意の時点で、1つのエージェントタイプから別のエージェントタイプにタスクを引き継ぐことができ、完全な会話履歴が引き継がれます。

![Chatビューのセッションタイプピッカーを示すスクリーンショット(ローカル、バックグラウンド、クラウド、サードパーティエージェントのオプション付き)。](images/agents-overview/sessions-type-picker.png)

[エージェントタイプと委譲](/docs/copilot/agents/overview.md)についてさらに詳しく知ってください。または[エージェントチュートリアル](/docs/copilot/agents/agents-tutorial.md)に従ってください。

### 構築前に計画する

ビルトイン**Plan**エージェントを使用して、コードを書く前に、タスクを構造化された実装計画に分割します。Planエージェントはコードベースを分析し、明確にする質問をし、ステップバイステップの計画を作成します。計画が正しく見える場合、実装エージェントに引き継いで、ローカルで、バックグラウンドで、またはクラウドで実行します。

<video src="images/overview/plan-intro.mp4" title="Planエージェントがアプリに認証を追加するための構造化実装計画を作成している様子を示すビデオ。" loop controls muted></video>

[エージェントを使用した計画](/docs/copilot/agents/planning.md)についてさらに詳しく知ってください。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントで機能を計画する">
Planエージェントを使用して、新機能の構造化実装計画を作成します。

* [VS Codeで開く](vscode://GitHub.Copilot-Chat/chat?agent=agent%26prompt=%2Fplan%20a%20terminal%20UI%20app%20to%20track%20my%20todo%20list.)

</div>

## できること

* **機能をエンドツーエンドで構築します。** 自然言語で機能を説明すると、エージェントはプロジェクトをスキャフォールドし、複数のファイルのロジックを実装し、テストを実行して結果を検証します。

* **テスト失敗をデバッグして修正します。** エージェントに失敗したテストを指摘すると、エラーを読み取り、コードベース全体の根本原因をトレースし、修正を適用し、修正を確認するためにテストを再度実行します。[AIでのデバッグ](/docs/copilot/guides/debug-with-copilot.md)についてさらに詳しく知ってください。

* **コードベースをリファクタリングまたはマイグレーションします。** エージェントにマイグレーション(例えば、あるフレームワークから別のフレームワークへ)を計画するよう依頼すると、ビルドで検証しながらファイル全体にわたる調整された変更を適用します。

* **Webアプリをテストして操作します。** _(実験的)_ エージェントに[統合ブラウザ](/docs/debugtest/integrated-browser.md)でWebアプリを開き、機能が機能することを確認し、レイアウトの問題をチェック、またはスクリーンショットを撮ることを依頼します。[ブラウザエージェントテストガイド](/docs/copilot/guides/browser-agent-testing-guide.md)に従ってください。

* **プルリクエスト経由でコラボレーションします。** クラウドエージェントにタスクを委譲してブランチを作成し、変更を実装し、チームがレビューするためのプルリクエストを開きます。[クラウドエージェント](/docs/copilot/agents/cloud-agents.md)についてさらに詳しく知ってください。

## 始める

### ステップ1: Copilotをセットアップする

1. ステータスバーのCopilotアイコンにマウスを置き、**Copilotをセットアップ**を選択します。

    ![ステータスバーのCopilotアイコンとCopilotをセットアップオプションを示すスクリーンショット。](images/setup/setup-copilot-status-bar.png)

1. サインイン方法を選択してプロンプトに従います。Copilotサブスクリプションがまだない場合は、[Copilot Freeプラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップされます。

### ステップ2: 最初のエージェントセッションを開始する

1. **Chat**ビューを開きます(`kb(workbench.action.chat.open)`)。

1. 構築したい内容を説明するプロンプトを入力します。例:

    ```prompt-agent
    レシピを共有するための基本的なNode.js Webアプリを作成します。モダンでレスポンシブな外観にしてください。
    ```

1. 生成されたコードを確認します。エージェントは、必要に応じてファイルを作成し、依存関係をインストールし、コマンドを実行します。

1. `/init`を入力して、プロジェクトをAIに対応させるよう設定します。これによって、エージェントがコードベースを理解し、より適切なコードを生成するのに役立つ[カスタム指示](/docs/copilot/customization/custom-instructions.md)が作成されます。

インライン候補、エージェント、インラインチャット、カスタマイズを含む完全な実践的なチュートリアルについては、[VS CodeのGitHub Copilotを始める](/docs/copilot/getting-started.md)を参照してください。

## AIでコーディングするその他の方法

### インライン候補

Copilotは、入力時にコード候補を提供し、単一行の補完から完全な関数実装まで対応します。次編集候補は、現在の編集に基づいて、次の論理的変更を予測します。

<video src="images/inline-suggestions/nes-video.mp4" title="エディター内でゴーストテキストとして表示されるインラインコード候補を示すビデオ。" loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

[VS Codeのインライン候補](/docs/copilot/ai-powered-suggestions.md)についてさらに詳しく知ってください。

### インラインチャット

`kb(inlinechat.start)`を押して、エディター内で直接チャットプロンプトを開きます。変更を説明すると、Copilotはその場で編集を提案するため、コーテキストを切り替えることなくコーディングの流れにとどまります。コンテキストを切り替えることなく、的を絞ったリファクタリング、説明、または迅速な修正に使用します。

[VS Codeのインラインチャット](/docs/copilot/chat/inline-chat.md)についてさらに詳しく知ってください。

### スマートアクション

VS Codeには、一般的なタスク用の事前定義されたAI搭載アクションが含まれています。コミットメッセージの生成、シンボルの名前変更、エラーの修正、プロジェクト全体でのセマンティック検索を実行します。

![VS Codeのスマートアクションメニューを示すスクリーンショット(テスト失敗を修正するオプション付き)。](images/overview/copilot-chat-fix-test-failure.png)

[VS Codeのスマートアクション](/docs/copilot/copilot-smart-actions.md)についてさらに詳しく知ってください。

## ワークフロー用AIをカスタマイズする

エージェントは、プロジェクトの規約を理解し、適切なツールを備え、タスクに適したモデルを使用する場合に最適に機能します。VS Codeは、AIがコードベースに最初からぴったり合うコードを生成するように調整する方法をいくつか提供しているため、生成後に手動で修正する必要がなくなります。

* **[カスタム指示](/docs/copilot/customization/custom-instructions.md)**: プロジェクト全体のコーディング規約を定義して、AIがスタイルに合致するコードを生成するようにします。
* **[エージェントスキル](/docs/copilot/customization/agent-skills.md)**: VS Code、GitHub Copilot CLI、GitHub Copilot Coding Agentで機能する特化した機能をCopilotに教えます。
* **[カスタムエージェント](/docs/copilot/customization/custom-agents.md)**: コードレビューアーやドキュメント作成者など、特定の役割を前提とし、独自のツールと指示を持つエージェントを作成します。
* **[MCPサーバー](/docs/copilot/customization/mcp-servers.md)**: MCPサーバーまたはMarketplaceスのツールでエージェントを拡張します。
* **[フック](/docs/copilot/customization/hooks.md)**: 自動化とポリシー実施のための特定のイベントでカスタムコマンドを実行します。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIをカスタマイズ">
ワークフロー用AIエクスペリエンスをカスタマイズするすべての方法を参照します。

* [カスタマイズ概要を開く](/docs/copilot/customization/overview.md)

</div>

## サポート

GitHub Copilot ChatのサポートはGitHubによって提供され、<https://support.github.com>で達することができます。

Copilotのセキュリティ、プライバシー、コンプライアンス、透透性について詳しく知るには、[GitHub Copilot Trust Center FAQ](https://copilot.github.trust.page/faq)を参照してください。

## 価格

月間制限付きでGitHub Copilotを無料で使用を開始できます。インライン候補とチャットインタラクション。より広範な使用については、さまざまな有料プランから選択できます。

[GitHub Copilot価格の詳細を確認](https://docs.github.com/en/copilot/get-started/plans)

## 次のステップ

* [GitHub Copilotはどのように機能するか](/docs/copilot/concepts/overview.md)
* [エージェントを始める](/docs/copilot/agents/agents-tutorial.md)
* [GitHub Copilotを使用した実践的なクイックスタート](/docs/copilot/getting-started.md)
* [エージェントタイプを知る](/docs/copilot/agents/overview.md)
* [ワークフロー用AIをカスタマイズ](/docs/copilot/customization/overview.md)
* [VS CodeでAIを使用するためのベストプラクティス](/docs/copilot/copilot-tips-and-tricks.md)
* [VS CodeでCopilotをセットアップ](/docs/copilot/setup.md)

