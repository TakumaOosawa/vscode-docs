---
ContentId: 7ab2cd6c-45fd-4278-a6e8-1c9e060593ea
DateApproved: 3/9/2026
MetaDescription: GitHub Copilot in VS Codeからのゴーストテキスト完成と次の編集提案を含む、AI搭載のインライン提案を取得します。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords: [nes, suggestions, inline completions, ghost text, next edit suggestions]
---
# VS CodeのGitHub Copilotからのインライン提案

VS CodeのGitHub Copilotは、入力中にコード、コメント、テストなどを完成させるAI搭載のインライン提案を提供します。インライン提案は、広範なプログラミング言語とフレームワークで動作します。これらは、[エージェント](/docs/copilot/agents/overview.md)（マルチファイル自動処理用）、[チャット](/docs/copilot/chat/copilot-chat.md)、[スマートアクション](/docs/copilot/copilot-smart-actions.md)と並ぶ、VS Codeのいくつかのいずれかのインターフェースです。

CopilotからのインラインSuggestions提案には2つの種類があり、どちらもコーディングスタイルと既存のコードを考慮しています：

* **ゴーストテキスト提案** - エディターで入力を開始すると、Copilotは現在のカーソル位置に薄い*ゴーストテキスト*提案を提供します。

* **次の編集提案** - Copilot次編集提案（Copilot NES）でコード編集の次の場所を予測します。行っている編集に基づいて、NESは次に編集したい場所と編集内容の両方を予測します。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="AIの使い始める">
VS Codeで初めてのアプリをAIで構築するための実際のチュートリアルに従ってください。

* [チュートリアルを開始](/docs/copilot/getting-started.md)

</div>

## 使い始める

1. GitHub Copilot拡張機能をインストールします。

    > <a class="install-extension-btn" href="vscode:extension/GitHub.copilot?referrer=docs-copilot-ai-powered-suggestions">GitHub Copilot拡張機能をインストール</a>

1. GitHubアカウントでサインインしてCopilotを使用します。

    > [!TIP]
    > Copilotサブスクリプションをまだお持ちでない場合は、[Copilot無料プラン](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で使用し、インライン提案とチャットインタラクションの月額制限を取得できます。

1. [Copilotクイックスタート](/docs/copilot/getting-started.md)でVS CodeのCopilotの主な機能を確認してください。

## 最初の提案を取得する

Copilotは入力するときに薄い*ゴーストテキスト*提案を提供します。しばしば現在の行の完成で、時には新しいコードのブロック全体です。提案をすべて、または一部受け入れることも、入力を続けて提案を無視することもできます。

次の例では、Copilotが薄い*ゴーストテキスト*を使用して`calculateDaysBetweenDates`JavaScriptファンクションの実装を提案する方法に注目してください：

![JavaScriptゴーストテキスト提案。](images/inline-suggestions/js-suggest.png)

インライン提案が表示されたら、`kbstyle(Tab)`キーで受け入れることができます。

Copilotは、既存のコードのコーディングスタイルを適用しようとします。次の例では、Copilotが`add`メソッドの同じ入力パラメーター命名スキームを提案された`subtract`メソッドに適用していることに注目してください。

![JavaScriptゴーストテキスト提案。](images/inline-suggestions/ts-suggest-parameter-names.png)

### 提案を部分的に受け入れる

GitHub Copilotからの提案全体を受け入れたくない場合があります。`kb(editor.action.inlineSuggest.acceptNextWord)`キーボードショートカットを使用して、提案の次の単語または次の行を受け入れることができます。

### 代替提案

特定の入力に対して、Copilotは複数の代替提案を提供する場合があります。提案にカーソルを合わせて、他の提案のいずれかを選択できます。

![インライン提案にカーソルを合わせると、複数の提案から選択できます](images/inline-suggestions/copilot-hover-highlight.png)

### コードコメントから提案を生成する

Copilotに提案を提供させることに依存するのではなく、使用可能なアルゴリズムやコンセプトを指定して（たとえば、「再帰を使用」または「シングルトンパターンを使用」）、あるいはクラスに追加するメソッドとプロパティを指定することで、予想されるコードについてのヒントを提供できます。

次の例は、TypeScriptでの学生を表すクラスを作成するようにCopilotに指示する方法を示していますが、メソッドとプロパティについての情報を提供します：

![コードコメントを使用して、プロパティとメソッドを持つTypeScriptのStudent クラスを生成するようにCopilotを指示します。](images/inline-suggestions/ts-suggest-code-comment.png)

## 次の編集提案

ゴーストテキスト提案は、コードのセクションの完成にはいいです。しかし、ほとんどのコード活動は既存のコードの編集であるため、インライン提案の自然な発展は、カーソルでと離れた両方の編集もサポートしています。編集は分け隔てなく作られていない場合が多くあります - 異なるシナリオで行う必要がある編集の論理的な流れがあります。次の編集提案（Copilot NES）はこの進化です。

<video src="./images/inline-suggestions/nes-video.mp4" title="Point typescriptクラスの操作中の次の編集提案を示すビデオ。" loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

行っている編集に基づいて、次の編集提案は、次の編集場所と編集内容の両方を予測します。Copilot NESは、流れに留まるのに役立ち、現在の作業に関連する今後の変更を提案し、`kbstyle(Tab)`を使用してCopilotの提案にすぐに移動して受け入れることができます。提案は、潜在的な変更の範囲に応じて、単一の記号、行全体、または複数の行にまたがる場合があります。

Copilot NESを使い始めるには、VS Code設定`setting(github.copilot.nextEditSuggestions.enabled)`を有効にします。

### 編集提案を移動して受け入れる

`kbstyle(Tab)`キーで提案されたコード変更にすぐに移動でき、次の関連する編集を見つけるのに時間を節約できます（ファイルまたは参照を手動で検索する必要はありません）。その後、`kbstyle(Tab)`キーで再度提案を受け入れることができます。

溝の矢印は、編集提案が利用可能かどうかを示します。矢印は、次の編集提案が現在のカーソル位置に相対的に配置されている場所を示します。

矢印にカーソルを合わせると、編集提案メニューを調べることができます。これには、キーボードショートカットと設定構成が含まれます：

![Copilot NES溝メニュー展開](./images/inline-suggestions/gutter-menu-highlighted-updated.png)

> [!IMPORTANT]
> [VS Code vim拡張機能](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)ユーザーの場合は、NESのキーバインドの競合を避けるために、最新バージョンの拡張機能を使用してください。

### 編集提案による気を散らすことを減らす

デフォルトでは、編集提案は溝の矢印で示され、コード変更はエディターに表示されます。`setting(editor.inlineSuggest.edits.showCollapsed)`設定を有効にして、`kbstyle(Tab)`キーを押して提案に移動するか、溝の矢印にカーソルを合わせるまで、コード変更をエディターにのみ表示します。または、溝の矢印にカーソルを合わせて、メニューから**表示折りたたみ**オプションを選択します。

### 次の編集提案のユースケース

**間違いの修正**

* **Copilotは、タイプミスなどの単純な間違いを手伝います。**`cont x = 5`や`conts x = 5`のように文字が不足しているか入れ替わっている場所で修正を提案し、`const x = 5`であるべきでした。

    ![「conts」から「const」へのタイプミスを修正するNES](./images/inline-suggestions/nes-typo.png)

* **Copilotは、ロジックのより挑戦的な間違いを手伝うこともできます**。反転された三項式など：

    ![三項ロジック間違いを修正するNES](./images/inline-suggestions/nes-ternary-logic.png)

    または、`||`の代わりに`&&`を使用すべき比較：

    ![if文の間違いを修正するNES](./images/inline-suggestions/nes-de-morgan.png)

**意図の変更**

* **Copilotは、意図の新しい変更に一致するコードの残りの部分への変更を提案します。**たとえば、クラスを`Point`から`Point3D`に変更する場合、Copilotはクラス定義に`z`変数を追加することを提案します。変更を受け入れた後、Copilot NESは次に距離計算に`z`を追加することを推奨しています：

    ![PointをPoint3Dに更新するためのNES gif](./images/inline-suggestions/nes-point.png)

**リファクタリング**

* **ファイルで一度に変数の名前を変更し、Copilotはそれを他の場所で更新することを提案します。**新しい名前または命名パターンを使用する場合、Copilotは後続のコードを同様に更新することを提案します。

    ![関数名を更新した後の変更を提案するCopilot NES](./images/inline-suggestions/nes-rename.png)

* **マッチするコードスタイル**。コードをコピーして貼り付けた後、Copilot貼り付けが発生した現在のコードに一致するようにコードを調整する方法を提案します。

## インライン提案を有効または無効にする

すべての言語に対して、または特定の言語のみに対して、インライン提案を有効または無効にすることができます。インライン提案を有効または無効にするには、ステータスバーのCopilotメニューを選択し、インライン提案を有効または無効にするオプションを確認または確認解除します。特定の言語に対するインライン提案を無効にするオプションは、アクティブなエディターの言語に依存します。

![スリープおよびスリープのキャンセルボタンが表示されたステータスバーのCopilotメニューのスクリーンショット。](images/inline-suggestions/snooze-code-completions.png)

または、設定エディターで`setting(github.copilot.enable)`設定を変更します。インライン提案を有効または無効にする各言語のエントリを追加します。すべての言語に対してインライン提案を有効または無効にするには、`*`の値を`true`または`false`に設定します。

エディター内のすべてのインライン提案を一時的に無効にするには、ステータスバーのCopilotメニューを選択し、**スリープ**ボタンを選択してスリープ時間を5分増やします。インライン提案を再開するには、Copilotメニューの**スリープのキャンセル**ボタンを選択します。

または、コマンドパレットで**Snooze Inline Suggestions**および**Cancel Snooze Inline Suggestions**コマンドを使用します。

## 提案するAIモデルを変更する

異なる大規模言語モデル（LLM）は異なるタイプのデータで訓練されており、異なる機能と強みを持っている場合があります。VS Codeで[異なるAI言語モデル間で選択する方法](/docs/copilot/customization/language-models.md)の詳細について説明します。

エディターのゴーストテキスト提案の生成に使用される言語モデルを変更するには：

1. コマンドパレット（`kbstyle(F1)`）を開きます。

1. **change completions model**を入力し、**GitHub Copilot: Change Completions Model**コマンドを選択します。

1. ドロップダウンメニューで、使用するモデルを選択します。

> [!NOTE]
> 利用可能なモデルのリストは異なる場合があり、時間とともに変わる場合があります。モデルピッカーは常に1つ以上のモデルを表示しない場合があり、プレビューモデルと追加のインライン提案モデルは、リリースされている場合は利用可能になります。Copilot BusinessまたはEnterpriseユーザーの場合、管理者は、GitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインすることで、組織の特定のモデルを有効にする必要があります。

## ヒントとコツ

### コンテキスト

関連するインライン提案を提供するために、Copilotは、現在のオープンファイルをエディターで調べて、コンテキストを分析し、適切な提案を作成します。Copilotを使用している間にVS Codeで関連ファイルを開いると、このコンテキストが設定され、Copilotはプロジェクトの大きな図を取得できます。

## 設定

### ゴーストテキスト提案設定

* `setting(github.copilot.enable)` - すべてまたは特定の言語のインライン完成を有効または無効にします。

* `setting(editor.inlineSuggest.fontFamily)` - インライン完成のフォントを構成します。

* `setting(editor.inlineSuggest.showToolbar)` - インライン完成に表示されるツールバーを有効または無効にします。

* `setting(editor.inlineSuggest.syntaxHighlightingEnabled)` - インライン完成の構文強調表示を有効または無効にします。

### 次の編集提案設定

* `setting(github.copilot.nextEditSuggestions.enabled)` - Copilot次編集提案を有効にします（Copilot NES）。

* `setting(editor.inlineSuggest.edits.allowCodeShifting)` - Copilot NESが提案を表示するためにコードをシフトできるかどうかを構成します。

* `setting(editor.inlineSuggest.edits.renderSideBySide)` - Copilot NESがより大きな提案を横並びに表示できるかどうかを構成し、可能であれば、またはCopilot NESが常により大きな提案を関連するコードの下に表示する必要があるかどうか。

     * **auto（デフォルト）**: ビューポートに十分なスペースがある場合、より大きな編集提案を横並びに表示し、そうでない場合は提案は関連するコードの下に表示されます。
     * **never**: 提案を横並びに表示しないで、常に提案を関連するコードの下に表示します。

* `setting(github.copilot.nextEditSuggestions.fixes)` - 診断（波線）に基づいて次の編集提案を有効にします。たとえば、欠落しているインポート。

* `setting(editor.inlineSuggest.minShowDelay)` - インライン提案を表示する前に待機する時間（ミリ秒）。デフォルトは`0`です。

## 次のステップ

* [クイックスタート](/docs/copilot/getting-started.md)で主な機能を確認してください。

* [VS Codeのチャット](/docs/copilot/chat/copilot-chat.md)でAIチャット会話を使用します。

* YouTubeの[VS Code Copilot Series](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)のビデオを見てください。

