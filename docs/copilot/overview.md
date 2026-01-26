---
ContentId: 0aefcb70-7884-487f-953e-46c3e07f7cbe
DateApproved: 01/08/2026
MetaDescription: Copilot is your AI pair programmer tool in Visual Studio Code. Get code suggestions as you type in the editor, or use natural language chat to ask about your code or start an editing session for implementing new feature and fixing bugs.
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS Code での GitHub Copilot

GitHub Copilot は、Visual Studio Code に統合された AI 搭載のコーディングアシスタントです。自然言語プロンプトと既存のコードコンテキストに基づいて、コードの提案、説明、自動実装を提供します。Copilot は公開コードリポジトリでトレーニングされており、ほとんどのプログラミング言語とフレームワークを支援できます。

<video src="images/overview/agent-mode-blog-video.mp4" title="Agent mode hero video" autoplay loop controls muted></video>

## コア機能

### インライン提案

Copilot は、入力中に、1行の補完から関数全体の実装まで、インラインでコード提案を提供します。次の編集提案により、現在のコンテキストに基づいて、次に論理的なコード変更を予測します。

<video src="images/inline-suggestions/nes-video.mp4" title="Copilot NES video" autoplay loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

**例:**

- `function calculateTax(` と入力すると、完全な税金計算の実装を取得できます
- `// Create a REST API endpoint for user authentication` と記述すると、Express.js ルートコードが生成されます
- `const UserProfile = ({` で React コンポーネントを開始すると、TypeScript 型を含む完全な関数コンポーネントを受け取ることができます

[VS Code のインライン提案](/docs/copilot/ai-powered-suggestions.md)の詳細をご覧ください。

### 自律型コーディング

> [!IMPORTANT]
> 組織によっては、VS Code でエージェントが無効になっている場合があります。この機能を有効にするには、管理者に連絡してください。

エージェントは、複雑な開発タスクを自律的に計画して実行し、ターミナルコマンドの実行や特殊なツールの呼び出しを伴うマルチステップワークフローを調整できます。高レベルの要件を動作するコードに変換できます。

Model Context Protocol (MCP) サーバーまたは Marketplace 拡張機能からツールをインストールして、自律型コーディングエクスペリエンスの機能をさらに強化します。たとえば、データベースから情報を取得したり、外部 API に接続したりします。

<video src="images/overview/agent-mode-short.mp4" title="Agent mode video" autoplay loop controls muted></video>

**タスクの例:**

- OAuth を使用した認証の実装
- コードベースの新しいフレームワークまたは言語への移行
- 失敗したテストのデバッグと修正の適用
- アプリケーション全体のパフォーマンスの最適化

[エージェントによる自律型コーディング](/docs/copilot/chat/copilot-chat.md)と[VS Code での MCP サーバーの構成](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

### 自然言語チャット

自然言語を使用して、チャットインターフェースを通じてコードベースと対話します。会話形式のプロンプトを使用して、質問したり、説明を求めたり、コード変更を指定したりできます。

単一のプロンプトを使用して、プロジェクト内の複数のファイルに変更を適用します。Copilot はプロジェクト構造を分析し、調整された変更を行います。

**一般的なクエリ:**

- 「このプロジェクトでは認証はどのように機能しますか？」
- 「データ処理機能におけるメモリリークの原因は何ですか？」
- 「支払い処理サービスにエラー処理を追加してください」
- 「ログインフォームとバックエンド API を追加してください」

![Web アプリにログインページを追加する方法を尋ねた際の回答を示すチャットビューのスクリーンショット。](images/overview/copilot-chat-view-add-page.png)

[VS Code でのチャットの使用](/docs/copilot/chat/copilot-chat.md)の詳細をご覧ください。

### スマートアクション

VS Code には、AI 機能で強化され、エディターに統合された、一般的な開発タスク用の事前定義済みアクションが多数あります。

コミットメッセージやプルリクエストの説明の作成、コードシンボルの名前変更、エディターでのエラー修正から、関連ファイルの検索に役立つセマンティック検索まで支援します。

![VS Code のスマートアクションメニューのスクリーンショット](images/overview/copilot-chat-fix-test-failure.png)

[VS Code のスマートアクション](/docs/copilot/copilot-smart-actions.md)の詳細をご覧ください。

## はじめに

### ステップ 1: Copilot のセットアップ

1. ステータスバーの Copilot アイコンにカーソルを合わせ、**Set up Copilot** を選択します。

    ![ステータスバーの Copilot アイコンにカーソルを合わせ、Set up Copilot を選択します。](images/setup/setup-copilot-status-bar.png)

1. サインイン方法を選択し、プロンプトに従います。まだ Copilot サブスクリプションをお持ちでない場合は、[Copilot Free プラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)に登録されます。

### ステップ 2: 基本的なインライン提案

1. 新しいファイルを作成し、入力を開始します。VS Code はエディター内に_ゴーストテキスト_でインライン提案を表示します。

    たとえば、新しい JavaScript ファイルを作成し、関数定義の入力を開始します：

    ```javascript
    // 新しい .js ファイルにこれを入力してみてください：
    function factorial(
    ```

1. `kbstyle(Tab)` キーを使用してインライン提案を受け入れます。

### ステップ 3: 自律型コーディング

自律的な方法でより複雑なタスクを実行するには、チャットインターフェースでエージェントを使用します。AI はタスクが完了するまでコードを反復処理します。

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)
1. エージェントピッカーから **Agent** を選択します
1. たとえば、次のように基本的な Web アプリの生成を依頼します：

    ```prompt
    レシピを共有するための基本的な node.js Web アプリを作成してください。モダンでレスポンシブな外観にしてください。
    ```

エージェントが複数のファイルにまたがって個別にコードを生成し、タスクに必要な依存関係をインストールする様子に注目してください。

### ステップ 4: インラインチャット

エディターで直接コードの生成、リファクタリング、または説明に関するヘルプを得るには、エディターのインラインチャットを使用できます。プロンプトを入力すると、AI が現在のファイルでコード変更を提案し、コーディングの流れを維持します。

1. エディターでコードを選択します
1. `kb(inlinechat.start)` を押してエディターのインラインチャットを開きます
1. 「このコードをリファクタリングして...」のように説明を求めたり、変更を依頼したりします
1. 提案された変更を確認して受け入れます

## 使用シナリオ

### コード分析とレビュー

既存のコードベースの理解と問題の特定：

- 「このアプリケーションの認証フローを説明してください」
- 「この支払いハンドラーの潜在的なセキュリティ問題は何ですか？」
- 「適切な JSDoc コメントでこの API エンドポイントを文書化してください」

### デバッグとトラブルシューティング

コードの問題の特定と解決：

- 「このコンポーネントが不必要に再レンダリングされるのはなぜですか？」
- 「このデータ処理パイプラインのメモリリークを見つけて修正してください」
- 「パフォーマンス向上のためにこのデータベースクエリを最適化してください」

[デバッグに AI を使用する](/docs/copilot/guides/debug-with-copilot.md)の詳細をご覧ください。

### 機能の実装

新しい機能の構築：

- 「メール認証付きのユーザー登録システムを作成してください」
- 「WebSockets を使用してリアルタイム通知を追加してください」
- 「ローカルストレージ永続化を備えたショッピングカートを実装してください」

### テストと品質保証

テストの生成とコード品質の確保：

- 「このサービスクラスの包括的な単体テストを生成してください」
- 「API エンドポイントの統合テストを作成してください」
- 「このデータ検証関数のプロパティベースのテストを追加してください」

[テストに AI を使用する](/docs/copilot/guides/test-with-copilot.md)の詳細をご覧ください。

### 学習とドキュメンテーション

新しいテクノロジーとパターンの理解：

- 「async/await と Promises の違いを教えてください」
- 「Python の代わりに Go でこのパターンをどのように実装しますか？」
- 「React でのエラー処理のベストプラクティスは何ですか？」

## ワークフローに合わせて AI をカスタマイズする

### カスタム指示

カスタム指示を使用して、プロジェクト固有のコーディング規約とパターンを定義すると、AI はスタイルに一致するコードを生成します。これらの指示をすべてのチャットリクエストに自動的に適用するか、特定のファイルタイプにのみ適用します。

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

[カスタム指示の使用](/docs/copilot/customization/custom-instructions.md)の詳細を参照して、コーディングスタイルに合わせて AI を調整してください。

### 言語モデル

さまざまな AI モデルをすばやく切り替えて、速度、推論、または特殊なタスクに合わせて最適化します。さまざまな組み込みモデルから選択するか、外部プロバイダーに接続して独自の API キーを持ち込みます。

![チャットビューのモデルピッカーを示すスクリーンショット。](images/language-models/model-dropdown-change-model.png)

[VS Code での言語モデル](/docs/copilot/customization/language-models.md)の詳細をご覧ください。

### カスタムエージェント

VS Code のチャットエクスペリエンスでは、さまざまなエージェントを使用して、質問、編集、または自律型コーディングセッションの実行を切り替えることができます。ワークフローに合ったカスタムエージェントを作成することもできます。たとえば、計画とアーキテクチャの議論に重点を置いたカスタムエージェントを作成します。エージェントが使用できるツールを指定し、エージェントが動作すべき適切なコンテキストを提供するためのカスタム指示を提供します。

![エージェントピッカーを強調表示したチャットビューを示すスクリーンショット。](images/overview/chat-mode-dropdown.png)

[独自のカスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)の詳細をご覧ください。

### ツールによるチャットの拡張

MCP サーバーまたは Marketplace 拡張機能の特殊なツールを使用して、チャットエクスペリエンスの機能を拡張します。たとえば、データベースのクエリ、外部 API への接続、または特殊なタスクの実行を行うツールを追加します。

![MCP ツールリスト](images/mcp-servers/agent-mode-select-tools.png)

[MCP サーバーとツールの使用](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

## ベストプラクティス

- タスクに適したツールを選択してください。コーディング中にインライン提案を取得し、自然言語クエリにはチャットを使用し、ワークフローに合ったエージェントを選択します。

- 効果的なプロンプトを作成して、最良の結果を得てください。具体的にし、適切なコンテキストを提供し、頻繁に反復します。

- カスタム指示、プロンプトファイル、またはカスタムエージェントを使用して、コーディングスタイルとプロジェクト規約に合わせて AI をカスタマイズします。
- MCP サーバーまたは Marketplace 拡張機能のツールを使用して、AI の機能を拡張します。

- タスクに最適化された言語モデルを選択してください。迅速なコード提案には高速モデル、より複雑なリクエストには推論モデルを使用します。

[VS Code で AI を使用するためのヒントとコツ](/docs/copilot/copilot-tips-and-tricks.md)をさらに入手してください。

## サポート

GitHub Copilot Chat のサポートは GitHub によって提供されており、<https://support.github.com> から連絡できます。

Copilot のセキュリティ、プライバシー、コンプライアンス、透明性の詳細については、[GitHub Copilot Trust Center FAQ](https://copilot.github.trust.page/faq) を参照してください。

## 価格

GitHub Copilot は、インライン提案とチャットのやり取りに月ごとの制限を設けて、無料で使用を開始できます。より広範な使用については、さまざまな有料プランから選択できます。

[GitHub Copilot の詳細な価格を表示](https://docs.github.com/en/copilot/get-started/plans)

## 次のステップ

- [VS Code で Copilot をセットアップする](/docs/copilot/setup.md)
- [ハンズオンの例で始める](/docs/copilot/getting-started.md)
- [ワークフローに合わせて AI をカスタマイズする](/docs/copilot/customization/overview.md)
- [VS Code での AI 使用のセキュリティに関する考慮事項について学ぶ](/docs/copilot/security.md)
- [エージェントの使用を開始する](/docs/copilot/agents/agents-tutorial.md)
