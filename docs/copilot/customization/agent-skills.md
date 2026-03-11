---
ContentId: a7d3e5f8-2c4b-4d9a-b8e1-3f6c9a2d7e41
DateApproved: 3/9/2026
MetaDescription: GitHub Copilotに特殊な能力を教えるVS CodeのAgent Skillsの使い方を学びます。VS Code、GitHub Copilot CLI、GitHub Copilot coding agentで動作します。
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

Agent Skillsは、GitHub Copilotが関連するタスクを実行するときにロードできる命令、スクリプト、およびリソースのフォルダです。Agent Skillsは、VS CodeのGitHub Copilot、GitHub Copilot CLI、GitHub Copilot coding agentを含む複数のAIエージェント全体で動作する[オープンスタンダード](https://agentskills.io)です。

主にコーディングガイドラインを定義する[カスタム命令](/docs/copilot/customization/custom-instructions.md)とは異なり、skillsは、スクリプト、例、およびその他のリソースを含むことができる特殊な機能とワークフローを有効にします。作成するskillはポータブルで、あらゆるskills互換エージェント全体で動作します。

Agent Skillsの主な利点：

* **Copilotを特化させる**：コンテキストを繰り返さずにドメイン固有のタスク用の機能を調整
* **繰り返しを削減**：一度作成してすべての会話で自動的に使用
* **機能を組み合わせる**：複数のskillsを組み合わせて複雑なワークフローを構築
* **効率的な読み込み**：必要なコンテンツのみがコンテキストに読み込まれます

> [!TIP]
> [Chat Customizationsエディタ](/docs/copilot/customization/overview.md#chat-customizations-editor)（プレビュー）を使用して、すべてのチャットカスタマイズを1か所で検出、作成、および管理します。コマンドパレットから**Chat: Open Chat Customizations**を実行します。

## Agent Skillsとカスタム命令の比較

Agent SkillsとカスタムinstructionsはどちらもCopilotの動作をカスタマイズするのに役立ちますが、別の目的に役立ちます：

| 機能 | Agent Skills | カスタム命令 |
| ------- | ------------ | ------------------- |
| **目的** | 特化した機能とワークフローを教える | コーディング標準とガイドラインを定義 |
| **移植性** | VS Code、Copilot CLI、およびCopilot coding agentで動作 | VS CodeおよびGitHub.comのみ |
| **コンテンツ** | 命令、スクリプト、例、およびリソース | 命令のみ |
| **スコープ** | タスク固有、オンデマンドで読み込み | 常に適用（またはglobパターン経由） |
| **標準** | オープンスタンダード（[agentskills.io](https://agentskills.io)） | VS Code固有 |

以下の場合にAgent Skillsを使用：

* 異なるAIツール全体で動作する再利用可能な機能を作成
* 命令と共にスクリプト、例、またはその他のリソースを含める
* より広いAIコミュニティと機能を共有
* テスト、デバッグ、またはデプロイメントプロセスのような特化したワークフローを定義

以下の場合にカスタム命令を使用：

* プロジェクト固有のコーディング標準を定義
* 言語またはフレームワークの慣例を設定
* コードレビューまたはコミットメッセージのガイドラインを指定
* globパターンを使用してファイルタイプに基づくルールを適用

## skillを作成

> [!TIP]
> チャット入力で`/skills`を入力して、**Configure Skills**メニューをすばやく開きます。

Skillsは、skillの動作を定義する`SKILL.md`ファイルを含むディレクトリに保存されます。VS Codeは2つのタイプのskillsをサポート：

| Skillタイプ | 場所 |
| ---------- | -------- |
| プロジェクトskills、リポジトリに保存 | `.github/skills/`、`.claude/skills/`、`.agents/skills/` |
| 個人用skills、ユーザープロファイルに保存 | `~/.copilot/skills/`、`~/.claude/skills/`、`~/.agents/skills/` |

> [!TIP]
> `setting(chat.agentSkillsLocations)`設定を使用して、VS Codeがskillsをリビューするさらに多くの場所を設定できます。これはプロジェクト全体でskillsを共有したり、中央の場所に保持するのに役立ちます。

skillを作成：

1. ワークスペースに`.github/skills`ディレクトリを作成。

1. skillのサブディレクトリを作成。各skillは独自のディレクトリを持つ必要があります（例えば、`.github/skills/webapp-testing`）。

1. skillディレクトリに以下の構造を含む`SKILL.md`ファイルを作成：

  ```markdown
  ---
  name: skill-name
  description: skillが何をするかと何に使用するかの説明
  ---

  # Skill Instructions

  詳細な命令、ガイドライン、および例がここに...
  ```

1. オプションで、skillディレクトリにスクリプト、例、またはその他のリソースを追加。

  たとえば、Webアプリケーションをテストするskillには：

  * `SKILL.md` - テストを実行する手順
  * `test-template.js` - テンプレートテストファイル
  * `examples/` - テストシナリオの例

### AIでskillを生成

skillの説明に基づいてAIを使用してskillを生成できます。チャットで`/create-skill`と入力し、必要なskillについて説明します（例えば、「統合テストを実行およびデバッグするためのskill」）。エージェントが明確化する質問をして、ディレクトリ構造、命令、およびfrontmatterを使用して`SKILL.md`ファイルを生成します。

継続中の会話から再利用可能なskillを抽出することもできます。たとえば、複雑な問題をデバッグしたマルチターンセッションの後で、「我々がちょうどデバッグした方法からskillを作成」と尋ねて、マルチステップの手順を再利用可能なskillとしてキャプチャします。

## SKILL.mdファイル形式

`SKILL.md`ファイルは、skillのメタデータと動作を定義するYAML frontmatterを持つMarkdownファイルです。

### ヘッダ（必須）

ヘッダは以下のフィールドを含むYAML frontmatterとしてフォーマット：

| フィールド | 必須 | 説明 |
|-------|----------|-------------|
| `name` | はい | skillの一意の識別子。小文字で、スペースにハイフンを使用（例えば、`webapp-testing`）。親ディレクトリ名と一致する必要があります。最大64文字。 |
| `description` | はい | skillが何をするか**およびいつ使用するか**の説明。Copilotがskillをいつロードするかを判断するのに役立つように、機能とユースケースの両方について具体的にしてください。最大1024文字。 |
| `argument-hint` | いいえ | skillがスラッシュコマンドとして呼び出されるときにチャット入力フィールドに表示されるヒントテキスト。ユーザーがどのような追加情報を提供する必要があるかを理解するのに役立ちます（例えば、`[test file] [options]`）。 |
| `user-invocable` | いいえ | skillが`/`メニューのスラッシュコマンドとして表示されるかどうかを制御。デフォルトは`true`。skillを`/`メニューから非表示にしながら、エージェントが自動的にロードすることを許可するには`false`に設定。 |
| `disable-model-invocation` | いいえ | エージェントが関連性に基づいてskillを自動的にロードできるかどうかを制御。デフォルトは`false`。スラッシュコマンド経由の手動呼び出しのみを必要とするには`true`に設定。 |

### 本文

skill本文には、このskillを使用するときにCopilotが従うべき命令、ガイドライン、および例が含まれています。以下を説明する明確で具体的な命令を作成：

* skillが何を達成するのに役立つか
* skillを使用するとき
* ステップバイステップの手順
* 予想される入力と出力の例
* 含まれているスクリプトまたはリソースへの参照

相対パスを使用してskillディレクトリ内のファイルを参照できます。たとえば、skillディレクトリのスクリプトを参照するには、`[test script](./test-template.js)`を使用。

## skillの例

以下の例は、作成できるさまざまな種類のskillsを示しています。

<details>
<summary>例：Webアプリケーションテストskill</summary>

````markdown
---
name: webapp-testing
description: Playwrightを使用したWebアプリケーションテストのガイド。ブラウザベースのテストの作成または実行を求められるときにこのskillを使用してください。
---

# Playwrightを使用したWebアプリケーションテスト

このskillは、Playwrightを使用してWebアプリケーション用のブラウザベースのテストを作成および実行するのに役立ちます。

## このskillを使用するとき

このskillが必要な場合に使用：
- Webアプリケーション用の新しいPlaywrightテストを作成
- 失敗したブラウザテストをデバッグ
- 新しいプロジェクトのテストインフラストラクチャを設定

## テストの作成

1. [テストテンプレート](./test-template.js)で標準的なテスト構造を確認
2. テストするユーザーフローを特定
3. `tests/`ディレクトリに新しいテストファイルを作成
4. Playwrightのロケータを使用して要素を検索（ロールベースのセレクタを推奨）
5. アサーションを追加して期待される動作を確認

## テストの実行

ローカルでテストを実行：
```bash
npx playwright test
```

テストをデバッグ：
```bash
npx playwright test --debug
```

## ベストプラクティス

- 動的コンテンツに対してdata-testid属性を使用
- テストを独立させて原子的に保つ
- 複雑なページにはPage Object Modelを使用
- 失敗時にスクリーンショットを撮成
````

</details>

<details>
<summary>例：GitHub Actionsデバッグskill</summary>

````markdown
---
name: github-actions-debugging
description: 失敗したGitHub Actionsワークフローをデバッグするためのガイド。失敗したGitHub Actionsワークフローをデバッグするよう求められるときにこのskillを使用してください。
---

# GitHub Actionsデバッグ

このskillは、プルリクエストで失敗したGitHub Actionsワークフローをデバッグするのに役立ちます。

## プロセス

1. `list_workflow_runs`toolを使用して、プルリクエストの最近のワークフロー実行とそのステータスを調べます
2. `summarize_job_log_failures`toolを使用して、失敗したジョブのログのAIサマリをを取得
3. さらに情報が必要な場合は、`get_job_logs`または`get_workflow_run_logs`toolを使用して完全な失敗ログを取得
4. 環境でローカルに失敗を再現
5. 失敗したビルドを修正し、変更をコミットする前に修正を確認

## 一般的な問題

- **環境変数がない**：すべての必要なシークレットが設定されていることを確認
- **バージョンの不一致**：アクションのバージョンと依存関係が互換性があることを確認
- **権限の問題**：ワークフローが必要な権限を持っていることを確認
- **タイムアウトの問題**：長時間実行されるジョブを分割するか、タイムアウト値を増やすことを検討
````

</details>

## skillsをスラッシュコマンドとして使用

Skillsは[プロンプトファイル](/docs/copilot/customization/prompt-files.md)と一緒にチャットのスラッシュコマンドとして利用できます。チャット入力フィールドで`/`を入力して、利用可能なskillsとプロンプトのリストを表示し、skillを選択して呼び出します。

スラッシュコマンドの後に追加のコンテキストを加えることができます。たとえば、`/webapp-testing for the login page`または`/github-actions-debugging PR #42`。

デフォルトでは、すべてのskillsが`/`メニューに表示されます。`user-invocable`および`disable-model-invocation` frontmatterプロパティを使用して、各skillがどのようにアクセスされるかを制御：

| 設定 | スラッシュコマンド | Copilotによる自動読み込み | ユースケース |
|---|---|---|---|
| デフォルト（両方のプロパティを省略） | はい | はい | 汎用skillsのための |
| `user-invocable: false` | いいえ | はい | モデルが関連するときにロードする背景知識skillのための |
| `disable-model-invocation: true` | はい | いいえ | オンデマンドのみで実行したいskillのための |
| 両方を設定 | いいえ | いいえ | 無効なskillのための |

## Copilotがskillsを使用する方法

Skillsはコンテキストを効率的に保つためにコンテンツを段階的にロードします。Copilotが`webapp-testing`skillを使用する方法の例：

1. **検出**：CopilotはYAML frontmatterからskillの`name`および`description`を読みます。「ログインページのテストを手伝ってください」と尋ねると、Copilotはそのdescriptionに基づいて`webapp-testing`skillにマッチします。

2. **命令の読み込み**：Copilotは`SKILL.md`本文をコンテキストにロードし、詳細なテスト手順とガイドラインへのアクセスを与えます。また、チャットで`/webapp-testing`を入力することでこのステップを直接トリガーできます。

3. **リソースアクセス**：Copilotが命令をステップバイステップで進めるにつれて、`test-template.js`やテストシナリオの例など、skillディレクトリ内のその他のファイルにアクセスするのは、参照するときのみです。

この3レベルの読み込みシステムは、コンテキストを消費せずに多くのskillsをインストールできることを意味します。Copilotは各タスクに関連するものだけをロードします。

## 共有skiliを使用

他のユーザーによって作成されたskillsを使用してCopilotの機能を強化できます。[github/awesome-copilot](https://github.com/github/awesome-copilot)リポジトリには、skillsの成長するコミュニティコレクション、カスタムエージェント、命令、およびプロンプトが含まれています。[anthropics/skills](https://github.com/anthropics/skills)リポジトリには、その他の参照skillsが含まれています。

[agentプラグイン](/docs/copilot/customization/agent-plugins.md)にバンドルされているskillsを検出およびインストールすることもできます。インストールされたプラグインからのskillsは、**Configure Skills**メニューのローカルに定義されたskillsと一緒に表示されます。

共有skillを使用：

1. リポジトリで利用可能なskillsを閲覧
1. skillディレクトリを`.github/skills/`フォルダにコピー
1. 必要に応じて`SKILL.md`ファイルを確認およびカスタマイズ
1. 必要に応じてリソースを変更または追加

> [!TIP]
> 共有skillsを使用する前に必ず確認してください。これらが要件とセキュリティ基準を満たしていることを確認します。VS Codeの[terminalツール](/docs/copilot/agents/agent-tools.md#terminal-commands)はスクリプト実行の制御を提供します。これには、設定可能なアローリストを使用する[自動承認オプション](/docs/copilot/agents/agent-tools.md#automatically-approve-terminal-commands)と、どのコードが実行されるかの厳密な制御が含まれます。[自動承認機能](/docs/copilot/security.md#automated-approval)のセキュリティに関する考慮事項についてさらに学びます。

## 拡張機能からskillsに貢献

拡張機能は、その`package.json`の`chatSkills`貢献ポイントを使用してskillsに貢献できます。パスは、[Agent Skillsの仕様](https://agentskills.io/specification)に従って`SKILL.md`ファイルを含むディレクトリを指す必要があります。

### 必要なフォルダ構造

skillディレクトリは、この構造に従う必要があります：

```text
extension-root/
└── skills/
  └── my-skill/           # ディレクトリ名はSKILL.mdの`name`フィールドと一致する必要があります
    └── SKILL.md         # 必須
```

### package.jsonでskillを登録

拡張機能の`package.json`に`chatSkills`貢献ポイントを追加。`path`プロパティは対応する`SKILL.md`ファイルを指す必要があります：

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
> `SKILL.md` frontmatterの`name`フィールドは親ディレクトリ名と一致する必要があります。たとえば、ディレクトリが`skills/my-skill/`の場合、`name`フィールドは`my-skill`である必要があります。名前が一致しない場合、skillはロードされません。

`SKILL.md`ファイルは[プロジェクトおよび個人用skills](#create-a-skill)と同じフォーマットに従います。例えば：

```markdown
---
name: my-skill
description: skillが何をするかとそれが何に使用されるかの説明。
---

# My Skill

skillの詳細な命令...
```

## Agent Skillsスタンダード

Agent Skillsは、異なるAIエージェント全体でのポータビリティを有効にするオープンスタンダードです。VS Codeで作成するskillsは、以下を含む複数のエージェントで動作：

* **VS CodeのGitHub Copilot**：チャットおよびエージェントモードで利用可能
* **GitHub Copilot CLI**：ターミナルで作業するときアクセス可能
* **GitHub Copilot coding agent**：自動化されたコーディングタスク中に使用

[agentskills.io](https://agentskills.io)でAgent Skillsスタンダードについて詳細を学びます。

## 関連リソース

* [AI応答カスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム命令を作成](/docs/copilot/customization/custom-instructions.md)
* [再利用可能なプロンプトファイルを作成](/docs/copilot/customization/prompt-files.md)
* [カスタムエージェントを作成](/docs/copilot/customization/custom-agents.md)
* [Agent Skillsの仕様](https://agentskills.io)
* [参照skillsリポジトリ](https://github.com/anthropics/skills)
* [agentプラグインを検出および管理](/docs/copilot/customization/agent-plugins.md)

