---
ContentId: a7d3e5f8-2c4b-4d9a-b8e1-3f6c9a2d7e41
DateApproved: 12/17/2025
MetaDescription: VS CodeでAgent Skillsを使用して、VS Code、GitHub Copilot CLI、GitHub Copilot coding agent全体で機能する専門的な機能をGitHub Copilotに教える方法について学習します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでAgent Skillsを使用する

Agent Skillsは、GitHub Copilotが専門的なタスクを実行するために関連する場合に読み込むことができる指示、スクリプト、およびリソースのフォルダーです。Agent Skillsは、VS CodeのGitHub Copilot、GitHub Copilot CLI、GitHub Copilot coding agentなど、複数のAIエージェント間で機能する[オープンスタンダード](https://agentskills.io)です。

主にコーディングガイドラインを定義する[カスタム指示](/docs/copilot/customization/custom-instructions.md)とは異なり、スキルは、スクリプト、例、その他のリソースを含めることができる専門的な機能とワークフローを可能にします。作成したスキルは移植性があり、スキル互換のあるすべてのエージェントで機能します。

Agent Skillsの主な利点:

- **Copilotの専門化**: コンテキストを繰り返すことなく、ドメイン固有のタスクに合わせて機能を調整します
- **繰り返しの削減**: 一度作成すれば、すべての会話で自動的に使用できます
- **機能の構成**: 複数のスキルを組み合わせて複雑なワークフローを構築します
- **効率的な読み込み**: 必要な場合にのみ、関連コンテンツがコンテキストに読み込まれます

> [!NOTE]
> VS CodeでのAgent Skillsのサポートは現在プレビュー段階であり、[VS Code Insiders](https://code.visualstudio.com/insiders/)でのみ利用可能です。Agent Skillsを使用するには、`setting(chat.useAgentSkills)`設定を有効にします。

## Agent Skillsとカスタム指示

Agent Skillsとカスタム指示はどちらもCopilotの動作をカスタマイズするのに役立ちますが、それぞれ異なる目的を果たします:

| 機能 | Agent Skills | カスタム指示 |
|---------|-------------|---------------------|
| **目的** | 専門的な機能とワークフローを教える | コーディング標準とガイドラインを定義する |
| **移植性** | VS Code、Copilot CLI、Copilot coding agent全体で機能 | VS CodeとGitHub.comのみ |
| **コンテンツ** | 指示、スクリプト、例、およびリソース | 指示のみ |
| **スコープ** | タスク固有、オンデマンドで読み込み | 常に適用 (またはglobパターン経由) |
| **標準** | オープンスタンダード ([agentskills.io](https://agentskills.io)) | VS Code固有 |

以下の場合にAgent Skillsを使用します:
- 異なるAIツール間で機能する再利用可能な機能を作成する
- 指示と一緒にスクリプト、例、またはその他のリソースを含める
- 機能をより広いAIコミュニティと共有する
- テスト、デバッグ、またはデプロイプロセスのような専門的なワークフローを定義する

以下の場合にカスタム指示を使用します:
- プロジェクト固有のコーディング標準を定義する
- 言語またはフレームワークの規則を設定する
- コードレビューまたはコミットメッセージのガイドラインを指定する
- globパターンを使用してファイルの種類に基づいたルールを適用する

## スキルの作成

スキルは、スキルの動作を定義する`SKILL.md`ファイルを含むディレクトリに保存されます。VS Codeは2つの場所でスキルをサポートしています:

* `.github/skills/` - Copilotで使用されるすべての新しいスキルに推奨される共有場所
* `.claude/skills/` - 下位互換性のためにサポートされているレガシーな場所

スキルを作成するには:

1. ワークスペースに`.github/skills`ディレクトリを作成します。

1. スキル用のサブディレクトリを作成します。各スキルには独自のディレクトリが必要です (例: `.github/skills/webapp-testing`)。

1. スキルディレクトリに以下の構造で`SKILL.md`ファイルを作成します:

    ```markdown
    ---
    name: skill-name
    description: スキルが何をするか、いつ使用するかの説明
    ---

    # スキルの指示

    詳細な指示、ガイドライン、および例をここに記述します...
    ```

1. オプションで、スクリプト、例、またはその他のリソースをスキルディレクトリに追加します。

    たとえば、ウェブアプリケーションをテストするためのスキルには以下が含まれる場合があります:
    - `SKILL.md` - テストを実行するための指示
    - `test-template.js` - テンプレートテストファイル
    - `examples/` - テストシナリオの例

### SKILL.mdファイル形式

`SKILL.md`ファイルは、スキルのメタデータと動作を定義するYAMLフロントマターを持つMarkdownファイルです。

#### ヘッダー (必須)

ヘッダーは、以下のフィールドを持つYAMLフロントマターとしてフォーマットされます:

| フィールド | 必須 | 説明 |
|-------|----------|-------------|
| `name` | はい | スキルの一意の識別子。小文字で、スペースにはハイフンを使用する必要があります (例: `webapp-testing`)。最大64文字。 |
| `description` | はい | スキルが何をするか、**いつ使用するか**の説明。Copilotがいつスキルを読み込むかを決定するのに役立つように、機能とユースケースの両方について具体的である必要があります。最大1024文字。 |

#### 本文

スキルの本文には、このスキルを使用する際にCopilotが従うべき指示、ガイドライン、および例が含まれています。以下を説明する明確で具体的な指示を記述してください:

- スキルが達成するのに役立つこと
- スキルをいつ使用するか
- 従うべき段階的な手順
- 想定される入力と出力の例
- 含まれているスクリプトまたはリソースへの参照

相対パスを使用して、スキルディレクトリ内のファイルを参照できます。たとえば、スキルディレクトリ内のスクリプトを参照するには、`[test script](./test-template.js)`を使用します。

## スキルの例

以下の例は、作成できるさまざまな種類のスキルを示しています。

<details>
<summary>例: ウェブアプリケーションテストスキル</summary>

````markdown
---
name: webapp-testing
description: Playwrightを使用したウェブアプリケーションのテストガイド。ブラウザーベースのテストを作成または実行するように求められた場合にこれを使用します。
---

# Playwrightを使用したウェブアプリケーションテスト

このスキルは、Playwrightを使用してウェブアプリケーションのブラウザーベースのテストを作成および実行するのに役立ちます。

## このスキルを使用する場合

以下の場合にこのスキルを使用します:
- ウェブアプリケーション用の新しいPlaywrightテストを作成する
- 失敗したブラウザーテストをデバッグする
- 新しいプロジェクトのテストインフラストラクチャをセットアップする

## テストの作成

1. 標準的なテスト構造について[テストテンプレート](./test-template.js)を確認します
2. テストするユーザーフローを特定します
3. `tests/`ディレクトリに新しいテストファイルを作成します
4. Playwrightのロケーターを使用して要素を見つけます (ロールベースのセレクターを推奨)
5. 期待される動作を確認するためのアサーションを追加します

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

- 動的コンテンツにはdata-testid属性を使用する
- テストは独立してアトミックに保つ
- 複雑なページにはPage Object Modelを使用する
- 失敗時にスクリーンショットを撮る
````

</details>

<details>
<summary>例: GitHub Actionsデバッグスキル</summary>

````markdown
---
name: github-actions-debugging
description: 失敗したGitHub Actionsワークフローをデバッグするためのガイド。失敗したGitHub Actionsワークフローをデバッグするように求められた場合にこれを使用します。
---

# GitHub Actionsのデバッグ

このスキルは、プルリクエストで失敗したGitHub Actionsワークフローをデバッグするのに役立ちます。

## プロセス

1. `list_workflow_runs`ツールを使用して、プルリクエストの最近のワークフロー実行とそのステータスを検索します
2. `summarize_job_log_failures`ツールを使用して、失敗したジョブのログのAIサマリーを取得します
3. 詳細情報が必要な場合は、`get_job_logs`または`get_workflow_run_logs`ツールを使用して、完全な失敗ログを取得します
4. 環境でローカルに失敗を再現してみます
5. 失敗したビルドを修正し、変更をコミットする前に修正を確認します

## 一般的な問題

- **環境変数の欠落**: 必要なすべてのシークレットが構成されていることを確認します
- **バージョンの不一致**: アクションのバージョンと依存関係に互換性があることを確認します
- **権限の問題**: ワークフローに必要な権限があることを確認します
- **タイムアウトの問題**: 実行時間の長いジョブを分割するか、タイムアウト値を増やすことを検討します
````

</details>

## Copilotがスキルを使用する方法

スキルは段階的開示を使用して、必要な場合にのみコンテンツを効率的に読み込みます。この3段階の読み込みシステムにより、コンテキストを消費することなく多くのスキルをインストールできます:

**レベル1: スキルの発見**

Copilotは、YAMLフロントマターから`name`と`description`を読み取ることで、利用可能なスキルを常に把握しています。このメタデータは軽量であり、Copilotがリクエストに関連するスキルを決定するのに役立ちます。

**レベル2: 指示の読み込み**

リクエストがスキルの説明と一致すると、Copilotは`SKILL.md`ファイルの本文をコンテキストに読み込みます。その時点で初めて、詳細な指示が利用可能になります。

**レベル3: リソースへのアクセス**

Copilotは、必要な場合にのみ、スキルディレクトリ内の追加ファイル (スクリプト、例、ドキュメント) にアクセスできます。これらのリソースは、Copilotが参照するまで読み込まれないため、コンテキストが効率的になります。

このアーキテクチャは、プロンプトに基づいてスキルが自動的にアクティブ化されることを意味します。手動で選択する必要はありません。多くのスキルをインストールしても、Copilotは各タスクに関連するものだけを読み込みます。

## 共有スキルの使用

他のユーザーが作成したスキルを使用して、Copilotの機能を強化できます。[github/awesome-copilot](https://github.com/github/awesome-copilot)リポジトリには、スキル、カスタムエージェント、指示、およびプロンプトの成長するコミュニティコレクションが含まれています。[anthropics/skills](https://github.com/anthropics/skills)リポジトリには、追加の参照スキルが含まれています。

共有スキルを使用するには:

1. リポジトリ内の利用可能なスキルを参照します
1. スキルディレクトリを`.github/skills/`フォルダーにコピーします
1. 必要に応じて`SKILL.md`ファイルを確認してカスタマイズします
1. オプションで、必要に応じてリソースを変更または追加します

> [!TIP]
> 共有スキルを使用する前に必ず確認し、要件とセキュリティ基準を満たしていることを確認してください。VS Codeの[ターミナルツール](/docs/copilot/chat/chat-tools.md#terminal-commands)は、構成可能な許可リストと、実行されるコードに対する厳密な制御を備えた[自動承認オプション](/docs/copilot/chat/chat-tools.md#automatically-approve-terminal-commands)を含む、スクリプト実行の制御を提供します。自動承認機能の[セキュリティに関する考慮事項](/docs/copilot/security.md#automated-approval)について詳しくは、こちらをご覧ください。

## Agent Skills標準

Agent Skillsは、異なるAIエージェント間での移植性を可能にするオープンスタンダードです。VS Codeで作成したスキルは、以下を含む複数のエージェントで機能します:

- **VS CodeのGitHub Copilot**: チャットモードとエージェントモードで利用可能
- **GitHub Copilot CLI**: ターミナルでの作業中にアクセス可能
- **GitHub Copilot coding agent**: 自動コーディングタスク中に使用

Agent Skills標準の詳細については、[agentskills.io](https://agentskills.io)をご覧ください。

## 関連リソース

* [AI応答のカスタマイズの概要](/docs/copilot/customization/overview.md)
* [カスタム指示の作成](/docs/copilot/customization/custom-instructions.md)
* [再利用可能なプロンプトファイルの作成](/docs/copilot/customization/prompt-files.md)
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)
* [Agent Skills仕様](https://agentskills.io)
* [参照スキルリポジトリ](https://github.com/anthropics/skills)
