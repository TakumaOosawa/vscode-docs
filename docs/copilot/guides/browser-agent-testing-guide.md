---
ContentId: 3f9e2b7d-6a8c-4d1e-9f2a-8c4b5d7e9f1a
DateApproved: 3/9/2026
MetaDescription: VS Codeのブラウザーエージェントツールを使用して、AIでWebアプリケーションを構築し、自動的にテストする方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- ai
- copilot
- agents
- browser
- integrated browser
- testing
- automation
- guide
- tutorial
---
# ブラウザーエージェントツールでWebアプリを構築・テストする

ブラウザーエージェントツールにより、AIがクローズドな開発ループでWebアプリケーションを自律的に構築・検証できます。エージェントはHTML、CSS、JavaScriptを作成し、統合ブラウザーでアプリを開き、機能を検証するために操作し、コンソールエラーと視覚検査を通じて問題を特定し、手動による介入なしに問題を修正できます。

このガイドでは、ブラウザーエージェントツールを使用して電卓アプリを構築し、エージェントが自動テストを通じてバグを発見・修正する様子を確認します。

> [!NOTE]
> ブラウザーエージェントツールは現在実験段階であり、将来のリリースで変更される可能性があります。

## 前提条件

このガイドを完了するには、以下が必要です:

* [コンピューターにインストールされたVisual Studio Code](/download)
* [GitHub Copilotサブスクリプション](/docs/copilot/setup.md)
* `setting(workbench.browser.enableChatTools)`設定でブラウザーエージェントツールが有効になっていること

## ブラウザーエージェントツールの仕組み

ブラウザーエージェントツールを有効にすると、エージェントは統合ブラウザー内のページを読み取り、操作するツールにアクセスできます。これらのツールには以下が含まれます:

* **ページナビゲーション:** `openBrowserPage`、`navigatePage`
* **ページコンテンツと外観:** `readPage`、`screenshotPage`
* **ユーザーインタラクション:** `clickElement`、`hoverElement`、`dragElement`、`typeInPage`、`handleDialog`
* **カスタムブラウザーオートメーション:** `runPlaywrightCode`

デフォルトでは、エージェントが開いたページはプライベートなメモリ内セッションで実行され、他のブラウザータブとクッキーやストレージを共有しません。これによりエージェントがアクセスできるブラウジングデータを制御できます。

[VS Codeの統合ブラウザー](/docs/debugtest/integrated-browser.md)の詳細を確認してください。

## ステップ1: エージェント向けブラウザーツールを有効にする

エージェントがブラウザーツールを使用する前に、チャットツールピッカーで明示的に有効にする必要があります。

1. チャットビュー（`kb(workbench.action.chat.open)`）を開き、エージェントドロップダウンから**Agent**を選択します。

1. チャット入力エリアの**Tools**ボタンを選択してツールピッカーを開きます。

1. すべてのブラウザーツールが有効になっていることを確認します（**Built-in** > **Browser**以下にグループ化されています）。

    ![チャットツールピッカーのスクリーンショット。ブラウザーツールが有効になっています。](../images/browser-agent-testing-guide/enable-browser-tools.png)

エージェントはこれらのツールを使用してWebページを操作できるようになりました。

## ステップ2: エージェントに電卓を構築させる

ブラウザーツールを有効にした状態で、エージェントに簡単な電卓アプリケーションを作成させます。

1. 新しいプロジェクトフォルダーを作成し、VS Codeで開きます。

1. チャットビューで、以下のプロンプトを入力します:

    ```prompt
    Create a calculator with buttons for digits 0-9, operations (add, subtract, multiply, divide), clear, and equals. Use HTML, CSS, and JavaScript. Style it with a clean, modern design.
    ```

1. エージェントが`index.html`、`styles.css`、`script.js`を作成する際に、生成されたファイルを確認します。

1. **Keep**を選択してファイルをワークスペースに保存します。

エージェントが電卓アプリケーションの基本構造を構築しました。

## ステップ3: エージェントに電卓をテストさせる

次に、エージェントに統合ブラウザーで電卓を開き、正しく動作することを確認させます。

1. チャットビューで、以下のプロンプトを入力します:

    ```prompt
    Open the calculator in the browser and test if all the operations work correctly.
    ```

1. エージェントが統合ブラウザーで`index.html`を開き、ページコンテンツを解析して構造を理解し、クリックをシミュレートして結果を確認することで、各ボタンと操作を体系的にテストする様子を観察します。

    <video src="../images/browser-agent-testing-guide/agent-testing-calculator.mp4" title="エージェントが統合ブラウザーで電卓をテストしている様子のビデオ。" autoplay loop controls muted></video>

エージェントは正しく動作する操作を報告し、発見したすべての問題を特定します。

## ステップ4: エージェントがデバッグして問題を修正する様子を観察する

エージェントがテスト中にバグを発見した場合、自動的に問題を分析し、修正を実装します。

1. ゼロで除算するチェックを削除してバグを導入しましょう:

    ```javascript
    function calculate() {
        if (!operator || shouldReset) return;

        const a = parseFloat(previous);
        const b = parseFloat(current);
        let result;

        switch (operator) {
        case '+': result = a + b; break;
        case '-': result = a - b; break;
        case '*': result = a * b; break;
        case '/': result = a / b; break;
    }
    ```

1. エージェントに除算操作をテストして、見つかった問題を修正させます:

    ```prompt
    Verify the division operation works correctly. If you find any issues, fix them.
    ```

1. エージェントがゼロで除算する場合のエラーを検出し、コードを分析・修正して、バグ修正を検証する様子を観察します。

エージェントはブラウザーオートメーションを使用して、完全な開発サイクル(構築、テスト、デバッグ、修正)を完了しました。

## ステップ5: ブラウザーページをエージェントと共有する(オプション)

また、手動でWebページを開き、分析または操作のためにエージェントと明示的に共有することもできます。デフォルトでは、エージェントは自分で開いたWebページとのみ相互作用できます。

1. コマンドパレット(`kb(workbench.action.showCommands)`)から**Browser: Open Integrated Browser**コマンドを実行して統合ブラウザーを開きます。

1. 分析または操作させたいWebページに移動します。

1. ブラウザーツールバーの**Share with Agent**ボタンを選択します。

    ブラウザータブの視覚インジケーターは、ページがエージェントと積極的に共有されていることを示します。

1. 共有ページでアクションを実行するようエージェントに依頼します:

    ```prompt
    What is the main heading on this page? Click the first link and tell me where it goes.
    ```

エージェントは共有ページにアクセスでき、あなたに代わって操作を実行できます。完了したら、**Share with Agent**ボタンをもう一度選択してアクセスを取り消します。

> [!TIP]
> 共有ページはクッキーとログイン状態を含む既存のブラウザーセッションを使用します。エージェントが開いたページは分離された一時的なセッションを使用するため、他のブラウザータブとクッキーやストレージを共有しません。

## これらのシナリオを試してみる

ブラウザーエージェントツールの仕組みを理解したので、これらのシナリオを試して、さまざまなユースケースを探索してください:

* **フォーム検証テスト**: エージェントに検証ルール、エラーメッセージ、正常な送信を検証させます。コンタクトフォームを構築・テストします。

* **レスポンシブレイアウト検証**: エージェントにさまざまなビューポートサイズでページをスクリーンショットして、レスポンシブ動作を検証させます(例: ナビゲーションメニュー付きのランディングページ)。

* **認証フロー テスト**: エージェントにログインページの認証情報検証、エラー処理、正常なリダイレクトをテストさせます。

* **インタラクティブ機能テスト**: エージェントにユーザーインタラクションと状態管理を検証させます。

* **アクセシビリティ監査**: エージェントにWebページの代替テキストの不備、見出しの階層、キーボードナビゲーション、色コントラスト比を確認させます。

## 関連リソース

* [統合ブラウザー](/docs/debugtest/integrated-browser.md)
* [VS CodeのAIの中核概念](/docs/copilot/concepts/overview.md)
* [エージェント概要](/docs/copilot/agents/overview.md)
* [Copilotでテストする](/docs/copilot/guides/test-with-copilot.md)

