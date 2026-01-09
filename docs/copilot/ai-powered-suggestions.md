---
ContentId: 7ab2cd6c-45fd-4278-a6e8-1c9e060593ea
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでのGitHub CopilotによるAI搭載のインライン提案でコーディングを強化します。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords: [nes, suggestions]
---
# VS CodeでのGitHub Copilotによるインライン提案

GitHub CopilotはAI搭載のペアプログラマーとして機能し、コード、コメント、テストなどを補完するためのインライン提案を自動的に提供します。コードを書いている最中にエディター内で直接提案を行い、幅広いプログラミング言語やフレームワークに対応しています。

Copilotからは2種類のインライン提案があり、どちらもあなたのコーディングスタイルに合わせ、既存のコードを考慮に入れています：

* **ゴーストテキストの提案** - エディターで入力を始めると、Copilotは現在のカーソル位置に薄い*ゴーストテキスト*の提案を表示します。

* **次の編集提案** - Copilot Next Edit Suggestions（Copilot NES）で次のコード編集を予測します。あなたが行っている編集に基づき、NESは次に編集したい場所と、その内容の両方を予測します。

## はじめに

1. GitHub Copilot拡張機能をインストールします。

    > <a class="install-extension-btn" href="vscode:extension/GitHub.copilot?referrer=docs-copilot-ai-powered-suggestions">GitHub Copilot拡張機能をインストールする</a>

1. Copilotを使用するにはGitHubアカウントでサインインします。

    > [!TIP]
    > Copilotのサブスクリプションをまだお持ちでない場合、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップすることでCopilotを無料で使用でき、月次制限付きでインライン提案とチャット機能を利用できます。

1. [Copilotクイックスタート](/docs/copilot/getting-started.md)でVS CodeでのCopilotの主な機能を確認してください。

## 最初の提案を取得する

Copilotは入力中に薄い*ゴーストテキスト*の提案を提供します：現在の行の補完であったり、新しいコードブロック全体であったりします。提案のすべて、または一部を受け入れることも、入力を続けて提案を無視することもできます。

次の例では、Copilotが薄い*ゴーストテキスト*を使用してJavaScript関数`calculateDaysBetweenDates`の実装を提案していることに注目してください：

![JavaScript ghost text suggestion.](images/inline-suggestions/js-suggest.png)

インライン提案が表示されたら、`kbstyle(Tab)`キーで受け入れることができます。

Copilotは、すでにコードにあるコーディングスタイルと同じスタイルを適用しようとします。次の例では、Copilotが`add`メソッドの入力パラメータの命名規則を、提案された`subtract`メソッドにも適用していることに注目してください。

![JavaScript ghost text suggestion.](images/inline-suggestions/ts-suggest-parameter-names.png)

### 提案の一部を受け入れる

GitHub Copilotからの提案全体を受け入れたくない場合があるかもしれません。キーボードショートカット`kb(editor.action.inlineSuggest.acceptNextWord)`を使用して、提案の次の単語、または次の行を受け入れることができます。

### 代替の提案

入力に対して、Copilotは複数の代替提案を提供する場合があります。提案の上にホバーすることで、他の提案に切り替えることができます。

![Hovering over inline suggestions enables you to select from multiple suggestions](images/inline-suggestions/copilot-hover-highlight.png)

### コードコメントから提案を生成する

Copilotに提案を任せる代わりに、コードコメントを使用して期待するコードについてのヒントを提供することができます。たとえば、使用するアルゴリズムや概念の種類（例：「再帰を使用する」や「シングルトンパターンを使用する」）、またはクラスに追加するメソッドやプロパティを指定できます。

次の例は、メソッドとプロパティに関する情報を提供して、学生を表すTypeScriptクラスを作成するようにCopilotに指示する方法を示しています：

![Use code comments to let Copilot generate a Student class in TypeScript with properties and methods.](images/inline-suggestions/ts-suggest-code-comment.png)

## 次の編集提案

ゴーストテキストの提案は、コードの一部を自動補完するのに優れています。しかし、コーディング活動のほとんどは既存のコードの編集であるため、インライン提案の自然な進化として、カーソル位置だけでなく、より離れた場所での編集も支援することになります。編集は多くの場合、単独で行われるものではありません。さまざまなシナリオでどのような編集が必要かという論理的な流れがあります。Next Edit Suggestions（Copilot NES）はこの進化形です。

<video src="./images/inline-suggestions/nes-video.mp4" title="Video showing next edit suggestions in action on a Point typescript class." autoplay loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

あなたが行っている編集に基づき、次の編集提案は次に編集したい場所とその内容の両方を予測します。Copilot NESはフローを維持するのに役立ち、現在の作業に関連する将来の変更を提案します。`kbstyle(Tab)`を押すだけで素早く移動してCopilotの提案を受け入れることができます。提案は、潜在的な変更のスコープに応じて、単一のシンボル、行全体、または複数行に及ぶ場合があります。

Copilot NESを開始するには、VS Code設定`setting(github.copilot.nextEditSuggestions.enabled)`を有効にします。

### 編集提案への移動と受け入れ

`kbstyle(Tab)`キーを使用して提案されたコード変更に素早く移動できるため、次に必要な編集を見つける時間を節約できます（ファイルや参照を手動で検索する必要はありません）。その後、もう一度`kbstyle(Tab)`キーを押すことで提案を受け入れることができます。

ガターにある矢印は、編集提案が利用可能かどうかを示します。矢印は、現在のカーソル位置に対する次の編集提案の位置を示します。

矢印の上にホバーすると、編集提案メニューが表示され、キーボードショートカットや設定構成が含まれています：

![Copilot NES gutter menu expanded](./images/inline-suggestions/gutter-menu-highlighted-updated.png)

> [!IMPORTANT]
> [VS Code Vim拡張機能](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)ユーザーの場合は、NESとのキーバインドの競合を避けるために、最新バージョンの拡張機能を使用してください。

### 編集提案による注意散漫の軽減

デフォルトでは、編集提案はガターの矢印で示され、コード変更はエディターに表示されます。`setting(editor.inlineSuggest.edits.showCollapsed)`設定を有効にすると、`kbstyle(Tab)`キーを押して提案に移動するか、ガターの矢印にホバーするまで、エディター内のコード変更を表示しないようにできます。または、ガターの矢印にホバーして、メニューから**Show Collapsed**オプションを選択します。

### 次の編集提案のユースケース

**間違いの発見と修正**

* **Copilotはタイプミスのような単純な間違いを支援します。** `cont x = 5`や`conts x = 5`のように文字が欠けていたり入れ替わっていたりする場合（正しくは`const x = 5`）、修正を提案してくれます。

    ![NES fixing a typo from "conts" to "const"](./images/inline-suggestions/nes-typo.png)

* **Copilotは論理的なより難しい間違いも支援できます**、たとえば反転した三項演算子など：

    ![NES fixing a ternary logic mistake](./images/inline-suggestions/nes-ternary-logic.png)

    あるいは`||`の代わりに`&&`を使用すべきだった比較など：

    ![NES fixing an if statement mistake](./images/inline-suggestions/nes-de-morgan.png)

**意図の変更**

* **Copilotは新しい意図の変更に合わせて、コードの残りの部分への変更を提案します。** たとえば、クラスを`Point`から`Point3D`に変更すると、Copilotはクラス定義に`z`変数を追加することを提案します。その変更を受け入れると、Copilot NESは次に距離計算に`z`を追加することを推奨します：

    ![NES gif for updating Point to Point3D](./images/inline-suggestions/nes-point.png)

**リファクタリング**

* **ファイル内で変数の名前を一度変更すると、Copilotは他のすべての場所でも更新するように提案します。** 新しい名前や命名パターンを使用すると、Copilotは後続のコードも同様に更新するように提案します。

    ![Copilot NES suggesting change after updating function name](./images/inline-suggestions/nes-rename.png)

* **コードスタイルの整合**。コードをコピー＆ペーストした後、Copilotはペーストが行われた現在のコードに合わせて調整する方法を提案します。

## インライン提案の有効化または無効化

インライン提案は、すべての言語または特定の言語に対して有効または無効にすることができます。インライン提案を有効または無効にするには、ステータスバーのCopilotメニューを選択し、インライン提案を有効または無効にするオプションをオンまたはオフにします。特定の言語に対するインライン提案を無効にするオプションは、アクティブなエディターの言語に依存します。

![Screenshot of the Copilot menu in the Status Bar with Snooze and Cancel Snooze buttons.](images/inline-suggestions/snooze-code-completions.png)

または、設定エディターで`setting(github.copilot.enable)`設定を変更します。インライン提案を有効または無効にしたい言語ごとにエントリを追加します。すべての言語でインライン提案を有効または無効にするには、`*`の値を`true`または`false`に設定します。

エディターですべてのインライン提案を一時的に無効にするには、ステータスバーのCopilotメニューを選択し、**Snooze**ボタンを選択してスヌーズ時間を5分ずつ増やします。インライン提案を再開するには、Copilotメニューの**Cancel Snooze**ボタンを選択します。

または、コマンドパレットの**Snooze Inline Suggestions**および**Cancel Snooze Inline Suggestions**コマンドを使用します。

## 提案のためのAIモデルの変更

大規模言語モデル（LLM）はそれぞれ異なる種類のデータでトレーニングされており、機能や強みが異なる場合があります。VS Codeで[異なるAI言語モデルの選択](/docs/copilot/customization/language-models.md)を行う方法について詳しく学んでください。

エディターでゴーストテキストの提案を生成するために使用される言語モデルを変更するには：

1. コマンドパレットを開きます（`kbstyle(F1)`）。

1. **change completions model**と入力し、**GitHub Copilot: Change Completions Model**コマンドを選択します。

1. ドロップダウンメニューから、使用したいモデルを選択します。

> [!NOTE]
> 利用可能なモデルのリストは異なり、時間とともに変更される可能性があります。モデルピッカーには複数のモデルが表示されない場合があり、プレビューモデルや追加のインライン提案モデルは、リリースされた場合に利用可能になります。Copilot BusinessまたはEnterpriseユーザーの場合、管理者がGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインすることで、組織に対して特定のモデルを有効にする必要があります。

## ヒントとコツ

### コンテキスト

関連性の高いインライン提案を提供するために、Copilotはエディター内の現在および開いているファイルを調べてコンテキストを分析し、適切な提案を作成します。Copilotを使用している間、VS Codeで関連ファイルを開いておくことは、このコンテキストを設定するのに役立ち、Copilotがプロジェクトの全体像を把握できるようになります。

## 設定

### ゴーストテキスト提案の設定

* `setting(github.copilot.enable)` - すべての言語または特定の言語に対してインライン補完を有効または無効にします。

* `setting(editor.inlineSuggest.fontFamily)` - インライン補完のフォントを設定します。

* `setting(editor.inlineSuggest.showToolbar)` - インライン補完に表示されるツールバーを有効または無効にします。

* `setting(editor.inlineSuggest.syntaxHighlightingEnabled)` - インライン補完のシンタックスハイライトを有効または無効にします。

### 次の編集提案の設定

* `setting(github.copilot.nextEditSuggestions.enabled)` - Copilot Next Edit Suggestions（Copilot NES）を有効にします。

* `setting(editor.inlineSuggest.edits.allowCodeShifting)` - Copilot NESが提案を表示するためにコードをシフトできるかどうかを設定します。

* `setting(editor.inlineSuggest.edits.renderSideBySide)` - 可能であればCopilot NESが大きな提案を並べて表示するか、常に関連コードの下に表示するかを設定します。

     * **auto (default)**: ビューポートに十分なスペースがある場合、大きな編集提案を並べて表示します。そうでない場合は、関連コードの下に提案を表示します。
     * **never**: 提案を並べて表示せず、常に関連コードの下に表示します。

* `setting(github.copilot.nextEditSuggestions.fixes)` - 診断（波線）に基づいた次の編集提案を有効にします。たとえば、不足しているインポートなどです。

* `setting(editor.inlineSuggest.minShowDelay)` - インライン提案を表示する前に待機する時間をミリ秒単位で指定します。デフォルトは`0`です。

## 次のステップ

* [クイックスタート](/docs/copilot/getting-started.md)で主な機能を確認してください。

* [VS Codeでのチャット](/docs/copilot/chat/copilot-chat.md)でAIチャット会話を使用してください。

* YouTubeの[VS Code Copilotシリーズ](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)の動画をご覧ください。
