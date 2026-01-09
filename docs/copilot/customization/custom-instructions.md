---
ContentId: 8b4f3c21-4e02-4a89-9f15-7a8d6b5c2e91
DateApproved: 12/10/2025
MetaDescription: VS CodeのGitHub Copilot Chat用にカスタム指示を作成して、AIの応答がコーディングプラクティス、プロジェクト要件、開発標準に一致するようにする方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでカスタム指示を使用する

カスタム指示を使用すると、AIがコードを生成し、その他の開発タスクを処理する方法に自動的に影響を与える一般的なガイドラインとルールを定義できます。チャットプロンプトごとにコンテキストを手動で含める代わりに、Markdownファイルでカスタム指示を指定して、コーディングプラクティスやプロジェクト要件に沿った一貫したAI応答を確保します。

カスタム指示は、すべてのチャットリクエストに自動的に適用するか、特定のファイルにのみ適用するように構成できます。あるいは、特定のチャットプロンプトに手動でカスタム指示を添付することもできます。

> [!NOTE]
> カスタム指示は、エディターで入力する際の[インライン候補](/docs/copilot/ai-powered-suggestions.md)では考慮されません。

## 指示ファイルの種類

VS Codeは、複数の種類のMarkdownベースの指示ファイルをサポートしています。プロジェクトに複数の種類の指示ファイルがある場合、VS Codeはそれらを組み合わせてチャットコンテキストに追加します。特定の順序は保証されません。

* 単一の[`.github/copilot-instructions.md`](#use-a-githubcopilotinstructionsmd-file)ファイル
    * ワークスペース内のすべてのチャットリクエストに自動的に適用されます
    * ワークスペース内に保存されます

* 1つ以上の[`.instructions.md`](#use-instructionsmd-files)ファイル
    * globパターンを使用して、ファイルの種類または場所に基づいて条件付きで指示を適用します
    * ワークスペースまたはユーザープロファイルに保存されます

* 1つ以上の[`AGENTS.md`](#use-an-agentsmd-file)ファイル
    * ワークスペース内で複数のAIエージェントを使用する場合に便利です
    * ワークスペース内のすべてのチャットリクエスト、または特定のサブフォルダー（実験的）に自動的に適用されます
    * ワークスペースのルートまたはサブフォルダー（実験的）に保存されます

指示間の空白は無視されるため、指示は単一の段落として記述したり、それぞれ新しい行に記述したり、読みやすくするために空行で区切ったりすることができます。

ファイルやURLなど、指示内の特定のコンテキストを参照するには、Markdownリンクを使用できます。

## カスタム指示の例

以下の例は、カスタム指示の使用方法を示しています。コミュニティから提供されたその他の例については、[Awesome Copilotリポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

<details>
<summary>例: 一般的なコーディングガイドライン</summary>

```markdown
---
applyTo: "**"
---
# プロジェクトの一般的なコーディング標準

## 命名規則
- コンポーネント名、インターフェース、型エイリアスにはPascalCaseを使用する
- 変数、関数、メソッドにはcamelCaseを使用する
- プライベートクラスメンバーの接頭辞にアンダースコア (_) を付ける
- 定数にはALL_CAPSを使用する

## エラー処理
- 非同期操作にはtry/catchブロックを使用する
- Reactコンポーネントに適切なエラー境界を実装する
- 常にコンテキスト情報とともにエラーをログに記録する
```

</details>

<details>
<summary>例: 言語固有のコーディングガイドライン</summary>

これらの指示が一般的なコーディングガイドラインファイルを参照していることに注目してください。指示を複数のファイルに分割して、整理し、特定のトピックに集中させることができます。

```markdown
---
applyTo: "**/*.ts,**/*.tsx"
---
# TypeScriptとReactのプロジェクトコーディング標準

すべてのコードに[一般的なコーディングガイドライン](./general-coding.instructions.md)を適用する。

## TypeScriptガイドライン
- すべての新しいコードにTypeScriptを使用する
- 可能な場合は関数型プログラミングの原則に従う
- データ構造と型定義にはインターフェースを使用する
- 不変データ (const、readonly) を優先する
- オプショナルチェーン (?.) とNull合体 (??) 演算子を使用する

## Reactガイドライン
- フック付きの関数コンポーネントを使用する
- Reactフックのルールに従う（条件付きフックなし）
- 子を持つコンポーネントにはReact.FC型を使用する
- コンポーネントを小さく、焦点を絞って保つ
- コンポーネントのスタイル設定にはCSSモジュールを使用する
```

</details>

<details>
<summary>例: ドキュメント作成ガイドライン</summary>

ドキュメントの作成などの非開発アクティビティを含む、さまざまな種類のタスク用の指示ファイルを作成できます。

```markdown
---
applyTo: "docs/**/*.md"
---
# プロジェクトドキュメント作成ガイドライン

## 一般的なガイドライン
- 明確かつ簡潔なドキュメントを作成する。
- 一貫した用語とスタイルを使用する。
- 該当する場合はコード例を含める。

## 文法
* 過去形 (was, opened) の代わりに現在形 (is, open) を使用する。
* 事実に基づく記述と直接的なコマンドを記述する。"could"や"would"のような仮定は避ける。
* 主語がアクションを実行する能動態を使用する。
* 読者に直接語りかけるように二人称 (you) で記述する。

## Markdownガイドライン
- 見出しを使用してコンテンツを整理する。
- リストには箇条書きを使用する。
- 関連リソースへのリンクを含める。
- コードスニペットにはコードブロックを使用する。
```

</details>

## `.github/copilot-instructions.md`ファイルを使用する

ワークスペースのルートにある単一の`.github/copilot-instructions.md`Markdownファイルでカスタム指示を定義します。VS Codeは、このファイルの指示をワークスペース内のすべてのチャットリクエストに自動的に適用します。

`.github/copilot-instructions.md`ファイルを使用するには:

1. `setting(github.copilot.chat.codeGeneration.useInstructionFiles)`設定を有効にします。

1. ワークスペースのルートに`.github/copilot-instructions.md`ファイルを作成します。必要に応じて、最初に`.github`ディレクトリを作成してください。

1. 自然言語とMarkdown形式を使用して指示を記述します。

> [!NOTE]
> Visual StudioおよびGitHub.comのGitHub Copilotも`.github/copilot-instructions.md`ファイルを検出します。VS CodeとVisual Studioの両方で使用するワークスペースがある場合は、同じファイルを使用して両方のエディターのカスタム指示を定義できます。

## `.instructions.md`ファイルを使用する

すべてのチャットリクエストに適用される単一の指示ファイルを使用する代わりに、特定のファイルの種類やタスクに適用される複数の`.instructions.md`ファイルを作成できます。たとえば、さまざまなプログラミング言語、フレームワーク、またはプロジェクトタイプ用の指示ファイルを作成できます。

指示ファイルヘッダーの`applyTo`フロントマタープロパティを使用すると、globパターンを指定して、指示を自動的に適用するファイルを定義できます。指示ファイルは、ファイルの作成または変更時に使用され、通常、読み取り操作には適用されません。

あるいは、チャットビューの**Add Context** > **Instructions**オプションを使用して、特定のチャットプロンプトに手動で指示ファイルを添付することもできます。

* **ワークスペース指示ファイル**: ワークスペース内でのみ使用でき、ワークスペースの`.github/instructions`フォルダーに保存されます。
* **ユーザー指示ファイル**: 複数のワークスペースで使用でき、現在の[VS Codeプロファイル](/docs/configure/profiles.md)に保存されます。

### 指示ファイルの形式

指示ファイルはMarkdownファイルであり、`.instructions.md`拡張子を使用し、次の構造を持っています。

#### ヘッダー (オプション)

ヘッダーは、次のフィールドを持つYAMLフロントマターとしてフォーマットされます。

| フィールド | 説明 |
| --------- | ------------------------------------------------- |
| `description` | 指示ファイルの短い説明。 |
| `name` | UIで使用される指示ファイルの名前。指定しない場合は、ファイル名が使用されます。 |
| `applyTo` | ワークスペースルートに対する相対パスで、指示を自動的に適用するファイルを定義するオプションのglobパターン。すべてのファイルに適用するには`**`を使用します。値を指定しない場合、指示は自動的に適用されませんが、チャットリクエストに手動で追加することはできます。 |

#### 本文

指示ファイルの本文には、指示が適用されたときにLLMに送信されるカスタム指示が含まれています。AIに従わせたい特定のガイドライン、ルール、またはその他の関連情報を提供します。

本文テキストでエージェントツールを参照するには、`#tool:<tool-name>`構文を使用します。たとえば、`githubRepo`ツールを参照するには、`#tool:githubRepo`を使用します。

例:

```markdown
---
applyTo: "**/*.py"
---
# Pythonのプロジェクトコーディング標準
- PythonのPEP 8スタイルガイドに従う。
- 常に読みやすさと明確さを優先する。
- 各関数に明確かつ簡潔なコメントを記述する。
- 関数に記述的な名前を付け、型ヒントを含めるようにする。
- 適切なインデントを維持する（インデントの各レベルに4つのスペースを使用する）。
```

### 指示ファイルを作成する

指示ファイルを作成するときに、ワークスペースに保存するかユーザープロファイルに保存するかを選択します。ワークスペース指示ファイルはそのワークスペースにのみ適用されますが、ユーザー指示ファイルは複数のワークスペースで使用できます。

指示ファイルを作成するには:

1. チャットビューで、**チャットの構成** (歯車アイコン) > **チャットの指示**を選択し、**新しい指示ファイル**を選択します。

    ![チャットビューとチャットの構成メニューを表示し、チャットの構成ボタンを強調表示しているスクリーンショット。](../images/customization/configure-chat-instructions.png)

    または、コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: New Instructions File**コマンドを使用します。

1. 指示ファイルを作成する場所を選択します。

    * **ワークスペース**: ワークスペースの`.github/instructions`フォルダーに指示ファイルを作成して、そのワークスペース内でのみ使用します。`setting(chat.instructionsFilesLocations)`設定を使用して、ワークスペースに指示フォルダーを追加します。

    * **ユーザープロファイル**: [現在のプロファイルフォルダー](/docs/configure/profiles.md)に指示ファイルを作成して、すべてのワークスペースで使用します。

1. 指示ファイルのファイル名を入力します。これは、UIで使用されるデフォルトの名前です。

1. Markdown形式を使用してカスタム指示を作成します。

    * ファイル上部のYAMLフロントマターに入力して、指示の説明、名前、適用時期を構成します。
    * ファイルの本文に指示を追加します。

既存の指示ファイルを変更するには、チャットビューで**チャットの構成** (歯車アイコン) > **チャットの指示**を選択し、リストから指示ファイルを選択します。または、コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: Configure Instructions**コマンドを使用し、クイックピックから指示ファイルを選択します。

## `AGENTS.md`ファイルを使用する

ワークスペースで複数のAIエージェントを使用する場合、ワークスペースのルートにある`AGENTS.md`Markdownファイルですべてのエージェントのカスタム指示を定義できます。VS Codeは、このファイルの指示をワークスペース内のすべてのチャットリクエストに自動的に適用します。

`AGENTS.md`ファイルのサポートを有効または無効にするには、`setting(chat.useAgentsMdFile)`設定を構成します。

### 複数の`AGENTS.md`ファイルを使用する (実験的)

サブフォルダーで複数の`AGENTS.md`ファイルを使用すると、プロジェクトのさまざまな部分に異なる指示を適用する場合に便利です。たとえば、フロントエンドコード用に1つの`AGENTS.md`ファイルを用意し、バックエンドコード用に別のファイルを用意できます。

ワークスペース内のネストされた`AGENTS.md`ファイルのサポートを有効または無効にするには、実験的な`setting(chat.useNestedAgentsMdFiles)`設定を使用します。

有効にすると、VS Codeはワークスペースのすべてのサブフォルダー内の`AGENTS.md`ファイルを再帰的に検索し、その相対パスをチャットコンテキストに追加します。エージェントは、編集中のファイルに基づいて使用する指示を決定できます。

> [!TIP]
> フォルダー固有の指示については、フォルダー構造に一致するさまざまな`applyTo`パターンを持つ複数の[`.instructions.md`](#use-instructionsmd-files)ファイルを使用することもできます。

## 設定でカスタム指示を指定する

VS Codeのユーザー設定またはワークスペース設定を使用して、特定のシナリオ用のカスタム指示を構成できます。

| 指示の種類 | 設定名 |
|---------------------|--------------|
| コードレビュー | `setting(github.copilot.chat.reviewSelection.instructions)` |
| コミットメッセージの生成 | `setting(github.copilot.chat.commitMessageGeneration.instructions)` |
| プルリクエストのタイトルと説明の生成 | `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` |
| コード生成 (非推奨)* | `setting(github.copilot.chat.codeGeneration.instructions)` |
| テスト生成 (非推奨)* | `setting(github.copilot.chat.testGeneration.instructions)` |

_\* `codeGeneration`および`testGeneration`設定は、VS Code 1.102の時点で非推奨です。代わりに指示ファイル（`.github/copilot-instructions.md`または`*.instructions.md`）を使用することをお勧めします。_

カスタム指示は、設定値（`text`プロパティ）のテキストとして定義するか、ワークスペース内の外部ファイル（`file`プロパティ）を参照して定義できます。

次のコードスニペットは、`settings.json`ファイルで一連の指示を定義する方法を示しています。

```json
{
    "github.copilot.chat.pullRequestDescriptionGeneration.instructions": [
        { "text": "常に主な変更点のリストを含める。" }
    ],
    "github.copilot.chat.reviewSelection.instructions": [
        { "file": "guidance/backend-review-guidelines.md" },
        { "file": "guidance/frontend-review-guidelines.md" }
    ]
}
```

## ワークスペースの指示ファイルを生成する

VS Codeは、ワークスペースを分析し、コーディングプラクティスやプロジェクト構造に一致するカスタム指示を含む一致する`.github/copilot-instructions.md`ファイルを生成できます。

ワークスペースの指示ファイルを生成するには:

1. チャットビューで、**チャットの構成** (歯車アイコン) > **チャットの指示を生成**を選択します。

1. 生成された指示ファイルを確認し、必要な編集を行います。

## ユーザー指示ファイルをデバイス間で同期する

VS Codeは、[設定の同期](/docs/configure/settings-sync.md)を使用して、ユーザー指示ファイルを複数のデバイス間で同期できます。

ユーザー指示ファイルを同期するには、プロンプトと指示ファイルの設定の同期を有効にします。

1. [設定の同期](/docs/configure/settings-sync.md)が有効になっていることを確認します。

1. コマンドパレット(`kb(workbench.action.showCommands)`)から**Settings Sync: Configure**を実行します。

1. 同期する設定のリストから**Prompts and Instructions**を選択します。

## カスタム指示を定義するためのヒント

* 指示は短く、自己完結型にしてください。各指示は、単一の単純なステートメントである必要があります。複数の情報を提供する必要がある場合は、複数の指示を使用してください。

* タスクまたは言語固有の指示については、トピックごとに複数の`*.instructions.md`ファイルを使用し、`applyTo`プロパティを使用して選択的に適用します。

* プロジェクト固有の指示をワークスペースに保存して、他のチームメンバーと共有し、バージョン管理に含めます。

* [プロンプトファイル](/docs/copilot/customization/prompt-files.md)や[カスタムエージェント](/docs/copilot/customization/custom-agents.md)で指示ファイルを再利用および参照して、クリーンで集中した状態を保ち、指示の重複を避けます。

## 関連リソース

* [AI応答のカスタマイズの概要](/docs/copilot/customization/overview.md)
* [エージェントスキルの使用](/docs/copilot/customization/agent-skills.md)
* [再利用可能なプロンプトファイルの作成](/docs/copilot/customization/prompt-files.md)
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)
* [VS Codeでのチャットの開始](/docs/copilot/chat/copilot-chat.md)
* [チャットでのツールの構成](/docs/copilot/chat/chat-tools.md)
* [コミュニティが貢献した指示、プロンプト、カスタムエージェント](https://github.com/github/awesome-copilot)
