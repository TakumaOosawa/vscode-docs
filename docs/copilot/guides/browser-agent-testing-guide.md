---
ContentId: 3f9e2b7d-6a8c-4d1e-9f2a-8c4b5d7e9f1a
DateApproved: 3/9/2026
MetaDescription: VS Codeのブラウザーエージェントツールを使用して、AIでWebアプリケーションを構築し、自動的にテストする方法を学習します。
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
# ブラウザーエージェントツールでWebアプリを構築およびテストする

ブラウザーエージェントツールを使用すると、AIはクローズドな開発ループ内でWebアプリケーションを自律的に構築および検証できます。エージェントはHTML、CSS、JavaScriptを作成し、統合ブラウザーでアプリを開き、機能を検証するために操作し、コンソールエラーと視覚的検査を通じて問題を特定し、手動操作なしで問題を修正できます。

このガイドでは、ブラウザーエージェントツールを使用して計算機アプリを構築し、エージェントが自動テストを通じてバグを発見および修正する様子を確認します。

> [!NOTE]
>ブラウザーエージェントツールは現在実験的であり、今後のリリースで変更される可能性があります。

## 前提条件

このガイドを完了するには、次が必要です:

* [コンピューターにVisual Studio Codeをインストール](/download)
* [GitHub Copilotサブスクリプション](/docs/copilot/setup.md)
* `setting(workbench.browser.enableChatTools)`設定を有効にしたブラウザーエージェントツール

## ブラウザーエージェントツールの仕組み

ブラウザーエージェントツールを有効にすると、エージェントは統合ブラウザー内のページを読み取り、操作できるツールにアクセスできます。これらのツールには次が含まれます:

* **ページナビゲーション:** `openBrowserPage`、`navigatePage`
* **ページコンテンツと外観:** `readPage`、`screenshotPage`
* **ユーザー操作:** `clickElement`、`hoverElement`、`dragElement`、`typeInPage`、`handleDialog`
* **カスタムブラウザー自動化:** `runPlaywrightCode`

デフォルトでは、エージェントによって開かれるページはプライベートなメモリ内セッションで実行され、他のブラウザータブとCookieやストレージを共有しません。これにより、エージェントがアクセスできるブラウジングデータを制御できます。

[VS Codeの統合ブラウザー](/docs/debugtest/integrated-browser.md)の詳細をご覧ください。

## ステップ1: エージェント用のブラウザーツールを有効にする

エージェントがブラウザーツールを使用する前に、チャットツールピッカーで明示的に有効にする必要があります。

1. チャットビュー(`kb(workbench.action.chat.open)`)を開き、[エージェント]ドロップダウンから**エージェント**を選択します。

1. チャット入力領域の**ツール**ボタンを選択して、ツールピッカーを開きます。

1. すべてのブラウザーツールが有効になっていることを確認します(これらは**組み込み** > **ブラウザー**の下にグループ化されています)。

    ![ブラウザーツールが有効になっているチャットツールピッカーを示すスクリーンショット。](../images/browser-agent-testing-guide/enable-browser-tools.png)

エージェントはこれらのツールを使用してWebページと対話できるようになりました。

## ステップ2: エージェントに計算機を構築するよう依頼する

ブラウザーツールを有効にしたら、エージェントに単純な計算機アプリケーションの作成を依頼します。

1. 新しいプロジェクトフォルダーを作成し、VS Codeで開きます。

1. チャットビューで、次のプロンプトを入力します:

    ```prompt
    Create a calculator with buttons for digits 0-9, operations (add, subtract, multiply, divide), clear, and equals. Use HTML, CSS, and JavaScript. Style it with a clean, modern design.
    ```

1. エージェントが`index.html`、`styles.css`、`script.js`を作成するときに、生成されたファイルを確認します。

1. **保持**を選択してファイルをワークスペースに保存します。

エージェントは計算機アプリケーションの基本構造を構築しました。

## ステップ3: エージェントに計算機をテストさせる

次に、エージェントに統合ブラウザーで計算機を開き、正しく動作することを確認するよう依頼します。

1. チャットビューで、次のプロンプトを入力します:

    ```prompt
    Open the calculator in the browser and test if all the operations work correctly.
    ```

1. エージェントが統合ブラウザーで`index.html`を開き、ページコンテンツを解析して構造を理解し、クリックを模擬してボタンと演算を体系的にテストし、結果を確認する様子を見ます。

    <video src="../images/browser-agent-testing-guide/agent-testing-calculator.mp4" title="統合ブラウザーで計算機をテストするエージェントを示すビデオ。" autoplay loop controls muted></video>

エージェントは、正しく動作する演算と発見した問題を報告します。

## ステップ4: エージェントがデバッグおよび修正するのを見る

エージェントがテスト中にバグを発見した場合、問題を自動的に分析し、修正を実装します。

1. ゼロ除算チェックを削除してバグを導入しましょう:

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

1. エージェントに除算演算をテストし、見つかった問題を修正するよう依頼します:

    ```prompt
    Verify the division operation works correctly. If you find any issues, fix them.
    ```

1. エージェントがゼロによる除算でエラーが発生し、コードを分析および修正し、最後にバグ修正を検証する様子を見ます。

エージェントは完全な開発サイクルを完了しました: ブラウザー自動化を使用して構築、テスト、デバッグ、修正します。

## ステップ5: ブラウザーページをエージェントと共有する(オプション)

また、Webページを手動で開き、明示的にエージェントと共有して分析または操作することもできます。デフォルトでは、エージェントは自身が開いたWebページでのみ操作できます。

1. コマンドパレット(`kb(workbench.action.showCommands)`)から**ブラウザー: 統合ブラウザーを開く**コマンドを実行して統合ブラウザーを開きます。

1. エージェントに分析または操作したいWebページに移動します。

1. ブラウザーツールバーの**エージェントと共有**ボタンを選択します。

    ブラウザータブの視覚的インジケーターがページがアクティブにエージェントと共有されていることを示します。

1. エージェントに共有ページで操作を実行するよう依頼します:

    ```prompt
    What is the main heading on this page? Click the first link and tell me where it goes.
    ```

エージェントは共有ページにアクセスでき、あなたに代わって操作を実行できます。完了したら、**エージェントと共有**ボタンを再度選択してアクセスを取り消します。

> [!TIP]
>共有ページはCookieとログイン状態を含む既存のブラウザーセッションを使用します。エージェントが開くページは分離された一時的なセッションを使用するため、他のブラウザータブとCookieやストレージを共有しません。

## これらのシナリオを試す

ブラウザーエージェントツールの仕組みを理解したら、さまざまなユースケースを探索するためにこれらのシナリオを試してください:

* **フォーム検証テスト**: エージェントに検証ルール、エラーメッセージ、および正常な送信を確認するために、問い合わせフォームを構築してテストさせる

* **レスポンシブレイアウト検証**: エージェントに異なるビューポートサイズでページのスクリーンショットを撮ってもらい、レスポンシブ動作を確認する(例: ナビゲーションメニュー付きのランディングページ)

* **認証フロー分析テスト**: エージェントに認証情報検証、エラー処理、ログインページでの正常なリダイレクトをテストさせる

* **インタラクティブ機能テスト**: エージェントにユーザー操作と状態管理を検証させる

* **アクセシビリティ監査**: エージェントにAltテキストの欠落、見出し階層、キーボード操作、色対比の問題についてWebページをチェックするよう依頼する

## 関連リソース

* [統合ブラウザー](/docs/debugtest/integrated-browser.md)
* [VS Codeの AI の核となる概念](/docs/copilot/concepts/overview.md)
* [エージェントの概要](/docs/copilot/agents/overview.md)
* [Copilotでテストする](/docs/copilot/guides/test-with-copilot.md)

