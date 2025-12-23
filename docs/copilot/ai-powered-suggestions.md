---
ContentId: 7ab2cd6c-45fd-4278-a6e8-1c9e060593ea
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub CopilotのAI搭載インライン提案を使用してコーディングを強化します。
MetaSocialImage: images/shared/github-copilot-social.png
Keywords: [nes, suggestions]
---
# VS CodeでのGitHub Copilotのインライン提案

GitHub CopilotはAI搭載のペアプログラマーとして機能し、コード、コメント、テストなどを補完するインライン提案を自動的に提示します。これらの提案はコードを書いている最中にエディター内へ直接表示され、幅広いプログラミング言語やフレームワークで利用できます。

Copilotのインライン提案には2種類があり、どちらもコーディングスタイルに合わせ、既存のコードを考慮します。

* **ゴーストテキストの提案** - エディターで入力を始めると、Copilotが現在のカーソル位置に薄く表示される*ゴーストテキスト*の提案を提示します。

* **次の編集の提案** - Copilotの次の編集の提案（Copilot NES）で、次に行うコード編集を予測します。NESは、あなたが行っている編集に基づいて、次に編集したくなる場所と、その編集内容の両方を予測します。

## はじめに

1. Install the GitHub Copilot extensions.

    > <a class="install-extension-btn" href="vscode:extension/GitHub.copilot?referrer=docs-copilot-ai-powered-suggestions">Install the GitHub Copilot extensions</a>

1. Copilotを使用するには、GitHubアカウントでサインインします。

    > [!TIP]
    > まだCopilotのサブスクリプションがない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップすることでCopilotを無料で利用でき、インライン提案とチャットのやり取りに月ごとの上限が付与されます。

1. [Copilotクイックスタート](/docs/copilot/getting-started.md)で、VS CodeでのCopilotの主な機能を確認します。

## 最初の提案を受け取る

Copilotは入力に合わせて薄く表示される*ゴーストテキスト*の提案を提示します。現在の行の補完の場合もあれば、新しいコードブロック全体の場合もあります。提案は全体を受け入れることも、一部だけ受け入れることもできますし、入力を続けて提案を無視することもできます。

次の例では、Copilotが薄い*ゴーストテキスト*を使って`calculateDaysBetweenDates` JavaScript関数の実装を提案していることがわかります。

![JavaScriptのゴーストテキストの提案。](images/inline-suggestions/js-suggest.png)

インライン提案が表示されたら、`kbstyle(Tab)`キーで受け入れることができます。

Copilotは、すでにコード内で使用しているコーディングスタイルを適用しようとします。次の例では、提案された`subtract`メソッドに対して、`add`メソッドと同じ入力パラメーターの命名規則が適用されています。

![JavaScriptのゴーストテキストの提案。](images/inline-suggestions/ts-suggest-parameter-names.png)

### 提案の一部を受け入れる

GitHub Copilotの提案をすべて受け入れたくない場合があります。`kb(editor.action.inlineSuggest.acceptNextWord)`キーボードショートカットを使用すると、提案の次の単語、または次の行を受け入れることができます。

### 代替の提案

同じ入力に対して、Copilotが複数の代替提案を提示する場合があります。提案にカーソルを合わせると、他の提案に切り替えることができます。

![インライン提案にカーソルを合わせると複数の提案から選択できます](images/inline-suggestions/copilot-hover-highlight.png)

### コードコメントから提案を生成する

Copilotの提案に任せるのではなく、コードコメントを使って期待するコードのヒントを与えることができます。たとえば、使用するアルゴリズムや概念の種類（例:「use recursion」や「use a singleton pattern」）を指定したり、クラスに追加するメソッドやプロパティを指定したりできます。

次の例は、メソッドとプロパティに関する情報を与えて、学生を表すTypeScriptのクラスを作成するようCopilotに指示する方法を示しています。

![コードコメントを使って、プロパティとメソッドを備えたStudentクラスをTypeScriptでCopilotに生成させます。](images/inline-suggestions/ts-suggest-code-comment.png)

## 次の編集の提案

ゴーストテキストの提案は、コードの一部をオートコンプリートするのに最適です。しかし、コーディング作業の多くは既存コードの編集であるため、カーソル位置や離れた場所の編集も支援できるようにインライン提案が進化するのは自然な流れです。編集は多くの場合、単独で行われるのではなく、シナリオごとに必要な編集には論理的な流れがあります。次の編集の提案（Copilot NES）は、その進化形です。

<video src="./images/inline-suggestions/nes-video.mp4" title="Video showing next edit suggestions in action on a Point typescript class." autoplay loop controls muted poster="./images/inline-suggestions/point3d.png"></video>

次の編集の提案は、あなたが行っている編集に基づいて、次に編集したくなる場所と、その編集内容の両方を予測します。Copilot NESは、現在の作業に関連する今後の変更を提案することで作業の流れを保てるよう支援し、`kbstyle(Tab)`を押すだけで提案へすばやく移動して受け入れられます。提案は、想定される変更の範囲に応じて、単一のシンボル、行全体、または複数行にまたがる場合があります。

Copilot NESを利用するには、VS Codeの設定`setting(github.copilot.nextEditSuggestions.enabled)`を有効にします。

### 編集の提案を移動して受け入れる

`kbstyle(Tab)`キーを使うと、提案されたコード変更へすばやく移動でき、次に関連する編集箇所を見つける時間を節約できます（ファイルや参照を手動で検索する必要はありません）。その後、もう一度`kbstyle(Tab)`キーを押して提案を受け入れられます。

ガターの矢印は、編集の提案が利用可能であることを示します。この矢印は、現在のカーソル位置に対して次の編集の提案がどこにあるかを示します。

矢印にカーソルを合わせると、キーボードショートカットや設定の構成を含む編集の提案メニューを確認できます。

![Copilot NESのガターメニュー（展開）](./images/inline-suggestions/gutter-menu-highlighted-updated.png)

> [!IMPORTANT]
> [VS Code vim拡張機能](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)を使用している場合は、NESとのキーバインドの競合を避けるため、拡張機能を最新バージョンにしてください。

### 編集の提案による注意散漫を減らす

既定では、編集の提案はガターの矢印で示され、コード変更がエディターに表示されます。`setting(editor.inlineSuggest.edits.showCollapsed)`設定を有効にすると、`kbstyle(Tab)`キーを押して提案へ移動するまで、またはガターの矢印にカーソルを合わせるまで、コード変更をエディターに表示しないようにできます。別の方法として、ガターの矢印にカーソルを合わせてメニューから**Show Collapsed**オプションを選択します。

### 次の編集の提案のユースケース

**ミスの検出と修正**

* **Copilotは、タイプミスのような単純なミスを支援します。** 文字の抜けや入れ替わりがある箇所に対して、`cont x = 5`や`conts x = 5`のようなものを、`const x = 5`に修正する提案をします。

    ![NES fixing a typo from "conts" to "const"](./images/inline-suggestions/nes-typo.png)

* **Copilotは、より難しいロジック上のミスにも役立ちます。** たとえば、三項演算子が逆になっている場合です。

    ![NES fixing a ternary logic mistake](./images/inline-suggestions/nes-ternary-logic.png)

    または、`||`ではなく`&&`を使うべき比較の場合です。

    ![NES fixing an if statement mistake](./images/inline-suggestions/nes-de-morgan.png)

**意図の変更**

* **Copilotは、意図の新しい変更に合うように残りのコードの変更を提案します。** たとえば、クラスを`Point`から`Point3D`に変更する場合、Copilotはクラス定義に`z`変数を追加する提案をします。変更を受け入れた後、Copilot NESは次に距離計算に`z`を追加することを推奨します。

    ![NES gif for updating Point to Point3D](./images/inline-suggestions/nes-point.png)

**リファクタリング**

* **ファイル内の変数名を一度変更すると、Copilotは他のすべての箇所も更新する提案をします。** 新しい名前や命名パターンを使用すると、Copilotは後続のコードも同様に更新する提案をします。

    ![Copilot NES suggesting change after updating function name](./images/inline-suggestions/nes-rename.png)

* **コードスタイルの一致**。コードをコピー＆ペーストした後、Copilotは貼り付け先の現在のコードに合うように調整する方法を提案します。

## インライン提案を有効化または無効化する

インライン提案は、すべての言語に対して、または特定の言語に対してのみ、有効化または無効化できます。インライン提案を有効化または無効化するには、ステータスバーのCopilotメニューを選択し、インライン提案の有効化/無効化オプションをオンまたはオフにします。特定の言語に対してインライン提案を無効化するオプションは、アクティブなエディターの言語に依存します。

![ステータスバーのCopilotメニュー（SnoozeボタンとCancel Snoozeボタン）](images/inline-suggestions/snooze-code-completions.png)

別の方法として、設定エディターで`setting(github.copilot.enable)`設定を変更します。インライン提案を有効化または無効化したい各言語に対してエントリを追加します。すべての言語のインライン提案を有効化または無効化するには、`*`の値を`true`または`false`に設定します。

エディター内のすべてのインライン提案を一時的に無効にするには、ステータスバーのCopilotメニューを選択し、**Snooze**ボタンを選択してスヌーズ時間を5分増やします。インライン提案を再開するには、Copilotメニューで**Cancel Snooze**ボタンを選択します。

別の方法として、コマンドパレットの**Snooze Inline Suggestions**コマンドと**Cancel Snooze Inline Suggestions**コマンドを使用します。

## 提案のAIモデルを変更する

Large Language Models（LLM）は学習に使用したデータの種類が異なり、能力や得意分野も異なる場合があります。VS Codeで[異なるAI言語モデルを選択する方法](/docs/copilot/customization/language-models.md)の詳細を確認してください。

エディターでゴーストテキストの提案を生成するために使用される言語モデルを変更するには、次の手順を実行します。

1. Open the Command Palette (`kbstyle(F1)`).

1. **change completions model**と入力し、**GitHub Copilot: Change Completions Model**コマンドを選択します。

1. ドロップダウンメニューで、使用するモデルを選択します。

> [!NOTE]
> 利用可能なモデルの一覧は、状況によって異なり、また時間とともに変更される場合があります。モデルピッカーに複数のモデルが常に表示されるとは限りません。また、プレビューモデルや追加のインライン提案モデルは、提供を開始した場合にここで利用できるようになります。Copilot BusinessまたはEnterpriseユーザーの場合、管理者がGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインし、組織で特定のモデルを有効にする必要があります。

## ヒントとコツ

### Context

関連性の高いインライン提案を提示するために、Copilotはエディターで現在のファイルと開いているファイルを参照してコンテキストを分析し、適切な提案を作成します。Copilotを使用する際にVS Codeで関連ファイルを開いておくと、このコンテキストの設定に役立ち、プロジェクトの全体像をCopilotが把握しやすくなります。

## Settings

### ゴーストテキストの提案の設定

* `setting(github.copilot.enable)` - enable or disable inline completions for all or specific languages.

* `setting(editor.inlineSuggest.fontFamily)` - configure the font for the inline completions.

* `setting(editor.inlineSuggest.showToolbar)` - enable or disable the toolbar that appears for inline completions.

* `setting(editor.inlineSuggest.syntaxHighlightingEnabled)` - enable or disable syntax highlighting for inline completions.

### 次の編集の提案の設定

* `setting(github.copilot.nextEditSuggestions.enabled)` - enable Copilot next edit suggestions (Copilot NES).

* `setting(editor.inlineSuggest.edits.allowCodeShifting)` - configure if Copilot NES is able to shift your code to show a suggestion.

* `setting(editor.inlineSuggest.edits.renderSideBySide)` - configure if Copilot NES can show larger suggestions side-by-side if possible, or if Copilot NES should always show larger suggestions below the relevant code.

     * **auto (default)**: show larger edit suggestions side-by-side if there is enough space in the viewport, otherwise the suggestions are shown below the relevant code.
     * **never**: never show suggestions side-by-side, always show suggestions below the relevant code.

* `setting(github.copilot.nextEditSuggestions.fixes)` - enable next edit suggestions based on diagnostics (squiggles). For example, missing imports.

* `setting(editor.inlineSuggest.minShowDelay)` - Time in milliseconds to wait before showing inline suggestions. Default is `0`.

## 次のステップ

* [クイックスタート](/docs/copilot/getting-started.md)で主な機能を確認します。

* [VS Codeでのチャット](/docs/copilot/chat/copilot-chat.md)でAIチャットの会話を利用します。

* YouTubeで[VS Code Copilotシリーズ](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)の動画を視聴します。
