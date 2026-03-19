---
ContentId: a7d3e5f8-2c4b-4d9a-b8e1-3f6c9a2d7e41
DateApproved: 3/9/2026
MetaDescription: VS CodeのAgent Skillsを使用して、GitHub Copilotに特殊な機能を教える方法について説明します。VS Code、GitHub Copilot CLI、GitHub Copilot coding agentで動作します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- copilot
- agents
- skills
- instructions
- customization
- ai
- claude
---
# VS CodeでAgent Skillsを使用する

Agent Skillsは、関連性がある場合にGitHub Copilotが読み込むことで特殊なタスクを実行できる、命令、スクリプト、リソースのフォルダです。Agent Skillsは[オープンスタンダード](https://agentskills.io)であり、VS CodeのGitHub Copilot、GitHub Copilot CLI、GitHub Copilot coding agentを含む複数のAIエージェント全体で動作します。

主にコーディングガイドラインを定義する[カスタム命令](/docs/copilot/customization/custom-instructions.md)とは異なり、スキルは、スクリプト、例、その他のリソースを含むことができる特殊な機能とワークフローを有効にします。作成したスキルはポータブルで、スキル互換のエージェントで動作します。

Agent Skillsの主な利点：

* **Copilotの専門化**：コンテキストを繰り返さずにドメイン固有のタスク用に機能をカスタマイズ
* **反復を減らす**：一度作成すれば、すべての会話で自動的に使用可能
* **機能を組み合わせる**：複数のスキルを組み合わせて複雑なワークフローを構築
* **効率的な読み込み**：必要に応じて関連するコンテンツのみがコンテキストに読み込まれる

> [!TIP]
> [Chat Customizations editor](/docs/copilot/customization/overview.md#chat-customizations-editor)（プレビュー）を使用して、1か所ですべてのチャットカスタマイズの検出、作成、管理ができます。コマンドパレットから**Chat: Open Chat Customizations**を実行します。

## Agent Skillsとカスタム命令の比較

Agent SkillsとカスタムプロンプトはどちらもCopilotの動作をカスタマイズするのに役立ちますが、異なる目的に機能します：

| 機能 | Agent Skills | カスタム命令 |
| ------- | ------------ | ------------------- |
| **目的** | 特殊な機能とワークフローを教える | コーディング基準とガイドラインを定義 |
| **ポータビリティ** | VS Code、Copilot CLI、Copilot coding agentで動作 | VS CodeとGitHub.comのみ |
| **内容** | 命令、スクリプト、例、およびリソース | 命令のみ |
| **スコープ** | タスク固有、オンデマンド読み込み | 常に適用（またはglobパターン経由） |
| **標準** | オープンスタンダード（[agentskills.io](https://agentskills.io)） | VS Code固有 |

以下のような場合はAgent Skillsを使用します：

* 異なるAIツール全体で動作する再利用可能な機能を作成したい
* 命令と一緒にスクリプト、例、またはその他のリソースを含めたい
* より広いAIコミュニティと機能を共有したい
* テスト、デバッグ、デプロイなどの特殊なワークフローを定義したい

以下のような場合はカスタム命令を使用します：

* プロジェクト固有のコーディング基準を定義したい
* 言語またはフレームワークの規則を設定したい
* コードレビューまたはコミットメッセージガイドラインを指定したい
* globパターンを使用してファイルタイプに基づいて規則を適用したい

## スキルを作成する

> [!TIP]
> チャット入力に`/skills`と入力すると、**Configure Skills**メニューがすぐに開きます。

スキルはスキルの動作を定義する`SKILL.md`ファイルを含むディレクトリに保存されます。VS Codeは2種類のスキルをサポートしています：

| スキルタイプ | 場所 |
| ---------- | -------- |
| プロジェクトスキル（リポジトリに保存） | `.github/skills/`、`.claude/skills/`、`.agents/skills/` |
| 個人スキル（ユーザープロファイルに保存） | `~/.copilot/skills/`、`~/.claude/skills/`、`~/.agents/skills/` |

> [!TIP]
> `setting(chat.agentSkillsLocations)`設定を使用して、VS Codeがスキルを検索する追加の場所を設定できます。これはスキルをプロジェクト全体で共有したり、一元管理場所に保持する場合に便利です。

スキルを作成するには：

1. ワークスペースに`.github/skills`ディレクトリを作成します。

1. スキル用のサブディレクトリを作成します。各スキルは独自のディレクトリを持つ必要があります（例：`.github/skills/webapp-testing`）。

1. スキルディレクトリに以下の構造の`SKILL.md`ファイルを作成します：

  ```markdown
  ---
  name: skill-name
  description: スキルが実行する内容と使用タイミングの説明
  ---

  # スキル命令

  詳細な命令、ガイドライン、例をここに入力します...
  ```

1. 必要に応じて、スクリプト、例、またはその他のリソースをスキルディレクトリに追加します。

  たとえば、Webアプリケーションをテストするためのスキルには、以下が含まれる場合があります：

  * `SKILL.md` - テストを実行するための命令
  * `test-template.js` - テンプレートテストファイル
  * `examples/` - テストシナリオの例

### AIを使用してスキルを生成する

機能の説明に基づいてAIでスキルを生成できます。チャットに`/create-skill`と入力して、必要なスキルについて説明します（例：「統合テストを実行およびデバッグするためのスキル」）。エージェントが確認質問をし、ディレクトリ構造、命令、フロントマターを含む`SKILL.md`ファイルを生成します。

継続的な会話から再利用可能なスキルを動かすこともできます。たとえば、複雑な問題をデバッグした複数ターンのセッション後に「先ほどデバッグしたやり方からスキルを作成して」と指示すれば、複数ステップの手順を再利用可能なスキルとして取得できます。

## SKILL.mdファイル形式

`SKILL.md`ファイルはYAMLフロントマターを持つMarkdownファイルで、スキルのメタデータと動作を定義します。

### ヘッダ（必須）

ヘッダはYAMLフロントマターとして以下のフィールドで形式化されます：

| フィールド | 必須 | 説明 |
|-------|----------|-------------|
| `name` | はい | スキルの一意の識別子。小文字を使用し、スペースにハイフンを使用します（例：`webapp-testing`）。親ディレクトリ名と一致する必要があります。最大64文字。 |
| `description` | はい | スキルが実行する内容**と使用タイミング**の説明。機能と使用例の両方について具体的に記述します。これはCopilotがスキルを読み込むかどうかを判断するのに役立ちます。最大1024文字。 |
| `argument-hint` | いいえ | スキルをスラッシュコマンドとして呼び出す際にチャット入力フィールドに表示されるヒントテキスト。ユーザーが追加情報を提供する内容を理解するのをサポートします（例：`[test file] [options]`）。 |
| `user-invocable` | いいえ | スキルがチャットメニューのスラッシュコマンドとして表示されるかどうかを制御します。デフォルトは`true`です。`false`に設定するとスキルを`/`メニューから非表示にしながら、エージェントが自動読み込みできるようにします。 |
| `disable-model-invocation` | いいえ | エージェントが関連性に基づいてスキルを自動的に読み込めるかどうかを制御します。デフォルトは`false`です。`true`に設定するとスラッシュコマンドによる手動呼び出しのみが必要になります。 |

### 本文

スキルの本文には、このスキルを使用する際にCopilotが従うべき命令、ガイドライン、例が含まれます。以下を説明する明確で具体的な命令を作成してください：

* スキルが実現する内容
* スキルを使用するタイミング
* 実行する段階的な手順
* 予想される入力と出力の例
* スキルディレクトリに含まれるスクリプトまたはリソースへの参照

スキルディレクトリ内のファイルを相対パスを使用して参照できます。たとえば、スキルディレクトリ内のスクリプトを参照するには`[test script](./test-template.js)`を使用します。

## スキルの例

以下の例は、作成できるさまざまなタイプのスキルを示しています。

<details>
<summary>例：Webアプリケーションテストスキル</summary>

````markdown
---
name: webapp-testing
description: Playwrightを使用したWebアプリケーションテストガイド。ブラウザベースのテストを作成または実行するよう求められたときに使用します。
---

# PlaywrightによるWebアプリケーションテスト

このスキルは、PlaywrightをしたWebアプリケーション用ブラウザベーステストの作成と実行をサポートします。

## このスキルを使用するタイミング

このスキルは以下が必要な場合に使用します：
- Webアプリケーション用の新しいPlaywrightテストの作成
- 失敗しているブラウザテストのデバッグ
- 新しいプロジェクトのテストインフラストラクチャのセットアップ

## テストの作成

1. [テンプレート](./test-template.js)の標準テスト構造を確認
2. テストするユーザーフロー確認
3. `tests/`ディレクトリで新しいテストファイルを作成
4. Playwrightのロケータを使用して要素を見つけます（ロールベースのセレクタを使用）
5. 予想される動作を検証するためのアサーションを追加

## テストの実行

ローカルでテストを実行するには：
```bash
npx playwright test
```

テストをデバッグするには：
```bash
npx playwright test --debug
```

## ベストプラクティス

- 動的コンテンツにdata-testid属性を使用
- テストを独立してアトミックに保つ
- 複雑なページにはPage Object Modelを使用
- 失敗時にスクリーンショットを取得
````

</details>

<details>
<summary>例：GitHub Actionsデバッグスキル</summary>

````markdown
---
name: github-actions-debugging
description: 失敗しているGitHub Actionsワークフローのデバッグガイド。失敗しているGitHub Actionsワークフローのデバッグを求められたときに使用します。
---

# GitHub Actionsのデバッグ

このスキルは、プルリクエスト内で失敗しているGitHub Actionsワークフローのデバッグをサポートします。

## プロセス

1. `list_workflow_runs`ツールを使用してプルリクエストの最近のワークフロー実行とそのステータスを確認
2. `summarize_job_log_failures`ツールを使用して失敗しているジョブのログのAI概要を取得
3. より詳しい情報が必要な場合、`get_job_logs`または`get_workflow_run_logs`ツールを使用して完全な失敗ログを取得
4. 環境内で失敗を再現してみる
5. 失敗するビルドを修正し、変更をコミットする前に修正を検証

## よくある問題

- **環境変数がない**：必要なシークレットがすべて設定されていることを確認
- **バージョン不一致**：アクションバージョンと依存関係の互換性を確認
- **権限の問題**：ワークフローに必要な権限があることを確認
- **タイムアウトの問題**：長時間実行ジョブの分割またはタイムアウト値の増加を検討
````

</details>

## スキルをスラッシュコマンドとして使用する

スキルは[プロンプトファイル](/docs/copilot/customization/prompt-files.md)と一緒にチャット内でスラッシュコマンドとして利用できます。チャット入力フィールドに`/`と入力すると、利用可能なスキルとプロンプトのリストが表示され、呼び出すスキルを選択できます。

スラッシュコマンドの後に追加のコンテキストを追加できます。たとえば、`/webapp-testing for the login page`または`/github-actions-debugging PR #42`です。

デフォルトでは、すべてのスキルが`/`メニューに表示されます。`user-invocable`および`disable-model-invocation`フロントマタープロパティを使用して、各スキルのアクセス方法を制御してください：

| 設定 | スラッシュコマンド | Copilotによる自動読み込み | ユースケース |
|---|---|---|---|
| デフォルト（両方のプロパティが省略） | はい | はい | 汎用スキル |
| `user-invocable: false` | いいえ | はい | モデルが関連性に基づいて読み込む背景知識スキル |
| `disable-model-invocation: true` | はい | いいえ | 必要に応じてのみ実行したいスキル |
| 両方を設定 | いいえ | いいえ | 無効なスキル |

## Copilotがスキルを使用する方法

スキルはコンテキストを効率的に保つためにコンテンツを段階的に読み込みます。以下は、Copilotが`webapp-testing`スキルを使用する方法の例です：

1. **検出**：Copilotはスキルの`name`と`description`をYAMLフロントマターから読み込みます。「ログインページのテストをサポート」と求めたとき、Copilotはこれを説明に基づいて`webapp-testing`スキルと一致させます。

2. **命令の読み込み**：Copilotは`SKILL.md`本文をコンテキストに読み込み、テスト手順とガイドラインへのアクセス権を付与します。チャットに`/webapp-testing`と入力することで、このステップを直接トリガーすることもできます。

3. **リソースへのアクセス**：Copilotが命令を実行すると、`test-template.js`やシナリオ例などのスキルディレクトリ内の追加ファイルに、参照する際にのみアクセスします。

この3段階の読み込みシステムは、コンテキストを消費することなく多くのスキルをインストールできることを示しています。Copilotは各タスクに関連するものだけを読み込みます。

## 共有スキルを使用する

他のユーザーが作成したスキルを使用して、Copilotの機能を強化できます。[github/awesome-copilot](https://github.com/github/awesome-copilot)リポジトリには、スキル、カスタムエージェント、命令、プロンプトの成長し続けるコミュニティコレクションが含まれています。[anthropics/skills](https://github.com/anthropics/skills)リポジトリには追加の参照スキルが含まれています。

[エージェントプラグイン](/docs/copilot/customization/agent-plugins.md)にバンドルされているスキルを検出およびインストールすることもできます。インストールされたプラグインからのスキルは、** Configure Skills**メニュー内でローカルに定義されたスキルと一緒に表示されます。

共有スキルを使用するには：

1. リポジトリ内で利用可能なスキルを参照
1. スキルディレクトリを`.github/skills/`フォルダにコピー
1. 必要に応じて`SKILL.md`ファイルを確認してカスタマイズ
1. 必要に応じてリソースを変更または追加

> [!TIP]
> 使用前に共有スキルを常に確認して、要件とセキュリティ基準を満たすことを確認してください。VS Codeの[ターミナルツール](/docs/copilot/agents/agent-tools.md#terminal-commands)はスクリプト実行用の制御を提供し、[自動承認オプション](/docs/copilot/agents/agent-tools.md#automatically-approve-terminal-commands)と実行するコードの厳格な制御が含まれます。自動承認機能の[セキュリティに関する考慮事項](/docs/copilot/security.md#automated-approval)についての詳細を学んでください。

## 拡張機能からスキルを投稿する

拡張機能は、`package.json`の`chatSkills`貢献ポイントを使用してスキルを投稿できます。パスは`SKILL.md`ファイルを含むディレクトリを指し、[Agent Skills仕様](https://agentskills.io/specification)に従う必要があります。

### 必須フォルダ構造

スキルディレクトリは以下の構造に従う必要があります：

```text
extension-root/
└── skills/
  └── my-skill/           # ディレクトリ名はSKILL.mdの`name`フィールドと一致する必要があります
    └── SKILL.md         # 必須
```

### package.jsonでスキルを登録する

拡張機能の`package.json`に`chatSkills`貢献ポイントを追加します。`path`プロパティは対応する`SKILL.md`ファイルを指す必要があります：

```json
{
  "contributes": {
  "chatSkills": [
    {
    "path": "./skills/my-skill/SKILL.md"
    }
  ]
  }
}
```

> [!IMPORTANT]
> `SKILL.md`フロントマターの`name`フィールドは親ディレクトリ名と合致する必要があります。たとえば、ディレクトリが`skills/my-skill/`の場合、`name`フィールドは`my-skill`である必要があります。名前が一致しない場合、スキルは読み込まれません。

`SKILL.md`ファイルは[プロジェクトと個人スキル](#create-a-skill)と同じ形式に従います。たとえば：

```markdown
---
name: my-skill
description: スキルが実行する内容と使用タイミングの説明。
---

# My Skill

スキルの詳細な命令...
```

## Agent Standard

Agent Skillsはオープンスタンダードで、異なるAIエージェント間のポータビリティを有効にします。VS Codeで作成したスキルは、以下を含む複数のエージェントで動作します：

* **VS CodeのGitHub Copilot**：チャットとエージェントモードで利用可能
* **GitHub Copilot CLI**：ターミナルで作業する際にアクセス可能
* **GitHub Copilot coding agent**：自動コーディングタスク中に使用

Agent Skills標準については[agentskills.io](https://agentskills.io)で詳しく学んでください。

## 関連リソース

* [AI応答カスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム命令を作成](/docs/copilot/customization/custom-instructions.md)
* [再利用可能なプロンプトファイルを作成](/docs/copilot/customization/prompt-files.md)
* [カスタムエージェントを作成](/docs/copilot/customization/custom-agents.md)
* [Agent Skills仕様](https://agentskills.io)
* [参照スキルリポジトリ](https://github.com/anthropics/skills)
* [エージェントプラグインの検出と管理](/docs/copilot/customization/agent-plugins.md)

