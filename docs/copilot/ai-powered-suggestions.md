---
ContentId: 7ab2cd6c-45fd-4278-a6e8-1c9e060593ea
DateApproved: 3/9/2026
MetaDescription: VS CodeのGitHub Copilotから、ghost text補完や次の編集提案を含む AI を活用したインライン提案を取得します。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords:
    - nes
    - 提案
    - インライン補完
    - ghost text
    - 次の編集提案
---
# VS CodeのGitHub Copilotによるインライン提案

VS CodeのGitHub Copilotは、入力に合わせてコード、コメント、テストなどを補完する、AI を活用したインライン提案を提供します。インライン提案は幅広いプログラミング言語やフレームワークで機能します。これは VS Codeにおける複数の AI サーフェスの 1 つであり、自律的なマルチファイルタスク向けの[エージェント](/docs/copilot/agents/overview.md)、[チャット](/docs/copilot/chat/copilot-chat.md)、[スマート アクション](/docs/copilot/copilot-smart-actions.md)と並ぶものです。

Copilotからは 2 種類のインライン提案を利用できます。どちらもあなたのコーディング スタイルに合わせ、既存のコードを考慮します。

* **Ghost text suggestions** - エディターで入力を始めると、Copilotが現在のカーソル位置に薄く表示された*ghost text*提案を表示します。

* **Next edit suggestions** - Copilotの次の編集提案、別名 Copilot NES で、次に行うコード編集を予測します。NES は、あなたが行っている編集に基づいて、次に行いたい編集の場所と、その編集内容の両方を予測します。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AI を使って始める">
VS CodeでAIを使って最初のアプリを作成するハンズオン チュートリアルに沿って進めます。

* [チュートリアルを開始する](/docs/copilot/getting-started.md)

</div>

## はじめに

1. GitHub Copilot拡張機能をインストールします。

    > <a class="install-extension-btn" href="vscode:extension/GitHub.copilot?referrer=docs-copilot-ai-powered-suggestions">Install the GitHub Copilot extensions</a>

1. GitHubアカウントでサインインして Copilot を使用します。

    > [!TIP]
    > まだ Copilot のサブスクリプションがない場合は、[Copilot Free プラン](https://github.com/github-copilot/signup)にサインアップして Copilot を無料で利用でき、インライン提案とチャット操作の月間上限が提供されます。

1. [Copilot クイックスタート](/docs/copilot/getting-started.md)で、VS Codeにおける Copilot の主な機能を確認します。

## 最初の提案を取得する

Copilotは、入力に合わせて薄く表示された*ghost text*提案を表示します。現在の行の補完である場合もあれば、まったく新しいコード ブロックである場合もあります。提案全体を受け入れることも、一部だけを受け入れることも、入力を続けて提案を無視することもできます。

次の例では、Copilotが薄く表示された*ghost text*を使って、`calculateDaysBetweenDates` JavaScript 関数の実装を提案していることに注目してください。

![JavaScriptの ghost text 提案。](images/inline-suggestions/js-suggest.png)

インライン提案が表示されたら、`kbstyle(Tab)`キーで受け入れることができます。

Copilotは、すでにコードで使われているコーディング スタイルをできるだけ適用しようとします。次の例では、提案された`subtract`メソッドに対して、Copilotが`add`メソッドと同じ入力パラメーターの命名規則を適用していることに注目してください。

![JavaScriptの ghost text 提案。](images/inline-suggestions/ts-suggest-parameter-names.png)

### 提案を部分的に受け入れる

GitHub Copilotからの提案全体を受け入れたくない場合もあります。`kb(editor.action.inlineSuggest.acceptNextWord)`キーボード ショートカットを使用すると、提案の次の単語、または次の行だけを受け入れることができます。

### 代替の提案

同じ入力に対して、Copilotが複数の代替提案を提示することがあります。提案の上にカーソルを合わせると、ほかの提案に切り替えることができます。

![インライン提案にカーソルを合わせると、複数の提案から選択できます](images/inline-suggestions/copilot-hover-highlight.png)

### コード コメントから提案を生成する

Copilotに提案を任せるだけでなく、コード コメントを使って期待するコードのヒントを与えることもできます。たとえば、使用するアルゴリズムや概念の種類を指定したり（たとえば、"use recursion"や"use a singleton pattern"）、クラスに追加するメソッドやプロパティを指定したりできます。

次の例は、メソッドやプロパティに関する情報を与えながら、学生を表すクラスを TypeScriptで作成するよう Copilotに指示する方法を示しています。

![コード コメントを使って、プロパティとメソッドを持つ Student クラスを TypeScriptで Copilotに生成させます。](images/inline-suggestions/ts-suggest-code-comment.png)

## 次の編集提案

Ghost text提案は、コードの一部を自動補完するのに適しています。しかし、コーディング作業の多くは既存コードの編集であるため、インライン提案がカーソル位置だけでなく離れた場所の編集も支援するよう進化するのは自然な流れです。編集は単独で行われることは少なく、状況ごとに必要な編集には論理的な流れがあります。次の編集提案（Copilot NES）は、その進化形です。

<video src="./images/inline-suggestions/nes-video.mp4" title="Point typescript クラスで次の編集提案が動作している様子を示す動画。" loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

次の編集提案は、あなたが行っている編集に基づいて、次に行いたい編集の場所と、その編集内容の両方を予測します。Copilot NES は、現在の作業に関連する今後の変更を提案することで、作業の流れを維持できるよう支援します。`kbstyle(Tab)`を使うと、Copilot の提案にすばやく移動して受け入れることができます。提案は、変更の想定範囲に応じて、単一のシンボル、行全体、または複数行にまたがることがあります。

Copilot NES を使い始めるには、VS Codeの設定`setting(github.copilot.nextEditSuggestions.enabled)`を有効にします。

### 編集提案に移動して受け入れる

`kbstyle(Tab)`キーを使うと、提案されたコード変更にすばやく移動できるため、次に関連する編集を見つける時間を節約できます（ファイルや参照を手動で探す必要はありません）。その後、`kbstyle(Tab)`キーをもう一度押して提案を受け入れることができます。

ガター内の矢印は、利用可能な編集提案があるかどうかを示します。この矢印は、現在のカーソル位置を基準として、次の編集提案がどこにあるかを示します。

矢印にカーソルを合わせると、キーボード ショートカットや設定構成を含む編集提案メニューを表示できます。

![展開された Copilot NES のガター メニュー](./images/inline-suggestions/gutter-menu-highlighted-updated.png)

> [!IMPORTANT]
> [VS Code vim extension](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)を使用している場合は、NES とのキー バインド競合を避けるため、拡張機能の最新バージョンを使用してください。

### 編集提案による気の散りを減らす

既定では、編集提案はガターの矢印で示され、コード変更はエディター内に表示されます。設定`setting(editor.inlineSuggest.edits.showCollapsed)`を有効にすると、提案に移動するために`kbstyle(Tab)`キーを押すか、ガターの矢印にカーソルを合わせるまで、エディター内では折りたたまれた状態でコード変更を表示できます。別の方法として、ガターの矢印にカーソルを合わせて、メニューから**Show Collapsed**オプションを選択することもできます。

### 次の編集提案の使用例

**ミスを見つけて修正する**

* **Copilotは、タイプミスのような単純なミスに役立ちます。** `const x = 5`であるべきところが、`cont x = 5`や`conts x = 5`のように文字が欠けたり入れ替わったりしている場合に、修正を提案します。

    ![NES が "conts" から "const" へのタイプミスを修正している様子](./images/inline-suggestions/nes-typo.png)

* **Copilotは、反転した三項演算子のような、より難しいロジックのミスにも役立ちます**。

    ![NES が三項演算子のロジック ミスを修正している様子](./images/inline-suggestions/nes-ternary-logic.png)

    または、`||`ではなく`&&`を使うべき比較にも対応します。

    ![NES が if ステートメントのミスを修正している様子](./images/inline-suggestions/nes-de-morgan.png)

**意図を変更する**

* **Copilotは、新しい意図の変更に合わせて、コードの残りの部分に対する変更を提案します。** たとえば、クラスを`Point`から`Point3D`に変更するとき、Copilotはクラス定義に`z`変数を追加することを提案します。その変更を受け入れた後、Copilot NES は次に距離計算へ`z`を追加することを推奨します。

    ![Point を Point3D に更新する NES の gif](./images/inline-suggestions/nes-point.png)

**リファクタリング**

* **ファイル内で一度変数名を変更すると、Copilotはそれ以外の箇所も更新するよう提案します。** 新しい名前や命名パターンを使うと、Copilotは後続のコードも同様に更新するよう提案します。

    ![関数名の更新後に変更を提案する Copilot NES](./images/inline-suggestions/nes-rename.png)

* **コード スタイルを合わせる**。コードをコピー アンド ペーストした後、Copilotは、貼り付け先の現在のコードに合わせてどのように調整すべきかを提案します。

## インライン提案を有効または無効にする

インライン提案は、すべての言語に対して、または特定の言語に対してのみ、有効または無効にできます。インライン提案を有効または無効にするには、ステータス バーの Copilot メニューを選択し、インライン提案を有効または無効にするオプションをオンまたはオフにします。特定の言語に対してインライン提案を無効にするオプションは、アクティブなエディターの言語に応じて表示されます。

![Snooze ボタンと Cancel Snooze ボタンがあるステータス バーの Copilot メニューのスクリーンショット。](images/inline-suggestions/snooze-code-completions.png)

または、設定エディターで`setting(github.copilot.enable)`設定を変更します。インライン提案を有効または無効にしたい各言語のエントリを追加します。すべての言語に対してインライン提案を有効または無効にするには、`*`の値を`true`または`false`に設定します。

エディター内のすべてのインライン提案を一時的に無効にするには、ステータス バーの Copilot メニューを選択し、**Snooze**ボタンを選択してスヌーズ時間を 5 分ずつ増やします。インライン提案を再開するには、Copilot メニューで**Cancel Snooze**ボタンを選択します。

または、コマンド パレットで**Snooze Inline Suggestions**コマンドと**Cancel Snooze Inline Suggestions**コマンドを使用します。

## 提案に使う AI モデルを変更する

異なる Large Language Models（LLMs）は、異なる種類のデータで学習されており、機能や強みが異なることがあります。VS Codeで[さまざまな AI 言語モデルを選択する方法](/docs/copilot/customization/language-models.md)の詳細を確認してください。

エディターで ghost text 提案を生成するために使用する言語モデルを変更するには、次の手順を実行します。

1. コマンド パレットを開きます（`kbstyle(F1)`）。

1. **change completions model**と入力し、**GitHub Copilot: Change Completions Model**コマンドを選択します。

1. ドロップダウン メニューで、使用するモデルを選択します。

> [!NOTE]
> 利用可能なモデルの一覧は、時間の経過とともに異なったり変化したりすることがあります。モデル ピッカーに常に複数のモデルが表示されるとは限らず、プレビュー モデルや追加のインライン提案モデルは、公開された場合にそこから利用できるようになります。Copilot Business または Enterprise のユーザーである場合は、管理者が GitHub.com の[Copilot ポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインし、組織向けに特定のモデルを有効にする必要があります。

## ヒントとコツ

### コンテキスト

Copilotは、関連性の高いインライン提案を提供するために、エディター内の現在のファイルと開いているファイルを見てコンテキストを分析し、適切な提案を作成します。Copilotを使うときに関連ファイルを VS Codeで開いておくと、このコンテキストの設定に役立ち、Copilotがプロジェクト全体像をより把握しやすくなります。

## 設定

### Ghost text 提案の設定

* `setting(github.copilot.enable)` - すべてまたは特定の言語に対してインライン補完を有効または無効にします。

* `setting(editor.inlineSuggest.fontFamily)` - インライン補完のフォントを構成します。

* `setting(editor.inlineSuggest.showToolbar)` - インライン補完に表示されるツール バーを有効または無効にします。

* `setting(editor.inlineSuggest.syntaxHighlightingEnabled)` - インライン補完のシンタックス ハイライトを有効または無効にします。

### 次の編集提案の設定

* `setting(github.copilot.nextEditSuggestions.enabled)` - Copilot の次の編集提案（Copilot NES）を有効にします。

* `setting(editor.inlineSuggest.edits.allowCodeShifting)` - Copilot NES が提案を表示するためにコードをシフトできるかどうかを構成します。

* `setting(editor.inlineSuggest.edits.renderSideBySide)` - Copilot NES が可能な場合に大きな提案を横並びで表示するか、それとも常に関連コードの下に表示するかを構成します。

     * **auto (default)**: ビューポートに十分な空きがある場合は大きな編集提案を横並びで表示し、それ以外の場合は関連コードの下に表示します。
     * **never**: 提案を横並びで表示せず、常に関連コードの下に表示します。

* `setting(github.copilot.nextEditSuggestions.fixes)` - 診断結果（波線）に基づく次の編集提案を有効にします。たとえば、不足しているインポートです。

* `setting(editor.inlineSuggest.minShowDelay)` - インライン提案を表示する前に待機する時間をミリ秒で指定します。既定値は`0`です。

## 次のステップ

* [クイックスタート](/docs/copilot/getting-started.md)で主な機能を確認します。

* [VS Codeでのチャット](/docs/copilot/chat/copilot-chat.md)で AI とのチャット会話を利用します。

* YouTubeで[VS Code Copilot Series](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)の動画を視聴します。
