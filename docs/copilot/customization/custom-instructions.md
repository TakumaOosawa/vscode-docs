---
ContentId: 8b4f3c21-4e02-4a89-9f15-7a8d6b5c2e91
DateApproved: 12/10/2025
MetaDescription: VS CodeでGitHub Copilot Chatのカスタム指示を作成して、AIの応答がコーディング手法、プロジェクト要件、開発標準に一致するようにする方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでカスタム指示を使用する

カスタム指示を使用すると、AIがコードを生成したり、他の開発タスクを扱ったりする方法に自動的に影響する、共通のガイドラインやルールを定義できます。すべてのチャットプロンプトに毎回コンテキストを手動で含める代わりに、Markdownファイルでカスタム指示を指定して、コーディング手法やプロジェクト要件に沿った一貫したAIの応答を確保します。

カスタム指示は、すべてのチャット要求に自動的に適用するように設定することも、特定のファイルのみに適用するように設定することもできます。あるいは、特定のチャットプロンプトに手動でカスタム指示を添付することもできます。

> [!NOTE]
> カスタム指示は、エディターで入力しているときの[インライン候補](/docs/copilot/ai-powered-suggestions.md)には考慮されません。

## 指示ファイルの種類

VS Codeは、Markdownベースの指示ファイルを複数の種類でサポートしています。プロジェクトに複数種類の指示ファイルがある場合、VS Codeはそれらを結合してチャットコンテキストに追加しますが、特定の順序は保証されません。

* 1つの[`.github/copilot-instructions.md`](#use-a-githubcopilotinstructionsmd-file)ファイル
    * ワークスペース内のすべてのチャット要求に自動的に適用されます
    * ワークスペース内に保存されます

* 1つ以上の[`.instructions.md`](#use-instructionsmd-files)ファイル
    * globパターンを使用して、ファイルの種類や場所に基づいて条件付きで指示を適用します
    * ワークスペースまたはユーザープロファイルに保存されます

* 1つ以上の[`AGENTS.md`](#use-an-agentsmd-file)ファイル
    * ワークスペースで複数のAIエージェントと作業する場合に便利です
    * ワークスペース内のすべてのチャット要求、または特定のサブフォルダー（試験運用）に自動的に適用されます
    * ワークスペースのルート、またはサブフォルダー（試験運用）に保存されます

指示間の空白は無視されるため、指示は1つの段落として書くことも、1行ごとに書くことも、可読性のために空行で区切ることもできます。

ファイルやURLなど、指示内で特定のコンテキストを参照するには、Markdownリンクを使用できます。

## カスタム指示の例

次の例は、カスタム指示の使用方法を示しています。コミュニティが提供した例については、[Awesome Copilotリポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

<details>
<summary>例: 一般的なコーディングガイドライン</summary>

```markdown
---
applyTo: "**"
---
# プロジェクトの一般的なコーディング標準

## 命名規則
- コンポーネント名、インターフェイス、型エイリアスにはPascalCaseを使用します
- 変数、関数、メソッドにはcamelCaseを使用します
- privateなクラスメンバーにはアンダースコア（_）を前置します
- 定数にはALL_CAPSを使用します

## エラー処理
- 非同期処理にはtry/catchブロックを使用します
- Reactコンポーネントで適切なエラーバウンダリを実装します
- コンテキスト情報とともに常にエラーをログに記録します
```

</details>

<details>
<summary>例: 言語固有のコーディングガイドライン</summary>

これらの指示が一般的なコーディングガイドラインファイルを参照していることに注目してください。指示は複数のファイルに分割して、整理し、特定のトピックに集中させることができます。

```markdown
---
applyTo: "**/*.ts,**/*.tsx"
---
# TypeScriptとReact向けのプロジェクトコーディング標準

すべてのコードに[一般的なコーディングガイドライン](./general-coding.instructions.md)を適用します。

## TypeScriptガイドライン
- 新規コードはすべてTypeScriptを使用します
- 可能な限り関数型プログラミングの原則に従います
- データ構造と型定義にはインターフェイスを使用します
- 不変データ（const、readonly）を優先します
- オプショナルチェーン（?.）およびNull合体（??）演算子を使用します

## Reactガイドライン
- フックを使った関数コンポーネントを使用します
- Reactフックのルールに従います（条件付きフックは不可）
- 子要素を持つコンポーネントにはReact.FC型を使用します
- コンポーネントは小さく、目的を絞って保ちます
- コンポーネントのスタイル設定にはCSS Modulesを使用します
```

</details>

<details>
<summary>例: ドキュメント執筆ガイドライン</summary>

ドキュメント作成のような非開発アクティビティを含め、さまざまな種類のタスクに向けた指示ファイルを作成できます。

```markdown
---
applyTo: "docs/**/*.md"
---
# プロジェクトのドキュメント執筆ガイドライン

## 一般的なガイドライン
- 明確で簡潔なドキュメントを書きます。
- 用語とスタイルの一貫性を保ちます。
- 適用可能な場合はコード例を含めます。

## 文法
* 過去形（was、opened）の代わりに現在形（is、open）を使用します。
* 事実の記述と直接的な命令を書きます。「could」や「would」のような仮定表現は避けます。
* 主語が動作を行う能動態を使用します。
* 読者に直接語りかけるため、二人称（you）で書きます。

## Markdownガイドライン
- 見出しを使って内容を整理します。
- 箇条書きにはバレットを使用します。
- 関連リソースへのリンクを含めます。
- コードスニペットにはコードブロックを使用します。
```

</details>

## `.github/copilot-instructions.md`ファイルを使用する

ワークスペースのルートにある1つの`.github/copilot-instructions.md`Markdownファイルでカスタム指示を定義します。VS Codeは、このファイルの指示をワークスペース内のすべてのチャット要求に自動的に適用します。

`.github/copilot-instructions.md`ファイルを使用するには:

1. `setting(github.copilot.chat.codeGeneration.useInstructionFiles)`設定を有効にします。

1. ワークスペースのルートに`.github/copilot-instructions.md`ファイルを作成します。必要に応じて、先に`.github`ディレクトリを作成します。

1. 自然言語で、Markdown形式を使って指示を記述します。

> [!NOTE]
> Visual StudioおよびGitHub.comのGitHub Copilotも`.github/copilot-instructions.md`ファイルを検出します。VS CodeとVisual Studioの両方で使用するワークスペースがある場合、同じファイルを使用して両方のエディター向けのカスタム指示を定義できます。

## `.instructions.md`ファイルを使用する

すべてのチャット要求に適用される単一の指示ファイルを使用する代わりに、特定のファイルの種類やタスクに適用される複数の`.instructions.md`ファイルを作成できます。たとえば、異なるプログラミング言語、フレームワーク、またはプロジェクト種類ごとに指示ファイルを作成できます。

指示ファイルヘッダーのフロントマターにある`applyTo`プロパティを使用すると、globパターンを指定して、どのファイルに指示を自動適用するかを定義できます。指示ファイルはファイルの作成または変更時に使用され、通常、読み取り操作には適用されません。

または、チャットビューで**コンテキストを追加**>**指示**オプションを使用して、特定のチャットプロンプトに手動で指示ファイルを添付できます。

* **ワークスペースの指示ファイル**: ワークスペース内でのみ利用でき、ワークスペースの`.github/instructions`フォルダーに保存されます。
* **ユーザーの指示ファイル**: 複数のワークスペースで利用でき、現在の[VS Codeプロファイル](/docs/configure/profiles.md)に保存されます。

### 指示ファイルの形式

指示ファイルはMarkdownファイルで、拡張子に`.instructions.md`を使用し、次の構造になります:

#### ヘッダー（省略可能）

ヘッダーは、次のフィールドを含むYAMLフロントマターとして書式設定します:

| Field     | Description                                                                                   |
| --------- | ------------------------------------------------- |
| `description` | 指示ファイルの簡単な説明。 |
| `name`        | UIで使用される指示ファイルの名前。指定しない場合はファイル名が使用されます。 |
| `applyTo`     | 指示をどのファイルに自動適用するかを定義する、省略可能なglobパターン（ワークスペースルートからの相対パス）。すべてのファイルに適用するには`**`を使用します。値を指定しない場合、指示は自動適用されませんが、チャット要求に手動で追加できます。 |

#### 本文

指示ファイルの本文には、指示が適用されるときにLLMへ送信されるカスタム指示が含まれます。AIに従わせたい具体的なガイドライン、ルール、またはその他の関連情報を記述します。

本文中でエージェントツールを参照するには、`#tool:<tool-name>`構文を使用します。たとえば、`githubRepo`ツールを参照するには`#tool:githubRepo`を使用します。

例:

```markdown
---
applyTo: "**/*.py"
---
# Python向けのプロジェクトコーディング標準
- PythonのPEP 8スタイルガイドに従います。
- 可読性と明確さを常に優先します。
- 各関数に明確で簡潔なコメントを書きます。
- 関数には説明的な名前を付け、型ヒントを含めます。
- 適切なインデントを維持します（インデントレベルごとに4スペースを使用します）。
```

### 指示ファイルを作成する

指示ファイルを作成する際は、ワークスペースに保存するか、ユーザープロファイルに保存するかを選択します。ワークスペースの指示ファイルはそのワークスペースにのみ適用され、ユーザーの指示ファイルは複数のワークスペースで利用できます。

指示ファイルを作成するには:

1. チャットビューで**チャットの構成**（歯車アイコン）>**チャット指示**を選択し、**新しい指示ファイル**を選択します。

    ![チャットビューとチャットの構成メニューを示し、チャットの構成ボタンが強調表示されているスクリーンショット。](../images/customization/configure-chat-instructions.png)

    または、コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: New Instructions File**コマンドを使用します。

1. 指示ファイルを作成する場所を選択します。

    * **ワークスペース**: ワークスペース内でのみ使用するために、ワークスペースの`.github/instructions`フォルダーに指示ファイルを作成します。`setting(chat.instructionsFilesLocations)`設定で、ワークスペースに指示フォルダーを追加できます。

    * **ユーザープロファイル**: すべてのワークスペースで使用するために、[現在のプロファイルフォルダー](/docs/configure/profiles.md)に指示ファイルを作成します。

1. 指示ファイルのファイル名を入力します。これはUIで使用される既定の名前です。

1. Markdown書式を使用してカスタム指示を作成します。

    * ファイル先頭のYAMLフロントマターに入力して、指示の説明、名前、適用条件を構成します。
    * ファイル本文に指示を追加します。

既存の指示ファイルを変更するには、チャットビューで**チャットの構成**（歯車アイコン）>**チャット指示**を選択し、一覧から指示ファイルを選択します。あるいは、コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: Configure Instructions**コマンドを使用し、クイックピックから指示ファイルを選択します。

## `AGENTS.md`ファイルを使用する

ワークスペースで複数のAIエージェントと作業する場合、ワークスペースのルートにある`AGENTS.md`Markdownファイルで、すべてのエージェント向けのカスタム指示を定義できます。VS Codeは、このファイルの指示をワークスペース内のすべてのチャット要求に自動的に適用します。

`AGENTS.md`ファイルのサポートを有効または無効にするには、`setting(chat.useAgentsMdFile)`設定を構成します。

### 複数の`AGENTS.md`ファイルを使用する（試験運用）

サブフォルダーに複数の`AGENTS.md`ファイルを使用すると、プロジェクトの異なる部分に異なる指示を適用したい場合に便利です。たとえば、フロントエンドコード用の`AGENTS.md`ファイルと、バックエンドコード用の別のファイルを用意できます。

試験運用の`setting(chat.useNestedAgentsMdFiles)`設定を使用して、ワークスペース内のネストされた`AGENTS.md`ファイルのサポートを有効または無効にします。

有効にすると、VS Codeはワークスペースのすべてのサブフォルダーを再帰的に検索して`AGENTS.md`ファイルを見つけ、それらの相対パスをチャットコンテキストに追加します。エージェントは、編集中のファイルに基づいてどの指示を使用するかを決定できます。

> [!TIP]
> フォルダー固有の指示には、フォルダー構造に一致する異なる`applyTo`パターンを持つ複数の[`.instructions.md`](#use-instructionsmd-files)ファイルも使用できます。

## 設定でカスタム指示を指定する

VS Codeのユーザー設定またはワークスペース設定を使用して、特殊なシナリオ向けにカスタム指示を構成できます。

| Type of instruction | Setting name |
|---------------------|--------------|
| コードレビュー | `setting(github.copilot.chat.reviewSelection.instructions)` |
| コミットメッセージ生成 | `setting(github.copilot.chat.commitMessageGeneration.instructions)` |
| プルリクエストのタイトルと説明の生成 | `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` |
| コード生成（非推奨）* | `setting(github.copilot.chat.codeGeneration.instructions)` |
| テスト生成（非推奨）* | `setting(github.copilot.chat.testGeneration.instructions)` |

_* `codeGeneration`および`testGeneration`設定は、VS Code 1.102で非推奨になりました。代わりに（`.github/copilot-instructions.md`または`*.instructions.md`の）指示ファイルを使用することを推奨します。_

設定値のテキスト（`text`プロパティ）としてカスタム指示を定義することも、ワークスペース内の外部ファイル（`file`プロパティ）を参照することもできます。

次のコードスニペットは、`settings.json`ファイルで指示セットを定義する方法を示しています。

```json
{
    "github.copilot.chat.pullRequestDescriptionGeneration.instructions": [
        { "text": "主要な変更の一覧を必ず含めてください。" }
    ],
    "github.copilot.chat.reviewSelection.instructions": [
        { "file": "guidance/backend-review-guidelines.md" },
        { "file": "guidance/frontend-review-guidelines.md" }
    ]
}
```

## ワークスペース向けの指示ファイルを生成する

VS Codeはワークスペースを分析し、コーディング手法とプロジェクト構造に一致するカスタム指示を含む`.github/copilot-instructions.md`ファイルを生成できます。

ワークスペース向けの指示ファイルを生成するには:

1. チャットビューで**チャットの構成**（歯車アイコン）>**チャット指示を生成**を選択します。

1. 生成された指示ファイルを確認し、必要に応じて編集します。

## デバイス間でユーザーの指示ファイルを同期する

VS Codeは[設定の同期](/docs/configure/settings-sync.md)を使用して、ユーザーの指示ファイルを複数デバイス間で同期できます。

ユーザーの指示ファイルを同期するには、プロンプトファイルと指示ファイルに対して設定の同期を有効にします:

1. [設定の同期](/docs/configure/settings-sync.md)が有効になっていることを確認します。

1. コマンドパレット（`kb(workbench.action.showCommands)`）から**Settings Sync: Configure**を実行します。

1. 同期する設定の一覧から**Prompts and Instructions**を選択します。

## カスタム指示を定義するためのヒント

* 指示は短く、自己完結に保ちます。各指示は単純な1文にします。複数の情報を提供する必要がある場合は、複数の指示を使用します。

* タスクまたは言語固有の指示には、トピックごとに複数の`*.instructions.md`ファイルを使用し、`applyTo`プロパティで選択的に適用します。

* プロジェクト固有の指示はワークスペースに保存して、他のチームメンバーと共有し、バージョン管理に含めます。

* 指示の重複を避け、内容を簡潔で焦点の合ったものに保つために、[プロンプトファイル](/docs/copilot/customization/prompt-files.md)や[カスタムエージェント](/docs/copilot/customization/custom-agents.md)で指示ファイルを再利用し、参照します。

## 関連リソース

* [AI応答をカスタマイズする概要](/docs/copilot/customization/overview.md)
* [エージェントスキルを使用する](/docs/copilot/customization/agent-skills.md)
* [再利用可能なプロンプトファイルを作成する](/docs/copilot/customization/prompt-files.md)
* [カスタムエージェントを作成する](/docs/copilot/customization/custom-agents.md)
* [VS Codeでチャットを開始する](/docs/copilot/chat/copilot-chat.md)
* [チャットでツールを構成する](/docs/copilot/chat/chat-tools.md)
* [コミュニティ提供の指示、プロンプト、カスタムエージェント](https://github.com/github/awesome-copilot)
