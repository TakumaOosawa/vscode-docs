---
ContentId: 5c8e7d42-9b1a-4f85-a3e2-6d5b8a9c1e43
DateApproved: 12/10/2025
MetaDescription: VS Code の GitHub Copilot Chat で再利用可能なプロンプトファイルを作成して、一般的な開発タスクを標準化し、コーディングワークフローの効率を向上させる方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Code でプロンプトファイルを使用する

プロンプトファイルは、コードの生成、コードレビューの実行、プロジェクトコンポーネントのスキャフォールディングなどの一般的な開発タスクの再利用可能なプロンプトを定義する Markdown ファイルです。これらはチャットで直接実行できるスタンドアロンのプロンプトであり、標準化された開発ワークフローのライブラリを作成できます。

タスク固有のガイドラインを含めたり、カスタム指示を参照して、一貫した実行を保証したりできます。すべてのリクエストに適用されるカスタム指示とは異なり、プロンプトファイルは特定のタスクに対してオンデマンドでトリガーされます。

VS Code は、プロンプトファイルに対して次の2種類のスコープをサポートしています。

* **ワークスペースプロンプトファイル**: ワークスペース内でのみ使用可能で、ワークスペースの `.github/prompts` フォルダーに保存されます。
* **ユーザープロンプトファイル**: 複数のワークスペースで使用可能で、現在の [VS Code プロファイル](/docs/configure/profiles.md)に保存されます。

## プロンプトファイルの構造

プロンプトファイルは Markdown ファイルであり、`.prompt.md` 拡張子を使用し、次の構造を持ちます。

### ヘッダー（オプション）

ヘッダーは YAML frontmatter としてフォーマットされており、次のフィールドがあります。

| フィールド | 説明 |
| --- | --- |
| `description`     | プロンプトの短い説明。 |
| `name`            | チャットで `/` を入力した後に使用されるプロンプトの名前。指定しない場合は、ファイル名が使用されます。 |
| `argument-hint`   | プロンプトとの対話方法についてユーザーをガイドするためにチャット入力フィールドに表示されるオプションのヒントテキスト。 |
| `agent`           | プロンプトの実行に使用されるエージェント: `ask`、`edit`、`agent`、または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)の名前。デフォルトでは、現在のエージェントが使用されます。ツールが指定され、現在のエージェントが `ask` または `edit` の場合、デフォルトのエージェントは `agent` になります。 |
| `model`           | プロンプトの実行時に使用される言語モデル。指定しない場合は、モデルピッカーで現在選択されているモデルが使用されます。 |
| `tools`           | このプロンプトで使用可能なツールまたはツールセット名のリスト。組み込みツール、ツールセット、MCPツール、または拡張機能によって提供されるツールを含めることができます。MCPサーバーのすべてのツールを含めるには、`<server name>/*` 形式を使用します。<br/>詳細については、[チャットツールの構成](/docs/copilot/chat/chat-tools.md)を参照してください。 |

> [!NOTE]
> プロンプトの実行時に指定されたツールが利用できない場合、そのツールは無視されます。

### 本文

プロンプトファイルの本文には、チャットでプロンプトを実行するときに LLM に送信されるプロンプトテキストが含まれます。AI に従わせたい具体的な指示、ガイドライン、またはその他の関連情報を提供します。

Markdown リンクを使用して、他のワークスペースファイルを参照できます。相対パスを使用してこれらのファイルを参照し、プロンプトファイルの場所に基づいてパスが正しいことを確認してください。

本文テキストでエージェントツールを参照するには、`#tool:<tool-name>` 構文を使用します。たとえば、`githubRepo` ツールを参照するには、`#tool:githubRepo` を使用します。

プロンプトファイル内では、`${variableName}` 構文を使用して変数を参照できます。参照できる変数は次のとおりです。

* ワークスペース変数 - `${workspaceFolder}`, `${workspaceFolderBasename}`
* 選択変数 - `${selection}`, `${selectedText}`
* ファイルコンテキスト変数 - `${file}`, `${fileBasename}`, `${fileDirname}`, `${fileBasenameNoExtension}`
* 入力変数 - `${input:variableName}`, `${input:variableName:placeholder}` (チャット入力フィールドからプロンプトに値を渡す)

### プロンプトファイルの例

次の例は、プロンプトファイルの使用方法を示しています。コミュニティが提供したその他の例については、[Awesome Copilot リポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

<details>
<summary>例: React フォームコンポーネントを生成する</summary>

```markdown
---
agent: 'agent'
model: GPT-4o
tools: ['githubRepo', 'search/codebase']
description: 'Generate a new React form component'
---
Your goal is to generate a new React form component based on the templates in #tool:githubRepo contoso/react-templates.

Ask for the form name and fields if not provided.

Requirements for the form:
* Use form design system components: [design-system/Form.md](../docs/design-system/Form.md)
* Use `react-hook-form` for form state management:
* Always define TypeScript types for your form data
* Prefer *uncontrolled* components using register
* Use `defaultValues` to prevent unnecessary rerenders
* Use `yup` for validation:
* Create reusable validation schemas in separate files
* Use TypeScript types to ensure type safety
* Customize UX-friendly validation rules
```

</details>

<details>
<summary>例: REST API のセキュリティレビューを実行する</summary>

```markdown
---
agent: 'ask'
model: Claude Sonnet 4
description: 'Perform a REST API security review'
---
Perform a REST API security review and provide a TODO list of security issues to address.

* Ensure all endpoints are protected by authentication and authorization
* Validate all user inputs and sanitize data
* Implement rate limiting and throttling
* Implement logging and monitoring for security events

Return the TODO list in a Markdown format, grouped by priority and issue type.
```

</details>

## プロンプトファイルを作成する

プロンプトファイルを作成するときは、ワークスペースに保存するか、ユーザープロファイルに保存するかを選択します。ワークスペースプロンプトファイルはそのワークスペースにのみ適用されますが、ユーザープロンプトファイルは複数のワークスペースで使用できます。

プロンプトファイルを作成するには:

1. チャットビューで、**チャットの構成** (歯車アイコン) > **プロンプトファイル**を選択し、**新しいプロンプトファイル**を選択します。

    ![チャットビューとチャットの構成メニューを示し、チャットの構成ボタンを強調表示したスクリーンショット。](../images/customization/configure-chat-instructions.png)

    または、コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: New Prompt File** または **Chat: New Untitled Prompt File** コマンドを使用します。

1. プロンプトファイルを作成する場所を選択します。

    * **ワークスペース**: ワークスペースの `.github/prompts` フォルダーにプロンプトファイルを作成して、そのワークスペース内でのみ使用します。`setting(chat.promptFilesLocations)` 設定を使用して、ワークスペースのプロンプトフォルダーを追加します。

    * **ユーザープロファイル**: [現在のプロファイルフォルダー](/docs/configure/profiles.md)にプロンプトファイルを作成して、すべてのワークスペースで使用します。

1. プロンプトファイルのファイル名を入力します。これは、チャットで `/` を入力したときに表示されるデフォルトの名前です。

1. Markdown フォーマットを使用してチャットプロンプトを作成します。

    * ファイルの上部にある YAML frontmatter に入力して、プロンプトの説明、エージェント、ツール、およびその他の設定を構成します。
    * ファイルの本文にプロンプトの指示を追加します。

既存のプロンプトファイルを変更するには、チャットビューで **チャットの構成** > **プロンプトファイル**を選択し、リストからプロンプトファイルを選択します。または、コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: Configure Prompt Files** コマンドを使用し、クイックピックからプロンプトファイルを選択します。

## チャットでプロンプトファイルを使用する

プロンプトファイルを実行するには、複数のオプションがあります。

* チャットビューで、チャット入力フィールドに `/` とプロンプト名を入力します。

    チャット入力フィールドに追加情報を追加できます。たとえば、`/create-react-form formName=MyForm` や `/create-api for listing customers` です。

* コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: Run Prompt** コマンドを実行し、クイックピックからプロンプトファイルを選択します。

* エディターでプロンプトファイルを開き、エディターのタイトル領域の再生ボタンを押します。現在のチャットセッションでプロンプトを実行するか、新しいチャットセッションを開くかを選択できます。

    このオプションは、プロンプトファイルをすばやくテストして反復処理する場合に便利です。

> [!TIP]
> 新しいチャットセッションを開始するときに推奨アクションとしてプロンプトを表示するには、`setting(chat.promptFilesRecommendations)` 設定を使用します。
>
> ![チャットビューで "explain" プロンプトファイルの推奨事項を示すスクリーンショット。](../images/customization/prompt-file-recommendations.png)

## ツールリストの優先順位

`tools` メタデータフィールドを使用して、カスタムエージェントとプロンプトファイルの両方で使用可能なツールのリストを指定できます。プロンプトファイルは、`agent` メタデータフィールドを使用してカスタムエージェントを参照することもできます。

チャットで使用可能なツールのリストは、次の優先順位で決定されます。

1. プロンプトファイルで指定されたツール（ある場合）
2. プロンプトファイルで参照されているカスタムエージェントのツール（ある場合）
3. 選択したエージェントのデフォルトツール（ある場合）

## デバイス間でユーザープロンプトファイルを同期する

VS Code は、[設定の同期](/docs/configure/settings-sync.md)を使用して、複数のデバイス間でユーザープロンプトファイルを同期できます。

ユーザープロンプトファイルを同期するには、プロンプトファイルと命令ファイルの設定の同期を有効にします。

1. [設定の同期](/docs/configure/settings-sync.md)が有効になっていることを確認します。

1. コマンドパレット (`kb(workbench.action.showCommands)`) から **Settings Sync: Configure** を実行します。

1. 同期する設定のリストから **Prompts and Instructions** を選択します。

## プロンプトファイルを定義するためのヒント

* プロンプトが達成すべきことと、期待される出力形式を明確に記述します。

* AI の応答をガイドするために、期待される入力と出力の例を提供します。

* 各プロンプトでガイドラインを重複させるのではなく、Markdown リンクを使用してカスタム指示を参照します。

* `${selection}` などの組み込み変数や入力変数を利用して、プロンプトをより柔軟にします。

* エディターの再生ボタンを使用してプロンプトをテストし、結果に基づいて調整します。

## 関連リソース

* [AI 応答のカスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム指示の作成](/docs/copilot/customization/custom-instructions.md)
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)
* [VS Code でのチャットの概要](/docs/copilot/chat/copilot-chat.md)
* [チャットツールの構成](/docs/copilot/chat/chat-tools.md)
* [コミュニティが貢献した指示、プロンプト、カスタムエージェント](https://github.com/github/awesome-copilot)
