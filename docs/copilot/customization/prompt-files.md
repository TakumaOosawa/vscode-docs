---
ContentId: 5c8e7d42-9b1a-4f85-a3e2-6d5b8a9c1e43
DateApproved: 01/08/2026
MetaDescription: VS Code の GitHub Copilot Chat 用の再利用可能なプロンプトファイルを作成して、一般的な開発タスクを標準化し、コーディングワークフローの効率を向上させる方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Code でプロンプトファイルを使用する

プロンプトファイルは、コードの生成、コードレビューの実行、プロジェクトコンポーネントのスキャフォールディングなど、一般的な開発タスク用の再利用可能なプロンプトを定義する Markdown ファイルです。これらはチャットで直接実行できるスタンドアロンのプロンプトであり、標準化された開発ワークフローのライブラリを作成できます。

タスク固有のガイドラインを含めたり、カスタム指示を参照して、一貫した実行を確保したりできます。すべてのリクエストに適用されるカスタム指示とは異なり、プロンプトファイルは特定のタスクに対してオンデマンドでトリガーされます。

VS Code は、プロンプトファイルの2種類のスコープをサポートしています。

* **ワークスペースプロンプトファイル**: ワークスペース内でのみ使用でき、ワークスペースの `.github/prompts` フォルダーに保存されます。
* **ユーザープロンプトファイル**: 複数のワークスペースで使用でき、現在の [VS Code プロファイル](/docs/configure/profiles.md)に保存されます。

## プロンプトファイルの構造

プロンプトファイルは Markdown ファイルであり、`.prompt.md` 拡張子を使用し、次の構造を持ちます。

### ヘッダー (オプション)

ヘッダーは、次のフィールドを持つ YAML フロントマターとしてフォーマットされます。

| フィールド | 説明 |
| --- | --- |
| `description`     | プロンプトの短い説明。 |
| `name`            | チャットで `/` を入力した後に使用されるプロンプトの名前。指定しない場合は、ファイル名が使用されます。 |
| `argument-hint`   | プロンプトとの対話方法をユーザーに案内するためにチャット入力フィールドに表示されるオプションのヒントテキスト。 |
| `agent`           | プロンプトの実行に使用されるエージェント: `ask`、`edit`、`agent`、または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)の名前。デフォルトでは、現在のエージェントが使用されます。ツールが指定されていて、現在のエージェントが `ask` または `edit` の場合、デフォルトのエージェントは `agent` になります。 |
| `model`           | プロンプトの実行時に使用される言語モデル。指定しない場合は、モデルピッカーで現在選択されているモデルが使用されます。 |
| `tools`           | このプロンプトで使用できるツールまたはツールセット名のリスト。組み込みツール、ツールセット、MCP ツール、または拡張機能によって提供されるツールを含めることができます。MCP サーバーのすべてのツールを含めるには、`<server name>/*` 形式を使用します。<br/>詳細については、[チャットのツール](/docs/copilot/chat/chat-tools.md)をご覧ください。 |

> [!NOTE]
> プロンプトの実行時に特定のツールが使用できない場合、それは無視されます。

### 本文

プロンプトファイルの本文には、チャットでプロンプトを実行したときに LLM に送信されるプロンプトテキストが含まれます。AI に従わせたい具体的な指示、ガイドライン、またはその他の関連情報を提供します。

Markdown リンクを使用して、他のワークスペースファイルを参照できます。相対パスを使用してこれらのファイルを参照し、プロンプトファイルの場所に基づいてパスが正しいことを確認してください。

本文テキストでエージェントツールを参照するには、`#tool:<tool-name>` 構文を使用します。たとえば、`githubRepo` ツールを参照するには、`#tool:githubRepo` を使用します。

プロンプトファイル内では、`${variableName}` 構文を使用して変数を参照できます。次の変数を参照できます。

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

    ![チャットビューと、チャットの構成ボタンを強調表示したチャットの構成メニューを示すスクリーンショット。](../images/customization/configure-chat-instructions.png)

    あるいは、コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: New Prompt File** または **Chat: New Untitled Prompt File** コマンドを使用します。

1. プロンプトファイルを作成する場所を選択します。

    * **ワークスペース**: ワークスペースの `.github/prompts` フォルダーにプロンプトファイルを作成して、そのワークスペース内でのみ使用します。`setting(chat.promptFilesLocations)` 設定を使用して、ワークスペースにプロンプトフォルダーを追加します。

    * **ユーザープロファイル**: [現在のプロファイルフォルダー](/docs/configure/profiles.md)にプロンプトファイルを作成して、すべてのワークスペースで使用します。

1. プロンプトファイルのファイル名を入力します。これは、チャットで `/` を入力したときに表示されるデフォルトの名前です。

1. Markdown フォーマットを使用してチャットプロンプトを作成します。

    * ファイルの上部にある YAML フロントマターに入力して、プロンプトの説明、エージェント、ツール、およびその他の設定を構成します。
    * ファイルの本文にプロンプトの指示を追加します。

既存のプロンプトファイルを変更するには、チャットビューで **チャットの構成** > **プロンプトファイル**を選択し、リストからプロンプトファイルを選択します。あるいは、コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: Configure Prompt Files** コマンドを使用して、クイックピックからプロンプトファイルを選択します。

## チャットでプロンプトファイルを使用する

プロンプトファイルを実行するには、いくつかのオプションがあります。

* チャットビューで、チャット入力フィールドに `/` とプロンプト名を入力します。

    チャット入力フィールドに追加情報を追加できます。たとえば、`/create-react-form formName=MyForm` または `/create-api for listing customers` です。

* コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: Run Prompt** コマンドを実行し、クイックピックからプロンプトファイルを選択します。

* エディターでプロンプトファイルを開き、エディターのタイトル領域にある再生ボタンを押します。現在のチャットセッションでプロンプトを実行するか、新しいチャットセッションを開くかを選択できます。

    このオプションは、プロンプトファイルをすばやくテストして反復処理する場合に便利です。

> [!TIP]
> 新しいチャットセッションを開始するときに推奨されるアクションとしてプロンプトを表示するには、`setting(chat.promptFilesRecommendations)` 設定を使用します。
>
> ![チャットビューに「説明」プロンプトファイルの推奨事項が表示されているスクリーンショット。](../images/customization/prompt-file-recommendations.png)

## ツールリストの優先順位

`tools` メタデータフィールドを使用して、カスタムエージェントとプロンプトファイルの両方で使用可能なツールのリストを指定できます。プロンプトファイルは、`agent` メタデータフィールドを使用してカスタムエージェントを参照することもできます。

チャットで使用可能なツールのリストは、次の優先順位で決定されます。

1. プロンプトファイルで指定されたツール (ある場合)
2. プロンプトファイルで参照されているカスタムエージェントのツール (ある場合)
3. 選択したエージェントのデフォルトツール (ある場合)

## デバイス間でユーザープロンプトファイルを同期する

VS Code は、[設定の同期](/docs/configure/settings-sync.md)を使用して、複数のデバイス間でユーザープロンプトファイルを同期できます。

ユーザープロンプトファイルを同期するには、プロンプトおよび指示ファイルの設定の同期を有効にします。

1. [設定の同期](/docs/configure/settings-sync.md)が有効になっていることを確認します。

1. コマンドパレット (`kb(workbench.action.showCommands)`) から **設定の同期: 設定 (Settings Sync: Configure)** を実行します。

1. 同期する設定のリストから **Prompts and Instructions** を選択します。

## プロンプトファイルを定義するためのヒント

* プロンプトで何を達成すべきか、どのような出力形式が期待されるかを明確に記述してください。

* 期待される入力と出力の例を提供して、AI の応答をガイドしてください。

* 各プロンプトでガイドラインを重複させるのではなく、Markdown リンクを使用してカスタム指示を参照してください。

* `${selection}` などの組み込み変数や入力変数を利用して、プロンプトをより柔軟にしてください。

* エディターの再生ボタンを使用してプロンプトをテストし、結果に基づいてプロンプトを調整してください。

## よくある質問

### プロンプトファイルがどこから来たのかを知るにはどうすればよいですか?

プロンプトファイルは、組み込み、プロファイル内のユーザー定義、現在のワークスペース内のワークスペース定義プロンプト、または拡張機能によって提供されるプロンプトなど、さまざまなソースから提供されます。

プロンプトファイルのソースを特定するには:

1. コマンドパレット (`kb(workbench.action.showCommands)`) から **Chat: Configure Prompt Files** を選択します。
1. リスト内のプロンプトファイルにカーソルを合わせます。ソースの場所がツールチップに表示されます。

## 関連リソース

* [AI 応答のカスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム指示を作成する](/docs/copilot/customization/custom-instructions.md)
* [カスタムエージェントを作成する](/docs/copilot/customization/custom-agents.md)
* [VS Code でのチャットの概要](/docs/copilot/chat/copilot-chat.md)
* [チャットでツールを構成する](/docs/copilot/chat/chat-tools.md)
* [コミュニティが提供した指示、プロンプト、およびカスタムエージェント](https://github.com/github/awesome-copilot)
