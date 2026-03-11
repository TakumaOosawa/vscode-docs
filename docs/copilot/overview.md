---
ContentId: 0aefcb70-7884-487f-953e-46c3e07f7cbe
DateApproved: 3/9/2026
MetaDescription: VS Codeで自動的に計画、実装、テストを行うAIエージェントを使用します。
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

GitHub Copilotは、Visual Studio CodeでAI搭載エージェントとコーディングツールを提供します。プロジェクト全体で変更を計画、実装、検証する自律型エージェントを使用して、コードベースの深いセマンティック理解を活用します。複数のエージェントセッションをローカル、バックグラウンド、またはクラウド環境で並行実行できます。Copilot、ClaudeやCodexなどのサードパーティエージェント、またはカスタムエージェントから選択できます。それらはすべて一元的なビューから管理できます。インライン提案、インラインチャット、スマートアクションがコーディングワークフロー全体をサポートします。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIを始める">
VS CodeでAIを使用して初めてのアプリを構築するハンズオンチュートリアルに従います。

* [チュートリアルを開始](/docs/copilot/getting-started.md)

</div>

## エージェントとエージェントセッション

エージェントは完全なコーディングタスクをエンドツーエンドで処理します。エージェントに高レベルのタスクを与えると、そのタスクを手順に分割し、ファイルを編集し、ターミナルコマンドを実行し、ツールを呼び出し、エラーまたはテスト失敗に直面したときに自己修正します。各タスクは**エージェントセッション**内で実行され、追跡、一時停止、再開、別のエージェントへの手渡しが可能な永続的な会話です。

<video src="images/overview/agents-intro.mp4" title="VS Codeで完全な機能を構築するエージェントセッションを示すビデオ。" loop controls muted></video>

> [!IMPORTANT]
> 組織がVS CodeのエージェントをDisableにした可能性があります。この機能を有効にするには、管理者に連絡してください。

### 一元的なビューからセッションを管理

複数のエージェントセッションを並行実行し、各セッションは異なるタスクに焦点を当てます。**Chat**パネルの**Sessions**ビューは、ローカル、バックグラウンド、クラウドで実行されているすべてのアクティブセッションを監視する1つの場所を提供します。各セッションのステータスを確認し、セッション間を切り替え、ファイル変更を確認し、中断した場所から再開できます。

<video src="images/overview/agent-sessions-demo.mp4" title="エージェントセッションリスト、フィルタリング、表示、アーカイブのデモンストレーションを示すビデオ。" loop controls muted></video>

[エージェントセッションの管理](/docs/copilot/chat/chat-sessions.md)について詳しく学びます。

### どこでもエージェントを実行

エージェントはインタラクティブな作業のためにVS Codeでローカルに実行でき、自律的なタスクのためにマシンのバックグラウンドで実行でき、プルリクエストを経由したチームコラボレーションのためにクラウドで実行できます。AnthropicやOpenAIなどのプロバイダーからサードパーティエージェントを使用することもできます。どの時点でも、あるエージェントタイプから別のエージェントタイプにタスクをハンドオフでき、完全な会話履歴が引き継がれます。

![Chat表示のセッションタイプピッカーを示すスクリーンショット、ローカル、バックグラウンド、クラウド、サードパーティエージェントのオプション。](images/agents-overview/sessions-type-picker.png)

[エージェントタイプと委譲](/docs/copilot/agents/overview.md)について詳しく学ぶか、[エージェントチュートリアル](/docs/copilot/agents/agents-tutorial.md)に従ってください。

### 構築する前に計画

組み込みの**Plan**エージェントを使用して、タスクをコード作成前に構造化された実装計画に分割します。Planエージェントはコードベースを分析し、明確化する質問をし、ステップバイステップの計画を作成します。計画が適切に見えたら、実装エージェントにハンドオフしてローカル、バックグラウンド、またはクラウドで実行します。

<video src="images/overview/plan-intro.mp4" title="Planエージェントがアプリに認証を追加するための構造化された実装計画を作成するビデオ。" loop controls muted></video>

[エージェントでの計画](/docs/copilot/agents/planning.md)について詳しく学びます。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントで機能を計画">
Planエージェントを使用して新機能の構造化された実装計画を作成します。

* [VS Codeで開く](vscode://GitHub.Copilot-Chat/chat?agent=agent%26prompt=%2Fplan%20a%20terminal%20UI%20app%20to%20track%20my%20todo%20list.)

</div>

## どのようなことができるか

* **機能をエンドツーエンドで構築します。** 自然言語で機能を説明すると、エージェントがプロジェクトをスキャフォールドし、複数のファイル間でロジックを実装し、テストを実行して結果を検証します。

* **失敗しているテストをDebugして修正します。** 失敗したテストをエージェントに指してください。エージェントはエラーを読み、コードベース全体の根本原因を追跡し、修正を適用し、テストを再実行して確認します。[AIでのDebug](/docs/copilot/guides/debug-with-copilot.md)について詳しく学びます。

* **コードベースをRefactorまたは移行します。** エージェントに移行を計画するよう指示します。たとえば、あるフレームワークから別のフレームワークへの移行などです。エージェントはファイル全体で調整された変更を適用し、構築を検証します。

* **WebアプリケーションをテストおよびInteractします。** _(実験的)_ エージェントに[統合ブラウザ](/docs/debugtest/integrated-browser.md)でWebアプリを開き、機能の検証、レイアウト問題の確認、またはスクリーンショット撮影を指示します。[ブラウザエージェントテストガイド](/docs/copilot/guides/browser-agent-testing-guide.md)に従ってください。

* **プルリクエストを使用してCollaborateします。** クラウドエージェントにタスクをDelegateして、ブランチを作成し、変更を実装して、チームがレビューするためのプルリクエストを開きます。[クラウドエージェント](/docs/copilot/agents/cloud-agents.md)について詳しく学びます。

## 始めよう

### ステップ1:Copilotをセットアップ

1. ステータスバーのCopilotアイコンにカーソルを合わせて、**Set up Copilot**を選択します。

    ![ステータスバーのCopilotアイコン、Set up Copilotオプションを示すスクリーンショット。](images/setup/setup-copilot-status-bar.png)

1. サインイン方法を選択してプロンプトに従います。Copilot購読がまだない場合、[Copilot Free plan](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップします。

### ステップ2:最初のエージェントセッションを開始

1. **Chat**ビュー(`kb(workbench.action.chat.open)`)を開きます。

1. 構築したい内容を説明するプロンプトを入力します。たとえば:

    ```prompt-agent
    Create a basic Node.js web app for sharing recipes. Make it look modern and responsive.
    ```

1. 生成されたコードを確認します。エージェントはファイルを作成し、依存関係をインストールし、必要に応じてコマンドを実行します。

1. `/init`を入力してAIのプロジェクトを設定します。これにより[カスタム手順](/docs/copilot/customization/custom-instructions.md)が作成され、エージェントがコードベースを理解して、より良いコードを生成するのに役立ちます。

インライン提案、エージェント、インラインチャット、およびカスタマイズをカバーする完全なハンズオンチュートリアルについては、[VS CodeでGitHub Copilot使用開始](/docs/copilot/getting-started.md)を参照してください。

## AIでコーディングするその他の方法

### インライン提案

Copilotは入力時にコード提案を提供し、単一行の補完から完全な関数実装までです。Nextの編集提案は、現在の編集に基づいて次の論理的な変更を予測します。

<video src="images/inline-suggestions/nes-video.mp4" title="エディターにゴーストテキストとして表示されるインラインコード提案を示すビデオ。" loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

[VS Codeのインライン提案](/docs/copilot/ai-powered-suggestions.md)について詳しく学びます。

### インラインチャット

`kb(inlinechat.start)`を押してエディターでチャットプロンプトを直接開きます。変更を説明すると、Copilotがインプレースで編集を提案するため、コーディングフローを保つことができます。Context切り替えなしでターゲットRefactor、説明、またはクイックFixに使用します。

[VS CodeのInline Chat](/docs/copilot/chat/inline-chat.md)について詳しく学びます。

### スマートアクション

VS Codeには、一般的なタスク用の事前定義されたAI搭載アクションが含まれています:commitメッセージの生成、記号の名前変更、エラーの修正、プロジェクト全体のセマンティック検索の実行。

![VS CodeのSmart Actionsメニュー、テスト失敗を修正するオプションを示すスクリーンショット。](images/overview/copilot-chat-fix-test-failure.png)

[VS CodeのSmart Actions](/docs/copilot/copilot-smart-actions.md)について詳しく学びます。

## ワークフロー向けのAIのカスタマイズ

エージェントは、プロジェクトの規約を理解し、適切なツールを持ち、タスクに適した モデルを使用する場合に最適に機能します。VS Codeは、[AIをカスタマイズ](/docs/copilot/customization/overview.md)して、事実上の修正が必要な代わりに、コードベースに適合するコードを最初から生成できるようにするいくつかの方法を提供します。

* **[カスタム手順](/docs/copilot/customization/custom-instructions.md)**:AIが自分のスタイルに合致するコードを生成するため、プロジェクト全体のコーディング規約を定義します。
* **[エージェント スキル](/docs/copilot/customization/agent-skills.md)**:Copilot、GitHub Copilot CLI、GitHub Copilotコーディングエージェント全体で機能する専門的な機能をCopilotに教えます。
* **[カスタムエージェント](/docs/copilot/customization/custom-agents.md)**:コードレビューアまたはドキュメント作成者など、特定の役割を想定したエージェントを、独自のツールと手順を備えて作成します。
* **[MCPサーバー](/docs/copilot/customization/mcp-servers.md)**:MCPサーバーまたはMarketplaceエクステンションのツールでエージェントを拡張します。
* **[Hooks](/docs/copilot/customization/hooks.md)**:自動化とPolicy適用のための特定のイベントでカスタムコマンドを実行します。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIをカスタマイズ">
ワークフロー全体のAI体験をカスタマイズするすべての方法を探します。

* [Customization Overviewを開く](/docs/copilot/customization/overview.md)

</div>

## サポート

GitHub Copilot Chatのサポートはgithubから提供され、<https://support.github.com>で利用できます。

Copilotのセキュリティ、プライバシー、Compliance、透明性について詳しく学ぶには、[GitHub Copilot Trust Center FAQ](https://copilot.github.trust.page/faq)を参照してください。

## 料金

インライン提案とチャットイタラクション月額制限でGitHub Copilotを無料で使用を開始できます。より広範な使用については、さまざまな有料プランから選択できます。

[詳細なGitHub Copilot料金を表示](https://docs.github.com/en/copilot/get-started/plans)

## 次のステップ

* [GitHub Copilotの仕組み](/docs/copilot/concepts/overview.md)
* [エージェントでの使用を開始](/docs/copilot/agents/agents-tutorial.md)
* [GitHub Copilotを使用したハンズオンクイックスタート](/docs/copilot/getting-started.md)
* [エージェントタイプについて学習](/docs/copilot/agents/overview.md)
* [ワークフロー向けのAIをカスタマイズ](/docs/copilot/customization/overview.md)
* [VS CodeでAIを使用するベストプラクティス](/docs/copilot/copilot-tips-and-tricks.md)
* [VS CodehemKonfiguracijas Copilot](/docs/copilot/setup.md)

