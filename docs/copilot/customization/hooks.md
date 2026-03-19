---
ContentId: 9c4d5e6f-7a8b-9c0d-1e2f-3a4b5c6d7e8f
DateApproved: 3/9/2026
MetaDescription: VS Code でエージェント セッション中の主要なライフサイクル ポイントで、カスタムシェルコマンドを実行するフックの使い方を学びます。自動化、検証、ポリシー実施に利用できます。
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

# Visual Studio Code のエージェント フック (プレビュー)

フックを使用すると、エージェント セッション中の重要なライフサイクル ポイントでカスタムシェルコマンドを実行できます。フックを使って、ワークフローを自動化したり、セキュリティ ポリシーを強制したり、操作を検証したり、外部ツールと統合したりできます。

フックがAIカスタマイズフレームワークにどのように適合するかについては、[カスタマイズの概念](/docs/copilot/concepts/customization.md#hooks)を参照してください。

この記事では、VS Code でフックを構成して使用する方法について説明します。

> [!NOTE]
> エージェント フックは現在プレビュー中です。構成形式と動作は今後のリリースで変更される可能性があります。

> [!IMPORTANT]
> 組織が VS Code でのフックの使用を無効化している可能性があります。詳細については管理者に問い合わせてください。詳細は[エンタープライズ ポリシー](/docs/enterprise/policies.md)を参照してください。

> [!TIP]
> [チャット カスタマイズ エディター](/docs/copilot/customization/overview.md#chat-customizations-editor)(プレビュー)を使用して、すべてのチャット カスタマイズを1か所で検出、作成、管理できます。コマンド パレットから**Chat: Open Chat Customizations**を実行します。

フックは、ローカル エージェント、バックグラウンド エージェント、クラウド エージェントを含むエージェント タイプ全体で機能するように設計されています。各フックは構造化JSON入力を受け取り、JSON出力を返してエージェント動作に影響を与えることができます。

## フックを使用する理由

フックは確定的でコード駆動の自動化を提供します。エージェント動作を導く指示またはカスタム プロンプトと異なり、フックは特定のライフサイクル ポイントで確実な結果をもたらすコードを実行します。

* **セキュリティ ポリシーを強制する**: `rm -rf`や`DROP TABLE`などの危険なコマンドを、エージェントがどのようにプロンプトされたかに関わらず実行前にブロックできます。

* **コード品質を自動化する**: ファイル変更後に自動的にフォーマッター、リンター、またはテストを実行します。

* **監査証跡を作成する**: コンプライアンスとデバッグのためにすべてのツール呼び出し、コマンド実行、またはファイル変更をログに記録します。

* **コンテキストを注入する**: プロジェクト固有情報、APIキー、または環境詳細を追加して、エージェントがより良い判断を下すのを支援します。

* **承認を制御する**: 安全な操作は自動的に承認し、機密操作は確認を必須にします。

## クイック スタート: 最初のフック

次の例は、ファイル編集後に毎回Prettier を実行するフックを作成しています。ワークスペースに`.github/hooks/format.json`ファイルを作成します。

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

このファイルを保存すると、VS Code は自動的にフックを読み込みます。次回エージェントがファイルを編集するとき、Prettier は変更されたファイルで実行されます。**GitHub Copilot Chat Hooks**出力チャネルでフックが実行されたことを確認してください。

カスタムスクリプトを使用するより複雑なフックについては、[使用シナリオ](#使用シナリオ)を参照してください。

## フック ライフサイクル イベント

VS Code は、エージェント セッション中の特定のポイントで発生する8つのフック イベントをサポートしています。

| フック イベント | 発生するタイミング | 一般的な使用例 |
|------------|---------------|------------------|
| `SessionStart` | ユーザーが新しいセッションの最初のプロンプトを送信する | リソースの初期化、セッション開始のログ記録、プロジェクト状態の検証 |
| `UserPromptSubmit` | ユーザーがプロンプトを送信する | ユーザー要求の監査、システム コンテキストの注入 |
| `PreToolUse` | エージェントがツールを呼び出す前 | 危険な操作のブロック、承認の要求、ツール入力の変更 |
| `PostToolUse` | ツールが正常に完了した後 | フォーマッターの実行、結果のログ記録、フォローアップアクションのトリガー |
| `PreCompact` | 会話コンテキストが圧縮される前 | 重要なコンテキストのエクスポート、切り詰め前の状態保存 |
| `SubagentStart` | サブエージェントが生成される | ネストされたエージェント使用の追跡、サブエージェント リソースの初期化 |
| `SubagentStop` | サブエージェントが完了する | 結果の集約、サブエージェント リソースのクリーンアップ |
| `Stop` | エージェント セッションが終了する | レポートの生成、リソースのクリーンアップ、通知の送信 |

## フックを構成する

フックは、ワークスペースまたはユーザー ディレクトリに保存されているJSON ファイルで構成されます。

### フック ファイルの場所

VS Code は以下の場所でフック構成ファイルを検索します。

| スコープ | デフォルト ファイルの場所 |
|-------|-----------------------|
| ワークスペース | `.github/hooks/*.json` |
| ワークスペース (Claude 形式) | `.claude/settings.json`, `.claude/settings.local.json` |
| ユーザー | `~/.claude/settings.json` |
| カスタム エージェント | `.agent.md` フロントマターの`hooks`フィールド ([エージェント スコープ フック](#エージェント-スコープ-フック)を参照) |

ワークスペース フックは、同じイベント タイプのユーザー フックより優先されます。

`setting(chat.hookFilesLocations)`設定を使用して、どのフック ファイルが読み込まれるかをカスタマイズします。フォルダへのパス (VS Code はフォルダ内のすべての`*.json`ファイルを読み込みます) または個別の`.json`ファイルへのパスを指定できます。相対パスとチルダ (`~`) パスのみがサポートされています。

デフォルト値には次の場所が含まれます。

```json
"chat.hookFilesLocations": {
  ".github/hooks": true,
  ".claude/settings.local.json": true,
  ".claude/settings.json": true,
  "~/.claude/settings.json": true
}
```

カスタム ロケーションを追加するには、この設定にエントリを追加します。

```json
"chat.hookFilesLocations": {
  "custom/hooks": true,
  "~/my-hooks/security.json": true
}
```

パスを`false`に設定すると、デフォルト ロケーションを含む、その場所からのフック読み込みを無効化できます。たとえば、Claude Code 構成ファイルからフック読み込みを停止するには。

```json
"chat.hookFilesLocations": {
  ".claude/settings.json": false,
  ".claude/settings.local.json": false,
  "~/.claude/settings.json": false
}
```

### エージェント スコープ フック

> [!NOTE]
> エージェント スコープ フックは現在プレビュー中です。

[カスタム エージェント](/docs/copilot/customization/custom-agents.md)のYAMLフロントマターでフックを直接定義できます。エージェント スコープ フックは、そのカスタム エージェントがアクティブな場合 (ユーザーによって選択されるか、サブエージェントとして呼び出される) にのみ実行されます。エージェント スコープ フックは、同じイベント用に構成されているワークスペース レベルまたはユーザー レベルのフックに加えて実行されます。

エージェント スコープ フックを有効にするには、`setting(chat.useCustomAgentHooks)`を`true`に設定します。

エージェント フロントマターに`hooks`フィールドを追加して、フック構成ファイルと同じ構造を使用します。イベント名をフック コマンド オブジェクトの配列にマップします。

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

イベント ごとに`hooks`オブジェクトとフック コマンドの配列を含むJSONファイルを作成します。VS Code は、互換性を保つため Claude Code および Copilot CLI と同じフック形式を使用します。

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

### フック コマンド プロパティ

各フック エントリには`type: "command"`と、少なくとも1つのコマンド プロパティが必要です。

| プロパティ | 型 | 説明 |
|----------|------|-------------|
| `type` | 文字列 | `"command"`である必要があります |
| `command` | 文字列 | デフォルト コマンド (クロスプラットフォーム) |
| `windows` | 文字列 | Windows 固有のコマンド上書き |
| `linux` | 文字列 | Linux 固有のコマンド上書き |
| `osx` | 文字列 | macOS 固有のコマンド上書き |
| `cwd` | 文字列 | 作業ディレクトリ (リポジトリ ルートから相対) |
| `env` | オブジェクト | 追加の環境変数 |
| `timeout` | 数値 | タイムアウト (秒単位) (デフォルト: 30) |

> [!NOTE]
> OS 固有のコマンドは拡張機能ホスト プラットフォームに基づいて選択されます。リモート開発シナリオ (SSH、コンテナー、WSL) では、これがローカルオペレーティング システムと異なる場合があります。

### OS 固有のコマンド

各オペレーティング システムに異なるコマンドを指定します。

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

実行サービスは、OS に基づいて適切なコマンドを選択します。OS 固有のコマンドが定義されていない場合は、`command`プロパティにフォールバックします。

## フック入出力

フックは stdin (入力) と stdout (出力) を使用したJSONを介して VS Code と通信します。

### 一般的な入力フィールド

すべてのフックは stdin 経由でこれらの共通フィールドを持つJSONオブジェクトを受け取ります。

```json
{
  "timestamp": "2026-02-09T10:30:00.000Z",
  "cwd": "/path/to/workspace",
  "sessionId": "session-identifier",
  "hookEventName": "PreToolUse",
  "transcript_path": "/path/to/transcript.json"
}
```

### 一般的な出力形式

フックは stdout 経由でJSONを返してエージェント動作に影響を与えることができます。すべてのフックはこれらの出力フィールドをサポートしています。

```json
{
  "continue": true,
  "stopReason": "Security policy violation",
  "systemMessage": "Unit tests failed"
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `continue` | ブール値 | 処理を停止するには`false`に設定します (デフォルト: `true`) |
| `stopReason` | 文字列 | `continue`が`false`のときの停止理由 (ユーザーに表示されます) |
| `systemMessage` | 文字列 | ユーザーに表示される警告メッセージ |

### 終了コード

フックの終了コードは、VS Code が結果をどのように処理するかを決定します。

| 終了コード | 動作 |
|-----------|----------|
| `0` | 成功: stdout をJSON として解析 |
| `2` | ブロック エラー: 処理を停止してエラーをモデルに表示 |
| その他 | ブロック以外の警告: ユーザーに警告を表示して処理を続行 |

### データを返す方法の選択

フックにはエージェント動作を制御するいくつかの方法があります。終了コード、トップレベル出力フィールド (`continue`、`stopReason`)、およびフック固有の出力フィールド (`hookSpecificOutput`) です。以下のようにそれらを組み合わせて使用します。

* **終了コード2**は操作をブロックする最も簡単な方法です。フックの stderr がコンテキストとしてモデルに表示されます。JSON出力は不要です。
* JSON出力の**`continue: false`**はエージェント セッション全体を停止します。`stopReason`を使用してユーザーに理由を伝えます。これは単一のツール呼び出しをブロックするより大きな影響があります。
* **`hookSpecificOutput`**は、各フック イベントに固有のきめ細かい制御を提供します。たとえば、`PreToolUse`フックは`permissionDecision`を使用して、セッションを停止することなく単一のツール呼び出しを許可、拒否、またはプロンプトします。
* **`systemMessage`**は、他の決定に関わらず、チャットでユーザーに警告を表示します。

複数の制御メカニズムが一緒に使用される場合、最も制限的なものが優先されます。たとえば、フックが`continue: false`と`permissionDecision: "allow"`を返す場合、セッションは依然として停止します。

## PreToolUse

`PreToolUse` フックはエージェントがツールを呼び出す前に発生します。

### PreToolUse 入力

共通フィールドに加えて、`PreToolUse`フックはこれらを受け取ります。

```json
{
  "tool_name": "editFiles",
  "tool_input": { "files": ["src/main.ts"] },
  "tool_use_id": "tool-123"
}
```

### PreToolUse 出力

`PreToolUse`フックは`hookSpecificOutput`オブジェクトを介してツール実行を制御できます。

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
| `permissionDecision` | `"allow"`, `"deny"`, `"ask"` | ツール承認を制御 |
| `permissionDecisionReason` | 文字列 | ユーザーに表示する理由 |
| `updatedInput` | オブジェクト | 変更されたツール入力 (オプション) |
| `additionalContext` | 文字列 | モデルの追加コンテキスト |

**許可決定の優先度**: 同じツール呼び出しに対して複数のフックが実行される場合、最も制限的な決定が優先されます。

1. `deny` (最も制限的): ツール実行をブロック
2. `ask`: ユーザー確認が必要
3. `allow` (最も制限的でない): 自動承認実行

**`updatedInput`形式**: `updatedInput`の形式を確認するには、[エージェント ログ](/docs/copilot/chat/chat-debug-view.md#agent-debug-panel)を開いて、ログされたツール スキーマを探してください。`updatedInput`が期待されるスキーマと一致しない場合、は無視されます。

## PostToolUse

`PostToolUse`フックはツールが正常に完了した後に発生します。

### PostToolUse 入力

共通フィールドに加えて、`PostToolUse`フックはこれらを受け取ります。

```json
{
  "tool_name": "editFiles",
  "tool_input": { "files": ["src/main.ts"] },
  "tool_use_id": "tool-123",
  "tool_response": "File edited successfully"
}
```

### PostToolUse 出力

`PostToolUse`フックはモデルに追加コンテキストを提供できます。または処理をブロックできます。

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
| `decision` | `"block"` | さらなる処理をブロック (オプション) |
| `reason` | 文字列 | ブロックの理由 (モデルに表示されます) |
| `hookSpecificOutput.additionalContext` | 文字列 | 会話に注入されるコンテキスト |

## UserPromptSubmit

`UserPromptSubmit`フックはユーザーがプロンプトを送信するときに発生します。

### UserPromptSubmit 入力

共通フィールドに加えて、`UserPromptSubmit`フックはユーザーが送信したテキストを含む`prompt`フィールドを受け取ります。

`UserPromptSubmit`フックは一般的な出力形式のみを使用します。

## SessionStart

`SessionStart`フックは新しいエージェント セッションが開始されるときに発生します。

### SessionStart 入力

共通フィールドに加えて、`SessionStart`フックはこれらを受け取ります。

```json
{
  "source": "new"
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `source` | 文字列 | セッションの開始方法。現在常に`"new"`。 |

### SessionStart 出力

`SessionStart`フックはエージェントの会話に追加コンテキストを注入できます。

```json
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Project: my-app v2.1.0 | Branch: main | Node: v20.11.0"
  }
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `additionalContext` | 文字列 | エージェントの会話に追加されるコンテキスト |

## Stop

`Stop`フックはエージェント セッションが終了するときに発生します。カスタム エージェントにスコープされた場合、`Stop`フックも`SubagentStop`として扱われます。

### Stop 入力

共通フィールドに加えて、`Stop`フックはこれらを受け取ります。

```json
{
  "stop_hook_active": false
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `stop_hook_active` | ブール値 | 前のstopフックの結果としてエージェントがすでに続行中のとき`true`。エージェントが無期限に実行されるのを防ぐため、この値をチェックしてください。 |

### Stop 出力

`Stop`フックはエージェントの停止を防ぐことができます。

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
| `decision` | `"block"` | エージェントの停止を防止 |
| `reason` | 文字列 | `decision`が`"block"`のときは必須。エージェントが続行し続けるべき理由を伝えます。 |

> [!IMPORTANT]
> `Stop`フックがエージェントの停止をブロックすると、エージェントは実行を続け、追加のターンは[プレミアム リクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests)を消費します。`stop_hook_active`フィールドをチェックしてエージェントが無期限に実行されるのを防いでください。

## SubagentStart

`SubagentStart`フックはサブエージェントが生成されるときに発生します。

### SubagentStart 入力

共通フィールドに加えて、`SubagentStart`フックはこれらを受け取ります。

```json
{
  "agent_id": "subagent-456",
  "agent_type": "Plan"
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `agent_id` | 文字列 | サブエージェントの一意識別子 |
| `agent_type` | 文字列 | エージェント名 (たとえば、ビルトイン エージェントの`"Plan"`またはカスタム エージェント名) |

### SubagentStart 出力

`SubagentStart`フックはサブエージェントの会話に追加コンテキストを注入できます。

```json
{
  "hookSpecificOutput": {
    "hookEventName": "SubagentStart",
    "additionalContext": "This subagent should follow the project coding guidelines"
  }
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `additionalContext` | 文字列 | サブエージェントの会話に追加されるコンテキスト |

## SubagentStop

`SubagentStop`フックはサブエージェントが完了するときに発生します。

### SubagentStop 入力

共通フィールドに加えて、`SubagentStop`フックはこれらを受け取ります。

```json
{
  "agent_id": "subagent-456",
  "agent_type": "Plan",
  "stop_hook_active": false
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `agent_id` | 文字列 | サブエージェントの一意識別子 |
| `agent_type` | 文字列 | エージェント名 (たとえば、ビルトイン エージェントの`"Plan"`またはカスタム エージェント名) |
| `stop_hook_active` | ブール値 | 前のstopフックの結果としてサブエージェントがすでに続行中のとき`true`。サブエージェントが無期限に実行されるのを防ぐため、この値をチェックしてください。 |

### SubagentStop 出力

`SubagentStop`フックはサブエージェントの停止を防ぐことができます。

```json
{
  "decision": "block",
  "reason": "Verify subagent results before completing"
}
```

| フィールド | 値 | 説明 |
|-------|--------|-------------|
| `decision` | `"block"` | サブエージェントの停止を防止 |
| `reason` | 文字列 | `decision`が`"block"`のときは必須。サブエージェントが続行し続けるべき理由を伝えます。 |

## PreCompact

`PreCompact`フックは会話コンテキストが圧縮される前に発生します。

### PreCompact 入力

共通フィールドに加えて、`PreCompact`フックはこれらを受け取ります。

```json
{
  "trigger": "auto"
}
```

| フィールド | 型 | 説明 |
|-------|------|-------------|
| `trigger` | 文字列 | 圧縮がトリガーされた方法。会話がプロンプト バジェットに対して長すぎるとき`"auto"`。 |

`PreCompact`フックは一般的な出力形式のみを使用します。

## UIでフックを構成する

以下のいくつかの方法でUIを介してフックを構成できます。

* チャット入力で`/hooks`を入力して`kbstyle(Enter)`を押します。
* コマンド パレット (`kb(workbench.action.showCommands)`) を開いて**Chat: Configure Hooks**を実行します。
* チャット ビューの上部の**設定**アイコン (<i class="codicon codicon-gear"></i>) を選択してから、**Hooks**を選択します。

フック構成メニューで。

1. リストからフック イベント タイプを選択します。

2. 編集する既存のフックを選択するか、**フックを新規追加**を選択して新しいフックを作成します。

3. フック構成ファイルを選択または作成します。

コマンドはフック ファイルをエディターで開き、コマンド フィールドに対してカーソルを配置して、編集する準備がしています。

### AIでフックを生成する

AIを使用してフック構成を生成できます。チャットで`/create-hook`と入力して、必要な自動化について説明します (たとえば、「すべてのファイル編集後にESLintを実行」)。エージェントは確認質問をして、適切なイベント タイプ、コマンド、設定を含むフック構成ファイルを生成します。

## 使用シナリオ

次の例は、一般的なフック パターンを示しています。

<details>
<summary>危険なターミナル コマンドをブロック</summary>

破壊的なコマンドを防ぐ`PreToolUse`フックを作成します。

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
<summary>編集後に自動的にコードをフォーマット</summary>

ファイル変更後に自動的にPrettierを実行します。

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
<summary>監査用にツール使用をログ</summary>

すべてのツール呼び出しの監査証跡を作成します。

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
<summary>特定のツールの承認が必要</summary>

インフラストラクチャを変更するツールに手動確認を強制します。

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

# 常に承認が必要なツール
SENSITIVE_TOOLS="runTerminalCommand|deleteFile|pushToGitHub"

if echo "$TOOL_NAME" | grep -qE "^($SENSITIVE_TOOLS)$"; then
  echo '{"hookSpecificOutput":{"permissionDecision":"ask","permissionDecisionReason":"This operation requires manual approval"}}'
else
  echo '{"hookSpecificOutput":{"permissionDecision":"allow"}}'
fi
```

</details>

<details>
<summary>セッション開始時にプロジェクト コンテキストを注入</summary>

セッションが開始されるときにプロジェクト固有の情報を提供します。

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

エージェントがフックで実行されるスクリプトを編集できる場合、実行中にスクリプトを変更し、記述したコードを実行する能力があります。`chat.tools.edits.autoApprove`を使用して、エージェントが手動承認なしでフック スクリプトを編集するのを許可しないことをお勧めします。

## トラブルシューティング

### フック診断を表示する

どのフックが読み込まれているか、構成エラーがあるか確認するには。

1. **ログを表示**を選択してすべてのログを表示します。

2. 「Load Hooks」を探して読み込まれたフックとそれらがどの場所から読み込まれたかを確認します。

### フック出力を表示する

フック出力とエラーを確認するには。

1. **出力**パネルを開きます。

2. チャネル リストから**GitHub Copilot Chat Hooks**を選択します。

### 一般的な問題

**フックが実行されない**: フック ファイルが`.github/hooks/`にあり`.json`拡張子を持つことを確認してください。`type`プロパティが`"command"`に設定されていることを確認します。

**アクセス許可が拒否されたエラー**: フック スクリプトに実行権限があることを確認してください (`chmod +x script.sh`)。

**タイムアウト エラー**: `timeout`値を増やすか、フック スクリプトを最適化してください。デフォルトは30秒です。

**JSON解析エラー**: フック スクリプトが stdout に有効なJSONを出力することを確認してください。`jq`またはJSONライブラリを使用して出力を構築します。

## よくある質問

### VS Code はClaude Code フック構成をどのように処理しますか?

VS Code は既定で`.claude/settings.json`、`.claude/settings.local.json`、および`~/.claude/settings.json`からフック構成を読み取ります。VS Code はマッチャー構文を含むClaude Code のフック構成形式を解析します。現在、VS Code はマッチャー値を無視するため、フックはマッチャーに関わらずすべてのツール呼び出しで実行されます。

Claude Code フックを VS Code 向けに調整している場合、次の違いに注意してください。

* **ツール入力プロパティ名**: Claude Code はツール入力プロパティに snake_case を使用する (たとえば、`tool_input.file_path`)、一方 VS Code ツールは camelCase を使用する (たとえば、`tool_input.filePath`)。正しいプロパティ名を読み取るようにフック スクリプトを更新します。
* **ツール名**: Claude Code と VS Code は異なるツール名を使用します。たとえば、Claude Code はファイル操作に`Write`と`Edit`を使用しますが、VS Code は`create_file`および`replace_string_in_file`などのツール名を使用します。`tool_name`入力フィールドでツール名を確認し、フック ロジックをそれに応じて更新します。
* **マッチャーは無視されます**: `"Edit|Write"`などのフック マッチャーは解析されますが、適用されません。すべてのフックはマッチャー内のツール名に関わらず、すべてのマッチング イベントで実行されます。

### VS Code はCopilot CLI フック構成をどのように処理しますか?

VS Code はCopilot CLI フック構成を解析し、lowerCamelCase フック イベント名 (`preToolUse`など) を VS Code で使用されるPascalCase 形式 (`PreToolUse`) に変換します。`bash`および`powershell`コマンドプロパティはOS 固有のコマンドにマップされます。`powershell`は`windows`にマップされ、`bash`は`osx`および`linux`にマップされます。

## セキュリティに関する考慮事項

> [!CAUTION]
> フックは VS Code と同じ権限でシェルコマンドを実行します。特に信頼できないソースからのフックを使用する場合は、フック構成を慎重に確認してください。

* **フック スクリプトを確認する**: すべてのフック スクリプトを有効にする前に検査してください。特に共有リポジトリ内のフックは。

* **フック権限を制限する**: 最小権限の原則を使用してください。フックは必要な機能にのみアクセスすべきです。

* **入力を検証する**: フック スクリプトはエージェントから入力を受け取ります。すべての入力を検証およびサニタイズしてインジェクション攻撃を防止します。

* **認証情報を保護する**: フック スクリプトに秘密情報をハードコードしないでください。環境変数またはセキュアな認証情報ストレージを使用します。

## 関連リソース

* [エージェント でツールを使用する](/docs/copilot/agents/agent-tools.md) - ツール承認と実行に関する情報
* [カスタム エージェント](/docs/copilot/customization/custom-agents.md) - 特殊なエージェント構成を作成
* [サブエージェント](/docs/copilot/agents/subagents.md) - コンテキスト分離されたサブエージェントにタスクを委譲
* [セキュリティに関する考慮事項](/docs/copilot/security.md) - VS Code でのAI セキュリティに関するベスト プラクティス

