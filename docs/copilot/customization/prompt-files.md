---
ContentId: 5c8e7d42-9b1a-4f85-a3e2-6d5b8a9c1e43
DateApproved: 12/10/2025
MetaDescription: VS CodeでGitHub Copilot Chat向けの再利用可能なプロンプトファイルを作成し、よくある開発タスクを標準化してコーディングワークフローの効率を高める方法を説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでプロンプトファイルを使用する

プロンプトファイルは、コード生成、コードレビューの実施、プロジェクトコンポーネントのスキャフォールディングなど、よくある開発タスク向けの再利用可能なプロンプトを定義するMarkdownファイルです。チャットから直接実行できる独立したプロンプトであり、標準化された開発ワークフローのライブラリを作成できます。

タスク固有のガイドラインを含めたり、カスタム指示を参照したりして、実行の一貫性を確保できます。すべてのリクエストに適用されるカスタム指示とは異なり、プロンプトファイルは特定のタスクに対してオンデマンドで実行されます。

VS Codeは、プロンプトファイルに対して2種類のスコープをサポートしています。

* **ワークスペースのプロンプトファイル**: ワークスペース内でのみ利用でき、ワークスペースの`.github/prompts`フォルダーに保存されます。
* **ユーザーのプロンプトファイル**: 複数のワークスペースで利用でき、現在の[VS Codeプロファイル](/docs/configure/profiles.md)に保存されます。

## プロンプトファイルの構造

プロンプトファイルはMarkdownファイルで、拡張子に`.prompt.md`を使用し、次の構造になっています。

### ヘッダー(任意)

ヘッダーはYAMLフロントマターとしてフォーマットされ、次のフィールドを含みます。

| Field | Description |
| --- | --- |
| `description`     | プロンプトの簡単な説明。 |
| `name`            | プロンプト名。チャットで`/`を入力した後に使用します。指定しない場合はファイル名が使われます。 |
| `argument-hint`   | 任意のヒントテキスト。チャットの入力欄に表示され、プロンプトの使い方を案内します。 |
| `agent`           | プロンプトの実行に使用するエージェント: `ask`、`edit`、`agent`、または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)名。既定では現在のエージェントが使用されます。ツールが指定され、現在のエージェントが`ask`または`edit`の場合、既定のエージェントは`agent`になります。 |
| `model`           | プロンプト実行時に使用する言語モデル。指定しない場合は、モデルピッカーで現在選択されているモデルが使用されます。 |
| `tools`           | このプロンプトで利用できるツール/ツールセット名の一覧。組み込みツール、ツールセット、MCPツール、拡張機能が提供するツールを含められます。MCPサーバーのすべてのツールを含めるには`<server name>/*`形式を使用します。<br/>詳細は[チャットのツール](/docs/copilot/chat/chat-tools.md)を参照してください。 |

> [!NOTE]
> プロンプト実行時に特定のツールが利用できない場合、そのツールは無視されます。

### Body

プロンプトファイルの本文には、チャットでプロンプトを実行する際にLLMへ送信されるプロンプトテキストが含まれます。AIに従ってほしい具体的な手順、ガイドライン、その他関連情報を記載します。

Markdownリンクを使って、他のワークスペースファイルを参照できます。これらのファイルを参照するには相対パスを使用し、プロンプトファイルの場所を基準にパスが正しいことを確認してください。

本文中でエージェントツールを参照するには、`#tool:<tool-name>`構文を使用します。たとえば`githubRepo`ツールを参照するには`#tool:githubRepo`を使用します。

プロンプトファイル内では、`${variableName}`構文を使って変数を参照できます。次の変数を参照できます。

* ワークスペース変数 - `${workspaceFolder}`、`${workspaceFolderBasename}`
* 選択範囲変数 - `${selection}`、`${selectedText}`
* ファイルコンテキスト変数 - `${file}`、`${fileBasename}`、`${fileDirname}`、`${fileBasenameNoExtension}`
* 入力変数 - `${input:variableName}`、`${input:variableName:placeholder}` (チャットの入力欄からプロンプトへ値を渡します)

### プロンプトファイルの例

次の例は、プロンプトファイルの使い方を示しています。コミュニティが提供する追加の例については、[Awesome Copilotリポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

<details>
<summary>例: Reactフォームコンポーネントを生成する</summary>

```markdown
---
agent: 'agent'
model: GPT-4o
tools: ['githubRepo', 'search/codebase']
description: '新しいReactフォームコンポーネントを生成する'
---
目標は、#tool:githubRepo contoso/react-templatesにあるテンプレートに基づいて、新しいReactフォームコンポーネントを生成することです。

指定されていない場合は、フォーム名とフィールドを尋ねてください。

フォームの要件:
* フォーム用デザインシステムコンポーネントを使用する: [design-system/Form.md](../docs/design-system/Form.md)
* フォーム状態管理に`react-hook-form`を使用する:
* フォームデータのTypeScript型を必ず定義する
* registerを使う*uncontrolled*コンポーネントを優先する
* 不要な再レンダリングを防ぐために`defaultValues`を使用する
* バリデーションに`yup`を使用する:
* 再利用可能なバリデーションスキーマを別ファイルに作成する
* TypeScript型を使って型安全性を確保する
* UXに配慮したバリデーションルールに調整する
```

</details>

<details>
<summary>例: REST APIのセキュリティレビューを実施する</summary>

```markdown
---
agent: 'ask'
model: Claude Sonnet 4
description: 'REST APIのセキュリティレビューを実施する'
---
REST APIのセキュリティレビューを実施し、対応すべきセキュリティ問題のTODOリストを提示してください。

* すべてのエンドポイントが認証と認可で保護されていることを確認する
* すべてのユーザー入力を検証し、データをサニタイズする
* レート制限とスロットリングを実装する
* セキュリティイベントのログ記録と監視を実装する

TODOリストはMarkdown形式で返し、優先度と問題種別ごとにグループ化してください。
```

</details>

## プロンプトファイルを作成する

プロンプトファイルを作成するときは、ワークスペースに保存するか、ユーザープロファイルに保存するかを選びます。ワークスペースのプロンプトファイルはそのワークスペースにのみ適用され、ユーザーのプロンプトファイルは複数のワークスペースで利用できます。

プロンプトファイルを作成するには:

1. チャットビューで**Configure Chat**(歯車アイコン) > **Prompt Files**を選択し、**New prompt file**を選択します。

    ![Screenshot showing the Chat view, and Configure Chat menu, highlighting the Configure Chat button.](../images/customization/configure-chat-instructions.png)

    または、コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: New Prompt File**または**Chat: New Untitled Prompt File**コマンドを使用します。

1. プロンプトファイルを作成する場所を選択します。

    * **Workspace**: ワークスペース内でのみ使用するために、ワークスペースの`.github/prompts`フォルダーにプロンプトファイルを作成します。`setting(chat.promptFilesLocations)`設定で、ワークスペースにプロンプトフォルダーを追加できます。

    * **User profile**: すべてのワークスペースで使用するために、[現在のプロファイルフォルダー](/docs/configure/profiles.md)にプロンプトファイルを作成します。

1. プロンプトファイルのファイル名を入力します。これはチャットで`/`を入力したときに表示される既定の名前です。

1. Markdown書式を使ってチャットプロンプトを作成します。

    * ファイル先頭のYAMLフロントマターを埋めて、プロンプトの説明、エージェント、ツール、その他の設定を構成します。
    * ファイル本文にプロンプトの指示を追加します。

既存のプロンプトファイルを変更するには、チャットビューで**Configure Chat** > **Prompt Files**を選択し、一覧からプロンプトファイルを選びます。または、コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: Configure Prompt Files**コマンドを使用し、クイックピックからプロンプトファイルを選択します。

## チャットでプロンプトファイルを使用する

プロンプトファイルを実行する方法はいくつかあります。

* チャットビューで、チャット入力欄に`/`に続けてプロンプト名を入力します。

    チャット入力欄に追加情報を入れることもできます。たとえば`/create-react-form formName=MyForm`や`/create-api for listing customers`のように入力します。

* コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: Run Prompt**コマンドを実行し、クイックピックからプロンプトファイルを選択します。

* エディターでプロンプトファイルを開き、エディタータイトル領域の再生ボタンを押します。プロンプトを現在のチャットセッションで実行するか、新しいチャットセッションを開くかを選べます。

    この方法は、プロンプトファイルを素早くテストして反復改善するのに便利です。

> [!TIP]
> `setting(chat.promptFilesRecommendations)`設定を使用すると、新しいチャットセッションの開始時に、推奨アクションとしてプロンプトを表示できます。
>
> ![Screenshot showing an "explain" prompt file recommendation in the Chat view.](../images/customization/prompt-file-recommendations.png)

## ツール一覧の優先順位

`tools`メタデータフィールドを使うことで、カスタムエージェントとプロンプトファイルの両方で利用可能なツール一覧を指定できます。また、プロンプトファイルは`agent`メタデータフィールドを使ってカスタムエージェントを参照することもできます。

チャットで利用できるツール一覧は、次の優先順位で決まります。

1. プロンプトファイルで指定されたツール(ある場合)
2. プロンプトファイルで参照しているカスタムエージェントのツール(ある場合)
3. 選択したエージェントの既定ツール(ある場合)

## デバイス間でユーザーのプロンプトファイルを同期する

VS Codeは[設定の同期](/docs/configure/settings-sync.md)を使用して、ユーザーのプロンプトファイルを複数のデバイス間で同期できます。

ユーザーのプロンプトファイルを同期するには、プロンプトファイルと指示ファイルに対して設定の同期を有効にします。

1. [設定の同期](/docs/configure/settings-sync.md)が有効になっていることを確認します。

1. コマンドパレット(`kb(workbench.action.showCommands)`)から**Settings Sync: Configure**を実行します。

1. 同期する設定の一覧から**Prompts and Instructions**を選択します。

## プロンプトファイル定義のヒント

* プロンプトが達成すべきことと、期待する出力形式を明確に記述します。

* 期待する入力例と出力例を提示して、AIの応答をガイドします。

* 各プロンプトにガイドラインを重複して書くのではなく、Markdownリンクを使ってカスタム指示を参照します。

* `${selection}`のような組み込み変数や入力変数を活用して、プロンプトの柔軟性を高めます。

* エディターの再生ボタンを使ってプロンプトをテストし、結果に基づいて改善します。

## 関連リソース

* [AI応答のカスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム指示を作成する](/docs/copilot/customization/custom-instructions.md)
* [カスタムエージェントを作成する](/docs/copilot/customization/custom-agents.md)
* [VS Codeでチャットを始める](/docs/copilot/chat/copilot-chat.md)
* [チャットでツールを構成する](/docs/copilot/chat/chat-tools.md)
* [コミュニティ提供の指示、プロンプト、カスタムエージェント](https://github.com/github/awesome-copilot)
