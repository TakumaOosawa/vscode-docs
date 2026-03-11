---
ContentId: a1b2c3d4-5e6f-7a8b-9c0d-1e2f3a4b5c6d
DateApproved: 3/9/2026
MetaDescription: VS Codeの AI機能の概要。インライン提案から自律エージェントまで、およびそれらの接続方法。
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

Visual Studio Codeの組み込みAI機能は、GitHub Copilotと大規模言語モデル(LLM)によって実現されています。これらの機能は、入力時のインライン提案から、機能全体を実装する自律エージェントまで、複数のサーフェスにわたります。この記事では、AI機能の概要とそれらの接続方法を説明します。実践チュートリアルについては、[クイックスタート](/docs/copilot/getting-started.md)を参照してください。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントを始める">
VS Codeでローカル、バックグラウンド、およびクラウドエージェントを体験する実践チュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## AI機能の概要

VS Codeは、異なるタスクに適した複数のインタラクションサーフェスにわたってAIを提供します:

* **[エージェント](/docs/copilot/agents/overview.md)**: 完全な[エージェントループ](/docs/copilot/concepts/agents.md#agent-loop)に従う自律セッション。ファイルの読み取り、複数ファイルにわたる調整された変更の実行、コマンドの実行、およびタスクが完了するまでの反復処理を行います。エージェントは、機能の実装からアーキテクチャレベルのリファクタリングとフレームワークマイグレーションまで、マルチステップタスクを徹底的に処理します。
* **[チャット](/docs/copilot/chat/copilot-chat.md)**: エージェントと対話し、マルチターン会話を行うための主要なインターフェース。チャットを使用してタスクを割り当て、質問をし、アイデアを探索したり、説明を取得します。目標に応じてAgent、Ask、Plan、およびカスタムエージェント間で切り替えます。
* **[インラインチャット](/docs/copilot/chat/inline-chat.md)**: エディター内で直接開く軽量チャットインターフェース。素早く、焦点を絞った編集用です。
* **[インライン提案](/docs/copilot/ai-powered-suggestions.md)**: 入力時にゴーストテキストとして表示されるコード提案。これらは特殊な補完モデルを使用し、エージェントループまたはツールは含まれません。[次の編集提案(NES)](/docs/copilot/ai-powered-suggestions.md#next-edit-suggestions)は、次の*編集がどこで行われるべきか*を予測することでさらに進みます。
* **[スマートアクション](/docs/copilot/copilot-smart-actions.md)**: コミットメッセージの生成や診断エラーの修正など、ワークフローに統合されたワンクリックAIアクション。

## 概念

次の概念記事では、これらのAI機能を支えるアーキテクチャとビルディングブロックについて説明します:

* [言語モデル](/docs/copilot/concepts/language-models.md): すべての機能を支えるAIモデル。モデルの選択と構成方法を含みます。
* [コンテキスト](/docs/copilot/concepts/context.md): VS Codeがファイルから会話履歴まで、モデルの情報をどのように組み立てるか。
* [ツール](/docs/copilot/concepts/tools.md): エージェントが開発環境で動作し、外部サービスに接続するためのメカニズム。
* [エージェント](/docs/copilot/concepts/agents.md): エージェントループ、エージェント型、サブエージェント、メモリ、およびプランニング。
* [カスタマイズ](/docs/copilot/concepts/customization.md): 指示、プロンプトファイル、カスタムエージェント、スキル、フック、およびプラグインでAI動作をカスタマイズする方法。
* [トラストとセーフティ](/docs/copilot/concepts/trust-and-safety.md): 制御メカニズム、AIの制限、およびセキュリティに関する考慮事項。

## 関連リソース

* [クイックスタート: VS Codeでの AI入門](/docs/copilot/getting-started.md)
* [VS CodeでAIを使用するためのベストプラクティス](/docs/copilot/best-practices.md)
* [VS Codeでエージェントを使用する](/docs/copilot/agents/overview.md)

