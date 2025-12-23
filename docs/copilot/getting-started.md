---
ContentId: 37fd3bd2-4209-49f6-bec5-c544d6b1b289
DateApproved: 12/10/2025
MetaDescription: VS CodeでGitHub Copilotを使って最初のWebアプリケーションを構築します。インライン提案、エージェント、インライン チャット、スマート アクション、そしてAIコーディング体験をパーソナライズする方法を学びます。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeでGitHub Copilotを使い始める

GitHub Copilotは、Visual Studio Codeでのコード作成方法を変革します。このハンズオン チュートリアルでは、完全なタスク管理Webアプリケーションを構築しながら、VS CodeのAI機能（インテリジェントなインライン提案、エージェントによる自律的な機能開発、インライン チャットによる正確な編集、統合されたスマート アクション、そして強力なカスタマイズ オプション）を学びます。

このチュートリアルを終える頃には、動作するWebアプリケーションと、あなたの開発スタイルに適応するパーソナライズされたAIコーディング環境の両方を手に入れられます。

## 前提条件

* お使いのマシンにVS Codeがインストールされていること。[Visual Studio CodeのWebサイト](https://code.visualstudio.com/)からダウンロードします。

* GitHub Copilotにアクセスできること。次の手順に従って[VS CodeでGitHub Copilotをセットアップする](/docs/copilot/setup.md)。

    > [!TIP]
    > Copilotのサブスクリプションをお持ちでない場合でも、VS Code内から直接Copilotの無料利用にサインアップでき、インライン提案とチャットのやり取りに月あたりの上限が付与されます。

## 手順1: インライン提案を体験する

AIによるインライン提案は入力と同時に表示され、より速く、より少ないミスでコードを書けるように支援します。まずはタスク マネージャーの基盤を作り始めましょう。

1. Create a new folder for your project and open it in VS Code.

1. プロジェクト用の新しいフォルダーを作成し、VS Codeで開きます。

1. `index.html`という新しいファイルを作成します。

1. 次の内容を入力し始めます。入力と同時に、VS Codeがインライン提案（_ゴースト テキスト_）を表示します。

    ```html
    <!DOCTYPE html>
    ```

    ![CopilotがHTML構造のインライン提案を提示しているスクリーンショット。](./images/getting-started/html-completion.png)

    大規模言語モデルは非決定的であるため、異なる提案が表示される場合があります。

1. `kbstyle(Tab)`を押して提案を受け入れます。

    おめでとうございます。これで、最初のAIによるインライン提案を受け入れました。

1. HTML構造の構築を続けます。`<body>`タグの内側で、次の入力を始めます。

    ```html
    <div class="container">
        <h1>My Task Manager</h1>
        <form id="task-form">
    ```

    アプリケーション構造を組み立てる中で、VS Codeが関連するHTML要素を継続して提案する様子に注目してください。

1. 複数の提案が表示された場合は、ゴースト テキストにカーソルを合わせてナビゲーション コントロールを表示するか、`kb(editor.action.inlineSuggest.showNext)`と`kb(editor.action.inlineSuggest.showPrevious)`を使って候補を切り替えます。

    ![インライン提案のナビゲーション コントロールを示すスクリーンショット。](./images/getting-started/inline-suggestion-navigation.png)

インライン提案は入力中に自動的に動作し、あなたの入力パターンやプロジェクトのコンテキストから学習します。定型コード、HTML構造、繰り返しパターンの作成に特に役立ちます。

## 手順2: エージェントで機能全体を構築する

エージェントは、VS Codeで最も強力なAI機能です。自然言語のプロンプトを与えると、複数ファイルにまたがる複雑な機能を自律的に計画し、実装します。これを使って、タスク マネージャーの中核機能を作成しましょう。

1. `kb(workbench.action.chat.open)`を押すか、VS Codeのタイトル バーにあるチャット アイコンを選択して、チャット ビューを開きます。

    チャット ビューでは、AIとの継続的な会話が可能になり、リクエストの洗練や、より良い結果の取得が容易になります。

1. チャット ビュー上部のエージェント ピッカーで**Agent**を選択し、自律コーディング モードに切り替えます。

    ![チャット ビューのエージェント ピッカーを示すスクリーンショット。](./images/getting-started/agent-mode-selection.png)

1. 次のプロンプトを入力して`kbstyle(Enter)`を押します。エージェントがリクエストを分析し、解決策の実装を開始します。

    ```prompt
    タスクを追加、削除、完了としてマークできる完全なタスク マネージャーWebアプリケーションを作成してください。モダンなCSSスタイルを含め、レスポンシブにしてください。セマンティックなHTMLを使用し、アクセシブルであることを確認してください。マークアップ、スタイル、スクリプトはそれぞれ別のファイルに分けてください。
    ```

    エージェントがリクエストを実装するために必要なファイルとコードを生成する様子を確認します。`index.html`ファイルの更新、スタイル用の`styles.css`ファイルの作成、機能用の`script.js`ファイルの作成が行われるはずです。

    > [!TIP]
    > 言語モデルによって得意分野が異なる場合があります。チャット ビューのモデル ドロップダウンを使用して、言語モデルを切り替えます。

1. 生成されたファイルを確認し、**Keep**を選択してすべての変更を受け入れます。

1. ブラウザーで`index.html`ファイルを開いて、タスク マネージャーが動作することを確認します。タスクの追加、完了のマーク、削除ができます。

    > [!TIP]
    > 開発中に変更をリアルタイムでVS Code上で確認するには、[Live Preview拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)を使用します。

1. 追加の機能を加えてみましょう。チャット入力欄に次のプロンプトを入力します。

    ```prompt
    すべてのタスク、完了したタスクのみ、未完了のタスクのみを表示するボタンを備えたフィルター システムを追加してください。既存のデザインに合うようにスタイルも更新してください。
    ```

    この機能を完全に実装するために、エージェントが複数ファイルにまたがる変更を調整する様子に注目してください。

エージェントは、高レベルの要件を理解して動作するコードに落とし込むことが得意です。新機能の実装、コードの大規模なリファクタリング、ゼロからのアプリケーション構築に最適です。

## 手順3: インライン チャットで正確に調整する

エージェントが大きな機能を扱う一方で、エディターのインライン チャットは、ファイル内の特定のコード セクションに対する的を絞った改善に最適です。これを使ってタスク マネージャー アプリを強化しましょう。

1. JavaScriptファイルを開き、新しいタスクを追加するコードを見つけます。

1. コード ブロックを選択し、`kb(inlinechat.start)`を押してエディターのインライン チャットを開きます。

    ![選択したコード ブロックに対してインライン チャットを開始しているスクリーンショット。](./images/getting-started/inline-chat-start.png)

    > [!NOTE]
    > 大規模言語モデルは非決定的であるため、正確なコードは異なる場合があります。

1. 次のプロンプトを入力します。

    ```text
    空のタスクが追加されないように入力の検証を追加し、タスク テキストの前後の空白をトリムしてください。
    ```

    インライン チャットが選択したコードに特化して、的を絞った改善を行う様子に注目してください。

    ![インライン チャットが選択した関数に検証を追加しているスクリーンショット。](./images/getting-started/inline-chat-validation.png)

1. 変更内容を確認し、**Keep**を選択して適用します。

エディターのインライン チャットは、広範なコードベースに影響を与えずに、エラー処理の追加、個別関数のリファクタリング、バグ修正などの小さく焦点を絞った変更を行うのに最適です。

## 手順4: AI体験をパーソナライズする

チャットをカスタマイズすると、特定のニーズやコーディング スタイルにより適合します。カスタム指示を設定したり、専用のカスタム エージェントを作成したりできます。プロジェクト向けに完全なパーソナライズ環境を作成しましょう。

### カスタム指示を作成する

カスタム指示は、コーディングの好みや標準をAIに伝えます。これらはすべてのチャットのやり取りに自動的に適用されます。

1. プロジェクト ルートに`.github`という新しいフォルダーを作成します。

1. `.github`フォルダーの中に`copilot-instructions.md`というファイルを作成します。

1. 次の内容を追加します。

    ```markdown
    # Project general coding guidelines

    ## Code Style
    - Use semantic HTML5 elements (header, main, section, article, etc.)
    - Prefer modern JavaScript (ES6+) features like const/let, arrow functions, and template literals

    ## Naming Conventions
    - Use PascalCase for component names, interfaces, and type aliases
    - Use camelCase for variables, functions, and methods
    - Prefix private class members with underscore (_)
    - Use ALL_CAPS for constants

    ## Code Quality
    - Use meaningful variable and function names that clearly describe their purpose
    - Include helpful comments for complex logic
    - Add error handling for user inputs and API calls
    ```

1. ファイルを保存します。これで、これらの指示がこのプロジェクト内のすべてのチャットのやり取りに適用されます。

1. エージェントに新機能の追加を依頼して、カスタム指示をテストします。

    ```prompt
    タスク マネージャーにダーク モードのトグル ボタンを追加してください。
    ```

    生成されたコードが指定したガイドラインに従っていることを確認します。VS Codeは、特定のファイル タイプに指示を適用するなど、より高度なカスタム指示にも対応しています。

### コード レビュー用のカスタム エージェントを作成する

カスタム エージェントは、特定のタスクに特化したAIのペルソナを作成します。分析とコードへのフィードバックに焦点を当てる「Code Reviewer」エージェントを作成しましょう。カスタム エージェント定義では、AIの役割、具体的なガイドライン、使用できるツールを定義できます。

1. コマンド パレットを開き、**Chat: New Custom Agent**コマンドを実行します。

1. 場所として`.github/agents`を選択します。

    このオプションにより、カスタム エージェントがワークスペースに追加され、他のチーム メンバーがプロジェクトを開いたときに利用できるようになります。

1. カスタム エージェントの名前を「Code Reviewer」にします。これにより、`.github/agents`フォルダーに`Code Reviewer.md`という新しいファイルが作成されます。

1. ファイルの内容を次の内容に置き換えます。このカスタム エージェントはコード変更を許可しない点に注意してください。

    ```markdown
    ---
    description: 'Review code for quality and adherence to best practices.'
    tools: ['usages', 'vscodeAPI', 'problems', 'fetch', 'githubRepo', 'search']
    ---
    # Code Reviewer agent

    You are an experienced senior developer conducting a thorough code review. Your role is to review the code for quality, best practices, and adherence to [project standards](../copilot-instructions.md) without making direct code changes.

    When reviewing code, structure your feedback with clear headings and specific examples from the code being reviewed.

    ## Analysis Focus
    - Analyze code quality, structure, and best practices
    - Identify potential bugs, security issues, or performance problems
    - Evaluate accessibility and user experience considerations

    ## Important Guidelines
    - Ask clarifying questions about design decisions when appropriate
    - Focus on explaining what should be changed and why
    - DO NOT write or suggest specific code changes directly
    ```

1. Save the file. In the Chat view, you can now select this custom agent from the agent picker.

1. ファイルを保存します。チャット ビューで、エージェント ピッカーからこのカスタム エージェントを選択できるようになります。

    ![エージェント ピッカーにCode Reviewerカスタム エージェントが表示されているスクリーンショット。](./images/getting-started/custom-mode-dropdown.png)

1. エージェント ピッカーから**Code Reviewer**を選択し、次のプロンプトを入力してカスタム エージェントをテストします。

    ```prompt
    プロジェクト全体をレビューしてください
    ```

    AIがコード レビュアーとして振る舞い、分析と改善提案を提供するようになったことを確認します。

    ![カスタム レビュアー エージェントがコードを分析しているスクリーンショット。](./images/getting-started/custom-reviewer-mode.png)

## 手順5: 事前構築されたAI支援のためにスマート アクションを使う

スマート アクションは、VS Codeのインターフェイスに直接統合されたAI機能を提供し、開発ワークフローにシームレスに組み込まれます。チャットのやり取りとは異なり、スマート アクションは必要な場所に文脈に応じて表示されます。例としてコミット メッセージ生成を見てみましょう。

1. `kb(workbench.view.scm)`を押すか、アクティビティ バーのソース管理アイコンを選択して、**Source Control**ビューを開きます。

1. プロジェクト用のGitリポジトリをまだ初期化していない場合は、Source Controlビューで**Initialize Repository**を選択して初期化します。

1. コミットしたいファイルの横にある**+**ボタンを選択して変更をステージします。

1. **きらめきアイコン**を選択して、ステージ済みの変更に基づくコミット メッセージを生成します。

    AIはステージ済みの変更を分析し、Conventional Commits標準に従った説明的なコミット メッセージを生成します。AIは次を考慮します。

    * どのファイルが変更されたか
    * 変更の性質（機能追加、バグ修正、リファクタリング）
    * 変更の範囲と影響

    ![Source Controlビューで生成されたコミット メッセージを示すスクリーンショット。](./images/getting-started/generated-commit-message.png)

1. 生成されたメッセージを確認します。満足できる場合はコミットを進めます。別のスタイルや焦点が必要な場合は、きらめきアイコンをもう一度選択して別のメッセージを生成します。

コミット メッセージ生成のようなスマート アクションは、チャット インターフェイスに切り替えることなく、AIが既存のワークフローに自然に統合されることを示します。VS Codeには、デバッグやテストなどを支援する他のスマート アクションも多数あります。

## 次のステップ

おめでとうございます。完全なタスク管理アプリケーションを構築し、VS Codeの中核機能全体でAIを効果的に活用する方法を学びました。

他のカスタマイズ オプションを探索することで、AIの機能をさらに強化できます。

* 計画、デバッグ、ドキュメント作成などのタスク向けに、より特化したエージェントを追加する。
* 特定のプログラミング言語やフレームワーク向けのカスタム指示を作成する。
* MCP（Model Context Protocol）サーバーやVS Code拡張機能の追加ツールで、AIの機能を拡張する。

## 関連リソース

* [エージェントのチュートリアル](/docs/copilot/agents/agents-tutorial.md): さまざまなエージェント タイプを扱うためのハンズオン チュートリアル

* [AI機能を使うためのチート シート](/docs/copilot/reference/copilot-vscode-features.md) - VS CodeにおけるGitHub Copilotの全機能のクイック リファレンス

* [チャットのドキュメント](/docs/copilot/chat/copilot-chat.md) - VS Codeでの自律コーディングを深掘り

* [カスタマイズ ガイド](/docs/copilot/customization/overview.md) - 高度なパーソナライズ手法

* [MCPツール](/docs/copilot/customization/mcp-servers.md) - 外部APIやサービスでエージェントを拡張
