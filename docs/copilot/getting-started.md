---
ContentId: 37fd3bd2-4209-49f6-bec5-c544d6b1b289
DateApproved: 3/9/2026
MetaDescription: VS Code で GitHub Copilot エージェントを使用して最初のアプリを構築します。機能を計画し、複数のファイルに実装し、AI ワークフローをカスタマイズします。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS Code で GitHub Copilot を始める

GitHub Copilot は Visual Studio Code でのコード記述方法を変わります。このハンズオンチュートリアルでは、完全なタスク管理 Web アプリケーションを構築しながら、VS Code の AI 機能を発見します。複数のファイルに機能を実装する自律型エージェント、インテリジェントなインライン候補、インラインチャットでの正密な編集、統合されたスマートアクション、および強力なカスタマイズオプション。

このチュートリアルを終了するまでに、動作する Web アプリケーションと、開発スタイルに適応する個人用 AI コーディング設定の両方が得られます。

<div class="docs-action" data-show-in-doc="true" data-show-in-sidebar="true" title="サンプルアプリを作成">
VS Code のチャットを使用してサンプルアプリケーションを一度に生成します。

* [VS Code で開く](vscode://GitHub.Copilot-Chat/chat?agent=agent%26prompt=%23newWorkspace%20task%20manager%20web%20application%20with%20the%20ability%20to%20add%2C%20delete%2C%20and%20mark%20tasks%20as%20completed.%20Add%20the%20code%2C%20custom%20instructions%2C%20and%20all%20custom%20agent%20definitions%20to%20this%20new%20workspace%20as%20described%20in%20https%3A%2F%2Fcode.visualstudio.com%2Fdocs%2Fcopilot%2Fgetting-started%0AAsk%20the%20user%20which%20tech%20stack%20they%20want%20to%20use.)

</div>

## 前提条件

* マシンにインストールされた VS Code。[Visual Studio Code ウェブサイト](https://code.visualstudio.com/)からダウンロードしてください。

* GitHub Copilot へのアクセス。以下の手順に従って[VS Code で GitHub Copilot をセットアップ](/docs/copilot/setup.md)します。

    > [!TIP]
    > Copilot サブスクリプションがない場合は、VS Code 内から直接 Copilot for free を使用するサインアップし、インライン候補とチャットインタラクションの月間制限を取得できます。

## ステップ 1：インライン候補を体験

AI を活用したインライン候補は入力時に表示され、コードをより速く、より少ないエラーで記述するのに役立ちます。タスクマネージャーの基盤の構築を開始しましょう。

1. プロジェクト用の新しいフォルダを作成し、VS Code で開きます。

1. `index.html` という新しいファイルを作成します。

1. 以下の入力を開始すると、入力時に VS Code はインライン候補（_ゴーストテキスト_）を提供します：

    ```html
    <!DOCTYPE html>
    ```

    ![Copilot が HTML 構造をインライン候補として提案するスクリーンショット。](./images/getting-started/html-completion.png)

    大規模言語モデルは[確定的ではない](/docs/copilot/concepts/language-models.md#key-characteristics)ため、異なる候補が表示される場合があります。

1. `kbstyle(Tab)` を押して候補を受け入れます。

    おめでとうございます。最初の AI を活用したインライン候補を受け入れました。

1. HTML 構造の構築を続行します。`<body>` タグ内で入力を開始します：

    ```html
    <div class="container">
        <h1>My Task Manager</h1>
        <form id="task-form">
    ```

    VS Code がアプリケーション構造を構築する際に、関連する HTML 要素を引き続き提案する方法に注意してください。

1. 複数の候補が表示される場合は、ゴーストテキストの上にマウスを置いてナビゲーション制御を表示するか、`kb(editor.action.inlineSuggest.showNext)` および `kb(editor.action.inlineSuggest.showPrevious)` を使用してオプションをループします。

    ![インライン候補ナビゲーション制御を示すスクリーンショット。](./images/getting-started/inline-suggestion-navigation.png)

インライン候補は入力時に自動的に動作し、パターンとプロジェクトのコンテキストから学習します。ボイラープレートコード、HTML 構造、および繰り返しパターンの記述に特に役立ちます。

## ステップ 2：エージェントで完全な機能を構築

AI エージェントは VS Code の最も強力な AI 機能です。自然言語プロンプトが与えられると、複雑な機能を複数のファイル全体で自律的に計画および実装します。それらを使用してタスクマネージャーアプリケーションのコア機能を作成しましょう。

1. `kb(workbench.action.chat.open)` を押すか、VS Code タイトルバーのチャットアイコンを選択してチャットビューを開きます。

    チャットビューは、自然言語プロンプトを使用して AI と相互作用する場所です。継続的な会話を行い、要求を反復的に改善してより良い結果を得ることができます。

1. エージェントドロップダウンメニューで**エージェント**を選択して、AI が要求を end-to-end で独立して実装するようにします。

    ![チャットビューのエージェントピッカーを示すスクリーンショット。](./images/getting-started/agent-mode-selection.png)

    > [!IMPORTANT]
    > エージェントオプションが表示されない場合は、VS Code の設定でエージェントが有効になっていることを確認します（`setting(chat.agent.enabled)`）。組織がエージェントを無効にしている場合もあります。管理者に連絡してこの機能を有効にしてください。

1. 以下のプロンプトを入力し、`kbstyle(Enter)` を押します。エージェントは要求を分析し、ソリューションの実装を開始します。

    ```prompt
    Create a complete task manager web application with the ability to add, delete, and mark tasks as completed. Include modern CSS styling and make it responsive. Use semantic HTML and ensure it's accessible. Separate markup, styles, and scripts into their own files.
    ```

    エージェントが要求を実装するために必要なファイルとコードを生成する様子を観察します。`index.html` ファイルを更新し、スタイル用に `styles.css` ファイルを作成し、機能用に `script.js` ファイルを作成する必要があります。

    > [!TIP]
    > 異なる言語モデルには異なる強度がある場合があります。チャットビューのモデルドロップダウンを使用して言語モデル間を切り替えます。

1. 生成されたファイルを確認し、**保持**を選択してすべての変更を受け入れます。

1. VS Code の統合ブラウザで `index.html` ファイルを開き、ファイルを右クリックして**プレビューを表示**を選択します。タスクを追加し、完了としてマークし、削除できます。

1. 次に、追加機能を追加しましょう。チャット入力ボックスに以下のプロンプトを入力します：

    ```prompt
    Add a filter system with buttons to show all tasks, only completed tasks, or only pending tasks. Update the styling to match the existing design.
    ```

    エージェントが複数のファイル全体での変更を調整して、この機能を完全に実装する方法に注意してください。

エージェントは高レベルの要件を理解し、それを動作するコードに変換することに優れています。新しい機能の実装、コードの大規模なセクションのリファクタリング、または最初からアプリケーション全体の構築に最適です。

## ステップ 3：インラインチャットで正密な調整を行う

エージェントが大きな機能を処理する一方、エディターのインラインチャットはファイル内の特定のコードセクションへの対象となった改善に最適です。それを使用してタスクマネージャーアプリを拡張しましょう。

1. JavaScript ファイルを開き、新しいタスクを追加するコードを見つけます。

1. コードブロックを選択してから `kb(inlinechat.start)` を押してエディターのインラインチャットを開きます。

    ![選択したコードブロックのインラインチャットの開始を示すスクリーンショット。](./images/getting-started/inline-chat-start.png)

    > [!NOTE]
    > 大規模言語モデルは確定的ではないため、正確なコードが異なる場合があります。

1. 以下のプロンプトを入力します：

    ```text
    Add input validation to prevent adding empty tasks and trim whitespace from task text.
    ```

    インラインチャットが選択したコードに特に焦点を当て、対象となった改善を行う方法に注意してください。

    ![選択した関数への検証の追加を示すインラインチャットのスクリーンショット。](./images/getting-started/inline-chat-validation.png)

1. 変更を確認し、**保持**を選択して適用します。

エディターのインラインチャットは、エラー処理の追加、個別の関数のリファクタリング、またはバグの修正など、より広いコードベースに影響を与えることなく、小さなフォーカスされた変更を行うのに最適です。

## ステップ 4：AI 体験を個人用に設定

チャットをカスタマイズすると、特定のニーズとコーディングスタイルに合わせて機能するようになります。カスタム指示を設定し、特別なカスタムエージェントを構築できます。プロジェクト用の完全なパーソナライゼーション設定を作成しましょう。

### カスタム指示を作成

カスタム指示は、AI にコーディングの外観と標準について伝えます。これらはすべてのチャットインタラクションに自動的に適用されます。

1. プロジェクトルートに `.github` という新しいフォルダを作成します。

1. `.github` フォルダ内に `copilot-instructions.md` というファイルを作成します。

1. 次の内容を追加します：

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

1. ファイルを保存します。これらの指示はこのプロジェクト内のすべてのチャットインタラクションに適用されます。

1. エージェントに新しい機能を追加するよう求めてカスタム指示をテストします：

    ```prompt
    Add a dark mode toggle button to the task manager.
    ```

    生成されたコードが指定したガイドラインに従う方法に注意してください。VS Code はファイルタイプに対する指示の適用など、より高度なカスタム指示をサポートしています。

> [!TIP]
> チャットの `/init` スラッシュコマンドを使用して、プロジェクトの構造とコーディングパターンに基づいてカスタム指示を自動生成します。既存のコードベースがある場合は、AI 支援の準備をするのに役立ちます。

### コードレビュー用のカスタムエージェントを作成

カスタムエージェントは特定のタスク用に特別な AI ペルソナを作成します。コードを分析し、コードに対するフィードバックを提供することに焦点を当てた「Code Reviewer」エージェントを作成しましょう。カスタムエージェント定義では、AI の役割、特定のガイドライン、および使用できるツールを定義できます。

1. コマンドパレットを開き、**Chat: New Custom Agent** コマンドを実行します。

1. 場所として `.github/agents` を選択します。

    このオプションは、カスタムエージェントをワークスペースに追加し、プロジェクトを開いたときに他のチームメンバーが使用できるようにします。

1. カスタムエージェントに「Reviewer」という名前を付けます。これにより、`.github/agents` フォルダに `Reviewer.agent.md` という新しいファイルが作成されます。

1. ファイルの内容を次の内容に置き換えます。このカスタムエージェントはコード変更を許可していないことに注意してください。

    ```markdown
    ---
    name: 'Reviewer'
    description: 'Review code for quality and adherence to best practices.'
    tools: ['vscode/askQuestions', 'vscode/vscodeAPI', 'read', 'agent', 'search', 'web']
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

1. ファイルを保存します。チャットビューで、エージェントピッカーからこのカスタムエージェントを選択できます。

    ![エージェントピッカーの Reviewer カスタムエージェントを示すスクリーンショット。](./images/getting-started/custom-mode-dropdown.png)

1. エージェントピッカーから**Reviewer**を選択し、次のプロンプトを入力してカスタムエージェントをテストします：

    ```prompt-Reviewer
    Review my full project
    ```

   AI がコードレビュアーのように動作し、改善のための分析と提案を提供する方法に注意してください。

    ![カスタムレビュアーエージェントがコードを分析するスクリーンショット。](./images/getting-started/custom-reviewer-mode.png)

## ステップ 5：スマートアクションを使用して事前構築された AI 支援を使用

スマートアクションは VS Code のインターフェースに直接統合された AI 機能を提供し、開発ワークフローにシームレスに接続します。チャットインタラクションとは異なり、スマートアクションは最も必要な場所に文脈的に表示されます。例として、コミットメッセージの生成を見てみましょう。

1. `kb(workbench.view.scm)` を押すか、アクティビティバーのソース管理アイコンを選択して、**ソース管理**ビューを開きます。

1. プロジェクト用に Git リポジトリをまだ初期化していない場合は、ソース管理ビューで**リポジトリの初期化**を選択して実行します。

1. コミットするファイルの横にある**+**ボタンを選択して変更をステージします。

1. **スパークルアイコン**を選択して、ステージされた変更に基づいてコミットメッセージを生成します。

    AI はステージされた変更を分析し、従来のコミット標準に従う説明的なコミットメッセージを生成します。AI は以下を考慮します：

    * 変更されたファイル
    * 変更の性質（機能の追加、バグ修正、リファクタリング）
    * 変更の範囲と影響

    ![ソース管理ビューで生成されたコミットメッセージを示すスクリーンショット。](./images/getting-started/generated-commit-message.png)

1. 生成されたメッセージを確認します。満足している場合は、コミットに進みます。別のスタイルまたはフォーカスが必要な場合は、スパークルアイコンを再度選択して別のメッセージを生成します。

コミットメッセージ生成などのスマートアクションは、AI がチャットインターフェースへのコンテキストの切り替えを必要とすることなく、既存のワークフローにどのように自然に統合されるかを示しています。VS Code には、デバッグ、テストなどに役立つ他の多くのスマートアクションがあります。

## 次のステップ

おめでとうございます。完全なタスク管理アプリケーションを構築し、VS Code のコア機能全体で AI を効果的に操作する方法を学習しました。

以下のカスタマイズオプションを探索することで、AI の機能をさらに向上させることができます：

* 計画、デバッグ、ドキュメント化などのさまざまなタスク用に、より特別なエージェントを追加します。
* 特定のプログラミング言語またはフレームワーク用のカスタム指示を作成します。
* MCP（Model Context Protocol）サーバーまたは VS Code 拡張機能の追加ツールで AI の機能を拡張します。

## 関連リソース

* [GitHub Copilot の仕組み](/docs/copilot/concepts/overview.md)：Copilot の機能の背後にある主要な概念、用語、およびアーキテクチャ

* [エージェントチュートリアル](/docs/copilot/agents/agents-tutorial.md)：異なるエージェントタイプを操作するためのハンズオンチュートリアル

* [AI 機能を使用するためのチートシート](/docs/copilot/reference/copilot-vscode-features.md)- VS Code のすべての GitHub Copilot 機能のクイックリファレンス

* [チャットドキュメント](/docs/copilot/chat/copilot-chat.md)- VS Code での自律型コーディングへの深い掘り下げ

* [カスタマイズガイド](/docs/copilot/customization/overview.md)- 高度なパーソナライゼーション技術

* [MCP ツール](/docs/copilot/customization/mcp-servers.md)- 外部 API およびサービスでエージェントを拡張

