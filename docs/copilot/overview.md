---
ContentId: 0aefcb70-7884-487f-953e-46c3e07f7cbe
DateApproved: 12/10/2025
MetaDescription: CopilotはVisual Studio CodeのAIペアプログラマーツールです。エディターで入力しながらコード候補を取得したり、自然言語チャットでコードについて質問したり、新機能の実装やバグ修正のための編集セッションを開始したりできます。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeのGitHub Copilot

GitHub CopilotはVisual Studio Codeに統合されたAI搭載のコーディングアシスタントです。自然言語のプロンプトと既存のコードコンテキストに基づいて、コード候補、説明、自動実装を提供します。Copilotは公開コードリポジトリで学習されており、ほとんどのプログラミング言語とフレームワークで支援できます。

<video src="images/overview/agent-mode-blog-video.mp4" title="Agent mode hero video" autoplay loop controls muted></video>

## Core capabilities

## 主な機能

### Inline suggestions

### インライン候補

Copilotは入力に合わせて、1行の補完から関数全体の実装までのインラインコード候補を提供します。次の編集候補では、現在のコンテキストに基づいて次に行うべき論理的なコード変更を予測します。

<video src="images/inline-suggestions/nes-video.mp4" title="Copilot NES video" autoplay loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

**Examples:**

**例:**

- `function calculateTax(`と入力すると、税計算の完全な実装を取得できます
- `// Create a REST API endpoint for user authentication`と書くと、Express.jsのルートコードを生成できます
- `const UserProfile = ({`でReactコンポーネントを開始すると、TypeScript型付きの完全な関数コンポーネントを受け取れます

[VS Codeのインライン候補](/docs/copilot/ai-powered-suggestions.md)の詳細をご覧ください。

### Autonomous coding

### 自律的なコーディング

エージェントは、ターミナルコマンドの実行や専用ツールの呼び出しを含むマルチステップのワークフローを調整しながら、複雑な開発タスクを自律的に計画して実行できます。高レベルの要件を動作するコードへ変換できます。

Marketplace拡張機能からModel Context Protocol (MCP)サーバーやツールをインストールして、自律的なコーディング体験の機能をさらに強化できます。たとえば、データベースから情報を取得したり、外部APIに接続したりできます。

<video src="images/overview/agent-mode-short.mp4" title="Agent mode video" autoplay loop controls muted></video>

**Example tasks:**

**タスク例:**

- OAuthを使用した認証を実装する
- コードベースを新しいフレームワークまたは言語へ移行する
- 失敗しているテストをデバッグして修正を適用する
- アプリケーション全体のパフォーマンスを最適化する

[エージェントによる自律的なコーディング](/docs/copilot/chat/copilot-chat.md)と、[VS CodeでのMCPサーバーの構成](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

### Natural language chat

### 自然言語チャット

チャットインターフェイスを通じて、自然言語でコードベースと対話します。質問したり、説明を依頼したり、会話形式のプロンプトでコード変更を指定したりできます。

単一のプロンプトでプロジェクト内の複数ファイルに変更を適用できます。Copilotはプロジェクト構造を分析し、連携した修正を行います。

**Common queries:**

**よくある質問例:**

- "How does authentication work in this project?"
- "What's causing the memory leak in the data processing function?"
- "Add error handling to the payment processing service"
- "Add a login form and backend API"

![Chatビューのスクリーンショット。Webアプリにログインページを追加する方法を尋ねた際の応答を示しています。](images/overview/copilot-chat-view-add-page.png)

[VS Codeでのチャットの使用](/docs/copilot/chat/copilot-chat.md)の詳細をご覧ください。

### Smart actions

### スマートアクション

VS Codeには、一般的な開発タスク向けの多くの定義済みアクションがあり、AI機能によって強化され、エディターに統合されています。

コミットメッセージやプルリクエストの説明の作成支援、コードシンボルの名前変更、エディター内のエラー修正、関連ファイルを見つけるのに役立つセマンティック検索まで対応します。

![VS Codeのスマートアクションメニューのスクリーンショット](images/overview/copilot-chat-fix-test-failure.png)

[VS Codeのスマートアクション](/docs/copilot/copilot-smart-actions.md)の詳細をご覧ください。

## Getting started

## 開始する

### Step 1: Set up Copilot

### 手順 1: Copilotをセットアップする

1. ステータスバーのCopilotアイコンにカーソルを合わせ、**Set up Copilot**を選択します。

    ![Hover over the Copilot icon in the Status Bar and select Set up Copilot.](images/setup/setup-copilot-status-bar.png)

1. サインイン方法を選択し、プロンプトに従います。まだCopilotサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップされます。

### Step 2: Basic inline suggestions

### 手順 2: 基本的なインライン候補

1. 新しいファイルを作成して入力を開始します。VS Codeはエディターでインライン候補を_ゴーストテキスト_として表示します。

    たとえば、新しいJavaScriptファイルを作成し、関数定義の入力を開始します。

    ```javascript
    // 新しい.jsファイルでこれを入力してみてください:
    function factorial(
    ```

1. `kbstyle(Tab)`キーでインライン候補を受け入れます。

### Step 3: Autonomous coding

### 手順 3: 自律的なコーディング

より複雑なタスクを自律的に実行するには、チャットインターフェイスでエージェントを使用します。AIはタスクが完了するまでコードを反復します。

1. Chatビューを開きます (`kb(workbench.action.chat.open)`)
1. エージェントピッカーから**Agent**を選択します
1. たとえば次のように、基本的なWebアプリの生成を依頼します。

    ```prompt
    レシピ共有のための基本的なnode.js Webアプリを作成してください。モダンでレスポンシブな見た目にしてください。
    ```

エージェントが複数のファイルにわたって独立してコードを生成し、タスクに応じて依存関係をインストールする様子に注目してください。

### Step 4: Inline chat

### 手順 4: インラインチャット

エディター内でコードの生成、リファクタリング、説明の支援を得るには、エディターのインラインチャットを使用できます。プロンプトを入力すると、AIが現在のファイルに対するコード変更を提案し、コーディングの流れを維持できます。

1. エディターでコードを一部選択します
1. `kb(inlinechat.start)`を押してエディターのインラインチャットを開きます
1. 説明や、たとえば「Refactor this code to ...」のような変更を依頼します
1. 提案された変更を確認して受け入れます

## Usage scenarios

## 利用シナリオ

### Code analysis and review

### コード分析とレビュー

既存のコードベースを理解し、問題を特定します。

- "Explain the authentication flow in this application"
- "What are the potential security issues in this payment handler?"
- "Document this API endpoint with proper JSDoc comments"

### Debugging and troubleshooting

### デバッグとトラブルシューティング

コードの問題を特定して解決します。

- "Why is this component re-rendering unnecessarily?"
- "Find and fix the memory leak in this data processing pipeline"
- "Optimize this database query for better performance"

[AIをデバッグに活用する](/docs/copilot/guides/debug-with-copilot.md)方法の詳細をご覧ください。

### Feature implementation

### 機能実装

新しい機能を構築します。

- "Create a user registration system with email verification"
- "Add real-time notifications using WebSockets"
- "Implement a shopping cart with local storage persistence"

### Testing and quality assurance

### テストと品質保証

テストを生成し、コード品質を確保します。

- "Generate comprehensive unit tests for this service class"
- "Create integration tests for the API endpoints"
- "Add property-based tests for this data validation function"

[AIをテストに活用する](/docs/copilot/guides/test-with-copilot.md)方法の詳細をご覧ください。

### Learning and documentation

### 学習とドキュメント

新しい技術やパターンを理解します。

- "Show me the differences between async/await and Promises"
- "How would you implement this pattern in Go instead of Python?"
- "What are the best practices for error handling in React?"

## Customize the AI to your workflow

## ワークフローに合わせてAIをカスタマイズする

### Custom instructions

### カスタム指示

カスタム指示を使用してプロジェクト固有のコーディング規約やパターンを定義すると、AIがそのスタイルに一致するコードを生成します。これらの指示を、すべてのチャット要求に自動適用することも、特定のファイル種類にのみ適用することもできます。

```markdown
---
applyTo: "**"
---
# My Coding Style
- Use arrow functions for components
- Prefer const over let
- Always include TypeScript types
- Use descriptive variable names
- Follow the Repository pattern for data access
```

Learn more about [using custom instructions](/docs/copilot/customization/custom-instructions.md) to tailor the AI to your coding style.

[カスタム指示の使用](/docs/copilot/customization/custom-instructions.md)の詳細をご覧ください。AIをコーディングスタイルに合わせて調整できます。

### Language models

### 言語モデル

速度、推論、特化タスクに合わせて最適化するために、異なるAIモデルをすばやく切り替えられます。さまざまな組み込みモデルから選択するか、外部プロバイダーに接続して自分のAPIキーを使用できます。

![Chatビューのモデルピッカーを示すスクリーンショット。](images/language-models/model-dropdown-change-model.png)

[VS Codeでの言語モデルの使用](/docs/copilot/customization/language-models.md)の詳細をご覧ください。

### Custom agents

### カスタムエージェント

VS Codeのチャット体験では、異なるエージェントを使用して、質問、編集、自律的なコーディングセッションの実行を切り替えられます。ワークフローに合うカスタムエージェントを作成することもできます。たとえば、計画やアーキテクチャの議論に特化したカスタムエージェントを作成できます。エージェントが使用できるツールを指定し、動作に必要なコンテキストを与えるカスタム指示を提供します。

![Chatビューのスクリーンショット。エージェントピッカーが強調表示されています。](images/overview/chat-mode-dropdown.png)

[独自のカスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)の詳細をご覧ください。

### Extend chat with tools

### ツールでチャットを拡張する

MCPサーバーやMarketplace拡張機能の専用ツールを使って、チャット体験の機能を拡張できます。たとえば、データベースへのクエリ、外部APIへの接続、特化タスクの実行のためのツールを追加できます。

![MCPツール一覧](images/mcp-servers/agent-mode-select-tools.png)

[MCPサーバーとツールの使用](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

## Best Practices

## ベストプラクティス

- タスクに適したツールを選択します。コーディング中はインライン候補を取得し、自然言語の問い合わせにはチャットを使用し、ワークフローに合うエージェントを選びます。

- 最良の結果を得るために効果的なプロンプトを書きます。具体的にし、適切なコンテキストを提供し、頻繁に反復します。

- カスタム指示、プロンプトファイル、またはカスタムエージェントを使用して、コーディングスタイルやプロジェクト規約に合わせてAIをカスタマイズします。
- MCPサーバーやMarketplace拡張機能のツールを使用して、AIの機能を拡張します。

- タスクに最適化された言語モデルを選択します。すばやいコード候補には高速なモデルを使用し、より複雑な要求には推論モデルを使用します。

[VS CodeでAIを使用するためのヒントとコツ](/docs/copilot/copilot-tips-and-tricks.md)をさらに確認してください。

## Support

## サポート

GitHub Copilot ChatのサポートはGitHubが提供しており、<https://support.github.com>から問い合わせできます。

Copilotのセキュリティ、プライバシー、コンプライアンス、透明性の詳細については、[GitHub Copilot Trust Center FAQ](https://copilot.github.trust.page/faq)をご覧ください。

## Pricing

## 料金

GitHub Copilotは、インライン候補とチャットのやり取りに月ごとの制限はありますが、無料で使い始められます。より多く利用したい場合は、さまざまな有料プランから選べます。

[GitHub Copilotの詳細な料金を確認する](https://docs.github.com/en/copilot/get-started/plans)

## Next steps

## 次のステップ

- [VS CodeでCopilotをセットアップする](/docs/copilot/setup.md)
- [ハンズオン例で開始する](/docs/copilot/getting-started.md)
- [ワークフローに合わせてAIをカスタマイズする](/docs/copilot/customization/overview.md)
- [VS CodeでAIを使用する際のセキュリティ上の考慮事項を学ぶ](/docs/copilot/security.md)
- [エージェントを使い始める](/docs/copilot/agents/agents-tutorial.md)
