---
ContentId: de6f9f68-7dd5-4de3-a210-3db57882384b
DateApproved: 3/9/2026
MetaDescription: GitHub Copilot in VS Code のクイックリファレンス。自律エージェント、マルチファイル編集、インライン提案、エンタープライズコントロールを含みます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilot in VS Code チートシート

GitHub Copilot in Visual Studio Code は、自律エージェント、インライン提案、チャット、スマートアクションを提供します。エージェントは複数のファイル全体で変更を計画、実装、および検証し、ローカル、バックグラウンド、またはクラウドで並列実行します。複数のAIモデルから選択し、MCPで外部ツールに接続し、チームのワークフローに合わせてエージェントをカスタマイズします。このチートシートで、すべての機能の概要をご確認ください。

> [!TIP]
> まだCopilot サブスクリプションがない場合、[Copilot Free プラン](https://github.com/github-copilot/signup)に登録して Copilot を無料で使用でき、インライン提案とチャットインタラクションの月単位の制限が適用されます。

## 重要なキーボードショートカット

* `kb(workbench.panel.chat)` - チャットビューを開く
* `kb(workbench.action.chat.startVoiceChat)` - チャットビューで音声チャットプロンプトを入力
* `kb(workbench.action.chat.newChat)` - チャットビューで新しいチャットセッションを開始
* `kb(workbench.action.chat.openAgent)` - チャットビューでエージェント使用に切り替え
* `kb(inlineChat.start)` - エディターまたはターミナルでインラインチャットを開始
* `kb(workbench.action.chat.startVoiceChat)` (長押し) - インライン音声チャットを開始
* `kb(editor.action.inlineSuggest.commit)` - インライン提案を承認するか、次の編集提案に移動
* `kb(editor.action.inlineSuggest.hide)` - インライン提案を非表示にする

## VS Code で AI にアクセス

* 自然言語を使ってチャット会話を開始
    * チャットビュー (`kb(workbench.action.chat.open)`): セカンダリサイドバーで継続的なチャット会話を実施
    * エディターまたはターミナルのインラインチャット (`kb(inlineChat.start)`): 作業中に質問を入力
    * クイックチャット (`kb(workbench.action.quickchat.toggle)`): 現在のタスクを離れずに簡単な質問を入力

* [エディター](/docs/copilot/ai-powered-suggestions.md)内の AI
    * インライン提案: 入力時に提案を取得し、`kb(editor.action.inlineSuggest.commit)`を押して提案を承認
    * エディットコンテキストメニューアクション: コードの説明やバグ修正、テスト生成、テキスト選択範囲のレビューなどの一般的なAIアクションにアクセス
    * コードアクション: エディターコードアクション (電球) を取得して、リント、コンパイラエラーを修正

* VS Code 全体の[スマートアクション](/docs/copilot/copilot-smart-actions.md)タスク固有
    * コミットメッセージ、プルリクエストタイトル、説明を生成
    * テストエラーを修正
    * セマンティックファイル検索提案

## VS Code のチャット体験

自然言語チャット会話を開始して、コーディングタスクについてサポートを受けます。例えば、コードブロックやプログラミングコンセプトの説明、コード片のリファクタリング、または新しい機能の実装をリクエストできます。[Copilot Chat](/docs/copilot/chat/copilot-chat.md)の使用に関する詳細情報を取得します。

| アクション | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.open)` | [チャットビュー](/docs/copilot/chat/copilot-chat.md)をセカンダリサイドバーで開きます。 |
| `kb(inlinechat.start)` | [インラインチャット](/docs/copilot/chat/inline-chat.md)を開始して、エディターまたはターミナルでチャットを開きます。 |
| `kb(workbench.action.quickchat.toggle)` | [クイックチャット](/docs/copilot/chat/copilot-chat.md)を開き、ワークフローを中断しません。 |
| `kb(workbench.action.chat.newChat)` | チャットビューで新しいチャットセッションを開始します。 |
| `kb(workbench.action.chat.toggleAgentMode)` | チャットビューで異なる[エージェント](/docs/copilot/customization/custom-agents.md)間で切り替え。 |
| `kb(workbench.action.chat.openModelPicker)` | モデルピッカーを表示してチャット用の[別のAIモデルを選択](/docs/copilot/customization/language-models.md)します。 |
| コンテキストウィンドウコントロール | チャット入力ボックスの視覚的インジケーター。[コンテキストウィンドウの使用方法](/docs/copilot/chat/copilot-chat-context.md#monitor-context-window-usage)を表示します。合計トークン数とカテゴリ別の内訳でホバーします。 |
| `Add Context...` | 異なるタイプの[コンテキストをチャットプロンプトに添付](/docs/copilot/chat/copilot-chat-context.md)します。 |
| `/` コマンド | 一般的なタスク用の[スラッシュコマンド](#slash-commands)を使用するか、[再利用可能なチャットプロンプト](/docs/copilot/customization/overview.md)を呼び出します。 |
| `#` メンション | 一般的なツールまたはチャット変数を参照して、プロンプト内で[コンテキストを提供](/docs/copilot/chat/copilot-chat-context.md)します。 |
| `@` メンション | [チャットパーティシパント](#chat-participants)を参照して、ドメイン固有のリクエストを処理します。 |
| 編集 (<i class="codicon codicon-pencil"></i>) | [前回のチャットプロンプトを編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)して、変更を元に戻します。 |
| 履歴 (<i class="codicon codicon-history"></i>) | チャットセッションの履歴にアクセスします。 |
| キューまたはステアリング | リクエストの実行中に[フォローアップメッセージを送信](/docs/copilot/chat/chat-sessions.md#send-messages-while-a-request-is-running)します。メッセージをキューイング、現在のリクエストをステアリング、または停止して即座に送信することを選択します。 |
| 音声 (<i class="codicon codicon-mic"></i>) | スピーチを使用してチャットプロンプトを入力します (音声チャット)。チャット応答は大音量で読み取られます。 |
| [KaTeX](https://katex.org) | チャット応答で数式をレンダリングします。`setting(chat.math.enabled)`で有効にします。数式を右クリックしてソース式をコピーします。 |
| [Mermaid](https://mermaid.js.org) | チャット応答で Mermaid 図をレンダリングします。`setting(mermaid-chat.enabled)`で有効にします。図を右クリックしてソースコードをコピーします。 |

> **ヒント**
>
> * `#` メンションを使用してチャットプロンプトに追加のコンテキストを追加します。
> * 具体的に、簡潔に、フォローアップ質問をして最高の結果を得ます。
> * 特定のタスクに適した組み込みエージェントまたはカスタムエージェントを選択します。

## プロンプトにコンテキストを追加

[チャットプロンプトにコンテキストを提供](/docs/copilot/chat/copilot-chat-context.md)して、より関連性の高い応答を取得します。ファイル、シンボル、エディター選択範囲、ソースコントロールコミット、テスト失敗などの異なるコンテキストタイプから選択します。

| アクション | 説明 |
|--------|-------------|
| **Add Context** | クイックピックを開いて、チャットプロンプトの関連コンテキストを選択します。ワークスペースファイル、シンボル、現在のエディター選択範囲、ターミナル選択範囲など、異なるコンテキストタイプから選択します。 |
| ドラッグ&ドロップファイル | エクスプローラーまたは検索ビューからファイルをドラッグ&ドロップするか、エディタータブをチャットビューにドラッグします。 |
| ドラッグ&ドロップフォルダ | フォルダーをチャットビューにドラッグ&ドロップして、その中のファイルを添付します。 |
| ドラッグ&ドロップ問題 | [問題]パネルからアイテムをドラッグ&ドロップします。 |
| `#<file\|folder\|symbol>` | `#`を入力してから、ファイル、フォルダー、またはシンボル名を入力して、チャットコンテキストとして追加します。 |
| `#` メンション | `#`を入力してから、[チャットツール](#chat-tools)を入力して、特定のコンテキストタイプまたはツールを追加します。 |

## チャットツール

チャットで[ツール](/docs/copilot/agents/agent-tools.md)を使用して、ユーザーリクエストを処理しながら専門的なタスクを実現します。このようなタスクの例には、ディレクトリ内のファイルをリストアップすること、ワークスペース内のファイルを編集すること、ターミナルコマンドを実行すること、ターミナルから出力を取得することなどがあります。

VS Code は組み込みツールを提供し、[MCPサーバー](/docs/copilot/customization/mcp-servers.md)と[拡張機能](/api/extension-guides/ai/tools.md)からのツールでチャットを拡張できます。[ツールのタイプ](/docs/copilot/agents/agent-tools.md#types-of-tools)の詳細を確認してください。

次の表は VS Code 組み込みツールを一覧表示します。

| チャット変数/ツール | 説明 |
|--------|-------------|
| `#changes` | ソースコントロール変更のリスト。 |
| `#codebase` | 現在のワークスペースでコード検索を実行して、チャットプロンプトの関連コンテキストを自動的に見つけます。 |
| `#createAndRunTask` | ワークスペースで新しい[タスク](/docs/debugtest/tasks.md)を作成して実行します。 |
| `#createDirectory` | ワークスペースに新しいディレクトリを作成します。 |
| `#createFile` | ワークスペースに新しいファイルを作成します。 |
| `#edit` (ツールセット) | ワークスペースで変更を有効にします。 |
| `#editFiles` | ワークスペース内のファイルに編集を適用します。 |
| `#editNotebook` | ノートブックに編集を加えます。 |
| `#extensions` | VS Code 拡張機能を検索して質問します。例: "Python #extensions?"で始める方法 |
| `#fetch` | 指定されたウェブページからコンテンツを取得します。例: "Summarize #fetch code.visualstudio.com/updates." |
| `#fileSearch` | グロブパターンを使用してワークスペース内のファイルを検索し、パスを返します。 |
| `#getNotebookSummary` | ノートブックセルのリストとその詳細を取得します。 |
| `#getProjectSetupInfo` | 異なるタイプのプロジェクトをスキャフォールディングするための指示と設定を提供します。 |
| `#getTaskOutput` | ワークスペースで[タスク](/docs/debugtest/tasks.md)を実行する出力を取得します。 |
| `#getTerminalOutput` | ワークスペースでターミナルコマンドを実行する出力を取得します。 |
| `#githubRepo` | GitHub リポジトリでコード検索を実行します。例: "what is a global snippet #githubRepo microsoft/vscode." |
| `#installExtension` | VS Code 拡張機能をインストールします。 |
| `#listDirectory` | ワークスペース内のディレクトリ内のファイル一覧を表示します。 |
| `#new` | デバッグと実行の設定で事前に設定された新しい VS Code ワークスペースをスキャフォールディングします。 |
| `#newJupyterNotebook` | 説明を指定して新しい Jupyter ノートブックをスキャフォールディングします。 |
| `#newWorkspace` | 新しいワークスペースを作成します。 |
| `#openSimpleBrowser` | [統合ブラウザー](/docs/debugtest/integrated-browser.md)を開き、ローカルにデプロイされたウェブアプリをプレビューします。 |
| `#browser` (ツールセット) | _(実験的)_ [統合ブラウザー](/docs/debugtest/integrated-browser.md)内のページと対話する: ナビゲート、ページコンテンツを読み取る、スクリーンショット、クリック、入力、ホバー、ドラッグ、ダイアログを処理します。`setting(workbench.browser.enableChatTools)`で有効にします。 |
| `#problems` | ワークスペースの問題と**問題**パネルからの問題をコンテキストとして追加します。コードを修正またはデバッグするときに役に立ちます。 |
| `#readFile` | ワークスペース内のファイルのコンテンツを読み込みます。 |
| `#readNotebookCellOutput` | ノートブックセル実行の出力を読み込みます。 |
| `#runCell` | ノートブックセルを実行します。 |
| `#runCommands` (ツールセット) | ターミナルでコマンドを実行して出力を読み込みます。 |
| `#runInTerminal` | 統合ターミナルで shell コマンドを実行します。 |
| `#runNotebooks` (ツールセット) | ノートブックセルを実行します。 |
| `#runTask` | ワークスペースで既存の[タスク](/docs/debugtest/tasks.md)を実行します。 |
| `#runTasks` (ツールセット) | ワークスペースで[タスク](/docs/debugtest/tasks.md)を実行して出力を読み込みます。 |
| `#runSubagent` | 独立した[サブエージェントコンテキスト](/docs/copilot/agents/subagents.md)でタスクを実行します。メインエージェントスレッドのコンテキスト管理を改善するのに役に立ちます。 |
| `#runTests` | ワークスペースで[単体テスト](/docs/debugtest/testing.md)を実行します。 |
| `#runVscodeCommand` | VS Code コマンドを実行します。例: "Enable zen mode #runVscodeCommand." |
| `#search` (ツールセット) | 現在のワークスペースでファイルを検索できます。 |
| `#searchResults` | 検索ビューから検索結果を取得します。 |
| `#selection` | 現在のエディター選択範囲を取得 (テキストが選択された場合のみ利用可能)。 |
| `#terminalLastCommand` | 最後に実行したターミナルコマンドとその出力を取得します。 |
| `#terminalSelection` | 現在のターミナル選択範囲を取得します。 |
| `#testFailure` | 単体テスト失敗情報を取得します。[テスト](/docs/debugtest/testing.md)を実行および診断するときに役に立ちます。 |
| `#textSearch` | ファイル内のテキストを検索します。 |
| `#todos` | チャットリクエストの実装と進捗を追跡する (todo リスト)。 |
| `#usages` | 「すべての参照を検索」、「実装を検索」、および「定義へ移動」の組み合わせ。 |
| `#VSCodeAPI` | VS Code 機能と拡張機能開発について質問します。 |

## スラッシュコマンド

スラッシュコマンドは、チャット内の特定の機能へのショートカットです。これらを使用して、問題の修正、テストの生成、コードの説明など、アクションを迅速に実行できます。

| スラッシュコマンド | 説明 |
|---------------|-------------|
| `/doc` | エディターのインラインチャットからコードドキュメンテーションコメントを生成します。 |
| `/explain` | コードブロック、ファイル、またはプログラミングコンセプトを説明します。 |
| `/fix` | コードブロックを修正するか、コンパイラーまたはリント エラーを解決するよう要求します。 |
| `/tests` | エディター内のすべての、またはそれぞれの選択されたメソッドと関数のテストを生成します。 |
| `/setupTests` | コードのテストフレームワークをセットアップするのに役に立つ情報を取得します。関連するテストフレームワークの推奨事項、セットアップと設定の手順、VS Code テスト拡張機能の提案を取得します。 |
| `/clear` | チャットビューで新しいチャットセッションを開始します。 |
| `/compact` | 会話コンテキストを要約してコンパクトにします。会話がモデルのコンテキストウィンドウに対して長すぎる場合に役に立ちます。 |
| `/fork` | 現在のチャットセッションを新しい独立したセッションにフォークして、完全な会話履歴を継承します。詳細は[チャットセッションのフォーク](/docs/copilot/chat/chat-sessions.md#fork-a-chat-session)を確認してください。 |
| `/debug` | チャットデバッグビューを表示して、[トラブルシューティング用のチャットログを検査](/docs/copilot/troubleshooting.md)します。 |
| `/new` | 新しい VS Code ワークスペースまたはファイルをスキャフォールディングします。必要なプロジェクト/ファイルのタイプを説明するのに自然言語を使用し、作成前にスキャフォールディングされたコンテンツをプレビューします。 |
| `/newNotebook` | 要件に基づいて新しい Jupyter ノートブックをスキャフォールディングします。ノートブックに含める内容を説明するのに自然言語を使用します。 |
| `/init` | プロジェクト構造とコーディングパターンに基づいて、ワークスペース命令 (`copilot-instructions.md`または`AGENTS.md`) を生成又は更新します。 |
| `/plan` | 複雑なコーディングタスクの詳細な実装計画を作成します。要件を調査し、明確化する質問をし、ステップ、検証、決定を含む構造化計画を生成します。 |
| `/search` | 検索ビュー用の検索クエリを生成します。検索する内容を説明するのに自然言語を使用します。 |
| `/startDebugging` | `launch.json`デバッグ設定ファイルを生成し、チャットビューからデバッグセッションを開始します。 |
| `/agents` | [カスタムエージェント](/docs/copilot/customization/custom-agents.md)を設定します。 |
| `/hooks` | [フック](/docs/copilot/customization/hooks.md)を設定します。 |
| `/instructions` | [カスタム命令](/docs/copilot/customization/custom-instructions.md)を設定します。 |
| `/prompts` | [再利用可能なプロンプトファイル](/docs/copilot/customization/prompt-files.md)を設定します。 |
| `/skills` | [エージェントスキル](/docs/copilot/customization/agent-skills.md)を設定します。 |
| `/create-prompt` | エージェントモードで AI の支援を使用して、[プロンプトファイル](/docs/copilot/customization/prompt-files.md)を生成します。 |
| `/create-instruction` | エージェントモードで AI の支援を使用して、[命令ファイル](/docs/copilot/customization/custom-instructions.md)を生成します。 |
| `/create-skill` | エージェントモードで AI の支援を使用して、[エージェントスキル](/docs/copilot/customization/agent-skills.md)を生成します。 |
| `/create-agent` | エージェントモードで AI の支援を使用して、[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を生成します。 |
| `/create-hook` | エージェントモードで AI の支援を使用して[フック](/docs/copilot/customization/hooks.md)設定を生成します。 |
| `/yolo`<br/>`/autoApprove` | すべてのツール呼び出しの[グローバル自動承認](/docs/copilot/agents/agent-tools.md#can-i-automatically-approve-all-tools-and-terminal-commands)を有効にします (`setting(chat.tools.global.autoApprove)`)。初回時に警告ダイアログが表示されます。 |
| `/disableYolo`<br/>`/disableAutoApprove` | すべてのツール呼び出しの[グローバル自動承認](/docs/copilot/agents/agent-tools.md#can-i-automatically-approve-all-tools-and-terminal-commands)を無効にします。 |
| `/<skill name>` | チャットで[エージェントスキル](/docs/copilot/customization/agent-skills.md)を実行します。例えば、`webapp-testing.md`という名前のスキルファイルがある場合、`/webapp-testing`と入力して実行できます。 |
| `/<prompt name>` | チャットで[再利用可能なプロンプト](/docs/copilot/customization/prompt-files.md)を実行します。 |

## チャットパーティシパント

チャットパーティシパントを使用して、チャット内のドメイン固有のリクエストを処理します。チャットパーティシパントは`@`が接頭辞で、特定のトピックについて質問するために使用できます。VS Code は`@github`、`@terminal`、`@vscode`などの組み込みチャットパーティシパントを提供し、拡張機能はパーティシパントを追加で提供できます。

| チャットパーティシパント | 説明 |
|------------------|-------------|
| `@github` | `@github`パーティシパントを使用して、GitHub リポジトリ、問題、プルリクエストなどについて質問します。[利用可能な GitHub スキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)に関する詳細情報を取得します。<br/>例: `@github What are all of the open PRs assigned to me?`、`@github Show me the recent merged PRs from @dancing-mona` |
| `@terminal` | `@terminal`パーティシパントを使用して、統合ターミナルまたは shell コマンドについて質問します。<br/>例: `@terminal list the 5 largest files in this workspace` |
| `@vscode` | `@vscode`パーティシパントを使用して、VS Code 機能、設定、VS Code 拡張機能 API について質問します。<br/>例: `@vscode how to enable word wrapping?` |

## エージェントを使用

[エージェント](/docs/copilot/agents/local-agents.md)を使用する場合、自然言語を使用してハイレベルなタスクを指定し、AI が自律的にリクエストについて推論し、必要な作業を計画し、コードベースに変更を適用できるようにします。エージェントは、指定したタスクを実現するためにコード編集とツール呼び出しの組み合わせを使用します。リクエストを処理する際に、編集とツールの結果を監視し、発生する問題を解決するために反復します。

| アクション | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.openAgent)` | チャットビューでエージェント使用に切り替え |
| ツール (<i class="codicon codicon-tools"></i>) | エージェント使用時に利用可能なツールを設定します。組み込みツール、MCPサーバー、拡張機能提供のツールから選択します。 |
| 権限レベル | 現在のセッションの[権限レベル](/docs/copilot/agents/agent-tools.md#permission-levels)を選択: **デフォルト承認**、**承認をバイパス**、または**オートパイロット** (プレビュー)。ツール承認の処理方法を制御します。 |
| ツールを自動承認 | エージェント使用時にすべてのツールの[自動承認](/docs/copilot/agents/agent-tools.md#auto-approve-all-tools)を有効にします (`setting(chat.tools.autoApprove)`)。 |
| ターミナルコマンドを自動承認 | エージェント使用時に[ターミナルコマンドの自動承認](/docs/copilot/agents/agent-tools.md#automatically-approve-terminal-commands)を有効にします (`setting(chat.tools.terminal.autoApprove)`)。 |
| MCP | エージェント機能とツールを拡張するために[MCPサーバー](/docs/copilot/customization/mcp-servers.md)を設定します。 |
| [サードパーティエージェント](/docs/copilot/agents/third-party-agents.md) | Claude Agent (プレビュー) や OpenAI Codex などの外部プロバイダーのエージェントを Copilot サブスクリプションで使用します。 |
| Claude Agent _(プレビュー)_ | Anthropic の Claude Agent SDK で実装された Claude Agent セッションを開始します。高度なワークフロー用に`/agents`、`/hooks`、`/memory`スラッシュコマンドを使用します。 |

> **ヒント**
>
> * エージェント使用時に追加のツールを追加して、その機能を拡張します。
> * カスタムエージェントを設定して、エージェントの操作方法を定義します。例えば、読み取り専用の計画モードを実装します。
> * カスタム命令を定義して、エージェントがコードを生成および構造化する方法をガイドします。
> * Claude Code や OpenAI Codex などのサードパーティエージェントを試して、別のエージェント型コーディング体験を利用してください。

## 計画

VS Code チャットの[計画エージェント](/docs/copilot/agents/planning.md)を使用して、複雑なコーディングタスクを開始する前に詳細な実装計画を作成します。承認した計画を実装エージェントに引き継ぎてコーディングを開始します。

| アクション | 説明 |
|--------|-------------|
| 計画エージェント | エージェントドロップダウンから**計画**エージェントを選択するか、`/plan`スラッシュコマンドを使用して、複雑なコーディングタスクの詳細な実装計画を作成します。 |
| Todo リスト | 複雑なタスクの進捗を追跡する todo リストを表示します。`setting(chat.tools.todos.showWidget`設定でこれを有効にしてください。 |
| [メモリー](/docs/copilot/agents/memory.md) | エージェントは会話全体で永続的なメモを保存および回想します。`setting(github.copilot.chat.tools.memory.enabled)`設定で有効または無効にします。**チャット: メモリーファイルを表示**コマンドを使用して保存されたメモリーを表示します。 |

## チャット体験のカスタマイズ

チャット体験をカスタマイズして、コーディングスタイル、ツール、開発者ワークフローに合わせた応答を生成します。VS Code でチャット体験をカスタマイズする方法はいくつかあります。

* [カスタム命令](/docs/copilot/customization/custom-instructions.md): コード生成、コードレビュー、コミットメッセージ生成などのタスクについて、共通のガイドラインまたはルールを定義します。カスタム命令は、AI が操作すべき条件を説明します (_タスクはどのように_実行すべきか)。

* [再利用可能なプロンプトファイル](/docs/copilot/customization/prompt-files.md): コード生成やコードレビュー実行などの一般的なタスク用に、再利用可能なプロンプトを定義します。プロンプトファイルはスタンドアロンプロンプトで、チャットで直接実行できます。これらは実行するべきタスクを説明します (_何を_実行すべきか)。

* [カスタムエージェント](/docs/copilot/customization/custom-agents.md): チャットの操作方法、使用できるツール、コードベースとの相互作用方法を定義します。各チャットプロンプトはエージェントの境界内で実行され、すべてのリクエストに対してツールと命令を設定する必要がありません。

> **ヒント**
>
> * 言語固有の命令を定義して、各言語の生成されたコードの精度を向上させます。
> * 指示をワークスペースに保存して、チームと簡単に共有します。
> * 一般的なタスク用に再利用可能なプロンプトファイルを定義して、時間を節約し、チームメンバーへの迅速なスタートを助成します。

## エディター AI 機能

エディターでコーディングを行う際、入力しながら Copilot を使用してインライン提案を生成できます。インラインチャットを呼び出して、Copilot に質問をしながらコーディングの流れを維持できます。例えば、関数またはメソッドの単体テストを生成するように Copilot に要求します。[インライン提案](/docs/copilot/ai-powered-suggestions.md)と[インラインチャット](/docs/copilot/chat/inline-chat.md)に関する詳細情報を取得します。

| アクション | 説明 |
|--------|-------------|
| インライン提案 | エディターで入力を開始して、コーディングスタイルに合致し、既存のコードを考慮した[インライン提案](/docs/copilot/ai-powered-suggestions.md)を取得します。 |
| コードコメント | コードコメントに指示を書くことで、インライン提案プロンプトを提供します。<br/>例: `# write a calculator class with methods for add, subtract, and multiply. Use static methods.` |
| `kb(inlinechat.start)` | エディターからチャットリクエストを直接送信するために、エディターのインラインチャットを開始します。自然言語を使用し、チャット変数とスラッシュコマンド参照してコンテキストを提供します。 |
| `kb(editor.action.rename)` | コード内のシンボルをリネームするときに、AI による提案を取得します。 |
| コンテキストメニューアクション | エディターコンテキストメニューを使用して、コードの説明、テスト生成、コードレビューなどの一般的なAIアクションにアクセスします。エディターを右クリックしてコンテキストメニューを開き、**コード生成**を選択します。 |
| コードアクション (電球) | エディターでコードアクション (電球) を選択して、リント、コンパイラーエラーを修正します。 |

> **ヒント**
>
> * 有意義なメソッド名また関数名を使用して、より早くインライン提案を取得します。
> * コードブロックを選択して、インラインチャットプロンプトの範囲を設定するか、ファイルまたはシンボルを添付して関連コンテキストを添付します。
> * エディターコンテキストメニューオプションを使用して、エディター内から共通のAI駆動アクションに直接アクセスします。

## ソースコントロールと問題

AI を使用してコミット、プルリクエストの変更を分析し、コミットメッセージ、プルリクエスト説明の提案を提供します。

| アクション | 説明 |
|--------|-------------|
| `#changes` | 現在のソースコントロール変更をチャットプロンプトのコンテキストとして追加します。 |
| コンテキストとしてコミット | ソースコントロール履歴からコミットをチャットプロンプトのコンテキストとして追加します。 |
| コミットメッセージ | ソースコントロールコミット内の現在の変更のコミットメッセージを生成します。 |
| マージコンフリクト (実験的) | AI を使用して[Git マージコンフリクト](/docs/sourcecontrol/overview#resolve-merge-conflicts-with-ai-experimental)を解決するのに役に立つ情報を取得します。 |
| プルリクエスト説明 | プルリクエストの変更に対応するプルリクエストタイトルと説明を生成します。 |
| `@github` | チャットで`@github`パーティシパントを使用して、問題、プルリクエスト、およびリポジトリ全体についての質問をします。[利用可能な GitHub スキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)に関する詳細情報を取得します。<br/>例: `@github What are all of the open PRs assigned to me?`、`@github Show me the recent merged pr's from @dancing-mona`  |

## コードをレビュー (実験的)

AI を使用してコードブロックのクイックレビューパスを実施するか、ワークスペース内のコミット未実施の変更をレビューします。レビューフィードバックはエディターにコメントとして表示され、提案を適用できます。

| アクション | 説明 |
|--------|-------------|
| **選択範囲をレビュー** _(プレビュー)_ | コードブロックを選択し、クイックレビューを実施するためにエディターコンテキストメニューから**コード生成** > **レビュー**を選択します。 |
| **コードレビュー** | ソースコントロールビューで**コードレビュー**ボタンを選択して、コミット未実施のすべての変更のより詳細なレビューを実施します。 |

## 検索と設定

検索ビューで意味的に関連性の高い検索結果を取得するか、設定エディターで設定検索について役に立つ情報を取得します。

| アクション | 説明 |
|--------|-------------|
| 設定検索 | 設定エディターに意味的検索結果を含めます (`setting(workbench.settings.showAISearchToggle)`)。 |
| セマンティック検索 _(プレビュー)_ | 検索ビューに意味的検索結果を含めます (`setting(search.searchView.semanticSearchBehavior)`)。 |

## テストを生成

VS Code は、チャット内のスラッシュコマンドを使用して、コードベース内の関数およびメソッドのテストを生成できます。スラッシュコマンドは、チャットプロンプトで使用できる一般的なタスク用の短記法です。スラッシュコマンドを使用するには、`/`の後にコマンド名を入力してください。

| アクション | 説明 |
|--------|-------------|
| `/tests` | エディター内のすべての、またはそれぞれの選択されたメソッドと関数のテストを生成します。生成されたテストは既存のテストファイルに追加されるか、新しいテストファイルが作成されます。  |
| `/setupTests` | コードのテストフレームワークをセットアップするのに役に立つ情報を取得します。関連するテストフレームワークの推奨事項、セットアップと設定の手順、VS Code テスト拡張機能の提案を取得します。   |
| `/fixTestFailure` | 失敗したテストを修正する方法について、Copilot に提案をリクエストします。 |
| テストカバレッジ _(実験的)_ | まだテストにカバーされていない関数およびメソッドのテストを生成します。[詳細情報](https://code.visualstudio.com/updates/v1_93#_generate-tests-based-on-test-coverage-experimental)を取得します。 |

> **ヒント**
>
> * 使用するテストフレームワークまたはライブラリについての詳細を提供します。

## デバッグと問題修正

Copilot を使用してコーディング問題の修正と VS Code でのデバッグセッションの設定および開始の支援を取得します。

| アクション | 説明 |
|--------|-------------|
| `/fix` | コードブロックを修正する方法または Node.js パッケージ名の未解決など、コンパイラーまたはリント エラーを解決する方法について、Copilot に提案をリクエストします。 |
| `/fixTestFailure` | 失敗したテストを修正する方法について、Copilot に提案をリクエストします。 |
| `/startDebugging` _(実験的)_ | `launch.json`デバッグ設定ファイルを生成し、[チャットビューからデバッグセッションを開始](/docs/copilot/guides/debug-with-copilot.md)します。 |
| `copilot-debug` コマンド | [プログラムをデバッグ](/docs/copilot/guides/debug-with-copilot.md)するのに役に立つターミナルコマンド。実行コマンドを接頭辞として付けて、そのデバッグセッションを開始します (例えば、`copilot-debug python foo.py`)。 |

> **ヒント**
>
> * メモリー消費かパフォーマンスの最適化など、必要な修正のタイプについての追加情報を提供します。
> * コード内の問題修正の提案をしているエディターで Copilot コードアクションに注意します。

## 新しいプロジェクトをスキャフォールディング

Copilot は、プロジェクト構造のスキャフォルディングを生成するか、要件に基づいてノートブックを生成することで、新しいプロジェクトを作成するのに役に立つ情報を提供できます。

| アクション | 説明 |
|--------|-------------|
| エージェント | [エージェント](/docs/copilot/agents/local-agents.md)を使用し、自然言語プロンプトを使用して新しいプロジェクトまたはファイルを作成します。例え: `Create a svelte web application to track my tasks`。 |
| `/new` | チャットビューで`/new`コマンドを使用して、新しいプロジェクトまたは新しいファイルをスキャフォールディングします。必要なプロジェクト/ファイルのタイプを説明するのに自然言語を使用し、作成前にスキャフォールディングされたコンテンツをプレビューします。<br/>例: `/new Express app using typescript and svelte` |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して、要件に基づいて新しい Jupyter ノートブックを生成します。ノートブックに含める内容を説明するのに自然言語を使用します。<br/>例: `/newNotebook get census data and preview key insights with Seaborn`。 |

## ターミナル

シェルコマンドについてのヘルプおよびターミナルでコマンド実行時のエラー解決方法を取得します。

| アクション | 説明 |
|--------|-------------|
| `kb(inlinechat.start)` | ターミナルのインラインチャットを開始して、シェルコマンドおよびターミナルについての質問をするのに自然言語を使用します。<br/>例: `how many cores on this machine?` |
| `@terminal` | チャットビューで`@terminal`パーティシパントを使用して、統合ターミナルまたは shell コマンドについて質問します。<br/>例: `@terminal list the 5 largest files in this workspace` |
| `@terminal /explain` | チャットビューで`/explain`コマンドを使用してターミナルからのものを説明します。<br/>例: `@terminal /explain top shell command` |

## Python およびノートブックサポート

ネイティブ Python REPL および Jupyter ノートブックで Python プログラミングタスクについてサポートを取得するためにチャットを使用できます。

| アクション | 説明 |
|--------|-------------|
| <i class="codicon codicon-sparkle"></i> 生成<br/>`kb(inlinechat.start)` | ノートブックのインラインチャットを開始して、코드블록または Markdown ブロックを生成します。 |
| `#` | チャットプロンプトに Jupyter カーネルから変数を添付して、より関連性の高い応答を取得します。 |
| ネイティブ REPL + `kb(inlinechat.start)` | ネイティブ Python REPL でインラインチャットを開始し、生成されたコマンドを実行します。 |
| `kb(workbench.action.chat.open)` | **チャットビュー**を開き、エージェントを使用してノートブック編集を実施します。 |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して、要件に基づいて新しい Jupyter ノートブックを生成します。ノートブックに含める内容を説明するのに自然言語を使用します。<br/>例: `/newNotebook get census data and preview key insights with Seaborn`。 |

## 次のステップ

* [チュートリアル: VS Code の AI 機能の使い方](/docs/copilot/getting-started.md)

