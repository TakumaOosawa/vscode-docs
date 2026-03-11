---
ContentId: 8b4f3c21-4e02-4a89-9f15-7a8d6b5c2e91
DateApproved: 3/9/2026
MetaDescription: VS CodeでGitHub Copilot Chatのカスタム命令を作成し、AI応答があなたのコーディング実践、プロジェクト要件、開発標準に合致することを確認する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- customize
- rules
- instructions
- copilot-instructions.md
- AGENTS.md
- CLAUDE.md
- coding standards
- ai
- copilot
---
# VS Codeでカスタム命令を使用する

カスタム命令を使用すると、AIがコードを生成し、その他の開発タスクを処理する方法に自動的に影響を与える共通のガイドラインとルールを定義できます。すべてのチャットプロンプトに手動でコンテキストを含める代わりに、カスタム命令をMarkdownファイルで指定して、コーディング実践とプロジェクト要件に合致した一貫性のあるAI応答を確保します。

カスタム命令を設定して、すべてのチャットリクエストまたは特定のファイルのみに自動的に適用することも、特定のチャットプロンプトに手動で添付することもできます。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="Generate instructions">
`/init`でプロジェクトをAI向けに設定し、プロジェクトに合わせたカスタム命令を生成します。

* [VS Codeで開く](vscode://GitHub.Copilot-Chat/chat?prompt=%2Finit)

</div>

> [!TIP]
> [チャットカスタマイゼーションエディタ](/docs/copilot/customization/overview.md#chat-customizations-editor)（プレビュー）を使用して、すべてのチャットカスタマイズを1つの場所で検出、作成、管理します。コマンドパレットから**Chat: Open Chat Customizations**を実行します。

> [!NOTE]
> カスタム命令は、エディタで入力時に[インライン提案](/docs/copilot/ai-powered-suggestions.md)には適用されません。

## 命令ファイルの種類

VS Codeは2つのカテゴリのカスタム命令をサポートしています。プロジェクトに複数の命令ファイルがある場合、VS Codeはそれらを結合してチャットコンテキストに追加します。特定の順序は保証されません。

### 常時有効な命令

常時有効な命令はすべてのチャットリクエストに自動的に含まれます。プロジェクト全体のコーディング標準、アーキテクチャの決定、すべてのコードに適用される規約に使用します。

* 単一の[`.github/copilot-instructions.md`](#use-a-githubcopilot-instructionsmd-file)ファイル
    * ワークスペース内のすべてのチャットリクエストに自動的に適用されます
    * ワークスペース内に保存されます

* 1つ以上の[`AGENTS.md`](#use-an-agentsmd-file)ファイル
    * ワークスペースで複数のAIエージェントと連携する場合に便利です
    * ワークスペースまたは特定のサブフォルダ内のすべてのチャットリクエストに自動的に適用されます（実験的）
    * ワークスペースのルートまたはサブフォルダに保存されます（実験的）

* [組織レベルの命令](#share-custom-instructions-across-teams)
    * GitHub組織内の複数のワークスペースとリポジトリ全体で命令を共有します
    * GitHub組織レベルで定義されます

* [`CLAUDE.md`](#use-a-claudemd-file)ファイル
    * Claude CodeおよびClaude構築のその他のツールとの互換性のため
    * ワークスペースルート、`.claude`フォルダ、またはユーザーホームディレクトリに保存されます

### ファイルベースの命令

ファイルベースの命令は、エージェントが作業しているファイルが指定されたパターンに一致する場合、または説明が現在のタスクに一致する場合に適用されます。言語固有の規約、フレームワークパターン、またはコードベースの特定の部分にのみ適用されるルールに使用します。

* 1つ以上の[`.instructions.md`](#use-instructionsmd-files)ファイル
    * globパターンを使用してファイルタイプまたは場所に基づいて命令を条件付きで適用します
    * ワークスペースまたはユーザープロフィール内に保存されます

命令内の特定のコンテキスト（ファイルやURLなど）を参照するには、Markdownリンクを使用できます。

> [!TIP]
> **どのアプローチを使用すべきですか？** プロジェクト全体のコーディング標準に対して、単一の`.github/copilot-instructions.md`ファイルで始めます。異なるファイルタイプまたはフレームワークに異なるルールが必要な場合は、`.instructions.md`ファイルを追加します。ワークスペースで複数のAIエージェントと連携する場合は、`AGENTS.md`を使用します。

## `.github/copilot-instructions.md`ファイルを使用する

VS Codeはワークスペースのルートに`.github/copilot-instructions.md` Markdownファイルを自動的に検出し、このファイルの命令をこのワークスペース内のすべてのチャットリクエストに適用します。

`copilot-instructions.md`を以下に使用します：

* プロジェクト全体に適用されるコーディングスタイルと命名規約
* テクノロジスタック宣言と推奨ライブラリ
* 従うべき、または避けるべきアーキテクチャパターン
* セキュリティ要件とエラー処理アプローチ
* ドキュメント標準

ワークスペースで`.github/copilot-instructions.md`ファイルを作成するには、以下の手順に従います：

1. ワークスペースのルートに`.github/copilot-instructions.md`ファイルを作成します。必要に応じて、最初に`.github`ディレクトリを作成します。

1. 命令をMarkdown形式で説明します。最適な結果のために、簡潔で焦点を絞った内容にしてください。

> [!NOTE]
> VS Codeは常時有効な命令用に[`AGENTS.md`ファイル](#use-an-agentsmd-file)の使用もサポートしています。

<details>
<summary>例：一般的なコーディングガイドライン</summary>

```markdown
---
applyTo: "**"
---
# プロジェクト一般的なコーディング標準

## 命名規約
- コンポーネント名、インターフェース、型の別名にはPascalCaseを使用します
- 変数、関数、メソッドにはcamelCaseを使用します
- プライベートクラスメンバーの前にアンダースコア(_)を付けます
- 定数にはALL_CAPSを使用します

## エラー処理
- 非同期操作にはtry/catchブロックを使用します
- ReactコンポーネントにはエラーバウンダリをImplementします
- 常にコンテキスト情報でエラーをログします
```

</details>

## `.instructions.md`ファイルを使用する

エージェントが作業しているファイルまたはタスクに基づいて動的に適用される`*.instructions.md` Markdownファイルでファイルベースの命令を作成できます。

エージェントは、命令ファイルヘッダーの`applyTo`プロパティで指定されたファイルパターン、または命令説明と現在のタスクのセマンティックマッチングに基づいて、どの命令ファイルを適用するかを決定します。

`.instructions.md`ファイルを以下に使用します：

* フロントエンドコードとバックエンドコードの異なる規約
* モノレポの言語固有のガイドライン
* 特定のモジュールのフレームワーク固有のパターン
* テストファイルまたはドキュメントの特殊なルール

### 命令ファイルの場所

特定のワークスペースまたはすべてのワークスペースに適用されるユーザーレベルで命令を定義できます。

| スコープ | デフォルトファイル場所 |
|-------|-----------------------|
| ワークスペース | `.github/instructions`フォルダ |
| ワークスペース（Claude形式） | `.claude/rules`フォルダ |
| ユーザープロフィール | `~/.copilot/instructions`、`~/.claude/rules`、現在の[VS Codeプロフィール](/docs/configure/profiles.md)の`instructions`フォルダ |

VS Codeはこれらのフォルダを再帰的に検索するため、命令ファイルをサブディレクトリに編成できます。例えば、チーム、言語、またはモジュール別に命令をグループ化できます：

```text
.github/instructions/
  frontend/
    react.instructions.md
    accessibility.instructions.md
  backend/
    api-design.instructions.md
  testing/
    unit-tests.instructions.md
```

`setting(chat.instructionsFilesLocations)`設定を使用して、ワークスペース命令ファイルの追加ファイルの場所を設定できます。これは、命令ファイルを異なるフォルダに保管したい場合や、より良く整理するために複数のフォルダを持ちたい場合に便利です。カスタム場所も再帰的に検索されます。

Claude CodeおよびClaude構築のその他のツールとの互換性のため、VS Codeは`.claude/rules`ワークスペースフォルダと`~/.claude/rules`ユーザーフォルダの命令ファイルも検出します。

以下のコードスニペットは、ワークスペースレベルのみの命令が有効で、ユーザーレベルの命令が無効な場合の命令ファイルの場所を設定する方法を示しています：

```json
"chat.instructionsFilesLocations": {
  ".github/instructions": true,
  ".claude/rules": true,
  "~/.copilot/instructions": false,
  "~/.claude/rules": false
}
```

### 命令ファイル形式

命令ファイルは`.instructions.md`拡張子を持つMarkdownファイルです。オプションのYAML前付けヘッダは命令がいつ適用されるかを制御します：

| フィールド | 必須 | 説明 |
|-------|----------|-------------|
| `name` | いいえ | UI に表示される表示名。デフォルトはファイル名です。 |
| `description` | いいえ | チャットビューでホバータイムに表示される短い説明。 |
| `applyTo` | いいえ | ワークスペースルートを基準とした相対的に命令を自動的に適用するファイルを定義するglobパターン。すべてのファイルに適用するには`**`を使用します。指定されていない場合、命令は自動的に適用されませんが、チャットリクエストに手動で追加できます。 |

本文にはMarkdown形式の命令が含まれます。エージェントツールを参照するには、`#tool:<tool-name>`構文を使用します（例：`#tool:githubRepo`）。

```markdown
---
name: 'Python Standards'
description: 'Pythonファイルのコーディング規約'
applyTo: '**/*.py'
---
# Python コーディング標準
- PEP 8 スタイルガイドに従います。
- すべての関数署名に型ヒントを使用します。
- パブリック関数用にdocstringsを記述します。
- インデントに4つのスペースを使用します。
```

### 命令ファイルを作成する

命令ファイルを作成する際に、ワークスペースまたはユーザープロフィール内に保存するかどうかを選択します。ワークスペース命令ファイルはそのワークスペースのみに適用され、ユーザー命令ファイルは複数のワークスペースで利用可能です。

命令ファイルを作成するには：

> [!TIP]
> チャット入力に`/instructions`と入力して、**命令とルールの設定**メニューをすばやく開きます。

1. チャットビューで、**チャットを設定**(ギアアイコン) > **命令とルール**を選択し、**新しい命令ファイル**を選択します。

    ![チャットビューとチャット設定メニューを示すスクリーンショット、チャット設定ボタンを強調表示します。](../images/customization/configure-chat-instructions.png)

    または、コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: New Instructions File**コマンドを使用します。

1. 命令ファイルを作成する場所を選択します。

1. 命令ファイルのファイル名を入力します。これはUIで使用されるデフォルト名です。

1. Markdown形式を使用してカスタム命令を作成します。

    * ファイルの上部のYAML前付けを入力して、命令の説明、名前、いつ適用されるかを設定します。
    * ファイルの本文に命令を追加します。

既存の命令ファイルを変更するには、チャットビューで**チャット設定**(ギアアイコン) > **チャット命令**を選択し、リストから命令ファイルを選択します。または、コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: Configure Instructions**コマンドを使用し、クイックピックから命令ファイルを選択します。

### AIで命令ファイルを生成する

AIを使用してターゲット命令ファイルを生成できます。チャットに`/create-instruction`と入力し、適用する規約またはガイドラインを説明してください（例：「このプロジェクトで常にタブとシングルクォートを使用します」）。エージェントは明確化を求め、適切な`applyTo`パターンと内容を含む`.instructions.md`ファイルを生成します。

進行中の会話から命令を抽出することもできます。例えば、チャットセッション中にエージェントのインポートスタイルを修正した場合、「これから命令を抽出します」と要求して、その修正をプロジェクト規約として取得します。

> [!NOTE]
> `/create-instruction`はターゲット化された、オンデマンドの命令ファイルを生成します。ワークスペース全体の常時有効な命令を生成するには、代わりに[`/init`コマンド](#generate-custom-instructions-for-your-workspace)を使用してください。

<details>
<summary>例：言語固有のコーディングガイドライン</summary>

これらの命令が一般的なコーディングガイドラインファイルを参照する方法に注意してください。命令を複数のファイルに分離して、特定のトピックに焦点を当てて整理できます。

```markdown
---
applyTo: "**/*.ts,**/*.tsx"
---
# TypeScriptとReactのプロジェクトコーディング標準

すべてのコードに[一般的なコーディングガイドライン](./general-coding.instructions.md)を適用します。

## TypeScript ガイドライン
- すべての新しいコードにTypeScriptを使用します
- 可能な限り関数型プログラミング原理に従います
- データ構造と型定義にインターフェースを使用します
- 不変データを優先します（const、readonly）
- オプショナルチェーニング(?.)とnullish合体(??)演算子を使用します

## React ガイドライン
- フックを持つ関数コンポーネントを使用します
- Reactフックのルール（条件付きフックなし）に従います
- 子供を持つコンポーネント用にReact.FC型を使用します
- コンポーネントを小さく焦点を絞った状態に保ちます
- コンポーネントスタイリングにCSSモジュールを使用します
```

</details>

<details>
<summary>例：ドキュメント作成ガイドライン</summary>

ドキュメント作成などの開発以外のアクティビティを含む、異なるタイプのタスク用命令ファイルを作成できます。

```markdown
---
applyTo: "docs/**/*.md"
---
# プロジェクトドキュメント作成ガイドライン

## 一般的なガイドライン
- 明確で簡潔なドキュメントを作成します。
- 一貫性のある用語とスタイルを使用します。
- 該当する場合はコード例を含めます。

## 文法
* 過去形（was、opened）の代わりに現在形動詞（is、open）を使用してください。
* 事実の陳述と直接コマンドを作成します。「could」や「would」のような仮定は避けてください。
* 主語がアクションを実行するアクティブボイスを使用します。
* 二人称（you）で読者に直接話しかけるために書きます。

## Markdownガイドライン
- 見出しを使用してコンテンツを整理します。
- リストに箇条書きを使用します。
- 関連リソースへのリンクを含めます。
- コードスニペットにコードブロックを使用します。
```

</details>

より多くのコミュニティ提供の例については、[Awesome Copilotリポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

## `AGENTS.md`ファイルを使用する

VS Codeはワークスペースのルートに`AGENTS.md` Markdownファイルを自動的に検出し、このファイルの命令をこのワークスペース内のすべてのチャットリクエストに適用します。これはワークスペースで複数のAIエージェントと連携する場合、またはモノレポの特定の部分に適用されるサブフォルダレベルの命令をしたい場合に便利です。

`AGENTS.md`を以下の場合に使用します：

* 複数のAIコーディングエージェントと連携し、すべてのエージェントが認識する単一の命令セットが必要な場合
* モノレポの特定の部分に適用されるサブフォルダレベルの命令が必要な場合

`AGENTS.md`ファイルのサポートを有効または無効にするには、`setting(chat.useAgentsMdFile)`設定を構成します。

### 複数の`AGENTS.md`ファイルを使用する（実験的）

サブフォルダ内で複数の`AGENTS.md`ファイルを使用すると、プロジェクトの異なる部分に異なる命令を適用する場合に便利です。例えば、フロントエンドコード用に1つの`AGENTS.md`ファイルとバックエンドコード用に別の`AGENTS.md`ファイルを持つことができます。

実験的な`setting(chat.useNestedAgentsMdFiles)`設定を使用して、ワークスペース内のネストされた`AGENTS.md`ファイルのサポートを有効または無効にします。

有効にすると、VS Codeはワークスペースのすべてのサブフォルダで`AGENTS.md`ファイルを再帰的に検索し、相対パスをチャットコンテキストに追加します。その後、エージェントは編集されているファイルに基づいて、どの命令を使用するかを決定できます。

> [!TIP]
> フォルダ固有の命令の場合は、フォルダ構造と一致する異なるの`applyTo`パターンを持つ複数の[`.instructions.md`](#use-instructionsmd-files)ファイルを使用することもできます。

## `CLAUDE.md`ファイルを使用する

VS Codeは`CLAUDE.md`ファイルを自動的に検出し、`AGENTS.md`と同様に常時有効な命令として適用します。これはVS CodeとともにClaude CodeまたはClaude構築のその他のツールを使用し、すべてのツールが認識する単一の命令セットを希望する場合に便利です。

VS Codeはこれらの場所で`CLAUDE.md`ファイルを検索します：

| 場所 | 説明 |
|----------|-------------|
| ワークスペースルート | ワークスペースのルートの`CLAUDE.md` |
| `.claude`フォルダ | ワークスペース内の`.claude/CLAUDE.md` |
| ユーザーホーム | すべてのプロジェクト全体の個人命令用`~/.claude/CLAUDE.md` |
| ローカル変種 | ローカルのみの命令用`CLAUDE.local.md`（バージョン管理にコミットされていません） |

`CLAUDE.md`ファイルのサポートを有効または無効にするには、`setting(chat.useClaudeMdFile)`設定を構成します。

> [!NOTE]
> `.claude/rules`命令ファイルの場合、VS Codeはglobパターンの`applyTo`の代わりに`paths`プロパティを使用します。[Claude Rules形式](https://code.claude.com/docs/en/memory#basic-structure)に従います。`paths`プロパティはglobパターンの配列を受け入れ、デフォルトは省略時に`**`(すべてのファイル)です。

## ワークスペース用のカスタム命令を生成する

VS Codeはワークスペースを分析し、コーディング実践とプロジェクト構造と一致する常時有効なカスタム命令を生成できます。これらの命令はワークスペース内のすべてのチャットリクエストに自動的に適用されます。

命令を生成する場合、VS Codeは以下の手順を実行します：

1. `copilot-instructions.md`または`AGENTS.md`ファイルなど、ワークスペース内の既存のAI規約を検出します。
1. プロジェクト構造とコーディングパターンを分析します。
1. プロジェクト向けのカスタマイズされた包括的なワークスペース命令を生成します。

### `/init`スラッシュコマンドを使用する

ワークスペースをカスタム命令でプライムする最速の方法は、チャット入力ボックスに`/init`スラッシュコマンドを入力することです。

`/init`コマンドは寄与された[プロンプトファイル](/docs/copilot/customization/prompt-files.md)として実装されるため、基礎となるプロンプトを変更してその動作をカスタマイズできます。

### コマンドを使用して命令を生成する

コマンドでワークスペース用のカスタム命令を生成するには：

1. チャットビューで、**チャット設定**(ギアアイコン) > **チャット命令を生成**を選択します。

1. 生成された命令ファイルを確認し、必要な編集を行なってください。

## チーム全体でカスタム命令を共有する

GitHub組織内の複数のワークスペースとリポジトリ全体でカスタム命令を共有するには、GitHub組織レベルで定義できます。

VS Codeは自動的に、アカウントがアクセスできるアカウントで定義されたカスタム命令を検出します。これらの命令は、個人およびワークスペース命令と同様に**チャット命令**メニューに表示され、すべてのチャットリクエストに自動的に適用されます。

組織レベルのカスタム命令の検出を有効にするには、`setting(github.copilot.chat.organizationInstructions.enabled)`を`true`に設定します。

GitHub documentation で[組織用にカスタム命令を追加](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-organization-instructions)する方法を学習してください。

## デバイス全体でユーザー命令ファイルを同期する

VS Codeは[設定同期](/docs/configure/settings-sync.md)を使用して、複数のデバイス全体でユーザー命令ファイルを同期できます。

ユーザー命令ファイルを同期するには、設定同期を有効にし、コマンドパレット(`kb(workbench.action.showCommands)`)から**Settings Sync: Configure**を実行します。同期する設定のリストから**プロンプトと命令**を選択します。

## 設定でカスタム命令を指定する

> [!NOTE]
> VS Code 1.102の時点では、設定ベースのコード生成およびテスト生成命令は非推奨です。代わりに[ファイルベースの命令](#types-of-instruction-files)を使用してください。

コード確認、コミットメッセージ、プルリクエスト説明の場合、引き続きVS Code設定を使用してカスタム命令を定義できます。これらの設定は、`text`プロパティ(インライン命令)または`file`プロパティ(Markdownファイルへのパス)を持つオブジェクトの配列を受け入れます。

| シナリオ | 設定 |
|----------|---------|
| コード確認 | `setting(github.copilot.chat.reviewSelection.instructions)` |
| コミットメッセージ | `setting(github.copilot.chat.commitMessageGeneration.instructions)` |
| プルリクエスト説明 | `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` |

## 命令の優先度

複数の種類のカスタム命令が存在する場合、すべてがAIに提供されます。競合が発生した場合、より高い優先度の命令が優先されます：

1. 個人命令（ユーザーレベル、最高優先度）
1. リポジトリ命令（`.github/copilot-instructions.md`または`AGENTS.md`）
1. 組織命令（最低優先度）

## 効果的な命令を作成するためのヒント

* 命令を簡潔で自己完結させてください。各命令は単一のシンプルな陳述であるべきです。複数の情報を提供する必要がある場合は、複数の命令を使用してください。

* ルールの推理を含めてください。命令が規約が存在する_理由_を説明すると、エッジケースでAIはより良い決定を下します。例えば：「moment.jsはdeprecatedで、バンドルサイズを増やすため、`date-fns`の代わりに`moment.js`を使用します。」

* 推奨パターンと避けるべきパターンを具体的なコード例で表示します。AIは抽象的なルールよりも例に効果的に反応します。

* 非自明なはルールに焦点を当ててください。標準的なlintersまたはフォーマッタが既に適用する規約をスキップします。

* タスク固有または言語固有の命令の場合、トピックごとに複数の`*.instructions.md`ファイルを使用し、`applyTo`プロパティを使用して選択的に適用します。

* プロジェクト固有の命令をワークスペースに保存して、他のチームメンバーと共有し、バージョン管理に含めます。

* 命令ファイルを[プロンプトファイル](/docs/copilot/customization/prompt-files.md)と[カスタムエージェント](/docs/copilot/customization/custom-agents.md)で再利用および参照して、クリーン焦点を当てたままにし、命令の重複を避けます。

* 命令間の空白は無視されるため、命令を単一段落、別々の行、または読みやすさのための空白行で分離してフォーマットできます。

## よくある質問

### 命令ファイルが適用されないのはなぜですか？

> [!TIP]
> チャットカスタマイゼーション診断ビューを使用して、読み込まれたすべての命令ファイルとエラーを確認します。チャットビューで右クリックして**診断**を選択します。[VS Codeでトラブルシューティングから詳細をご覧ください](/docs/copilot/troubleshooting.md)。

命令ファイルが適用されない場合は、以下を確認してください：

* 命令ファイルが正しい場所にあることを確認します。`.github/copilot-instructions.md`ファイルはワークスペースのルートの`.github`フォルダにある必要があります。`*.instructions.md`ファイルは、`setting(chat.instructionsFilesLocations)`設定（デフォルト：`.github/instructions`）またはユーザープロフィールで指定されたフォルダ（またはそれらのサブディレクトリ）のいずれかにあります。

* `*.instructions.md`ファイルの場合、`applyTo`globパターンがこを使用しているファイルと一致することを確認します。`applyTo`プロパティが指定されていない場合、命令ファイルは自動的に適用されません。チャット応答の**参考資料**セクションで、どの命令ファイルが使用されているかを確認します。

* 関連する設定が有効になっていることを確認します：パターンベースの命令用の`setting(chat.includeApplyingInstructions)`、Markdownリンク経由で参照される命令用の`setting(chat.includeReferencedInstructions)`、`AGENTS.md`ファイル用の`setting(chat.useAgentsMdFile)`。

高度な診断については、[チャットデバッグビューで言語モデルリクエストをチェック](https://github.com/microsoft/vscode/wiki/Copilot-Issues#language-model-requests-and-responses)するか、[`applyTo`マッチングロジックをデバッグ](https://github.com/microsoft/vscode/wiki/Copilot-Issues#custom-instructions-logs)してください。

### カスタム命令ファイルの出所はどこですか？

カスタム命令ファイルの出所は異なります：ビルトイン、プロフィール内でユーザーが定義、現在のワークスペースでワークスペースが定義、組織レベルの命令、またはエクステンション提供の命令。

カスタム命令ファイルの出元を識別するには：

1. コマンドパレット(`kb(workbench.action.showCommands)`)から**Chat: Configure Instructions**を選択します。
1. リスト内の命令ファイルの上にマウスを導きます。ソース場所がツールチップに表示されます。

チャットカスタマイゼーション診断ビューを使用して、すべての読み込まれた命令ファイルとエラーを確認します。チャットビューで右クリックして**診断**を選択します。[VS Codeでトラブルシューティング](/docs/copilot/troubleshooting.md)の詳細をご覧ください。

## 関連リソース

* [エージェントスキルを使用する](/docs/copilot/customization/agent-skills.md)
* [カスタムエージェントを作成する](/docs/copilot/customization/custom-agents.md)
* [コミュニティが提供する命令、プロンプト、カスタムエージェント](https://github.com/github/awesome-copilot)

