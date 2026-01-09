---
ContentId: 276ecd8f-2a76-467e-bf82-846d49c13ab5
DateApproved: 12/10/2025
MetaDescription: Learn how to create custom agents (formerly custom chat modes) to tailor AI chat behavior in VS Code for your specific workflows and development scenarios.
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Code のカスタムエージェント

カスタムエージェントを使用すると、特定の開発者の役割やタスクに合わせてパーソナライズされたペルソナを採用するように AI を構成できます。たとえば、セキュリティレビュー担当者、プランナー、ソリューションアーキテクト、またはその他の専門的な役割のためのエージェントを作成できます。各ペルソナは、独自の動作、使用可能なツール、および指示を持つことができます。

また、ハンドオフを使用してエージェント間のガイド付きワークフローを作成し、ワンクリックである専門エージェントから別のエージェントにシームレスに移行できます。たとえば、計画エージェントから実装エージェントに直接移動したり、関連するコンテキストを持ってコードレビュー担当者に引き継いだりできます。

この記事では、VS Code でカスタムエージェントを作成および管理する方法について説明します。

> [!NOTE]
> カスタムエージェントは、VS Code リリース 1.106 以降で使用できます。カスタムエージェントは以前はカスタムチャットモードと呼ばれていました。

## カスタムエージェントとは?

[組み込みエージェント](/docs/copilot/chat/copilot-chat.md#switch-between-agents)は、VS Code のチャットに汎用的な構成を提供します。よりカスタマイズされたチャットエクスペリエンスが必要な場合は、独自のカスタムエージェントを作成できます。

カスタムエージェントは、そのエージェントに切り替えたときに適用される一連の指示とツールで構成されます。たとえば、「Plan (計画)」エージェントには、実装計画を生成するための指示が含まれ、読み取り専用ツールのみを使用する場合があります。カスタムエージェントを作成することで、毎回関連するツールや指示を手動で選択しなくても、その特定の構成にすばやく切り替えることができます。

カスタムエージェントは `.agent.md` マークダウンファイルで定義され、ワークスペースに保存して他のユーザーが使用できるようにしたり、ユーザープロファイルに保存して異なるワークスペース間で再利用したりできます。

カスタムエージェントは[バックグラウンドエージェント](/docs/copilot/agents/background-agents.md)や[クラウドエージェント](/docs/copilot/agents/cloud-agents.md)で再利用できるため、同じ専門的な構成で自律的なタスクを実行できます。

## なぜカスタムエージェントを使用するのか?

タスクによって必要な機能は異なります。計画エージェントは、誤ったコード変更を防ぐために調査と分析のための読み取り専用ツールのみを必要とする場合がありますが、実装エージェントには完全な編集機能が必要です。カスタムエージェントを使用すると、タスクごとに使用可能なツールを正確に指定できるため、AI が作業に適した機能を備えていることが保証されます。

また、カスタムエージェントを使用すると、AI の動作方法を定義する専門的な指示を提供できます。たとえば、計画エージェントは、プロジェクトのコンテキストを収集して詳細な実装計画を生成するように AI に指示する場合がありますが、コードレビューエージェントは、セキュリティの脆弱性を特定し、改善を提案することに重点を置く場合があります。これらの専門的な指示により、そのエージェントに切り替えるたびに、一貫したタスクに適した応答が保証されます。

> [!NOTE]
> サブエージェントはカスタムエージェントで実行できます。詳細については、[カスタムエージェントでのサブエージェントの実行](/docs/copilot/chat/chat-sessions.md#use-a-custom-agent-with-subagents-experimental) (試験機能) を参照してください。

## ハンドオフ

ハンドオフを使用すると、提案された次のステップを使用してエージェント間を移行するガイド付きシーケンシャルワークフローを作成できます。チャットの応答が完了すると、ユーザーが関連するコンテキストと事前に入力されたプロンプトを持って次のエージェントに移動できるハンドオフボタンが表示されます。

ハンドオフは、開発者が次のステップに進む前に各ステップを確認および承認するための制御を提供するマルチステップワークフローを調整する場合に役立ちます。次に例を示します。

* **計画 → 実装**: 計画エージェントで計画を生成し、実装エージェントに引き継いでコーディングを開始します。
* **実装 → レビュー**: 実装を完了してから、コードレビューエージェントに切り替えて品質とセキュリティの問題を確認します。
* **失敗するテストの作成 → 合格するテストの作成**: 大きな実装よりもレビューしやすい失敗するテストを生成し、引き継いで必要なコード変更を実装してそれらのテストに合格させます。

エージェントファイルでハンドオフを定義するには、フロントマターに追加します。各ハンドオフには、ターゲットエージェント、ボタンラベル、および送信するオプションのプロンプトを指定します。

```markdown
---
description: Generate an implementation plan
tools: ['search', 'fetch']
handoffs:
  - label: Start Implementation
    agent: implementation
    prompt: Now implement the plan outlined above.
    send: false
---
```

ユーザーがハンドオフボタンを表示して選択すると、プロンプトが事前に入力された状態でターゲットエージェントに切り替わります。`send: true`の場合、プロンプトは自動的に送信され、次のワークフローステップが開始されます。

## カスタムエージェントファイルの構造

カスタムエージェントファイルはマークダウンファイルであり、`.agent.md`拡張子を使用し、次の構造を持っています。

> [!NOTE]
> VS Code は、ワークスペースの `.github/agents` フォルダーにあるすべての `.md` ファイルをカスタムエージェントとして検出します。

### ヘッダー (オプション)

ヘッダーは YAML フロントマターとしてフォーマットされ、次のフィールドがあります。

| フィールド | 説明 |
| --- | --- |
| `description`     | カスタムエージェントの簡単な説明。チャット入力フィールドにプレースホルダーテキストとして表示されます。 |
| `name`            | カスタムエージェントの名前。指定しない場合、ファイル名が使用されます。 |
| `argument-hint`   | チャット入力フィールドに表示されるオプションのヒントテキストで、カスタムエージェントとの対話方法をユーザーに案内します。 |
| `tools`           | このカスタムエージェントで使用可能なツールまたはツールセット名のリスト。組み込みツール、ツールセット、MCP ツール、または拡張機能によって提供されるツールを含めることができます。MCP サーバーのすべてのツールを含めるには、`<server name>/*` 形式を使用します。<br/>詳細については、[チャットでのツール](/docs/copilot/chat/chat-tools.md)を参照してください。 |
| `model`           | プロンプトを実行するときに使用する AI モデル。指定しない場合、モデルピッカーで現在選択されているモデルが使用されます。 |
| `infer`           | カスタムエージェントを[サブエージェント](/docs/copilot/chat/chat-sessions.md#context-isolated-subagents)として使用できるようにするオプションのブール値フラグ (デフォルトは `true`)。 |
| `target`          | カスタムエージェントのターゲット環境またはコンテキスト (`vscode` または `github-copilot`)。 |
| `mcp-servers`     | [GitHub Copilot のカスタムエージェント](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-custom-agents) (ターゲット: `github-copilot`) で使用する Model Context Protocol (MCP) サーバー構成 json のオプションリスト。 |
| `handoffs`        | カスタムエージェント間を移行するための提案された次のアクションまたはプロンプトのオプションリスト。ハンドオフボタンは、チャット応答が完了した後にインタラクティブな提案として表示されます。 |
| `handoffs.label`  | ハンドオフボタンに表示されるテキスト。 |
| `handoffs.agent`  | 切り替え先のターゲットエージェント識別子。 |
| `handoffs.prompt` | ターゲットエージェントに送信するプロンプトテキスト。 |
| `handoffs.send`   | プロンプトを自動送信するオプションのブール値フラグ (デフォルトは `false`) |

> [!NOTE]
> 指定されたツールがカスタムエージェントを使用するときに使用できない場合、そのツールは無視されます。

### 本文

カスタムエージェントファイルの本文には、マークダウンとしてフォーマットされたカスタムエージェントの実装が含まれます。ここでは、このカスタムエージェントにいるときに AI に従わせたい特定のプロンプト、ガイドライン、またはその他の関連情報を提供します。

マークダウンリンクを使用して他のファイルを参照できます。たとえば、説明ファイルを再利用する場合などです。

本文テキストでエージェントツールを参照するには、`#tool:<tool-name>` 構文を使用します。たとえば、`githubRepo` ツールを参照するには、`#tool:githubRepo` を使用します。

チャットビューでカスタムエージェントを選択すると、カスタムエージェントファイル本文のガイドラインがユーザーのチャットプロンプトの先頭に追加されます。

### カスタムエージェントの例

次のコードスニペットは、実装計画を生成し、コード編集を行わない「Plan (計画)」カスタムエージェントファイルの例を示しています。その他のコミュニティ提供の例については、[Awesome Copilot リポジトリ](https://github.com/github/awesome-copilot/tree/main)を参照してください。

```markdown
---
description: Generate an implementation plan for new features or refactoring existing code.
name: Planner
tools: ['fetch', 'githubRepo', 'search', 'usages']
model: Claude Sonnet 4
handoffs:
  - label: Implement Plan
    agent: agent
    prompt: Implement the plan outlined above.
    send: false
---
# Planning instructions
You are in planning mode. Your task is to generate an implementation plan for a new feature or for refactoring existing code.
Don't make any code edits, just generate a plan.

The plan consists of a Markdown document that describes the implementation plan, including the following sections:

* Overview: A brief description of the feature or refactoring task.
* Requirements: A list of requirements for the feature or refactoring task.
* Implementation Steps: A detailed list of steps to implement the feature or refactoring task.
* Testing: A list of tests that need to be implemented to verify the feature or refactoring task.
```

## カスタムエージェントの作成

カスタムエージェントファイルは、ワークスペースまたはユーザープロファイルに作成できます。

1. エージェントのドロップダウンから **[Configure Custom Agents (カスタムエージェントの構成)]** を選択し、**[Create new custom agent (新しいカスタムエージェントの作成)]** を選択するか、コマンドパレット (`kb(workbench.action.showCommands)`) で **[Chat: New Custom Agent]** コマンドを実行します。

1. カスタムエージェントファイルを作成する場所を選択します。

    * **Workspace (ワークスペース)**: ワークスペースの `.github/agents` フォルダーにカスタムエージェント定義ファイルを作成し、そのワークスペース内でのみ使用します

    * **User profile (ユーザープロファイル)**: [現在のプロファイルフォルダー](/docs/configure/profiles.md)にカスタムエージェント定義ファイルを作成し、すべてのワークスペースで使用します

1. カスタムエージェントのファイル名を入力します。これは、エージェントのドロップダウンに表示されるデフォルトの名前です。

1. 新しく作成された `.agent.md` ファイルにカスタムエージェントの詳細を入力します。

    * ファイルの上部にある YAML フロントマターに入力して、カスタムエージェントの名前、説明、ツール、およびその他の設定を構成します。
    * ファイルの本文にカスタムエージェントの指示を追加します。

カスタムエージェント定義ファイルを更新するには、エージェントのドロップダウンから **[Configure Custom Agents (カスタムエージェントの構成)]** を選択し、リストから変更するカスタムエージェントを選択します。

> [!NOTE]
> 以前にワークスペースの `.github/chatmodes` フォルダーに `.chatmode.md` 拡張子を持つカスタムチャットモードを作成した場合でも、VS Code はそれらのファイルをカスタムエージェントとして認識します。クイックフィックスアクションを使用して、名前を変更し、`.agent.md` 拡張子を持つ新しい `.github/agents` フォルダーに移動できます。

## エージェントのドロップダウンリストのカスタマイズ

複数のカスタムエージェントがある場合は、エージェントのドロップダウンに表示するエージェントをカスタマイズできます。特定のカスタムエージェントを表示または非表示にするには:

1. エージェントのドロップダウンから **[Configure Custom Agents (カスタムエージェントの構成)]** を選択します。

1. リスト内のカスタムエージェントにカーソルを合わせ、目のアイコンを選択して、エージェントのドロップダウンから表示または非表示にします。

## ツールリストの優先順位

`tools` メタデータフィールドを使用して、カスタムエージェントとプロンプトファイルの両方で使用可能なツールのリストを指定できます。プロンプトファイルは、`agent` メタデータフィールドを使用してカスタムエージェントを参照することもできます。

チャットで使用可能なツールのリストは、次の優先順で決定されます。

1. プロンプトファイルで指定されたツール (ある場合)
2. プロンプトファイルで参照されているカスタムエージェントのツール (ある場合)
3. 選択したエージェントのデフォルトツール (ある場合)

## チーム間でのカスタムエージェントの共有 (試験機能)

チーム全体でカスタムエージェントを共有するには、ワークスペースレベルのカスタムエージェント (`.github/agents` フォルダー) を作成できます。組織内の複数のワークスペースでカスタムエージェントを共有する場合は、GitHub 組織レベルで定義できます。

VS Code は、アカウントがアクセスできる組織レベルで定義されたカスタムエージェントを自動的に検出します。これらのエージェントは、チャットのエージェントドロップダウンに、組み込みエージェント、および個人用およびワークスペースのカスタムエージェントと一緒に表示されます。

組織レベルのカスタムエージェントの検出を有効にするには、`setting(github.copilot.chat.customAgents.showOrganizationAndEnterpriseAgents)` を `true` に設定します。

GitHub ドキュメントで、[組織向けのカスタムエージェントの作成](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-custom-agents)方法について詳しく学習してください。

## よくある質問

### カスタムエージェントはチャットモードと異なりますか?

カスタムエージェントは以前はカスタムチャットモードと呼ばれていました。機能は同じですが、特定のタスクに合わせて AI の動作をカスタマイズするという目的をより適切に反映するように用語が更新されました。

VS Code は、既存の `.chatmode.md` ファイルをカスタムエージェントとして認識します。クイックフィックスアクションを使用して、名前を変更し、`.agent.md` 拡張子を持つ新しい `.github/agents` フォルダーに移動できます。

## 関連リソース

* [カスタム指示による AI のカスタマイズ](/docs/copilot/customization/custom-instructions.md)
* [再利用可能なプロンプトファイルの作成](/docs/copilot/customization/prompt-files.md)
* [チャットでのツールの使用](/docs/copilot/chat/chat-tools.md)
