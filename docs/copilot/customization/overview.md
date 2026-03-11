---
ContentId: 16c73175-a606-4aab-8ae5-a5071d3b9e24
DateApproved: 3/9/2026
MetaDescription: Visual Studio Code でカスタム指示、プロンプトファイル、カスタムエージェント、MCP サーバーなど、AI をカスタマイズして始めましょう。AI の応答をコーディング実践と一致させます。
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
# Visual Studio Code で AI をカスタマイズする

Visual Studio Code では、AI にコードベース、コーディング標準、ワークフローについて教える方法がいくつかあります。この記事では、カスタマイズオプションを紹介し、始め方をご説明します。

<div class="docs-action" data-show-in-doc="true" data-show-in-sidebar="true" title="基本概念">
異なるカスタマイズタイプと、それぞれの使用時期について学習します。

* [カスタマイズの概念](/docs/copilot/concepts/customization.md)

</div>

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="チュートリアル">
プロジェクト用に AI をカスタマイズするための実践的なチュートリアルに従います。

* [プロジェクト用に AI をカスタマイズする](/docs/copilot/guides/customize-copilot-guide.md)

</div>

カスタマイズにアクセスするには、チャットビューで**チャットを構成（歯車アイコン）**を選択してください。

## カスタマイズシナリオ

以下のセクションでは、一般的なカスタマイズシナリオと、それぞれに使用するオプションについて説明します。

### コーディング標準を定義する

[カスタム指示](/docs/copilot/customization/custom-instructions.md)を使用して、プロジェクト全体のルールと規約を AI と共有します。常にオンの指示はすべてのリクエストに適用され、ファイルベースの指示は特定のファイルタイプまたはフォルダをターゲットにします。たとえば、すべてのファイル全体で ESLint ルールを適用し、`.tsx`ファイルでのみ React パターンを適用します。

### タスクとワークフローを自動化する

[プロンプトファイル](/docs/copilot/customization/prompt-files.md)を作成して、コンポーネントのスキャフォールディングやプルリクエストの準備など、頻繁に実行する繰り返しタスク用。

スクリプトと外部ツールを含む、より複雑な複数ステップのワークフローの場合は、[エージェントスキル](/docs/copilot/customization/agent-skills.md)としてパッケージ化します。

### AI を専門化する

セキュリティレビュアー、データベース管理者、プランナーなど、特定のペルソナを採用する[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成します。各エージェントは、独自の動作、利用可能なツール、言語モデルの設定を定義します。異なるタスクに異なる[言語モデル](/docs/copilot/customization/language-models.md)を選択するか、独自の API キーを持参して追加のモデルにアクセスします。

### プラグインを検出してインストールする

[エージェントプラグイン](/docs/copilot/customization/agent-plugins.md)（プレビュー）をインストールして、プラグインマーケットプレイスからカスタマイズの事前パッケージ化されたバンドルを追加します。1 つのプラグインでスラッシュコマンド、スキル、カスタムエージェント、フック、MCP サーバーを提供できます。

### 外部ツールとデータを接続する

[MCP サーバー](/docs/copilot/customization/mcp-servers.md)を追加して、[Model Context Protocol](https://modelcontextprotocol.io/)を通じてデータベース、API、その他のサービスに AI がアクセスできるようにします。[フック](/docs/copilot/customization/hooks.md)を使用して、ファイル編集後のフォーマッタの実行やセキュリティポリシーの強制など、主要なライフサイクルポイントでシェルコマンドを実行します。

## 始める

AI のカスタマイズを段階的に実装します。基本から始めて、必要に応じてさらに追加します。実践的なチュートリアルについては、[プロジェクト用に AI をカスタマイズする](/docs/copilot/guides/customize-copilot-guide.md)ガイドを参照してください。

1. **プロジェクトを初期化する**：チャットで`/init`と入力して、コードベースに合わせたコーディング標準を含む`.github/copilot-instructions.md`ファイルを生成します。

1. **ターゲット規則を追加する**：言語規約やフレームワークパターンなど、コードベースの特定の部分用に、ファイルベースの`*.instructions.md`ファイルを作成します。

1. **繰り返しタスクを自動化する**：一般的なワークフロー用にプロンプトファイルを作成し、外部サービスを接続するために MCP サーバーを追加します。

1. **特殊なワークフローを作成する**：特定の役割用のカスタムエージェントを構築します。ツール全体で共有するエージェントスキルとして再利用可能な機能をパッケージ化します。

1. **AI を使用してカスタマイズを生成する**：チャットで`/create-prompt`、`/create-instruction`、`/create-skill`、`/create-agent`、または`/create-hook`と入力して、AI 支援でカスタマイズファイルを生成します。

## チャットカスタマイズエディター

> [!NOTE]
> チャットカスタマイズエディターは現在プレビュー中です。

チャットカスタマイズエディターは、1 つの場所ですべてのカスタマイズを検出、作成、管理するための一元化された UI を提供します。このエディターから、カスタマイズカテゴリ（エージェント、スキル、指示、プロンプト、フック、MCP サーバー）を参照し、オプションの AI ガイド付き生成で新しい項目を作成し、埋め込みコードエディターで既存のカスタマイズを編集できます。

チャットカスタマイズエディターを開くには、コマンドパレット（`kb(workbench.action.showCommands)`）から**チャット：チャットカスタマイズを開く**を実行します。

![チャットカスタマイズエディターのスクリーンショット。カスタマイズカテゴリを含むサイドバーと、カスタムエージェントをリストする主ビューを表示します。](../images/customization/chat-customizations-editor.png)

## カスタマイズの問題をトラブルシューティングする

カスタマイズが適用されていない場合や予期しない動作が発生する場合は、チャットビューで**チャットを構成（歯車アイコン）** > **エージェントログを表示**を選択して、[エージェント問題をトラブルシューティング](/docs/copilot/troubleshooting.md)してください。

## 関連リソース

* [カスタマイズの概念](/docs/copilot/concepts/customization.md)
* [プロジェクト用に AI をカスタマイズするガイド](/docs/copilot/guides/customize-copilot-guide.md)

