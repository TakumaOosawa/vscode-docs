---
ContentId: a1b2c3d4-5e6f-7a8b-9c0d-1e2f3a4b5c6d
DateApproved: 3/9/2026
MetaDescription: VS Codeの AI機能の概要。インライン提案から自律エージェントまで、それらがどのようにつながっているかについて説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- copilot
- ai
- concepts
- overview
- agents
- chat
- inline suggestions
- smart actions
---

# VS CodeのAI機能

Visual Studio Codeに搭載されたAI機能は、GitHub Copilotと大規模言語モデル(LLM)によって実現されています。これらの機能は、入力時のインライン提案から、機能全体を実装する自律エージェントまで、複数のインターフェースに対応しています。この記事では、AI機能の概要と、それらがどのようにつながっているかについて説明します。実践的なチュートリアルについては、[クイックスタート](/docs/copilot/getting-started.md)を参照してください。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントの使い始める">
VS Codeで、ローカル、バックグラウンド、クラウドエージェントを体験する実践的なチュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## 一目でわかるAI機能

VS Codeは、さまざまなタスクに適した複数のインターフェースを通じてAIを提供しています。

* **[エージェント](/docs/copilot/agents/overview.md)**: 完全な[エージェントループ](/docs/copilot/concepts/agents.md#agent-loop)に従い、ファイルを読み取り、複数のファイル間で調整された変更を実行し、コマンドを実行し、タスクが完了するまで反復する自律セッション。エージェントは、機能の実装からアーキテクチャレベルのリファクタリングとフレームワークマイグレーションまで、マルチステップタスクをエンドツーエンドで処理します。
* **[チャット](/docs/copilot/chat/copilot-chat.md)**: エージェントと対話したり、複数ターンの会話をしたりするためのプライマリインターフェース。チャットを使用してタスクを割り当てたり、質問をしたり、アイデアを探索したり、説明を取得したりできます。目標に応じて、エージェント、質問、プラン、カスタムエージェント間で切り替えます。
* **[インラインチャット](/docs/copilot/chat/inline-chat.md)**: エディター内で直接開く軽量なチャットインターフェース。迅速でフォーカスした編集に対応しています。
* **[インライン提案](/docs/copilot/ai-powered-suggestions.md)**: 入力時にゴーストテキストとして表示されるコード提案。これらは、エージェントループやツールを使用しません。[次の編集提案(NES)](/docs/copilot/ai-powered-suggestions.md#next-edit-suggestions)では、次の編集が*どこで*行われるべきかを予測しさらに進めます。
* **[スマートアクション](/docs/copilot/copilot-smart-actions.md)**: コミットメッセージの生成や診断エラーの修正など、ワークフローに統合されたワンクリックAIアクション。

## コンセプト

次の概念記事は、これらのAI機能を支えるアーキテクチャと構成要素について説明しています。

* [言語モデル](/docs/copilot/concepts/language-models.md): すべての機能を支えるAIモデル。モデルの選択と設定方法についても説明します。
* [コンテキスト](/docs/copilot/concepts/context.md): VS Codeがモデル用に情報を集める方法。ファイルから会話履歴まで。
* [ツール](/docs/copilot/concepts/tools.md): エージェントが開発環境で動作し、外部サービスに接続できるようにするメカニズム。
* [エージェント](/docs/copilot/concepts/agents.md): エージェントループ、エージェントタイプ、サブエージェント、メモリ、計画。
* [カスタマイズ](/docs/copilot/concepts/customization.md): 指示、プロンプトファイル、カスタムエージェント、スキル、フック、プラグインでAI動作をカスタマイズする方法。
* [信頼とセキュリティ](/docs/copilot/concepts/trust-and-safety.md): 制御メカニズム、AIの制限、セキュリティに関する注意事項。

## 関連リソース

* [クイックスタート: VS CodeでAIを始める](/docs/copilot/getting-started.md)
* [VS CodeでAIを使用するためのベストプラクティス](/docs/copilot/best-practices.md)
* [VS CodeでエージェントをYes](/docs/copilot/agents/overview.md)

