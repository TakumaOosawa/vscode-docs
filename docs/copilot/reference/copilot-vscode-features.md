---
ContentId: de6f9f68-7dd5-4de3-a210-3db57882384b
DateApproved: 3/9/2026
MetaDescription: GitHub Copilot in VS Code のクイックリファレンス。自律型エージェント、複数ファイル編集、インライン提案、エンタープライズコントロールを含みます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilot in VS Code チートシート

GitHub Copilot in Visual Studio Code は、自律型エージェント、インライン提案、チャット、スマートアクションを提供します。エージェントは複数のファイル全体をプランニング、実装、検証し、ローカル、バックグラウンド、またはクラウドで並行実行できます。複数の AI モデルから選択したり、MCP で外部ツールを接続したり、チーム向けにエージェントをカスタマイズできます。このチートシートは、全機能の概要を提供します。

> [!TIP]
> まだ Copilot サブスクリプションがない場合は、[Copilot Free プラン](https://github.com/github-copilot/signup)にサインアップして Copilot を無料で使用でき、インライン提案とチャット操作の月間制限を取得できます。

## 主要なキーボードショートカット

* `kb(workbench.panel.chat)` - チャットビューを開く
* `kb(workbench.action.chat.startVoiceChat)` - チャットビューでボイスチャットプロンプトを入力
* `kb(workbench.action.chat.newChat)` - チャットビューで新しいチャットセッションを開始
* `kb(workbench.action.chat.openAgent)` - チャットビューでエージェントの使用に切り替え
* `kb(inlineChat.start)` - エディターまたはターミナルでインラインチャットを開始
* `kb(workbench.action.chat.startVoiceChat)` (長押し) - インラインボイスチャットを開始
* `kb(editor.action.inlineSuggest.commit)` - インライン提案を受け入れるか、次の編集提案に移動
* `kb(editor.action.inlineSuggest.hide)` - インライン提案を非表示

## VS Code で AI にアクセス

* 自然言語を使用してチャットを開始
    * チャットビュー（`kb(workbench.action.chat.open)`）: セカンダリサイドバーで進行中のチャットを保持
    * エディターまたはターミナルでインラインチャット（`kb(inlineChat.start)`）: 流れの中で質問する
    * クイックチャット（`kb(workbench.action.quickchat.toggle)`）: 現在のタスクを離れずに素早く質問

* [エディター](/docs/copilot/ai-powered-suggestions.md)での AI
    * インライン提案: 入力時に提案を取得し、`kb(editor.action.inlineSuggest.commit)`を押して提案を受け入れ
    * 編集コンテキストメニューアクション: コード説明、修正、テスト生成、テキスト選択のレビューなどの一般的な AI アクションにアクセス
    * コードアクション: エディターコードアクション（電球）でリンティングやコンパイラエラーを修正

* VS Code 全体の[スマートアクション](/docs/copilot/copilot-smart-actions.md)
    * コミットメッセージとプルリクエストタイトル・説明を生成
    * テストエラーを修正
    * セマンティックファイル検索提案

## VS Code のチャット体験

自然言語チャット会話を開始してコーディングタスクを支援してもらいます。例えば、コードブロックまたはプログラミング概念の説明をリクエストしたり、コードをリファクタリングしたり、新機能を実装してもらえます。[Copilot Chat](/docs/copilot/chat/copilot-chat.md)の使用方法について詳しくご覧ください。

| アクション | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.open)` | セカンダリサイドバーの[チャットビュー](/docs/copilot/chat/copilot-chat.md)を開く |
| `kb(inlinechat.start)` | [インラインチャット](/docs/copilot/chat/inline-chat.md)を開始してエディターまたはターミナルでチャットを開く |
| `kb(workbench.action.quickchat.toggle)` | ワークフローを中断せずに[クイックチャット](/docs/copilot/chat/copilot-chat.md)を開く |
| `kb(workbench.action.chat.newChat)` | チャットビューで新しいチャットセッションを開始 |
| `kb(workbench.action.chat.toggleAgentMode)` | チャットビューで異なる[エージェント](/docs/copilot/customization/custom-agents.md)を切り替え |
| `kb(workbench.action.chat.openModelPicker)` | モデルピッカーを表示してチャット用に[異なる AI モデルを選択](/docs/copilot/customization/language-models.md) |
| コンテキストウインドウコントロール | チャット入力ボックスの視覚的インジケーターが[コンテキストウインドウ使用状況](/docs/copilot/chat/copilot-chat-context.md#monitor-context-window-usage)を表示。マウスホバーでトークン総数とカテゴリ別の内訳が表示 |
| `Add Context...` | [チャットプロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md) |
| `/`コマンド | [スラッシュコマンド](#slash-commands)を使用した一般的なタスクまたは[再利用可能なチャットプロンプト](/docs/copilot/customization/overview.md)を呼び出し |
| `#`メンション | [プロンプト内でコンテキスト提供](/docs/copilot/chat/copilot-chat-context.md)するための一般的なツールやチャット変数を参照 |
| `@`メンション | ドメイン固有のリクエストを処理するための[チャット参加者](#chat-participants)を参照 |
| 編集 (<i class="codicon codicon-pencil"></i>) | [前回のチャットプロンプトを編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)して変更を元に戻す |
| 履歴 (<i class="codicon codicon-history"></i>) | チャットセッションの履歴にアクセス |
| キュー送信またはステアリング | [リクエスト実行中にフォローアップメッセージを送信](/docs/copilot/chat/chat-sessions.md#send-messages-while-a-request-is-running)。メッセージをキュー送信、現在のリクエストをステアリング、または停止して即座に送信するかを選択 |
| ボイス (<i class="codicon codicon-mic"></i>) | 音声（ボイスチャット）を使用してチャットプロンプトを入力。チャット応答は大声で読み上げられます |
| [KaTeX](https://katex.org) | チャット応答で数式をレンダリング。`setting(chat.math.enabled)`で有効化。数式を右クリックしてソース式をコピー |
| [Mermaid](https://mermaid.js.org) | チャット応答で Mermaid 図をレンダリング。`setting(mermaid-chat.enabled)`で有効化。図を右クリックしてソースコードをコピー |

> **ヒント**
>
> * `#`メンションを使用してチャットプロンプトにさらにコンテキストを追加。
> * 具体的に、シンプルに保ち、フォローアップ質問をする最高の結果を得る。
> * 特定のタスクに適した組み込みエージェントまたはカスタムエージェントを選択。

## プロンプトにコンテキストを追加

[チャットプロンプトにコンテキストを提供](/docs/copilot/chat/copilot-chat-context.md)して、より関連性の高い応答を取得します。ファイル、シンボル、エディター選択、ソースコントロールコミット、テスト失敗など、異なるコンテキストタイプから選択。

| アクション | 説明 |
|--------|-------------|
| **Add Context** | クイックピックを開いてチャットプロンプト用の関連コンテキストを選択。ワークスペースファイル、シンボル、現在のエディター選択、ターミナル選択など、異なるコンテキストタイプから選択 |
| ドラッグ&ドロップファイル | Explorer またはサーチビューからチャットビュー上のファイルをドラッグ&ドロップ、またはエディタータブをチャットビューにドラッグ |
| ドラッグ&ドロップフォルダー | フォルダーをチャットビューにドラッグ&ドロップしてその中のファイルを添付 |
| ドラッグ&ドロップ問題 | プロブレムスパネルの項目をドラッグ&ドロップ |
| `#<file\|folder\|symbol>` | `#`に続けてファイル、フォルダー、またはシンボル名を入力してチャットコンテキストとして追加 |
| `#`メンション | `#`に続けて[チャットツール](#chat-tools)を入力して特定のコンテキストタイプまたはツールを追加 |

## チャットツール

ユーザーリクエストを処理する際に、チャットの[ツール](/docs/copilot/agents/agent-tools.md)を使用して特化したタスクを実行します。ディレクトリ内のファイル一覧表示、ワークスペース内のファイル編集、ターミナルコマンド実行、ターミナル出力取得など。

VS Code は組み込みツールを提供し、[MCP サーバー](/docs/copilot/customization/mcp-servers.md)と[拡張機能](/api/extension-guides/ai/tools.md)からツールでチャットを拡張できます。[ツールの種類](/docs/copilot/agents/agent-tools.md#types-of-tools)について詳しくご覧ください。

следующая表は VS Code の組み込みツール一覧です：

| チャット変数/ツール | 説明 |
|--------|-------------|
| `#changes` | ソースコントロール変更のリスト |
| `#codebase` | 現在のワークスペースでコード検索を実行し、チャットプロンプト用の関連コンテキストを自動的に見つける |
| `#createAndRunTask` | ワークスペースで新しい[タスク](/docs/debugtest/tasks.md)を作成して実行 |
| `#createDirectory` | ワークスペースに新しいディレクトリを作成 |
| `#createFile` | ワークスペースに新しいファイルを作成 |
| `#edit` (ツールセット) | ワークスペース内の変更を有効化 |
| `#editFiles` | ワークスペース内のファイルに編集を適用 |
| `#editNotebook` | ノートブックを編集 |
| `#extensions` | VS Code 拡張機能を検索して質問。例： "how to get started with Python #extensions?" |
| `#fetch` | 指定の Web ページからコンテンツを取得。例： "Summarize #fetch code.visualstudio.com/updates." |
| `#fileSearch` | グロブパターンを使用してワークスペース内のファイルを検索してパスを返す |
| `#getNotebookSummary` | ノートブックセルのリストと詳細を取得 |
| `#getProjectSetupInfo` | 異なるプロジェクトタイプをスキャフォルディングするための命令と構成を提供 |
| `#getTaskOutput` | ワークスペースで実行中の[タスク](/docs/debugtest/tasks.md)からの出力を取得 |
| `#getTerminalOutput` | ワークスペースでターミナルコマンド実行からの出力を取得 |
| `#githubRepo` | GitHub リポでコード検索を実行。例： "what is a global snippet #githubRepo microsoft/vscode." |
| `#installExtension` | VS Code 拡張機能をインストール |
| `#listDirectory` | ワークスペース内のディレクトリ内のファイルを一覧表示 |
| `#new` | デバッグと実行構成を事前設定した新しい VS Code ワークスペースをスキャフォルディング |
| `#newJupyterNotebook` | 説明に基づいて新しい Jupyter ノートブックをスキャフォルディング |
| `#newWorkspace` | 新しいワークスペースを作成 |
| `#openSimpleBrowser` | [統合ブラウザー](/docs/debugtest/integrated-browser.md)を開いてローカルデプロイ済みウェブアプリをプレビュー |
| `#browser` (ツールセット) | _(実験的)_[統合ブラウザー](/docs/debugtest/integrated-browser.md)内のページと対話：ナビゲート、ページコンテンツ読込、スクリーンショット取得、クリック、入力、ホバー、ドラッグ、ダイアログ処理。`setting(workbench.browser.enableChatTools)`で有効化 |
| `#problems` | **プロブレムス**パネルからワークスペース問題と問題をコンテキストとして追加。コード修正やデバッグに役立ちます |
| `#readFile` | ワークスペース内のファイルのコンテンツを読み込む |
| `#readNotebookCellOutput` | ノートブックセル実行からの出力を読み込む |
| `#runCell` | ノートブックセルを実行 |
| `#runCommands` (ツールセット) | ターミナルでコマンドを実行して出力を読み込み |
| `#runInTerminal` | 統合ターミナルでシェルコマンドを実行 |
| `#runNotebooks` (ツールセット) | ノートブックセルを実行 |
| `#runTask` | ワークスペースで既存の[タスク](/docs/debugtest/tasks.md)を実行 |
| `#runTasks` (ツールセット) | ワークスペースで[タスク](/docs/debugtest/tasks.md)を実行して出力を読み込み |
| `#runSubagent` | 隔離された[サブエージェント環境](/docs/copilot/agents/subagents.md)でタスクを実行。メインエージェントスレッドのコンテキスト管理改善に役立ちます |
| `#runTests` | ワークスペースで[単体テスト](/docs/debugtest/testing.md)を実行 |
| `#runVscodeCommand` | VS Code コマンドを実行。例： "Enable zen mode #runVscodeCommand." |
| `#search` (ツールセット) | 現在のワークスペースでファイルを検索 |
| `#searchResults` | サーチビューから検索結果を取得 |
| `#selection` | 現在のエディター選択を取得（テキスト選択された場合のみ利用可能） |
| `#terminalLastCommand` | 最後に実行したターミナルコマンドとその出力を取得 |
| `#terminalSelection` | 現在のターミナル選択を取得 |
| `#testFailure` | 単体テスト失敗情報を取得。[テスト](/docs/debugtest/testing.md)の実行と診断に役立ちます |
| `#textSearch` | ファイル内のテキストを検索 |
| `#todos` | トゥードゥリストでチャットリクエストの実装と進行状況を追跡 |
| `#usages` | 「すべての参照を検索」、「実装を検索」、「定義に移動」の組み合わせ |
| `#VSCodeAPI` | VS Code 機能と拡張機能開発について質問 |

## スラッシュコマンド

スラッシュコマンドはチャット内の特定の機能へのショートカット。それらを使用してコード修正、テスト生成、コード説明など、素早くアクション実行。

| スラッシュコマンド | 説明 |
|---------------|-------------|
| `/doc` | エディターインラインチャットからコード文書化コメントを生成 |
| `/explain` | コードブロック、ファイル、またはプログラミング概念を説明 |
| `/fix` | コードブロック修正またはコンパイラもしくはリンティングエラーを解決 |
| `/tests` | エディターで選択されたメソッドと関数のすべて、または選択されたもののみのテストを生成 |
| `/setupTests` | テストフレームワークの設定支援を取得。関連するテストフレームワークの推奨、設定と構成のステップ、VS Code テスト拡張機能の提案を取得 |
| `/clear` | チャットビューで新しいチャットセッションを開始 |
| `/compact` | 会話コンテキストをサマリーでコンパクト化。会話がモデルのコンテキストウインドウに対して長くなりすぎた場合に役立ちます |
| `/fork` | 現在のチャットセッションを新しい独立したセッションにフォーク。完全な会話履歴を継承。[チャットセッションをフォーク](/docs/copilot/chat/chat-sessions.md#fork-a-chat-session)について詳しくご覧ください |
| `/debug` | チャットデバッグビューを表示して[トラブルシューティング用チャットログを検査](/docs/copilot/troubleshooting.md) |
| `/new` | 新しい VS Code ワークスペースまたはファイルをスキャフォルディング。自然言語でプロジェクト/ファイルタイプの説明を行い、作成前にスキャフォルディング内容をプレビュー |
| `/newNotebook` | 要件に基づいて新しい Jupyter ノートブックをスキャフォルディング。ノートブックに含める内容を自然言語で説明 |
| `/init` | プロジェクト構造とコーディングパターンに基づいてワークスペース命令(`copilot-instructions.md`または`AGENTS.md`)を生成または更新 |
| `/plan` | 複雑なコーディングタスク用の詳細な実装プラン作成。要件を研究し、明確化質問を行い、ステップ、検証、決定を含む構造化プランを生成 |
| `/search` | サーチビュー用の検索クエリを生成。検索したい内容を自然言語で説明 |
| `/startDebugging` | `launch.json`デバッグ構成ファイルを生成してチャットビューからデバッグセッションを開始 |
| `/agents` | [カスタムエージェント](/docs/copilot/customization/custom-agents.md)を構成 |
| `/hooks` | [フック](/docs/copilot/customization/hooks.md)を構成 |
| `/instructions` | [カスタム命令](/docs/copilot/customization/custom-instructions.md)を構成 |
| `/prompts` | [再利用可能なプロンプトファイル](/docs/copilot/customization/prompt-files.md)を構成 |
| `/skills` | [エージェントスキル](/docs/copilot/customization/agent-skills.md)を構成 |
| `/create-prompt` | エージェントモードで AI 支援を受けて[プロンプトファイル](/docs/copilot/customization/prompt-files.md)を生成 |
| `/create-instruction` | エージェントモードで AI 支援を受けて[命令ファイル](/docs/copilot/customization/custom-instructions.md)を生成 |
| `/create-skill` | エージェントモードで AI 支援を受けて[エージェントスキル](/docs/copilot/customization/agent-skills.md)を生成 |
| `/create-agent` | エージェントモードで AI 支援を受けて[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を生成 |
| `/create-hook` | エージェントモードで AI 支援を受けて[フック](/docs/copilot/customization/hooks.md)構成を生成 |
| `/yolo`<br/>`/autoApprove` | すべてのツール呼び出しの[グローバル自動承認](/docs/copilot/agents/agent-tools.md#can-i-automatically-approve-all-tools-and-terminal-commands)を有効化(`setting(chat.tools.global.autoApprove)`)。初回は警告ダイアログを表示 |
| `/disableYolo`<br/>`/disableAutoApprove` | すべてのツール呼び出しの[グローバル自動承認](/docs/copilot/agents/agent-tools.md#can-i-automatically-approve-all-tools-and-terminal-commands)を無効化 |
| `/<skill name>` | チャットで[エージェントスキル](/docs/copilot/customization/agent-skills.md)を実行。例えば、`webapp-testing.md`という名前のスキルファイルがある場合、`/webapp-testing`を入力して実行 |
| `/<prompt name>` | チャットで[再利用可能なプロンプト](/docs/copilot/customization/prompt-files.md)を実行 |

## チャット参加者

チャット参加者を使用してチャットでドメイン固有のリクエストを処理。チャット参加者は`@`の前置で、特定のトピックについて質問するために使用できます。VS Code は`@github`、`@terminal`、`@vscode`など組み込みチャット参加者を提供し、拡張機能は追加の参加者を提供できます。

| チャット参加者 | 説明 |
|------------------|-------------|
| `@github` | `@github`参加者を使用して GitHub リポ、問題、プルリクエストなどについて質問。[利用可能な GitHub スキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)について詳しくご覧ください。<br/>例： `@github What are all of the open PRs assigned to me?`、`@github Show me the recent merged PRs from @dancing-mona` |
| `@terminal` | `@terminal`参加者を使用して統合ターミナルやシェルコマンドについて質問。<br/>例： `@terminal list the 5 largest files in this workspace` |
| `@vscode` | `@vscode`参加者を使用して VS Code 機能、設定、VS Code 拡張機能 API について質問。<br/>例： `@vscode how to enable word wrapping?` |

## エージェントを使用

[エージェント](/docs/copilot/agents/local-agents.md)を使用する場合、自然言語で高レベルなタスクを指定し、AI がリクエストを自律的に推論し、必要な作業をプランニングし、コードベースに変更を適用できます。エージェントはタスク達成するためにコード編集とツール呼び出しの組み合わせを使用。リクエストを処理する際に、編集とツールの成果を監視し、発生する問題を解決するために反復。

| アクション | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.openAgent)` | チャットビューでエージェント使用に切り替え |
| ツール (<i class="codicon codicon-tools"></i>) | エージェント使用時に利用可能なツールを構成。組み込みツール、MCP サーバー、拡張機能提供ツールから選択 |
| パーミッションレベル | 現在のセッション用に[パーミッションレベル](/docs/copilot/agents/agent-tools.md#permission-levels)を選択： **Default Approvals**、**Bypass Approvals**、**Autopilot** (preview)。ツール承認を処理する方法を制御 |
| 自動承認ツール | エージェント使用時にすべてのツールの[自動承認](/docs/copilot/agents/agent-tools.md#auto-approve-all-tools)を有効化(`setting(chat.tools.autoApprove)`) |
| 自動承認ターミナルコマンド | エージェント使用時にターミナルコマンドの[自動承認](/docs/copilot/agents/agent-tools.md#automatically-approve-terminal-commands)を有効化(`setting(chat.tools.terminal.autoApprove)`) |
| MCP | [MCP サーバー](/docs/copilot/customization/mcp-servers.md)を構成してエージェント機能とツールを拡張 |
| [サードパーティエージェント](/docs/copilot/agents/third-party-agents.md) | Claude Agent (preview) や OpenAI Codex など、Copilot サブスクリプションで外部プロバイダーのエージェントを使用 |
| Claude Agent _(preview)_ | Anthropic の Claude Agent SDK で動作する Claude Agent セッションを開始。高度なワークフロー用に`/agents`、`/hooks`、`/memory`スラッシュコマンドを使用 |

> **ヒント**
>
> * エージェント使用時に追加ツールを追加して機能を拡張。
> * カスタムエージェント定義してエージェント動作を定義。例えば、読み取り専用プランニングモード実装。
> * カスタム命令定義してエージェントコード生成と構造化を案内。
> * Claude Code や OpenAI Codex などのサードパーティエージェント試してコーディング体験。

## プランニング

VS Code チャットで[プランエージェント](/docs/copilot/agents/planning.md)を使用して複雑なコーディングタスク開始前に詳細な実装プランを作成。承認されたプランを実装エージェントに引き渡してコーディング開始。

| アクション | 説明 |
|--------|-------------|
| プランエージェント | エージェントドロップダウンで**Plan**エージェントを選択するか、`/plan`スラッシュコマンドを使用して複雑なコーディングタスク用の詳細な実装プランを作成 |
| トゥードゥリスト | 複雑なタスクの進行状況を追跡するためのトゥードゥリストを表示。`setting(chat.tools.todos.showWidget`設定で有効化 |
| [メモリー](/docs/copilot/agents/memory.md) | エージェントが会話全体で永続的なメモを保存して呼び出し。`setting(github.copilot.chat.tools.memory.enabled)`設定で有効化/無効化。**Chat: Show Memory Files**コマンドを使用して保存されたメモを表示 |

## チャット体験をカスタマイズ

チャット体験をカスタマイズしてコーディングスタイル、ツール、開発者ワークフローに合わせた応答を生成。VS Code のチャット体験をカスタマイズする複数の方法があります：

* [カスタム命令](/docs/copilot/customization/custom-instructions.md)： コード生成、コードレビュー実行、コミットメッセージ生成など、タスク用の一般的なガイドラインやルールを定義。カスタム命令はタスク実行する条件(_どのように_実行するか)を説明。

* [再利用可能なプロンプトファイル](/docs/copilot/customization/prompt-files.md)： コード生成やコードレビュー実行など、一般的なタスク用の再利用可能なプロンプトを定義。プロンプトファイルは直接チャットで実行できるスタンドアロンプロンプト。タスク実行(_何_をするか)を説明。

* [カスタムエージェント](/docs/copilot/customization/custom-agents.md)： チャット動作、使用できるツール、コードベースとのインタラクション方法を定義。各チャットプロンプトはエージェント境界内で実行され、すべてのリクエストにツールと命令を構成する必要なし。

> **ヒント**
>
> * 言語固有の命令を定義して各言語用のより正確なコード生成を取得。
> * 命令をワークスペースに保存してチーム間で簡単に共有。
> * 一般的なタスク用の再利用可能なプロンプトファイルを定義して時間節約とチームメンバーの素早いスタート支援。

## エディター AI 機能

エディターでコーディング中に、Copilot を使用してインライン提案を入力時に生成。エディターを離れずにインラインチャットを呼び出して質問し、Copilot から支援を取得。例えば、Copilot にメソッドまたは関数の単体テストを生成してもらえます。[インライン提案](/docs/copilot/ai-powered-suggestions.md)と[インラインチャット](/docs/copilot/chat/inline-chat.md)について詳しくご覧ください。

| アクション | 説明 |
|--------|-------------|
| インライン提案 | エディターで入力を開始してコーディングスタイルに合わせ、既存コードを考慮した[インライン提案](/docs/copilot/ai-powered-suggestions.md)を取得 |
| コードコメント | コードコメントに命令を書いてインライン提案プロンプトを提供。<br/>例： `# write a calculator class with methods for add, subtract, and multiply. Use static methods.` |
| `kb(inlinechat.start)` | エディターインラインチャットを開始してエディターから直接チャットリクエストを送信。自然言語を使用してチャット変数とスラッシュコマンドを参照してコンテキストを提供 |
| `kb(editor.action.rename)` | コード内のシンボル名変更時に AI 提案を取得 |
| コンテキストメニューアクション | エディターコンテキストメニューを使用してコード説明、テスト生成、コードレビューなど、一般的な AI アクションにアクセス。エディターを右クリックしてコンテキストメニューを開き、**Generate Code**を選択 |
| コードアクション (電球) | エディターのコードアクション (電球)を選択してコード内のリンティングまたはコンパイラエラーを修正 |

> **ヒント**
>
> * 意味のあるメソッドまたは関数名を使用してより速くインライン提案を取得。
> * コードブロック選択してインラインチャットプロンプトをスコープするか、ファイルまたはシンボルを添付して関連コンテキストを添付。
> * エディターコンテキストメニューオプションを使用してエディターから直接一般的な AI 駆動アクションにアクセス。

## ソースコントロールと問題

AI を使用して、コミットとプルリクエストの変更を分析して、コミットメッセージとプルリクエスト説明の提案を提供。

| アクション | 説明 |
|--------|-------------|
| `#changes` | 現在のソースコントロール変更をチャットプロンプトにコンテキストとして追加 |
| コンテキストとしてコミット | ソースコントロール履歴からコミットをチャットプロンプトにコンテキストとして追加 |
| コミットメッセージ | ソースコントロールコミット内の現在の変更用コミットメッセージを生成 |
| マージコンフリクト (実験的) | [AI で Git マージコンフリクト解決](/docs/sourcecontrol/overview#resolve-merge-conflicts-with-ai-experimental)の支援を取得 |
| プルリクエスト説明 | プルリクエスト内の変更に対応するプルリクエストタイトルと説明を生成 |
| `@github` | チャットで`@github`参加者を使用して、リポ全体の問題、プルリクエストなどについて質問。[利用可能な GitHub スキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)について詳しくご覧ください。<br/>例： `@github What are all of the open PRs assigned to me?`、`@github Show me the recent merged pr's from @dancing-mona` |

## コード レビュー (実験的)

AI を使用してコードブロックをすばやくレビューするか、ワークスペース内のコミットされていない変更をレビュー。レビューフィードバックはエディター内のコメントとして表示され、提案を適用できます。

| アクション | 説明 |
|--------|-------------|
| **Review Selection** _(Preview)_ | コードブロック選択して、エディターコンテキストメニューから**Generate Code**> **Review**を選択してすばやくレビューパス実施 |
| **Code Review** | ソースコントロールビュー内の**Code Review**ボタン選択して、すべてのコミットされていない変更のより深いレビュー実施 |

## 検索と設定

サーチビューでセマンティック検索結果を取得するか、設定エディターでの設定検索を支援。

| アクション | 説明 |
|--------|-------------|
| 設定検索 | 設定エディターにセマンティック検索結果を含める(`setting(workbench.settings.showAISearchToggle)`) |
| セマンティック検索 _(preview)_ | サーチビューにセマンティック検索結果を含める(`setting(search.searchView.semanticSearchBehavior)`) |

## テストを生成

VS Code はチャットのスラッシュコマンドを使用してコードベース内の関数とメソッド用テストを生成できます。スラッシュコマンドはチャットプロンプトで使用できる一般的なタスク用の省略記号。`/`に続けてコマンド名を入力してスラッシュコマンドを使用。

| アクション | 説明 |
|--------|-------------|
| `/tests` | エディターで選択されたメソッドと関数のすべて、または選択されたもののみのテストを生成。生成されたテストは既存テストファイルに追加されるか、新しいテストファイルが作成されます |
| `/setupTests` | コード用のテストフレームワーク設定支援を取得。関連するテストフレームワークの推奨、設定と構成のステップ、VS Code テスト拡張機能の提案を取得 |
| `/fixTestFailure` | テスト失敗修正方法の提案を Copilot から取得 |
| テストカバレッジ _(実験的)_ | テストでまだカバーされていない関数とメソッド用にテストを生成。[詳しくご覧ください](https://code.visualstudio.com/updates/v1_93#_generate-tests-based-on-test-coverage-experimental) |

> **ヒント**
>
> * 使用するテストフレームワークやライブラリの詳細を提供。

## デバッグと問題修正

Copilot を使用してコーディング問題を修正し、VS Code でのデバッグセッション構成と開始に支援を取得。

| アクション | 説明 |
|--------|-------------|
| `/fix` | コードブロック修正方法またはコンパイラもしくはリンティングエラー解決方法の提案を Copilot から取得。例えば、解決されていない Node.js パッケージ名を修正する支援など |
| `/fixTestFailure` | テスト失敗修正方法の提案を Copilot から取得 |
| `/startDebugging` _(実験的)_ | `launch.json`デバッグ構成ファイルを生成してチャットビューから[デバッグセッションを開始](/docs/copilot/guides/debug-with-copilot.md) |
| `copilot-debug`コマンド | [プログラムをデバッグ](/docs/copilot/guides/debug-with-copilot.md)するためのターミナルコマンド。実行コマンドの前置詞としてしてデバッグセッションを開始(例： `copilot-debug python foo.py`) |

> **ヒント**
>
> * 必要な修正タイプ(例：メモリー消費量またはパフォーマンス最適化)などの追加情報を提供。
> * コード内の問題修正提案を示す Copilot コードアクションをエディターで注視。

## 新しいプロジェクトをスキャフォルディング

Copilot はプロジェクト構造のスキャフォルディングを生成することでプロジェクトを作成、または要件に基づいたノートブックを生成するのに役立ちます。

| アクション | 説明 |
|--------|-------------|
| エージェント | [エージェント](/docs/copilot/agents/local-agents.md)を使用して自然言語プロンプトで新しいプロジェクトまたはファイルを作成。例： `Create a svelte web application to track my tasks` |
| `/new` | チャットビューで`/new`コマンドを使用して新しいプロジェクトまたは新しいファイルをスキャフォルディング。自然言語でプロジェクト/ファイルタイプの説明を行い、作成前にスキャフォルディング内容をプレビュー。<br/>例： `/new Express app using typescript and svelte` |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して要件に基づいて新しい Jupyter ノートブックを生成。ノートブックに含める内容を自然言語で説明。<br/>例： `/newNotebook get census data and preview key insights with Seaborn` |

## ターミナル

シェルコマンドについて支援を取得し、ターミナルでコマンド実行時のエラー解決方法を取得。

| アクション | 説明 |
|--------|-------------|
| `kb(inlinechat.start)` | ターミナルインラインチャットを開始してシェルコマンドとターミナルについて自然言語で質問。<br/>例： `how many cores on this machine?` |
| `@terminal` | チャットビューで`@terminal`参加者を使用して統合ターミナルやシェルコマンドについて質問。<br/>例： `@terminal list the 5 largest files in this workspace` |
| `@terminal /explain` | チャットビューで`/explain`コマンドを使用してターミナル項目を説明。<br/>例： `@terminal /explain top shell command` |

## Python とノートブック対応

チャットを使用して Native Python REPL と Jupyter ノートブックでの Python プログラミングタスク支援を取得できます。

| アクション | 説明 |
|--------|-------------|
| <i class="codicon codicon-sparkle"></i>生成<br/>`kb(inlinechat.start)` | ノートブックでインラインチャット開始してコードブロックまたはマークダウンブロック生成 |
| `#` | チャットプロンプトで Jupyter カーネルから変数を添付してより関連性の高い応答を取得 |
| Native REPL + `kb(inlinechat.start)` | Native Python REPL でインラインチャット開始して、生成されたコマンド実行 |
| `kb(workbench.action.chat.open)` | **チャットビュー**を開いてエージェント使用してノートブック編集を実施 |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して要件に基づいて新しい Jupyter ノートブック生成。ノートブックに含める内容を自然言語で説明。<br/>例： `/newNotebook get census data and preview key insights with Seaborn` |

## 次のステップ

* [チュートリアル: VS Code の AI 機能を始める](/docs/copilot/getting-started.md)

