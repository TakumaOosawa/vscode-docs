---
ContentId: 16c73175-a606-4aab-8ae5-a5071d3b9e24
DateApproved: 3/9/2026
MetaDescription: Visual Studio Codeでカスタム指示、プロンプトファイル、カスタムエージェント、MCPサーバーなど、AIカスタマイズを始めて、AIレスポンスをコーディング慣行に合わせます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- copilot
- customization
- chat
- instructions
- rules
- slash commands
- prompt files
- custom agents
- agent skills
- mcp
---
# Visual Studio CodeのAIをカスタマイズする

Visual Studio Codeは、コードベース、コーディング標準、ワークフローについてAIに学習させるための複数の方法を提供します。この記事では、カスタマイズオプションを紹介し、開始方法をお伝えします。

<div class="docs-action" data-show-in-doc="true" data-show-in-sidebar="true" title="Core concepts">
異なるカスタマイズタイプと、それぞれを使用する場合について学習します。

* [カスタマイズの概念](/docs/copilot/concepts/customization.md)

</div>

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="Tutorial">
プロジェクト用のAIをカスタマイズする実践的なチュートリアルに従います。

* [プロジェクト用のAIをカスタマイズする](/docs/copilot/guides/customize-copilot-guide.md)

</div>

カスタマイズにアクセスするには、チャットビューで**チャット設定（ギアアイコン）**を選択します。

## カスタマイズシナリオ

次のセクションは、一般的なカスタマイズシナリオと、個々に使用するオプションについて説明します。

### コーディング標準を定義する

[カスタム指示](/docs/copilot/customization/custom-instructions.md)を使用して、プロジェクト全体の規則と慣行をAIと共有します。常時有効な指示はすべてのリクエストに適用され、ファイルベースの指示は特定のファイルタイプまたはフォルダーを対象とします。例えば、すべてのファイルでESLintルールのサポートを適用し、`.tsx`ファイルでのみReactパターンを適用します。

### タスクとワークフローの自動化

コンポーネントのスキャフォルディング、プルリクエストの準備など、よく実行する反復可能なタスク用の[プロンプトファイル](/docs/copilot/customization/prompt-files.md)を作成します。

スクリプトと外部ツールを含むより複雑な複数ステップのワークフローの場合は、[エージェントスキル](/docs/copilot/customization/agent-skills.md)としてパッケージ化します。

### AIを専門化させる

セキュリティレビュアー、データベース管理者、プランナーなどの特定のペルソナを採用する[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成します。各エージェントは独自の動作、利用可能なツール、言語モデルの選択肢を定義します。異なるタスクに異なる[言語モデル](/docs/copilot/customization/language-models.md)を選択するか、独自のAPIキーを持ち込んで追加のモデルにアクセスします。

### プラグインを検出およびインストールする

[エージェントプラグイン](/docs/copilot/customization/agent-plugins.md)（プレビュー）をインストールして、プラグインマーケットプレイスからカスタマイズの事前パッケージ化されたバンドルを追加します。1つのプラグインは、スラッシュコマンド、スキル、カスタムエージェント、フック、MCPサーバーを提供できます。

### 外部ツールとデータを接続する

[MCPサーバー](/docs/copilot/customization/mcp-servers.md)を追加して、[Model Context Protocol](https://modelcontextprotocol.io/)を通じてAIにデータベース、API、その他のサービスへのアクセスを提供します。[フック](/docs/copilot/customization/hooks.md)を使用して、すべてのファイル編集後にフォーマッターを実行したり、セキュリティポリシーを適用したりするなど、ライフサイクルの主要なポイントでシェルコマンドを実行します。

## 開始する

AIカスタマイズを段階的に実装します。基本から開始して、必要に応じてさらに追加します。実践的なチュートリアルについては、[プロジェクト用のAIをカスタマイズする](/docs/copilot/guides/customize-copilot-guide.md)ガイドを参照してください。

1. **プロジェクトを初期化する**:チャットで`/init`と入力して、コードベースに合わせたコーディング標準を含む`.github/copilot-instructions.md`ファイルを生成します。

1. **対象となるルールを追加する**:言語の慣行やフレームワークのパターンなど、コードベースの特定の部分にファイルベースの`*.instructions.md`ファイルを作成します。

1. **反復的なタスクを自動化する**:一般的なワークフロー用のプロンプトファイルを作成し、MCPサーバーを追加して外部サービスを接続します。

1. **特殊なワークフローを作成する**:特定のロール用のカスタムエージェントを構築します。再利用可能な機能をエージェントスキルとしてパッケージ化して、ツール全体で共有します。

1. **AIでカスタマイズを生成する**:チャットで`/create-prompt`、`/create-instruction`、`/create-skill`、`/create-agent`、または`/create-hook`と入力して、AI支援でカスタマイズファイルを生成します。

## チャットカスタマイズエディター

> [!NOTE]
> チャットカスタマイズエディターは現在プレビュー中です。

チャットカスタマイズエディターは、すべてのカスタマイズを1つの場所で検出、作成、管理するための集中UIを提供します。エディターから、カスタマイズカテゴリー（エージェント、スキル、指示、プロンプト、フック、MCPサーバー）を参照して、オプションのAIガイド付き生成で新しいアイテムを作成し、埋め込みコードエディターで既存のカスタマイズを編集できます。

チャットカスタマイズエディターを開くには、コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: Open Chat Customizations**を実行します。

![チャットカスタマイズエディターのスクリーンショット。サイドバーでカスタマイズカテゴリーを表示し、メインビューでカスタムエージェントを一覧表示しています。](../images/customization/chat-customizations-editor.png)

## カスタマイズの問題をトラブルシューティングする

カスタマイズが適用されていない場合や予期しない動作が発生する場合は、チャットビューで**チャット設定（ギアアイコン）** > **エージェントログを表示**を選択して、[エージェントの問題をトラブルシューティング](/docs/copilot/troubleshooting.md)します。

## 関連リソース

* [カスタマイズの概念](/docs/copilot/concepts/customization.md)
* [プロジェクト用のAIをカスタマイズするガイド](/docs/copilot/guides/customize-copilot-guide.md)

