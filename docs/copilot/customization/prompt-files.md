---
ContentId: 5c8e7d42-9b1a-4f85-a3e2-6d5b8a9c1e43
DateApproved: 3/9/2026
MetaDescription: VS Codeで GitHub Copilot Chatの再利用可能なプロンプトファイルを作成して、一般的な開発タスクを標準化し、コーディングワークフローの効率を向上させる方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- prompt files
- slash commands
- reusable prompts
- copilot
- ai
- task automation
---
# VS Codeでプロンプトファイルを使用する

プロンプトファイル（スラッシュコマンドとも呼ばれます）を使用すると、一般的なタスク用のプロンプトをスタンドアロンのMarkdownファイルとしてエンコーディングし、チャットで直接呼び出すことで、プロンプト作成を簡素化できます。各プロンプトファイルには、タスク固有のコンテキストとタスク実行方法に関するガイドラインが含まれています。

自動的に適用される[カスタム指示](/docs/copilot/customization/custom-instructions.md)とは異なり、プロンプトファイルはチャットで手動で呼び出します。

プロンプトファイルの用途：

* 新しいコンポーネントのスキャフォルディング、テストの実行と修正、プルリクエストの準備など、一般的なタスク用のプロンプト作成を簡素化する
* 最小限の実装計画を作成したり、APIコール用のモックアップを生成したりするなど、カスタムエージェントのデフォルト動作をオーバーライドする

> [!TIP]
> **プロンプトファイル、エージェント、またはスキル？** 軽量で単一タスクのプロンプト用にはプロンプトファイルを使用します。独自のツール制限とハンドオフを備えた永続的なペルソナが必要な場合には[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を使用します。スクリプトとリソースを備えたポータブルでマルチファイル機能が必要な場合には[エージェントスキル](/docs/copilot/customization/agent-skills.md)を使用します。

> [!TIP]
> [Chat Customizations エディター](/docs/copilot/customization/overview.md#chat-customizations-editor)（プレビュー）を使用して、1つの場所ですべてのチャットカスタマイズを検出、作成、管理できます。コマンドパレットから**Chat: Open Chat Customizations**を実行します。

## プロンプトファイルの場所

特定のワークスペース用またはユーザーレベルでプロンプトファイルを定義でき、すべてのワークスペースで利用可能です。

| スコープ | デフォルトファイルの場所 |
|-------|-----------------------|
| ワークスペース | `.github/prompts`フォルダー |
| ユーザープロフィール | 現在の[VS Codeプロフィール](/docs/configure/profiles.md)の`prompts`フォルダー |

`setting(chat.promptFilesLocations)`設定でワークスペースプロンプトファイルの追加ファイルの場所を構成できます。

## プロンプトファイルの形式

プロンプトファイルは、`.prompt.md`拡張子を持つMarkdownファイルです。オプションのYAML frontmatterヘッダーはプロンプトの動作を構成します：

| フィールド | 必須 | 説明 |
| --- | --- | --- |
| `description` | いいえ | プロンプトの簡潔な説明。 |
| `name` | いいえ | プロンプトの名前。チャットで`/`の後に表示されます。指定されない場合はファイル名が使用されます。 |
| `argument-hint` | いいえ | チャット入力フィールドに表示されるヒントテキスト。ユーザーがプロンプトとどのように対話するかをガイドします。 |
| `agent` | いいえ | プロンプトを実行するために使用されるエージェント：`ask`、`agent`、`plan`、または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)の名前。デフォルトでは、現在のエージェントが使用されます。ツールが指定されている場合、デフォルトエージェントは`agent`です。 |
| `model` | いいえ | プロンプト実行時に使用される言語モデル。指定されない場合は、モデルピッカーで現在選択されているモデルが使用されます。 |
| `tools` | いいえ | このプロンプトで利用可能なツールまたはツールセット名のリスト。組み込みツール、ツールセット、MCPツール、または拡張機能によって提供されるツールを含むことができます。MCPサーバーのすべてのツールを含めるには、`<server name>/*`形式を使用します。<br/>[チャットのツール](/docs/copilot/agents/agent-tools.md)の詳細を学びます。 |

> [!NOTE]
> プロンプト実行時に指定されたツールが利用できない場合は、無視されます。

本文には、Markdown形式のプロンプトテキストが含まれます。AIが従う必要のある具体的な指示、ガイドライン、またはその他の関連情報を提供します。

Markdownリンクを使用してその他のワークスペースファイルを参照できます。これらのファイルを参照するために相対パスを使用し、プロンプトファイルの場所に基づいてパスが正しいことを確認します。

本文テキストでエージェントツールを参照するには、`#tool:<tool-name>`構文を使用します。たとえば、`browser`ツールを参照するには、`#tool:browser`を使用します。

> [!TIP]
> ユーザーが追加情報を提供する場合は、`vscode/askQuestion`ツールを使用できます。また、`${input:variableName}`、`${input:variableName:placeholder}`などの構文を使用することもできます。ほとんどの言語モデルはこの構文を理解し、これらの入力を促します。

次の例は、プロンプトファイルの使用方法を示しています。より多くのコミュニティが提供する例については、[Awesome Copilotリポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

<details>
<summary>例：Reactフォームコンポーネントを生成する</summary>

```markdown
---
agent: 'agent'
model: GPT-4o
tools: ['search/codebase', 'vscode/askQuestions']
description: '新しいReactフォームコンポーネントを生成する'
---
Githubリポジトリcontoso/react-templatesのテンプレートに基づいて、新しいReactフォームコンポーネントを生成することが目標です。

プロンプトが提供されていない場合は、#tool:vscode/askQuestionsを使用してフォーム名とフィールドを確認します。

フォームの要件：
* フォームデザインシステムコンポーネントを使用します：[design-system/Form.md](../docs/design-system/Form.md)
* フォーム状態管理に`react-hook-form`を使用します：
* フォームデータのTypeScript型を常に定義します
* `register`を使用した制御されていないコンポーネントを優先します
* `defaultValues`を使用して不要な再レンダリングを防ぎます
* 検証に`yup`を使用します：
* 独立したファイルに再利用可能な検証スキーマを作成します
* TypeScript型を使用して型安全性を確保します
* UXフレンドリーな検証ルールをカスタマイズします
```

</details>

<details>
<summary>例：REST APIのセキュリティレビューを実行する</summary>

```markdown
---
agent: 'ask'
model: Claude Sonnet 4
description: 'REST APIセキュリティレビューを実行する'
---
REST APIセキュリティレビューを実行し、対処すべきセキュリティ問題のTODOリストを提供します。

* すべてのエンドポイントが認証と認可で保護されていることを確認します
* すべてのユーザー入力を検証し、データをサニタイズします
* レート制限とスロットリングを実装します
* セキュリティイベント用のロギングと監視を実装します

TODOリストをMarkdown形式で返します。優先度と問題の種類でグループ化します。
```

</details>

## プロンプトファイルを作成する

プロンプトファイルを作成する際には、ワークスペースまたはユーザープロフィールに保存するかどうかを選択します。ワークスペースプロンプトファイルはそのワークスペースにのみ適用され、ユーザープロンプトファイルは複数のワークスペース全体で利用可能です。

プロンプトファイルを作成するには：

> [!TIP]
> チャット入力に`/prompts`と入力して、**プロンプトファイルを構成**メニューをすばやく開きます。

1. Chat ビューで、**Configure Chat**（ギアアイコン）>**Prompt Files**を選択し、**New prompt file**を選択します。

    ![Chat ビュー、Configure Chat メニュー、Configure Chat ボタンがハイライトされているスクリーンショット。](../images/customization/configure-chat-instructions.png)

    または、コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: New Prompt File**または**Chat: New Untitled Prompt File**コマンドを使用します。

1. プロンプトファイルを作成する場所を選択します。

1. プロンプトファイルのファイル名を入力します。これは、チャットで`/`と入力した時に表示されるデフォルト名です。

1. Markdown フォーマットを使用してチャットプロンプトを作成します。

    * ファイルの上部にあるYAML frontmatterを入力して、プロンプトの説明、エージェント、ツール、その他の設定を構成します。
    * ファイルの本文にプロンプト用の指示を追加します。

既存のプロンプトファイルを変更するには、Chat ビューで**Configure Chat**>**Prompt Files**を選択し、リストからプロンプトファイルを選択します。または、コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: Configure Prompt Files**コマンドを使用し、Quick Pickからプロンプトファイルを選択します。

### AIを使用してプロンプトファイルを生成する

タスクの説明に基づいてAIを使用してプロンプトファイルを生成できます。チャットに`/create-prompt`と入力し、自動化するタスクを説明します（例：「単体テストを生成するためのプロンプト」）。エージェントが明確にするための質問をし、適切なfrontmatterと指示を含む`.prompt.md`ファイルを生成し、ワークスペースまたはユーザーストレージの選択肢を提供します。

進行中の会話から再利用可能なプロンプトを抽出することもできます。たとえば、マルチターンチャットセッションの後に、「これを再利用可能なプロンプトにする」または「このワークフローをプロンプトとして保存する」と依頼すると、エージェントはワークフローをキャプチャするプロンプトファイルを作成します。

## チャットでプロンプトファイルを使用する

プロンプトファイルを実行するには、複数のオプションがあります：

* Chat ビューで、チャット入力フィールドに`/`の後に続けてプロンプト名を入力します。[エージェントスキル](/docs/copilot/customization/agent-skills.md)もプロンプトファイルと一緒にスラッシュコマンドとして表示されます。

    チャット入力フィールドに追加情報を追加できます。たとえば、`/create-react-form formName=MyForm`または`/create-api for listing customers`。

* コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: Run Prompt**コマンドを実行し、Quick Pickからプロンプトファイルを選択します。

* エディターでプロンプトファイルを開き、エディタータイトル領域の再生ボタンを押します。現在のチャットセッションでプロンプトを実行するか、新しいチャットセッションを開くかを選択できます。

    このオプションは、プロンプトファイルを迅速にテストして反復処理するのに役立ちます。

> [!TIP]
> `setting(chat.promptFilesRecommendations)`設定を使用して、新しいチャットセッションを開始するときに推奨アクションとしてプロンプトを表示します。
>
> ![Chat ビューで「説明」プロンプトファイルの推奨事項を示すスクリーンショット。](../images/customization/prompt-file-recommendations.png)

## ツールリストの優先度

`tools`メタデータフィールドを使用して、カスタムエージェントとプロンプトファイルの両方で利用可能なツールのリストを指定できます。プロンプトファイルは、`agent`メタデータフィールドを使用してカスタムエージェントを参照することもできます。

チャット内の利用可能なツール リストは、次の優先度順で決定されます：

1. プロンプトファイルで指定されたツール（ある場合）
2. プロンプトファイルで参照されるカスタムエージェントのツール（ある場合）
3. 選択したエージェントのデフォルトツール（ある場合）

## デバイス間でユーザープロンプトファイルを同期する

VS Codeは、[Settings Sync](/docs/configure/settings-sync.md)を使用して、複数のデバイス間でユーザープロンプトファイルを同期できます。

ユーザープロンプトファイルを同期するには、Settings Syncを有効にし、コマンドパレット（`kb(workbench.action.showCommands)`）から**Settings Sync: Configure**を実行します。同期するための設定リストから**Prompts and Instructions**を選択します。

## 効果的なプロンプト作成のヒント

* プロンプトが何を達成すべきか、および期待される出力形式を明確に説明します。

* 期待される入力と出力の例を提供して、AIのレスポンスをガイドします。

* Markdownリンクを使用して、各プロンプトでガイドラインを複製するのではなく、カスタム指示を参照します。

* `${selection}`とInput 変数などの組み込み変数を活用して、プロンプトをより柔軟にします。

* エディターの再生ボタンを使用してプロンプトをテストし、結果に基づいて改善します。

## よくある質問

### プロンプトファイルの出所をどのようにして知るのですか？

プロンプトファイルは、異なるソースから取得できます：組み込み、プロフィールで定義されたユーザー定義、現在のワークスペースのワークスペース定義プロンプト、または拡張機能が提供するプロンプト。

プロンプトファイルのソースを識別するには：

1. コマンドパレット（`kb(workbench.action.showCommands)`）から**Chat: Configure Prompt Files**を選択します。
1. リスト内のプロンプトファイルにマウスをホバーします。ソース位置はツールチップに表示されます。

> [!TIP]
> Chat Customizations 診断ビューを使用して、読み込まれたすべてのプロンプトファイルとエラーを確認します。Chat ビューを右クリックして、**Diagnostics**を選択します。[VS Codeの AIのトラブルシューティング](/docs/copilot/troubleshooting.md)の詳細を学びます。

## 関連リソース

* [カスタム指示を作成する](/docs/copilot/customization/custom-instructions.md)
* [チャットのツールを構成する](/docs/copilot/agents/agent-tools.md)
* [コミュニティが提供する指示、プロンプト、カスタムエージェント](https://github.com/github/awesome-copilot)

