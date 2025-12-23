---
ContentId: a7d3e5f8-2c4b-4d9a-b8e1-3f6c9a2d7e41
DateApproved: 12/17/2025
MetaDescription: VS CodeでAgent Skillsを使用して、VS Code、GitHub Copilot CLI、GitHub Copilot coding agent全体で動作するGitHub Copilotの専門的な機能を教える方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでAgent Skillsを使用する

Agent Skillsは、関連する場合にGitHub Copilotが読み込んで専門的なタスクを実行できる、指示、スクリプト、リソースのフォルダーです。Agent Skillsは、VS CodeのGitHub Copilot、GitHub Copilot CLI、GitHub Copilot coding agentなど、複数のAIエージェントで動作する[オープン標準](https://agentskills.io)です。

主にコーディングガイドラインを定義する[カスタム指示](/docs/copilot/customization/custom-instructions.md)とは異なり、スキルはスクリプト、例、その他のリソースを含められる専門的な機能とワークフローを有効にします。作成したスキルはポータブルで、スキル互換のどのエージェントでも動作します。

Agent Skillsの主な利点:

- **Copilotを専門化**: コンテキストを繰り返さずに、ドメイン固有のタスク向けに機能を調整
- **繰り返しを削減**: 一度作成すれば、すべての会話で自動的に使用
- **機能を合成**: 複数のスキルを組み合わせて複雑なワークフローを構築
- **効率的な読み込み**: 必要なときに関連するコンテンツだけをコンテキストに読み込む

> [!NOTE]
> VS CodeでのAgent Skillsサポートは現在プレビューで、[VS Code Insiders](https://code.visualstudio.com/insiders/)でのみ利用できます。Agent Skillsを使用するには、`setting(chat.useAgentSkills)`設定を有効にしてください。

## Agent Skillsとカスタム指示の違い

Agent Skillsもカスタム指示もCopilotの動作をカスタマイズするのに役立ちますが、目的が異なります。

| 特徴 | Agent Skills | カスタム指示 |
|---------|-------------|---------------------|
| **目的** | 専門的な機能とワークフローを教える | コーディング標準とガイドラインを定義する |
| **可搬性** | VS Code、Copilot CLI、Copilot coding agent全体で動作 | VS CodeとGitHub.comのみ |
| **内容** | 指示、スクリプト、例、リソース | 指示のみ |
| **スコープ** | タスク固有、オンデマンドで読み込み | 常に適用(またはglobパターン経由) |
| **標準** | オープン標準([agentskills.io](https://agentskills.io)) | VS Code固有 |

次の場合はAgent Skillsを使用します。
- 異なるAIツール間で動作する再利用可能な機能を作成したい
- 指示に加えてスクリプト、例、その他のリソースも含めたい
- より広いAIコミュニティと機能を共有したい
- テスト、デバッグ、デプロイプロセスのような専門的なワークフローを定義したい

次の場合はカスタム指示を使用します。
- プロジェクト固有のコーディング標準を定義したい
- 言語やフレームワークの規約を設定したい
- コードレビューやコミットメッセージのガイドラインを指定したい
- globパターンを使ってファイル種類に基づくルールを適用したい

## スキルを作成する

スキルは、スキルの動作を定義する`SKILL.md`ファイルを含むディレクトリに保存します。VS Codeは2つの場所のスキルをサポートしています。

* `.github/skills/` - Copilotで使用する新しいスキルすべてに推奨される共有場所
* `.claude/skills/` - 互換性維持のためにサポートされるレガシーの場所

スキルを作成するには:

1. ワークスペースに`.github/skills`ディレクトリを作成します。

1. スキル用のサブディレクトリを作成します。各スキルには専用のディレクトリが必要です(例: `.github/skills/webapp-testing`)。

1. 次の構造で、スキルディレクトリに`SKILL.md`ファイルを作成します。

    ```markdown
    ---
    name: skill-name
    description: スキルが何を行い、いつ使用するかの説明
    ---

    # スキルの指示

    ここに詳細な指示、ガイドライン、例を記述します...
    ```

1. 必要に応じて、スキルのディレクトリにスクリプト、例、その他のリソースを追加します。

    たとえば、Webアプリケーションのテスト用スキルには次が含まれることがあります。
    - `SKILL.md` - Instructions for running tests
    - `test-template.js` - A template test file
    - `examples/` - Example test scenarios

### SKILL.mdファイル形式

`SKILL.md`ファイルは、スキルのメタデータと動作を定義するYAMLフロントマターを含むMarkdownファイルです。

#### ヘッダー(必須)

ヘッダーは、次のフィールドを含むYAMLフロントマターとして書式設定します。

| フィールド | 必須 | 説明 |
|-------|----------|-------------|
| `name` | はい | スキルの一意の識別子。小文字で、スペースにはハイフンを使用します(例: `webapp-testing`)。最大64文字。 |
| `description` | はい | スキルが何を行うか**およびいつ使用するか**の説明。Copilotがスキルを読み込むタイミングを判断できるよう、機能とユースケースの両方を具体的に記述します。最大1024文字。 |

#### 本文

スキル本文には、このスキルを使用するときにCopilotが従うべき指示、ガイドライン、例を含めます。次を説明する、明確で具体的な指示を書いてください。

- スキルが達成を支援する内容
- スキルを使用するタイミング
- 従うべき手順(ステップバイステップ)
- 期待される入力と出力の例
- 同梱するスクリプトやリソースへの参照

相対パスを使用して、スキルディレクトリ内のファイルを参照できます。たとえば、スキルディレクトリ内のスクリプトを参照するには、`[test script](./test-template.js)`を使用します。

## スキルの例

次の例は、作成できるさまざまな種類のスキルを示しています。

<details>
<summary>例: Webアプリケーションテストスキル</summary>

````markdown
---
name: webapp-testing
description: Playwrightを使用してWebアプリケーションをテストするためのガイド。ブラウザベースのテストを作成または実行するよう求められたときに使用します。
---

# PlaywrightによるWebアプリケーションテスト

このスキルは、Playwrightを使用してWebアプリケーションのブラウザベースのテストを作成および実行するのに役立ちます。

## このスキルを使用するタイミング

次の場合にこのスキルを使用します。
- Create new Playwright tests for web applications
- Debug failing browser tests
- Set up test infrastructure for a new project

## テストの作成

1. Review the [test template](./test-template.js) for the standard test structure
2. Identify the user flow to test
3. Create a new test file in the `tests/` directory
4. Use Playwright's locators to find elements (prefer role-based selectors)
5. Add assertions to verify expected behavior

## テストの実行

ローカルでテストを実行するには:
```bash
npx playwright test
```

テストをデバッグするには:
```bash
npx playwright test --debug
```

## ベストプラクティス

- Use data-testid attributes for dynamic content
- Keep tests independent and atomic
- Use Page Object Model for complex pages
- Take screenshots on failure
````

</details>

<details>
<summary>例: GitHub Actionsデバッグスキル</summary>

````markdown
---
name: github-actions-debugging
description: 失敗しているGitHub Actionsワークフローをデバッグするためのガイド。失敗しているGitHub Actionsワークフローのデバッグを求められたときに使用します。
---

# GitHub Actionsのデバッグ

このスキルは、プルリクエスト内で失敗しているGitHub Actionsワークフローのデバッグに役立ちます。

## 手順

1. `list_workflow_runs`ツールを使用して、プルリクエストの最近のワークフロー実行とそのステータスを確認します
2. `summarize_job_log_failures`ツールを使用して、失敗したジョブのログのAI要約を取得します
3. さらに情報が必要な場合は、`get_job_logs`または`get_workflow_run_logs`ツールを使用して、完全な失敗ログを取得します
4. 手元の環境でローカルに失敗を再現してみます
5. 失敗しているビルドを修正し、変更をコミットする前に修正を検証します

## よくある問題

- **環境変数の不足**: 必要なシークレットがすべて構成されていることを確認します
- **バージョンの不一致**: アクションのバージョンと依存関係に互換性があることを確認します
- **権限の問題**: ワークフローに必要な権限があることを確認します
- **タイムアウトの問題**: 長時間実行されるジョブを分割するか、タイムアウト値を増やすことを検討します
````

</details>

## Copilotがスキルを使用する仕組み

スキルはプログレッシブディスクロージャーを使用して、必要なときにのみコンテンツを効率的に読み込みます。この3レベルの読み込みシステムにより、コンテキストを消費せずに多数のスキルをインストールできます。

**レベル1: スキルの検出**

CopilotはYAMLフロントマターから`name`と`description`を読み取ることで、利用可能なスキルを常に把握しています。このメタデータは軽量で、Copilotがどのスキルがリクエストに関連するかを判断するのに役立ちます。

**レベル2: 指示の読み込み**

リクエストがスキルの説明に一致すると、Copilotは`SKILL.md`ファイル本文をコンテキストに読み込みます。詳細な指示が利用可能になるのはその後です。

**レベル3: リソースへのアクセス**

Copilotは、必要に応じてのみスキルディレクトリ内の追加ファイル(スクリプト、例、ドキュメント)にアクセスできます。これらのリソースはCopilotが参照するまで読み込まれないため、コンテキストを効率的に保てます。

このアーキテクチャにより、スキルはプロンプトに基づいて自動的に有効化され、手動で選択する必要はありません。多数のスキルをインストールでき、Copilotは各タスクに関連するものだけを読み込みます。

## 共有スキルを使用する

他の人が作成したスキルを使用して、Copilotの機能を強化できます。[github/awesome-copilot](https://github.com/github/awesome-copilot)リポジトリには、スキル、カスタムエージェント、指示、プロンプトのコミュニティコレクションが増え続けています。[anthropics/skills](https://github.com/anthropics/skills)リポジトリには、追加の参照スキルが含まれています。

共有スキルを使用するには:

1. リポジトリで利用可能なスキルを参照します
1. スキルディレクトリを`.github/skills/`フォルダーにコピーします
1. 必要に応じて`SKILL.md`ファイルをレビューしてカスタマイズします
1. 必要に応じてリソースを変更または追加します

> [!TIP]
> 共有スキルは使用前に必ずレビューし、要件とセキュリティ標準を満たしていることを確認してください。VS Codeの[ターミナルツール](/docs/copilot/chat/chat-tools.md#terminal-commands)は、構成可能な許可リストや、実行されるコードを厳密に制御する機能など、スクリプト実行のコントロールを提供します( [自動承認オプション](/docs/copilot/chat/chat-tools.md#automatically-approve-terminal-commands)を含む)。自動承認機能の[セキュリティ上の考慮事項](/docs/copilot/security.md#automated-approval)について詳しくは、こちらを参照してください。

## Agent Skills標準

Agent Skillsは、異なるAIエージェント間での可搬性を可能にするオープン標準です。VS Codeで作成したスキルは、次を含む複数のエージェントで動作します。

- **VS CodeのGitHub Copilot**: チャットおよびエージェントモードで利用可能
- **GitHub Copilot CLI**: ターミナルで作業するときにアクセス可能
- **GitHub Copilot coding agent**: 自動化されたコーディングタスク中に使用

Agent Skills標準について詳しくは[agentskills.io](https://agentskills.io)を参照してください。

## 関連リソース

* [AI応答のカスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム指示を作成する](/docs/copilot/customization/custom-instructions.md)
* [再利用可能なプロンプトファイルを作成する](/docs/copilot/customization/prompt-files.md)
* [カスタムエージェントを作成する](/docs/copilot/customization/custom-agents.md)
* [Agent Skills仕様](https://agentskills.io)
* [参照スキルリポジトリ](https://github.com/anthropics/skills)
