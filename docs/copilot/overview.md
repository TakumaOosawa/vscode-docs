---
ContentId: 0aefcb70-7884-487f-953e-46c3e07f7cbe
DateApproved: 12/10/2025
MetaDescription: Copilot is your AI pair programmer tool in Visual Studio Code. Get code suggestions as you type in the editor, or use natural language chat to ask about your code or start an editing session for implementing new feature and fixing bugs.
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeでのGitHub Copilot

GitHub Copilotは、Visual Studio Codeに統合されたAI搭載のコーディングアシスタントです。自然言語プロンプトと既存のコードコンテキストに基づいて、コードの提案、説明、自動実装を提供します。Copilotは公開コードリポジトリでトレーニングされており、ほとんどのプログラミング言語とフレームワークを支援できます。

<video src="images/overview/agent-mode-blog-video.mp4" title="Agent mode hero video" autoplay loop controls muted></video>

## コア機能

### インライン提案

Copilotは、入力中にインラインでコード提案を提供します。1行の補完から関数全体の実装まで多岐にわたります。次の編集提案では、現在のコンテキストに基づいて次の論理的なコード変更を予測します。

<video src="images/inline-suggestions/nes-video.mp4" title="Copilot NES video" autoplay loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

**例:**

- `function calculateTax(`と入力して、完全な税計算実装を取得する
- `// Create a REST API endpoint for user authentication`と記述して、Express.jsのルートコードを生成する
- Reactコンポーネントを`const UserProfile = ({`で開始して、TypeScriptの型を含む完全な関数コンポーネントを受け取る

[VS Codeでのインライン提案](/docs/copilot/ai-powered-suggestions.md)の詳細をご覧ください。

### 自律型コーディング

エージェントは、ターミナルコマンドの実行や特殊なツールの呼び出しを含むマルチステップワークフローを調整しながら、複雑な開発タスクを自律的に計画および実行できます。高レベルの要件を動作するコードに変換できます。

Model Context Protocol (MCP)サーバーまたはMarketplace拡張機能のツールをインストールして、自律型コーディング体験の機能をさらに強化します。たとえば、データベースから情報を取得したり、外部APIに接続したりします。

<video src="images/overview/agent-mode-short.mp4" title="Agent mode video" autoplay loop controls muted></video>

**タスクの例:**

- OAuthを使用した認証の実装
- コードベースの新しいフレームワークまたは言語への移行
- 失敗したテストのデバッグと修正の適用
- アプリケーション全体のパフォーマンスの最適化

[エージェントによる自律型コーディング](/docs/copilot/chat/copilot-chat.md)および[VS CodeでのMCPサーバーの構成](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

### 自然言語チャット

自然言語を使用して、チャットインターフェイスを通じてコードベースと対話します。質問、説明の要求、または会話型のプロンプトを使用してコード変更を指定します。

単一のプロンプトを使用して、プロジェクト内の複数のファイルに変更を適用します。Copilotはプロジェクト構造を分析し、調整された修正を行います。

**一般的なクエリ:**

- 「このプロジェクトでの認証の仕組みはどうなっていますか？」
- 「データ処理関数のメモリリークの原因は何ですか？」
- 「支払い処理サービスにエラー処理を追加してください」
- 「ログインフォームとバックエンドAPIを追加してください」

![Webアプリにログインページを追加する方法を尋ねた際の応答を示すチャットビューのスクリーンショット。](images/overview/copilot-chat-view-add-page.png)

[VS Codeでのチャットの使用](/docs/copilot/chat/copilot-chat.md)の詳細をご覧ください。

### スマートアクション

VS Codeには、AI機能で強化されエディターに統合された、一般的な開発タスク用の事前定義されたアクションが多数あります。

コミットメッセージやプルリクエストの説明の作成支援、コードシンボルの名前変更、エディター内のエラー修正から、関連ファイルを見つけるのに役立つセマンティック検索まで。

![VS Codeのスマートアクションメニューのスクリーンショット](images/overview/copilot-chat-fix-test-failure.png)

[VS Codeのスマートアクション](/docs/copilot/copilot-smart-actions.md)の詳細をご覧ください。

## はじめに

### ステップ 1: Copilotのセットアップ

1. ステータスバーのCopilotアイコンにカーソルを合わせ、**Copilotのセットアップ**を選択します。

    ![ステータスバーのCopilotアイコンにカーソルを合わせ、[Copilotのセットアップ]を選択します。](images/setup/setup-copilot-status-bar.png)

1. サインイン方法を選択し、プロンプトに従います。まだCopilotサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free)にサインアップされます。

### ステップ 2: 基本的なインライン提案

1. 新しいファイルを作成し、入力を開始します。VS Codeはエディターの_ゴーストテキスト_にインライン提案を表示します。

    たとえば、新しいJavaScriptファイルを作成し、関数定義の入力を開始します:

    ```javascript
    // 新しい.jsファイルにこれを入力してみてください:
    function factorial(
    ```

1. `kbstyle(Tab)`キーでインライン提案を受け入れます。

### ステップ 3: 自律型コーディング

自律的な方法でより複雑なタスクを実行するには、チャットインターフェイスのエージェントを使用します。AIはタスクが完了するまでコードを反復します。

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)
1. エージェントピッカーから**Agent**を選択します
1. たとえば、次のような基本的なWebアプリの生成を依頼します:

    ```prompt
    レシピ共有用の基本的なnode.js Webアプリを作成してください。モダンでレスポンシブな外観にしてください。
    ```

エージェントが複数のファイルにわたってコードを独立して生成し、タスクに必要な依存関係をインストールする様子に注目してください。

### ステップ 4: インラインチャット

エディターで直接コードの生成、リファクタリング、または説明の支援を受けるには、エディターインラインチャットを使用できます。プロンプトを入力すると、AIが現在のファイル内のコード変更を提案し、コーディングの流れを維持します。

1. エディターでコードを選択します
1. `kb(inlinechat.start)`を押してエディターインラインチャットを開きます
1. 「このコードを...にリファクタリングしてください」のように説明または修正を依頼します
1. 提案された変更を確認して受け入れます

## 使用シナリオ

### コード分析とレビュー

既存のコードベースの理解と問題の特定:

- 「このアプリケーションの認証フローを説明してください」
- 「この支払いハンドラーの潜在的なセキュリティ問題は何ですか？」
- 「適切なJSDocコメントでこのAPIエンドポイントを文書化してください」

### デバッグとトラブルシューティング

コードの問題の特定と解決:

- 「なぜこのコンポーネントは不必要に再レンダリングされるのですか？」
- 「このデータ処理パイプラインのメモリリークを見つけて修正してください」
- 「パフォーマンス向上のためにこのデータベースクエリを最適化してください」

[デバッグにAIを使用する](/docs/copilot/guides/debug-with-copilot.md)の詳細をご覧ください。

### 機能の実装

新しい機能の構築:

- 「メール検証付きのユーザー登録システムを作成してください」
- 「WebSocketを使用してリアルタイム通知を追加してください」
- 「ローカルストレージ永続化を備えたショッピングカートを実装してください」

### テストと品質保証

テストの生成とコード品質の保証:

- 「このサービスクラスの包括的な単体テストを生成してください」
- 「APIエンドポイントの統合テストを作成してください」
- 「このデータ検証関数のプロパティベースのテストを追加してください」

[テストにAIを使用する](/docs/copilot/guides/test-with-copilot.md)の詳細をご覧ください。

### 学習とドキュメント

新しいテクノロジーとパターンの理解:

- 「async/awaitとPromisesの違いを教えてください」
- 「Pythonの代わりにGoでこのパターンをどのように実装しますか？」
- 「Reactでのエラー処理のベストプラクティスは何ですか？」

## AIをワークフローに合わせてカスタマイズする

### カスタム手順

カスタム手順を使用して、プロジェクト固有のコーディング規約とパターンを定義すると、AIはスタイルに合ったコードを生成します。これらの手順をすべてのチャットリクエストに自動的に適用するか、特定のファイルタイプにのみ適用します。

```markdown
---
applyTo: "**"
---
# 私のコーディングスタイル
- コンポーネントにはアロー関数を使用する
- letよりもconstを優先する
- 常にTypeScriptの型を含める
- わかりやすい変数名を使用する
- データアクセスにはリポジトリパターンに従う
```

AIをコーディングスタイルに合わせて調整するための[カスタム手順の使用](/docs/copilot/customization/custom-instructions.md)の詳細をご覧ください。

### 言語モデル

速度、推論、または特殊なタスクに合わせて最適化するために、さまざまなAIモデルをすばやく切り替えます。さまざまな組み込みモデルから選択するか、外部プロバイダーに接続して独自のAPIキーを持ち込みます。

![チャットビューのモデルピッカーを示すスクリーンショット。](images/language-models/model-dropdown-change-model.png)

[VS Codeでの言語モデル](/docs/copilot/customization/language-models.md)の使用の詳細をご覧ください。

### カスタムエージェント

VS Codeのチャット体験では、さまざまなエージェントを使用して、質問、編集、自律型コーディングセッションの実行を切り替えることができます。ワークフローに合わせたカスタムエージェントを作成することもできます。たとえば、計画とアーキテクチャの議論に焦点を当てたカスタムエージェントを作成します。エージェントが使用できるツールを指定し、エージェントが動作すべき正しいコンテキストを提供するためにカスタム手順を提供します。

![エージェントピッカーを強調表示したチャットビューを示すスクリーンショット。](images/overview/chat-mode-dropdown.png)

[独自のカスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)の詳細をご覧ください。

### ツールを使用したチャットの拡張

MCPサーバーまたはMarketplace拡張機能の特殊なツールを使用して、チャット体験の機能を拡張します。たとえば、データベースクエリ、外部APIへの接続、または特殊なタスクを実行するためのツールを追加します。

![MCPツールリスト](images/mcp-servers/agent-mode-select-tools.png)

[MCPサーバーとツールの使用](/docs/copilot/customization/mcp-servers.md)の詳細をご覧ください。

## ベストプラクティス

- タスクに適したツールを選択してください。コーディング中はインライン提案を取得し、自然言語クエリにはチャットを使用し、ワークフローに合ったエージェントを選択してください。

- 最良の結果を得るために効果的なプロンプトを作成してください。具体的にし、正しいコンテキストを提供し、頻繁に反復してください。

- カスタム手順、プロンプトファイル、またはカスタムエージェントを使用して、コーディングスタイルとプロジェクト規約に合わせてAIをカスタマイズしてください。
- MCPサーバーまたはMarketplace拡張機能のツールを使用して、AIの機能を拡張してください。

- タスクに最適化された言語モデルを選択してください。素早いコード提案には高速モデルを、より複雑なリクエストには推論モデルを使用してください。

[VS CodeでのAI使用のヒントとコツ](/docs/copilot/copilot-tips-and-tricks.md)の詳細をご覧ください。

## サポート

GitHub Copilot ChatのサポートはGitHubによって提供されており、<https://support.github.com>で連絡できます。

Copilotのセキュリティ、プライバシー、コンプライアンス、透明性の詳細については、[GitHub CopilotトラストセンターFAQ](https://copilot.github.trust.page/faq)をご覧ください。

## 価格

インライン提案とチャットインタラクションの月間制限付きでGitHub Copilotを無料で使用開始できます。より広範な使用については、さまざまな有料プランから選択できます。

[GitHub Copilotの詳細な価格を見る](https://docs.github.com/en/copilot/get-started/plans)

## 次のステップ

- [VS CodeでのCopilotのセットアップ](/docs/copilot/setup.md)
- [ハンズオン例の使用開始](/docs/copilot/getting-started.md)
- [ワークフローに合わせたAIのカスタマイズ](/docs/copilot/customization/overview.md)
- [VS CodeでのAI使用のセキュリティに関する考慮事項について学ぶ](/docs/copilot/security.md)
- [エージェントの使用開始](/docs/copilot/agents/agents-tutorial.md)
