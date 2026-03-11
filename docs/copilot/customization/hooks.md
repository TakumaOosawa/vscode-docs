---
ContentId: 9c4d5e6f-7a8b-9c0d-1e2f-3a4b5c6d7e8f
DateApproved: 3/9/2026
MetaDescription: VS Codeでエージェントセッション中のキーライフサイクルポイントで、カスタムシェルコマンドを実行するためのフックの使用方法を学びます。自動化、検証、ポリシー実行に対応しています。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- copilot
- ai
- agents
- hooks
- automation
- lifecycle
- preToolUse
- postToolUse
---

# Visual Studio Codeのエージェントフック (プレビュー)

フックを使用すると、エージェントセッション中のキーライフサイクルポイントでカスタムシェルコマンドを実行できます。ワークフローの自動化、セキュリティポリシーの実施、操作の検証、外部ツールとの統合にフックを使用します。

フックがAIカスタマイズフレームワークにどのように適合するかについて、[カスタマイズの概念](/docs/copilot/concepts/customization.md#hooks)を参照してください。

この記事では、VS Codeでフックを構成および使用する方法を説明します。

> [!NOTE]
> エージェントフックは現在プレビュー段階です。構成形式と動作は、今後のリリースで変更される可能性があります。

> [!IMPORTANT]
> 組織がVS Codeでのフックの使用を無効にしている可能性があります。詳細については、管理者に問い合わせてください。詳細は[エンタープライズポリシー](/docs/enterprise/policies.md)を参照してください。

> [!TIP]
> [チャットカスタマイズエディター](/docs/copilot/customization/overview.md#chat-customizations-editor)(プレビュー)を使用して、すべてのチャットカスタマイズを1か所で発見、作成、管理できます。コマンドパレットから**Chat: Open Chat Customizations**を実行します。

フックは、ローカルエージェント、バックグラウンドエージェント、クラウドエージェントなど、さまざまなエージェントタイプで動作するように設計されています。各フックは構造化されたJSON入力を受け取り、JSON出力を返してエージェントの動作に影響を与えることができます。

## なぜフックを使用するのか?

フックは確定的なコード駆動型の自動化を提供します。エージェントの動作をガイドするための指示やカスタムプロンプトとは異なり、フックは特定のライフサイクルポイントでコードを実行し、保証された結果を得られます:

* **セキュリティポリシーの実施**: `rm -rf`や`DROP TABLE`などの危険なコマンドを、エージェントのプロンプト方法に関わらず実行前にブロックします。

* **コード品質の自動化**: ファイルの変更後、自動的にフォーマッター、リンター、テストを実行します。

* **監査証跡の作成**: すべてのツール呼び出し、コマンド実行、またはファイル変更をログに記録して、コンプライアンスとデバッグに対応します。

* **コンテキストの挿入**: プロジェクト固有の情報、APIキー、または環境の詳細を追加して、エージェントがより良い決定を下すのを支援します。

* **承認の制御**: 安全な操作を自動的に承認し、機密操作の確認を要求します。

## クイックスタート: 最初のフック

次の例は、ファイル編集後にPrettierを実行するフックを作成します。ワークスペースに`.github/hooks/format.json`ファイルを作成します:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
      }
    ]
  }
}
```

このファイルを保存した後、VS Codeは自動的にフックを読み込みます。次回エージェントがファイルを編集する時、Prettierが変更されたファイルで実行されます。**GitHub Copilot Chat Hooks**出力チャネルを確認して、フックが実行されたことを確認してください。

カスタムスクリプトを使用するより複雑なフックについては、[使用シナリオ](#使用シナリオ)を参照してください。

## フックライフサイクルイベント

VS Codeは、エージェントセッション中の特定のポイントで発火する8つのフックイベントをサポートしています:

| フックイベント | 発火時期 | 一般的なユースケース |
|------------|---------------|------------------|
| `SessionStart` | ユーザーが新しいセッションの最初のプロンプトを送信した時 | リソースの初期化、セッション開始ログ、プロジェクト状態の検証 |
| `UserPromptSubmit` | ユーザーがプロンプトを送信した時 | ユーザーリクエストの監査、システムコンテキストの挿入 |
| `PreToolUse` | エージェントがツールを呼び出す前 | 危険な操作のブロック、承認の要求、ツール入力の変更 |
| `PostToolUse` | ツールが正常に完了した後 | フォーマッターの実行、結果のログ、フォローアップアクションの実行 |
| `PreCompact` | 会話コンテキストが圧縮される前 | 重要なコンテキストのエクスポート、切り詰め前の状態保存 |
| `SubagentStart` | サブエージェントが生成された時 | ネストされたエージェント使用の追跡、サブエージェントリソースの初期化 |
| `SubagentStop` | サブエージェントが完了した時 | 結果の集約、サブエージェントリソースのクリーンアップ |
| `Stop` | エージェントセッション終了時 | レポートの生成、リソースのクリーンアップ、通知の送信 |

## フックの構成

フックはワークスペースまたはユーザーディレクトリに保存されたJSONファイルで構成されます。

### フックファイルの場所

VS Codeは、これらの場所でフック構成ファイルを検索します:

| スコープ | デフォルトファイル場所 |
|-------|-----------------------|
| ワークスペース | `.github/hooks/*.json` |
| ワークスペース (Claude形式) | `.claude/settings.json`, `.claude/settings.local.json` |
| ユーザー | `~/.claude/settings.json` |
| カスタムエージェント | `.agent.md`フロントマターの`hooks`フィールド([エージェントスコープのフック](#エージェントスコープのフック)を参照) |

同じイベントタイプの場合、ワークスペースフックはユーザーフックより優先されます。

`setting(chat.hookFilesLocations)`設定を使用して、どのフックファイルを読み込むかをカスタマイズします。フォルダへのパスを指定できます(VS Codeはフォルダ内のすべての`*.json`ファイルを読み込みます)。または、個別の`.json`ファイルへの直接パスを指定できます。相対パスとチルダ(`~`)パスのみがサポートされています。

デフォルト値には、これらの場所が含まれます:

```json
"chat.hookFilesLocations": {
  ".github/hooks": true,
  ".claude/settings.local.json": true,
  ".claude/settings.json": true,
  "~/.claude/settings.json": true
}
```

カスタム場所を追加するには、この設定にエントリを追加します:

```json
"chat.hookFilesLocations": {
  "custom/hooks": true,
  "~/my-hooks/security.json": true
}
```

パスを`false`に設定して、デフォルト場所を含む、その場所からフックの読み込みを無効にします。たとえば、Claude Code構成ファイルからのフック読み込みを停止するには:

```json
"chat.hookFilesLocations": {
  ".claude/settings.json": false,
  ".claude/settings.local.json": false,
  "~/.claude/settings.json": false
}
```

### エージェントスコープのフック

> [!NOTE]
> エージェントスコープのフックは現在プレビュー段階です。

[カスタムエージェント](/docs/copilot/customization/custom-agents.md)のYAMLフロントマターで直接フックを定義できます。エージェントスコープのフックは、そのカスタムエージェントがアクティブな場合(ユーザーによって選択されるか、サブエージェントとして呼び出される)のみ実行されます。エージェントスコープのフックは、同じイベント用に構成されたワークスペースまたはユーザーレベルのフックに加えて実行されます。

エージェントスコープのフックを有効にするには、`setting(chat.useCustomAgentHooks)`を`true`に設定します。

エージェントフロントマターに`hooks`フィールドを追加し、フック構成ファイルと同じ構造を使用します: イベント名はフックコマンドオブジェクトの配列にマップされます。

```markdown
---
name: "Strict Formatter"
description: "Agent that auto-formats code after every edit"
hooks:
  PostToolUse:
    - type: command
      command: "./scripts/format-changed-files.sh"
---

You are a code editing agent. After making changes, files are automatically formatted.
```

### フック構成形式

各イベントタイプのフックコマンド配列を含む`hooks`オブジェクトを含むJSONファイルを作成します。VS Codeは、Claude CodeおよびCopilot CLIと互換性を持つ同じフック形式を使用します:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/validate-tool.sh",
        "timeout": 15
      }
    ],
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
      }
    ]
  }
}
```

### フックコマンドプロパティ

各フックエントリは`type: "command"`および少なくとも1つのコマンドプロパティを持つ必要があります:

| プロパティ | タイプ | 説明 |
|----------|------|-------------|
| `type` | 文字列 | `"command"`である必要があります |
| `command` | 文字列 | デフォルトコマンド(クロスプラットフォーム) |
| `windows` | 文字列 | Windows固有のコマンド上書き |
| `linux` | 文字列 | Linux固有のコマンド上書き |
| `osx` | 文字列 | macOS固有のコマンド上書き |
| `cwd` | 文字列 | 作業ディレクトリ(リポジトリルートに対する相対パス) |
| `env` | オブジェクト | 追加の環境変数 |
| `timeout` | 数値 | タイムアウト(秒)(デフォルト: 30) |

> [!NOTE]
> OS固有のコマンドは、拡張機能ホストプラットフォームに基づいて選択されます。リモート開発シナリオ(SSH、Containers、WSL)の場合、これはローカルオペレーティングシステムと異なる可能性があります。

### OS固有のコマンド

各オペレーティングシステムに異なるコマンドを指定します:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "./scripts/format.sh",
        "windows": "powershell -File scripts\\format.ps1",
        "linux": "./scripts/format-linux.sh",
        "osx": "./scripts/format-mac.sh"
      }
    ]
  }
}
```

実行サービスはOSに基づいて適切なコマンドを選択します。OS固有のコマンドが定義されていない場合、`command`プロパティにフォールバックされます。

## フック入出力

フックは、JSON を使用してstdin(入力)およびstdout(出力)経由でVS Codeと通信します。

### 共通入力フィールド

すべてのフックは、これらの共通フィールドを含むJSONオブジェクトをstdin経由で受け取ります:

```json
{
  "timestamp": "2026-02-09T10:30:00.000Z",
  "cwd": "/path/to/workspace",
  "sessionId": "session-identifier",
  "hookEventName": "PreToolUse",
  "transcript_path": "/path/to/transcript.json"
}
```

### 共通出力形式

フックはstdout経由でJSONを返して、エージェントの動作に影響を与えることができます。すべてのフックは、これらの出力フィールドをサポートしています:

```json
{
  "continue": true,
  "stopReason": "Security policy violation",
  "systemMessage": "Unit tests failed"
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `continue` | ブール値 | 処理を停止するには`false`に設定します(デフォルト: `true`) |
| `stopReason` | 文字列 | `continue`が`false`の場合、停止の理由(ユーザーに表示) |
| `systemMessage` | 文字列 | ユーザーに表示される警告メッセージ |

### 終了コード

フックの終了コードは、VS Codeが結果をどのように処理するかを決定します:

| 終了コード | 動作 |
|-----------|----------|
| `0` | 成功: stdoutをJSONとして解析 |
| `2` | ブロッキングエラー: 処理を停止し、エラーをモデルに表示 |
| その他 | ブロッキング以外の警告: 警告ユーザーに表示、処理を続行 |

### データ返却方法の選択

フックは、エージェントの動作を制御するためのいくつかの方法があります: 終了コード、トップレベル出力フィールド(`continue`、`stopReason`)、およびフック固有の出力フィールド(`hookSpecificOutput`)。これらを以下のように組み合わせて使用​​します:

* **終了コード2**は、操作をブロックする最も簡単な方法です。フックのstderrはモデルへのコンテキストとして表示されます。JSON出力は必要ありません。
* **JSON出力の`continue: false`**はエージェントセッション全体を停止します。停止理由を`stopReason`で伝えてください。これは単一のツール呼び出しのブロッキングより大幅です。
* **`hookSpecificOutput`**は、各フックイベントに固有の詳細制御を提供します。たとえば、`PreToolUse`フックは`permissionDecision`を使用して、セッション全体を停止せずに単一のツール呼び出しを許可、拒否、またはプロンプトを実行します。
* **`systemMessage`**は、他の決定に関わらず、チャットに警告をユーザーに表示します。

複数の制御メカニズムを一緒に使用する場合、最も制限的なものが優先されます。たとえば、フックが`continue: false`と`permissionDecision: "allow"`を返す場合、セッションは依然として停止します。

## PreToolUse

`PreToolUse`フックはエージェントがツールを呼び出す前に発火します。

### PreToolUse入力

共通フィールドに加えて、`PreToolUse`フックは以下を受け取ります:

```json
{
  "tool_name": "editFiles",
  "tool_input": { "files": ["src/main.ts"] },
  "tool_use_id": "tool-123"
}
```

### PreToolUse出力

`PreToolUse`フックは、`hookSpecificOutput`オブジェクトを通じてツール実行を制御できます:

```json
{
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "permissionDecision": "deny",
    "permissionDecisionReason": "Destructive command blocked by policy",
    "updatedInput": { "files": ["src/safe.ts"] },
    "additionalContext": "User has read-only access to production files"
  }
}
```

| フィールド | 値 | 説明 |
|-------|--------|-------------|
| `permissionDecision` | `"allow"`, `"deny"`, `"ask"` | ツール承認の制御 |
| `permissionDecisionReason` | 文字列 | ユーザーに表示される理由 |
| `updatedInput` | オブジェクト | 変更されたツール入力(オプション) |
| `additionalContext` | 文字列 | モデル用の追加コンテキスト |

**許可決定の優先度**: 同じツール呼び出しに対して複数のフックが実行される場合、最も制限的な決定が優先されます:

1. `deny`(最も制限的): ツール実行をブロック
2. `ask`: ユーザー確認が必要
3. `allow`(最も制限的でない): 実行を自動承認

**`updatedInput`形式**: `updatedInput`の形式を確認するには、[エージェントログ](/docs/copilot/chat/chat-debug-view.md#agent-debug-panel)を開き、ログされたツールスキーマを探します。`updatedInput`が予期されるスキーマと一致しない場合、それは無視されます。

## PostToolUse

`PostToolUse`フックはツールが正常に完了した後に発火します。

### PostToolUse入力

共通フィールドに加えて、`PostToolUse`フックは以下を受け取ります:

```json
{
  "tool_name": "editFiles",
  "tool_input": { "files": ["src/main.ts"] },
  "tool_use_id": "tool-123",
  "tool_response": "File edited successfully"
}
```

### PostToolUse出力

`PostToolUse`フックはモデルに追加コンテキストを提供するか、さらなる処理をブロックできます:

```json
{
  "decision": "block",
  "reason": "Post-processing validation failed",
  "hookSpecificOutput": {
    "hookEventName": "PostToolUse",
    "additionalContext": "The edited file has lint errors that need to be fixed"
  }
}
```

| フィールド | 値 | 説明 |
|-------|--------|-------------|
| `decision` | `"block"` | さらなる処理をブロック(オプション) |
| `reason` | 文字列 | ブロック理由(モデルに表示) |
| `hookSpecificOutput.additionalContext` | 文字列 | 会話に挿入された追加コンテキスト |

## UserPromptSubmit

`UserPromptSubmit`フックはユーザーがプロンプトを送信した時に発火します。

### UserPromptSubmit入力

共通フィールドに加えて、`UserPromptSubmit`フックはユーザーが送信したテキストを含む`prompt`フィールドを受け取ります。

`UserPromptSubmit`フックは共通出力形式のみを使用します。

## SessionStart

`SessionStart`フックは新しいエージェントセッションが開始された時に発火します。

### SessionStart入力

共通フィールドに加えて、`SessionStart`フックは以下を受け取ります:

```json
{
  "source": "new"
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `source` | 文字列 | セッションが開始された方法。現在は常に`"new"`です。 |

### SessionStart出力

`SessionStart`フックはエージェントの会話に追加コンテキストを挿入できます:

```json
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Project: my-app v2.1.0 | Branch: main | Node: v20.11.0"
  }
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `additionalContext` | 文字列 | エージェントの会話に追加されたコンテキスト |

## Stop

`Stop`フックはエージェントセッションが終了した時に発火します。カスタムエージェントにスコープされている場合、`Stop`フックは`SubagentStop`としても扱われます。

### Stop入力

共通フィールドに加えて、`Stop`フックは以下を受け取ります:

```json
{
  "stop_hook_active": false
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `stop_hook_active` | ブール値 | 前のstopフックの結果としてエージェントがすでに続行されている時、`true`です。値をチェックして、エージェントが無限に実行されるのを防いでください。 |

### Stop出力

`Stop`フックはエージェントが停止するのを防ぐことができます:

```json
{
  "hookSpecificOutput": {
    "hookEventName": "Stop",
    "decision": "block",
    "reason": "Run the test suite before finishing"
  }
}
```

| フィールド | 値 | 説明 |
|-------|--------|-------------|
| `decision` | `"block"` | エージェントが停止されるのを防ぐ |
| `reason` | 文字列 | `decision`が`"block"`の場合は必須。エージェントが継続すべき理由を指示します。 |

> [!IMPORTANT]
> `Stop`フックがエージェントの停止をブロックする場合、エージェントは実行を継続し、追加のターンが[プレミアムリクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests)を消費します。エージェントが無限に実行されるのを防ぐために、常に`stop_hook_active`フィールドをチェックしてください。

## SubagentStart

`SubagentStart`フックはサブエージェントが生成された時に発火します。

### SubagentStart入力

共通フィールドに加えて、`SubagentStart`フックは以下を受け取ります:

```json
{
  "agent_id": "subagent-456",
  "agent_type": "Plan"
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `agent_id` | 文字列 | サブエージェントの一意識別子 |
| `agent_type` | 文字列 | エージェント名(たとえば、組み込みエージェント用の`"Plan"`またはカスタムエージェント名) |

### SubagentStart出力

`SubagentStart`フックはサブエージェントの会話に追加コンテキストを挿入できます:

```json
{
  "hookSpecificOutput": {
    "hookEventName": "SubagentStart",
    "additionalContext": "This subagent should follow the project coding guidelines"
  }
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `additionalContext` | 文字列 | サブエージェントの会話に追加されたコンテキスト |

## SubagentStop

`SubagentStop`フックはサブエージェントが完了した時に発火します。

### SubagentStop入力

共通フィールドに加えて、`SubagentStop`フックは以下を受け取ります:

```json
{
  "agent_id": "subagent-456",
  "agent_type": "Plan",
  "stop_hook_active": false
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `agent_id` | 文字列 | サブエージェントの一意識別子 |
| `agent_type` | 文字列 | エージェント名(たとえば、組み込みエージェント用の`"Plan"`またはカスタムエージェント名) |
| `stop_hook_active` | ブール値 | 前のstopフックの結果としてサブエージェントがすでに続行されている時、`true`です。値をチェックして、サブエージェントが無限に実行されるのを防いでください。 |

### SubagentStop出力

`SubagentStop`フックはサブエージェントが停止されるのを防ぐことができます:

```json
{
  "decision": "block",
  "reason": "Verify subagent results before completing"
}
```

| フィールド | 値 | 説明 |
|-------|--------|-------------|
| `decision` | `"block"` | サブエージェントが停止されるのを防ぐ |
| `reason` | 文字列 | `decision`が`"block"`の場合は必須。サブエージェントが継続すべき理由を指示します。 |

## PreCompact

`PreCompact`フックは会話コンテキストが圧縮される前に発火します。

### PreCompact入力

共通フィールドに加えて、`PreCompact`フックは以下を受け取ります:

```json
{
  "trigger": "auto"
}
```

| フィールド | タイプ | 説明 |
|-------|------|-------------|
| `trigger` | 文字列 | 圧縮がトリガーされた方法。会話がプロンプト予算に対して長い場合は`"auto"`です。 |

`PreCompact`フックは共通出力形式のみを使用します。

## UIでフックを構成する

いくつかの方法でUIを通じてフックを構成できます:

* チャット入力に「`/hooks`」と入力し、`kbstyle(Enter)`を押します。
* コマンドパレット(`kb(workbench.action.showCommands)`)を開いて、**Chat: Configure Hooks**を実行します。
* チャットビューの上部にある**設定**アイコン(<i class="codicon codicon-gear"></i>)を選択し、**Hooks**を選択します。

フック構成メニューで:

1. リストからフックイベントタイプを選択します。

1. 既存のフックを選択して編集するか、**Add new hook**を選択して新しいフックを作成します。

1. フック構成ファイルを選択または作成します。

コマンドはフックファイルをエディターで開き、カーソルをコマンドフィールドに配置し、編集できます。

### AIでフックを生成する

AIを使用してフック構成を生成できます。チャットに「`/create-hook`」と入力し、必要な自動化を説明します(たとえば、「すべてのファイル編集後にESLintを実行する」)。エージェントが明確な質問をしてから、適切なイベントタイプ、コマンド、設定を含むフック構成ファイルを生成します。

## 使用シナリオ

次の例は、一般的なフックパターンを示しています。

<details>
<summary>危険なターミナルコマンドをブロック</summary>

破壊的なコマンドを防ぐ`PreToolUse`フックを作成します:

**.github/hooks/security.json**:
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/block-dangerous.sh",
        "timeoutSec": 5
      }
    ]
  }
}
```

**scripts/block-dangerous.sh**:
```bash
#!/bin/bash
INPUT=$(cat)
TOOL_NAME=$(echo "$INPUT" | jq -r '.tool_name')
TOOL_INPUT=$(echo "$INPUT" | jq -r '.tool_input')

if [ "$TOOL_NAME" = "runTerminalCommand" ]; then
  COMMAND=$(echo "$TOOL_INPUT" | jq -r '.command // empty')

  if echo "$COMMAND" | grep -qE '(rm\s+-rf|DROP\s+TABLE|DELETE\s+FROM)'; then
    echo '{"hookSpecificOutput":{"permissionDecision":"deny","permissionDecisionReason":"Destructive command blocked by security policy"}}'
    exit 0
  fi
fi

echo '{"continue":true}'
```

</details>

<details>
<summary>編集後のコード自動フォーマット</summary>

ファイル変更後にPrettierを自動的に実行します:

**.github/hooks/formatting.json**:
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "./scripts/format-changed-files.sh",
        "windows": "powershell -File scripts\\format-changed-files.ps1",
        "timeout": 30
      }
    ]
  }
}
```

**scripts/format-changed-files.sh**:
```bash
#!/bin/bash
INPUT=$(cat)
TOOL_NAME=$(echo "$INPUT" | jq -r '.tool_name')

if [ "$TOOL_NAME" = "editFiles" ] || [ "$TOOL_NAME" = "createFile" ]; then
  FILES=$(echo "$INPUT" | jq -r '.tool_input.files[]? // .tool_input.path // empty')

  for FILE in $FILES; do
    if [ -f "$FILE" ]; then
      npx prettier --write "$FILE" 2>/dev/null
    fi
  done
fi

echo '{"continue":true}'
```

</details>

<details>
<summary>監査ログで使用ツール</summary>

すべてのツール呼び出しの監査証跡を作成します:

**.github/hooks/audit.json**:
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/log-tool-use.sh",
        "env": {
          "AUDIT_LOG": ".github/hooks/audit.log"
        }
      }
    ]
  }
}
```

**scripts/log-tool-use.sh**:
```bash
#!/bin/bash
INPUT=$(cat)
TIMESTAMP=$(echo "$INPUT" | jq -r '.timestamp')
TOOL_NAME=$(echo "$INPUT" | jq -r '.tool_name')
SESSION_ID=$(echo "$INPUT" | jq -r '.sessionId')

echo "[$TIMESTAMP] Session: $SESSION_ID, Tool: $TOOL_NAME" >> "${AUDIT_LOG:-audit.log}"
echo '{"continue":true}'
```

</details>

<details>
<summary>特定のツールに対する承認の要求</summary>

インフラストラクチャを変更するツールの手動確認を義務付けます:

**.github/hooks/approval.json**:
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/require-approval.sh"
      }
    ]
  }
}
```

**scripts/require-approval.sh**:
```bash
#!/bin/bash
INPUT=$(cat)
TOOL_NAME=$(echo "$INPUT" | jq -r '.tool_name')

# ツール常に承認が必要
SENSITIVE_TOOLS="runTerminalCommand|deleteFile|pushToGitHub"

if echo "$TOOL_NAME" | grep -qE "^($SENSITIVE_TOOLS)$"; then
  echo '{"hookSpecificOutput":{"permissionDecision":"ask","permissionDecisionReason":"This operation requires manual approval"}}'
else
  echo '{"hookSpecificOutput":{"permissionDecision":"allow"}}'
fi
```

</details>

<details>
<summary>セッション開始時にプロジェクトコンテキストを挿入</summary>

セッションが開始された時、プロジェクト固有の情報を提供します:

**.github/hooks/context.json**:
```json
{
  "hooks": {
    "SessionStart": [
      {
        "type": "command",
        "command": "./scripts/inject-context.sh"
      }
    ]
  }
}
```

**scripts/inject-context.sh**:
```bash
#!/bin/bash
PROJECT_INFO=$(cat package.json 2>/dev/null | jq -r '.name + " v" + .version' || echo "Unknown project")
BRANCH=$(git branch --show-current 2>/dev/null || echo "unknown")

cat <<EOF
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Project: $PROJECT_INFO | Branch: $BRANCH | Node: $(node -v 2>/dev/null || echo 'not installed')"
  }
}
EOF
```

</details>

## セキュリティ

エージェントがフックによって実行されるスクリプトを編集できるアクセス権がある場合、独自の実行中にこれらのスクリプトを変更し、書き込むコードを実行する機能があります。`chat.tools.edits.autoApprove`を使用して、エージェントが手動承認なしでフックスクリプトを編集できないようにすることをお勧めします。

## トラブルシューティング

### フック診断を表示

読み込まれているフックを確認し、構成エラーをチェックします:

1. **View Logs**を選択してすべてのログを表示します。

1. 「Load Hooks」を探してロードされたフックと読み込み元の場所を確認します。

### フック出力を表示

フック出力とエラーを確認します:

1. **Output**パネルを開きます。

1. チャネルリストから**GitHub Copilot Chat Hooks**を選択します。

### 一般的な問題

**フックが実行されない**: フックファイルが`.github/hooks/`にあり、`.json`拡張子を持つことを確認してください。`type`プロパティが`"command"`に設定されていることを確認してください。

**権限拒否エラー**: フックスクリプトに実行権限があることを確認してください(`chmod +x script.sh`)。

**タイムアウトエラー**: `timeout`値を増やすか、フックスクリプトを最適化してください。デフォルトは30秒です。

**JSON解析エラー**: フックスクリプトが有効なJSONをstdoutに出力することを確認してください。`jq`またはJSONライブラリを使用して出力を構成します。

## よくある質問

### VS CodeはClaude Codeフック構成をどのように処理しますか?

VS Codeはデフォルトで`.claude/settings.json`、`.claude/settings.local.json`、および`~/.claude/settings.json`からフック構成を読み取ります。VS CodeはClaude Codeのフック構成形式をマッチャー構文を含めて解析します。現在、VS Codeはマッチャー値を無視するため、フックはマッチャーに関わらずすべてのツール呼び出しで実行されます。

Claude CodeフックをVS Codeに対応させる場合、次の違いに注意してください:

* **ツール入力プロパティ名**: Claude Codeはツール入力プロパティにsnake_caseを使用します(たとえば、`tool_input.file_path`)。一方、VS CodeツールはcamelCaseを使用します(たとえば、`tool_input.filePath`)。フックスクリプトを更新して、正しいプロパティ名を読み込みます。
* **ツール名**: Claude CodeとVS Codeは異なるツール名を使用します。たとえば、Claude Codeはファイル操作に`Write`と`Edit`を使用し、VS Codeは`create_file`や`replace_string_in_file`などのツール名を使用します。`tool_name`入力フィールドでツール名を確認し、フックロジックを更新してください。
* **マッチャーは無視されます**: `"Edit|Write"`のようなフックマッチャーは解析されますが、適用されません。すべてのフックは、マッチャー内のツール名に関わらず、すべてのマッチングイベントで実行されます。

### VS CodeはCopilot CLIフック構成をどのように処理しますか?

VS CodeはCopilot CLIフック構成を解析し、lowerCamelCaseフックイベント名(たとえば`preToolUse`)をVS Codeで使用されるPascalCase形式(`PreToolUse`)に変換します。`bash`および`powershell`コマンドプロパティはOS固有のコマンドにマップされます: `powershell`は`windows`にマップされ、`bash`は`osx`および`linux`にマップされます。

## セキュリティに関する考慮事項

> [!CAUTION]
> フックはVS Codeと同じ権限でシェルコマンドを実行します。フック構成を慎重に確認してください。特に信頼されていないソースからのフックを使用する場合は注意してください。

* **フックスクリプトを確認**: すべてのフックスクリプトを有効にする前に検査してください。特に共有リポジトリ内では注意してください。

* **フック権限を制限**: 最小権限の原則を使用してください。フックは必要なものへのアクセス権のみを持つべきです。

* **入力を検証**: フックスクリプトはエージェントから入力を受け取ります。すべての入力を検証および削除して、インジェクション攻撃を防ぎます。

* **認証情報をセキュアに**: フックスクリプトにシークレットをハードコードしないでください。環境変数または安全な認証情報ストレージを使用します。

## 関連リソース

* [エージェントでツールを使用](/docs/copilot/agents/agent-tools.md) - ツール承認と実行について学習
* [カスタムエージェント](/docs/copilot/customization/custom-agents.md) - 専門的なエージェント構成を作成
* [サブエージェント](/docs/copilot/agents/subagents.md) - コンテキスト分離されたサブエージェントにタスクをデリゲート
* [セキュリティに関する考慮事項](/docs/copilot/security.md) - VS CodeのAIセキュリティのベストプラクティス
