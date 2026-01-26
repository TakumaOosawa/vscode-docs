---
ContentId: 7ab2cd6c-45fd-4278-a6e8-1c9e060593ea
DateApproved: 01/08/2026
MetaDescription: Visual Studio CodeのGitHub CopilotによるAI搭載のインライン提案でコーディングを強化します。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords: [nes, suggestions]
---
# VS CodeでのGitHub Copilotからのインライン提案

GitHub Copilotは、AI搭載のペアプログラマーとして機能し、コード、コメント、テストなどを補完するためのインライン提案を自動的に提供します。これらはコードを書いている間、エディター内で直接提供され、幅広いプログラミング言語やフレームワークに対応しています。

Copilotからは2種類のインライン提案が表示されることがあり、どちらもコーディングスタイルに合わせて、既存のコードを考慮に入れます：

* **ゴーストテキスト提案** - エディターで入力を開始すると、Copilotが現在のカーソル位置に淡色表示の*ゴーストテキスト*提案を表示します。

* **次の編集提案** - Copilot Next Edit Suggestions (Copilot NES) で次のコード編集を予測します。行っている編集に基づいて、NESは次に編集したい場所とその内容を予測します。

## はじめに

1. GitHub Copilot拡張機能をインストールします。

    > <a class="install-extension-btn" href="vscode:extension/GitHub.copilot?referrer=docs-copilot-ai-powered-suggestions">GitHub Copilot拡張機能をインストールする</a>

1. Copilotを使用するには、GitHubアカウントでサインインします。

    > [!TIP]
    > Copilotのサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)に登録することで、インライン提案とチャット対話の月間制限付きでCopilotを無料で使用できます。

1. [Copilotクイックスタート](/docs/copilot/getting-started.md)で、VS CodeにおけるCopilotの主要機能をご覧ください。

## 最初の提案を取得する

Copilotは入力中に淡色表示の*ゴーストテキスト*提案を提供します：現在の行の補完であったり、新しいコードブロック全体であったりします。提案のすべて、または一部を受け入れることも、入力を続けて提案を無視することもできます。

次の例では、Copilotが淡色表示の*ゴーストテキスト*を使用して、JavaScript関数`calculateDaysBetweenDates`の実装を提案していることに注目してください：

![JavaScript ghost text suggestion.](images/inline-suggestions/js-suggest.png)

インライン提案が表示されたら、`kbstyle(Tab)`キーで受け入れることができます。

Copilotは、コードに既に存在するコーディングスタイルを適用しようとします。次の例では、Copilotが提案された`subtract`メソッドに対して、`add`メソッドと同じ入力パラメータの命名規則を適用していることに注目してください。

![JavaScript ghost text suggestion.](images/inline-suggestions/ts-suggest-parameter-names.png)

### 提案の一部を受け入れる

GitHub Copilotからの提案全体を受け入れたくない場合があります。`kb(editor.action.inlineSuggest.acceptNextWord)`キーボードショートカットを使用して、提案の次の単語、または次の行を受け入れることができます。

### 代替提案

任意の入力に対して、Copilotは複数の代替提案を提供する場合があります。提案の上にホバーして、他の提案のいずれかを選択できます。

![Hovering over inline suggestions enables you to select from multiple suggestions](images/inline-suggestions/copilot-hover-highlight.png)

### コードコメントから提案を生成する

提案を提供するためにCopilotに頼る代わりに、コードコメントを使用して期待するコードについてのヒントを提供できます。たとえば、使用するアルゴリズムや概念の種類（例：「再帰を使用する」や「シングルトンパターンを使用する」）、またはクラスに追加するメソッドやプロパティを指定できます。

次の例は、メソッドとプロパティに関する情報を提供して、学生を表すTypeScriptクラスを作成するようにCopilotに指示する方法を示しています：

![Use code comments to let Copilot generate a Student class in TypeScript with properties and methods.](images/inline-suggestions/ts-suggest-code-comment.png)

## 次の編集提案

ゴーストテキスト提案は、コードの一部を自動補完するのに優れています。しかし、コーディング活動の多くは既存のコードの編集であるため、カーソル位置だけでなく、離れた場所での編集も支援することは、インライン提案の自然な進化です。編集は単独で行われることは少なく、さまざまなシナリオで行う必要がある編集の論理的な流れがあります。Next Edit Suggestions (Copilot NES) はこの進化系です。

<video src="./images/inline-suggestions/nes-video.mp4" title="Video showing next edit suggestions in action on a Point typescript class." autoplay loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

行っている編集に基づいて、次の編集提案は次に編集したい場所とその内容を予測します。Copilot NESはフローを維持するのに役立ち、現在の作業に関連する将来の変更を提案します。`kbstyle(Tab)`を押すだけで、Copilotの提案に素早く移動して受け入れることができます。提案は、潜在的な変更の範囲に応じて、単一のシンボル、行全体、または複数行にまたがる場合があります。

Copilot NESの使用を開始するには、VS Codeの設定`setting(github.copilot.nextEditSuggestions.enabled)`を有効にします。

### 編集提案への移動と受け入れ

`kbstyle(Tab)`キーを使用して提案されたコード変更に素早く移動できるため、次の関連する編集を見つける時間を節約できます（ファイルや参照を手動で検索する必要はありません）。その後、もう一度`kbstyle(Tab)`キーを押して提案を受け入れることができます。

ガターの矢印は、編集提案が利用可能かどうかを示します。矢印は、現在のカーソル位置に対する次の編集提案の場所を示します。

矢印の上にホバーして、キーボードショートカットや設定構成を含む編集提案メニューを探索できます：

![Copilot NES gutter menu expanded](./images/inline-suggestions/gutter-menu-highlighted-updated.png)

> [!IMPORTANT]
> [VS Code vim拡張機能](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)ユーザーの場合は、NESとのキーバインドの競合を避けるために、拡張機能の最新バージョンを使用してください。

### 編集提案による気が散る要素を減らす

デフォルトでは、編集提案はガターの矢印で示され、コードの変更はエディターに表示されます。`setting(editor.inlineSuggest.edits.showCollapsed)`設定を有効にすると、`kbstyle(Tab)`キーを押して提案に移動するか、ガターの矢印にホバーするまで、エディターでのコード変更の表示を省略できます。または、ガターの矢印にホバーして、メニューから**折りたたんで表示**オプションを選択します。

### 次の編集提案のユースケース

**間違いの発見と修正**

* **Copilotはタイプミスのような単純な間違いを助けます。** 文字が欠落していたり入れ替わっていたりする修正を提案します。たとえば、`cont x = 5`や`conts x = 5`などは、`const x = 5`であるべきです。

    ![NES fixing a typo from "conts" to "const"](./images/inline-suggestions/nes-typo.png)

* **Copilotは、論理上のより困難な間違いも助けることができます**。たとえば、反転した三項演算子などです：

    ![NES fixing a ternary logic mistake](./images/inline-suggestions/nes-ternary-logic.png)

    または、`||`の代わりに`&&`を使用すべきだった比較など：

    ![NES fixing an if statement mistake](./images/inline-suggestions/nes-de-morgan.png)

**意図の変更**

* **Copilotは、意図の新しい変更に一致するコードの残りの部分への変更を提案します。** たとえば、クラスを`Point`から`Point3D`に変更する場合、Copilotはクラス定義に`z`変数を追加することを提案します。変更を受け入れた後、Copilot NESは次に距離計算に`z`を追加することを推奨します：

    ![NES gif for updating Point to Point3D](./images/inline-suggestions/nes-point.png)

**リファクタリング**

* **ファイル内で変数の名前を1回変更すると、Copilotは他のすべての場所でも更新することを提案します。** 新しい名前や命名パターンを使用すると、Copilotは後続のコードも同様に更新することを提案します。

    ![Copilot NES suggesting change after updating function name](./images/inline-suggestions/nes-rename.png)

* **コードスタイルのマッチング**。コードをコピー＆ペーストした後、Copilotは貼り付けが行われた現在のコードに合わせて調整する方法を提案します。

## インライン提案の有効化または無効化

すべての言語、または特定の言語に対してのみ、インライン提案を有効または無効にできます。インライン提案を有効または無効にするには、ステータスバーのCopilotメニューを選択し、インライン提案を有効または無効にするオプションをオンまたはオフにします。特定の言語に対してインライン提案を無効にするオプションは、アクティブなエディターの言語に依存します。

![Screenshot of the Copilot menu in the Status Bar with Snooze and Cancel Snooze buttons.](images/inline-suggestions/snooze-code-completions.png)

または、設定エディターで`setting(github.copilot.enable)`設定を変更します。インライン提案を有効または無効にする言語ごとにエントリを追加します。すべての言語に対してインライン提案を有効または無効にするには、`*`の値を`true`または`false`に設定します。

エディターですべてのインライン提案を一時的に無効にするには、ステータスバーのCopilotメニューを選択し、**スヌーズ**ボタンを選択してスヌーズ時間を5分ずつ延長します。インライン提案を再開するには、Copilotメニューの**スヌーズ解除**ボタンを選択します。

または、コマンドパレットの**インライン提案をスヌーズ**および**インライン提案のスヌーズ解除**コマンドを使用します。

## 提案用のAIモデルを変更する

大規模言語モデル(LLM)によって、異なる種類のデータでトレーニングされており、機能や強みが異なる場合があります。VS Codeで[異なるAI言語モデルを選択する](/docs/copilot/customization/language-models.md)方法の詳細をご覧ください。

エディターでゴーストテキスト提案を生成するために使用される言語モデルを変更するには：

1. コマンドパレット(`kbstyle(F1)`)を開きます。

1. **change completions model**と入力し、**GitHub Copilot: Change Completions Model**コマンドを選択します。

1. ドロップダウンメニューから、使用したいモデルを選択します。

> [!NOTE]
> 利用可能なモデルのリストは、時間の経過とともに変化する可能性があります。モデルピッカーには複数のモデルが表示されない場合があり、プレビューモデルや追加のインライン提案モデルは、リリースされ次第利用可能になります。Copilot BusinessまたはEnterpriseユーザーの場合、管理者はGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインすることで、組織に対して特定のモデルを有効にする必要があります。

## ヒントとコツ

### コンテキスト

関連性の高いインライン提案を提供するために、Copilotはエディター内の現在および開いているファイルを調べてコンテキストを分析し、適切な提案を作成します。Copilotの使用中にVS Codeで関連ファイルを開いておくことは、このコンテキストを設定するのに役立ち、Copilotがプロジェクトの全体像を把握できるようにします。

## 設定

### ゴーストテキスト提案の設定

* `setting(github.copilot.enable)` - すべてまたは特定の言語に対するインライン補完を有効または無効にします。

* `setting(editor.inlineSuggest.fontFamily)` - インライン補完のフォントを設定します。

* `setting(editor.inlineSuggest.showToolbar)` - インライン補完に表示されるツールバーを有効または無効にします。

* `setting(editor.inlineSuggest.syntaxHighlightingEnabled)` - インライン補完の構文ハイライトを有効または無効にします。

### 次の編集提案の設定

* `setting(github.copilot.nextEditSuggestions.enabled)` - Copilot Next Edit Suggestions (Copilot NES) を有効にします。

* `setting(editor.inlineSuggest.edits.allowCodeShifting)` - Copilot NESが提案を表示するためにコードをシフトできるかどうかを設定します。

* `setting(editor.inlineSuggest.edits.renderSideBySide)` - Copilot NESが大きい提案を可能な場合に並べて表示できるか、それとも常に関連するコードの下に表示するかを設定します。

     * **auto (default)**: ビューポートに十分なスペースがある場合、大きい編集提案を並べて表示します。それ以外の場合は、提案を関連するコードの下に表示します。
     * **never**: 提案を並べて表示せず、常に提案を関連するコードの下に表示します。

* `setting(github.copilot.nextEditSuggestions.fixes)` - 診断（波線）に基づく次の編集提案を有効にします。たとえば、不足しているインポートなどです。

* `setting(editor.inlineSuggest.minShowDelay)` - インライン提案を表示する前に待機する時間（ミリ秒単位）。デフォルトは`0`です。

## 次のステップ

* [クイックスタート](/docs/copilot/getting-started.md)で主要な機能を発見してください。

* [VS Codeでのチャット](/docs/copilot/chat/copilot-chat.md)でAIチャット会話を使用してください。

* YouTubeの[VS Code Copilotシリーズ](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)のビデオをご覧ください。
