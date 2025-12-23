---
ContentId: de6f9f68-7dd5-4de3-a210-3db57882384b
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeのAI機能の概要をすばやく確認できます。GitHub Copilotは、より速く、より少ない労力でコードを書けるようにするAI搭載機能を提供します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeのGitHub Copilotチートシート

Visual Studio CodeのGitHub Copilotは、より速く、より少ない労力でコードを書けるようにするAI搭載機能を提供します。このチートシートでは、Visual Studio CodeのGitHub Copilotの機能をすばやく概観できます。

> [!TIP]
> まだCopilotサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップすることでCopilotを無料で利用でき、インライン提案とチャットのやり取りに月間上限が適用されます。

## 主要なキーボードショートカット

* `kb(workbench.panel.chat)` - チャットビューを開く
* `kb(workbench.action.chat.startVoiceChat)` - チャットビューで音声チャットのプロンプトを入力する
* `kb(workbench.action.chat.newChat)` - チャットビューで新しいチャットセッションを開始する
* `kb(workbench.action.chat.openAgent)` - チャットビューでエージェントの使用に切り替える
* `kb(inlineChat.start)` - エディターまたはターミナルでインラインチャットを開始する
* `kb(workbench.action.chat.startVoiceChat)` (hold) - インライン音声チャットを開始する
* `kb(editor.action.inlineSuggest.commit)` - インライン提案を受け入れる、または次の編集提案に移動する
* `kb(editor.action.inlineSuggest.hide)` - インライン提案を閉じる

## VS CodeでAIにアクセスする

* 自然言語を使ってチャット会話を開始する
    * チャットビュー (`kb(workbench.action.chat.open)`): セカンダリ サイド バーで継続的なチャット会話を維持する
    * エディターまたはターミナルのインラインチャット (`kb(inlineChat.start)`): 作業の流れを止めずに質問する
    * クイックチャット (`kb(workbench.action.quickchat.toggle)`): 現在のタスクを離れずに素早く質問する

* [エディター](/docs/copilot/ai-powered-suggestions.md)のAI
    * インライン提案: 入力に応じて提案を取得し、`kb(editor.action.inlineSuggest.commit)`を押して提案を受け入れる
    * 編集コンテキスト メニューのアクション: コードの説明や修正、テストの生成、テキスト選択範囲のレビューなど、一般的なAIアクションにアクセスする
    * コードアクション: エディターのコードアクション(電球)を取得して、lintやコンパイラーエラーを修正する

* VS Code全体のタスク固有の[スマートアクション](/docs/copilot/copilot-smart-actions.md)
    * コミットメッセージ、プルリクエストのタイトルと説明を生成する
    * テストエラーを修正する
    * セマンティックなファイル検索の提案

## VS Codeでのチャット体験

自然言語のチャット会話を開始して、コーディング作業の支援を受けます。たとえば、コードブロックやプログラミング概念の説明、コードのリファクタリング、新機能の実装などを依頼できます。[Copilot Chat](/docs/copilot/chat/copilot-chat.md)の利用方法について詳しくは、ドキュメントを参照してください。

| 操作 | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.open)` | セカンダリ サイド バーで[チャットビュー](/docs/copilot/chat/copilot-chat.md)を開きます。 |
| `kb(inlinechat.start)` | [インラインチャット](/docs/copilot/chat/inline-chat.md)を開始し、エディターまたはターミナルでチャットを開きます。 |
| `kb(workbench.action.quickchat.toggle)` | ワークフローを中断せずに[クイックチャット](/docs/copilot/chat/copilot-chat.md)を開きます。 |
| `kb(workbench.action.chat.newChat)` | チャットビューで新しいチャットセッションを開始します。 |
| `kb(workbench.action.chat.toggleAgentMode)` | チャットビューで異なる[エージェント](/docs/copilot/customization/custom-agents.md)を切り替えます。 |
| `kb(workbench.action.chat.openModelPicker)` | モデル ピッカーを表示して、チャットに使用する[別のAIモデル](/docs/copilot/customization/language-models.md)を選択します。 |
| `Add Context...` | さまざまな種類の[コンテキストをチャットプロンプトに追加](/docs/copilot/chat/copilot-chat-context.md)します。 |
| `/`-command | 一般的なタスクに[スラッシュコマンド](#slash-commands)を使用する、または[再利用可能なチャットプロンプト](/docs/copilot/customization/overview.md)を呼び出します。 |
| `#`-mention | 一般的なツールやチャット変数を参照して、プロンプト内で[コンテキストを提供](/docs/copilot/chat/copilot-chat-context.md)します。 |
| `@`-mention | [チャット参加者](#chat-participants)を参照して、ドメイン固有の要求を処理します。 |
| Edit (<i class="codicon codicon-pencil"></i>) | [以前のチャットプロンプトを編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)して変更を元に戻します。 |
| History (<i class="codicon codicon-history"></i>) | チャットセッションの履歴にアクセスします。 |
| Voice (<i class="codicon codicon-mic"></i>) | 音声(ボイスチャット)を使用してチャットプロンプトを入力します。チャット応答は音声で読み上げられます。 |
| [KaTeX](https://katex.org) | チャット応答で数式をレンダリングします。`setting(chat.math.enabled)`で有効化します。数式を右クリックしてソース式をコピーします。 |

> **ヒント**
>
> * `#`-mentionを使って、チャットプロンプトにより多くのコンテキストを追加します。
> * `/`コマンドと`@`参加者を使って、より正確で関連性の高い回答を得ます。
> * 具体的に、シンプルにし、最適な結果を得るために追加の質問をします。
> * ニーズに合ったエージェントを選択します: Ask、Edit、Agent、またはカスタム エージェントの作成。

## プロンプトにコンテキストを追加する

[チャットプロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)することで、より関連性の高い応答を得られます。ファイル、シンボル、エディターの選択範囲、ソース コントロールのコミット、テスト失敗など、さまざまなコンテキスト タイプから選択できます。

| 操作 | 説明 |
|--------|-------------|
| **Add Context** | クイック ピックを開いて、チャットプロンプトに関連するコンテキストを選択します。ワークスペース ファイル、シンボル、現在のエディターの選択範囲、ターミナルの選択範囲など、さまざまなコンテキスト タイプから選択できます。 |
| ファイルをドラッグ & ドロップ | エクスプローラーまたは検索ビューからファイルをドラッグ & ドロップするか、エディターのタブをチャットビューにドラッグします。 |
| フォルダーをドラッグ & ドロップ | フォルダーをチャットビューにドラッグ & ドロップして、その中のファイルを添付します。 |
| 問題をドラッグ & ドロップ | 問題パネルの項目をドラッグ & ドロップします。 |
| `#<file\|folder\|symbol>` | `#`に続けてファイル名、フォルダー名、またはシンボル名を入力し、チャット コンテキストとして追加します。 |
| `#`-mention | `#`に続けて[チャットツール](#chat-tools)を入力し、特定のコンテキスト タイプまたはツールを追加します。 |

## チャットツール

チャットで[ツール](/docs/copilot/chat/chat-tools.md)を使用すると、ユーザー要求を処理しながら特定のタスクを実行できます。例として、ディレクトリ内のファイル一覧表示、ワークスペース内のファイル編集、ターミナル コマンドの実行、ターミナル出力の取得などがあります。

VS Codeには組み込みツールが用意されており、[MCPサーバー](/docs/copilot/customization/mcp-servers.md)や[拡張機能](/api/extension-guides/ai/tools.md)のツールでチャットを拡張できます。[ツールの種類](/docs/copilot/chat/chat-tools.md#types-of-tools)について詳しく学べます。

次の表は、VS Codeの組み込みツールを示しています。

| チャット変数/ツール | 説明 |
|--------|-------------|
| `#changes` | List of source control changes. |
| `#codebase` | Perform a code search in the current workspace to automatically find relevant context for the chat prompt. |
| `#createAndRunTask` | Create and run a new [task](/docs/debugtest/tasks.md) in the workspace. |
| `#createDirectory` | Create a new directory in the workspace. |
| `#createFile` | Create a new file in the workspace. |
| `#edit` (tool set) | Enable modifications in the workspace. |
| `#editFiles` | Apply edits to files in the workspace. |
| `#editNotebook` | Make edits to a notebook. |
| `#extensions` | Search for and ask about VS Code extensions. For example, "how to get started with Python #extensions?" |
| `#fetch` | Fetch the content from a given web page. For example, "Summarize #fetch code.visualstudio.com/updates." |
| `#fileSearch` | Search for files in the workspace by using glob patterns and returns their path. |
| `#getNotebookSummary` | Get the list of notebook cells and their details. |
| `#getProjectSetupInfo` | Provide instructions and configuration for scaffolding different types of projects. |
| `#getTaskOutput` | Get the output from running a [task](/docs/debugtest/tasks.md) in the workspace. |
| `#getTerminalOutput` | Get the output from running a terminal command in the workspace. |
| `#githubRepo` | Perform a code search in a GitHub repo. For example, "what is a global snippet #githubRepo microsoft/vscode." |
| `#installExtension` | Install a VS Code extension. |
| `#listDirectory` | List files in a directory in the workspace. |
| `#new` | Scaffold a new VS Code workspace, preconfigured with debug and run configurations. |
| `#newJupyterNotebook` | Scaffold a new Jupyter notebook given a description. |
| `#newWorkspace` | Create a new workspace. |
| `#openSimpleBrowser` | Open the built-in Simple Browser and preview a locally-deployed web app. |
| `#problems` | Add workspace issues and problems from the **Problems** panel as context. Useful while fixing code or debugging. |
| `#readFile` | Read the content of a file in the workspace. |
| `#readNotebookCellOutput` | Read the output from a notebook cell execution. |
| `#runCell` | Run a notebook cell. |
| `#runCommands` (tool set) | Enable running commands in the terminal and reading the output. |
| `#runInTerminal` | Run a shell command in the integrated terminal. |
| `#runNotebooks` (tool set) | Enable running notebook cells. |
| `#runTask` | Run an existing [task](/docs/debugtest/tasks.md) in the workspace. |
| `#runTasks` (tool set) | Enable running [tasks](/docs/debugtest/tasks.md) in the workspace and reading the output. |
| `#runSubagent` | Run a task in an isolated [subagent context](/docs/copilot/chat/chat-sessions.md#subagents). Helps to improve the context management of the main agent thread. |
| `#runTests` | Run [unit tests](/docs/debugtest/testing.md) in the workspace. |
| `#runVscodeCommand` | Run a VS Code command. For example, "Enable zen mode #runVscodeCommand." |
| `#search` (tool set) | Enable searching for files in the current workspace. |
| `#searchResults` | Get the search results from the Search view. |
| `#selection` | Get the current editor selection (only available when text is selected). |
| `#terminalLastCommand` | Get the last run terminal command and its output. |
| `#terminalSelection` | Get the current terminal selection. |
| `#testFailure` | Get unit test failure information. Useful when running and diagnosing [tests](/docs/debugtest/testing.md). |
| `#textSearch` | Find text in files. |
| `#todos` | Track implementation and progress of a chat request with a todo list. |
| `#usages` | Combination of "Find All References", "Find Implementation", and "Go to Definition". |
| `#VSCodeAPI` | Ask about VS Code functionality and extension development. |

## スラッシュコマンド

スラッシュコマンドは、チャット内の特定機能へのショートカットです。問題の修正、テストの生成、コードの説明などの操作をすばやく実行できます。

| スラッシュコマンド | 説明 |
|---------------|-------------|
| `/doc` | エディターのインラインチャットからコードのドキュメント コメントを生成します。 |
| `/explain` | コード ブロック、ファイル、またはプログラミング概念を説明します。 |
| `/fix` | コード ブロックの修正、またはコンパイラーやlintエラーの解決を依頼します。 |
| `/tests` | エディター内のすべて、または選択したメソッド/関数のみのテストを生成します。 |
| `/setupTests` | コードのテスト フレームワークのセットアップ支援を受けます。適切なテスト フレームワークの推奨、セットアップと構成の手順、VS Codeテスト拡張機能の提案を取得します。 |
| `/clear` | チャットビューで新しいチャットセッションを開始します。 |
| `/new` | 新しいVS Codeワークスペースまたはファイルをスキャフォールドします。必要なプロジェクト/ファイルの種類を自然言語で説明し、作成前にスキャフォールド内容をプレビューします。 |
| `/newNotebook` | 要件に基づいて新しいJupyterノートブックをスキャフォールドします。ノートブックに含める内容を自然言語で説明します。 |
| `/search` | 検索ビュー用の検索クエリを生成します。検索したい内容を自然言語で説明します。 |
| `/startDebugging` | `launch.json`デバッグ構成ファイルを生成し、チャットビューからデバッグセッションを開始します。 |
| `/<prompt name>` | チャットで[再利用可能なプロンプト](/docs/copilot/customization/prompt-files.md)を実行します。 |

## チャット参加者

チャット参加者を使用すると、チャット内でドメイン固有の要求を処理できます。チャット参加者は`@`で始まり、特定のトピックについて質問するために使えます。VS Codeには`@github`、`@terminal`、`@vscode`などの組み込みチャット参加者があり、拡張機能で追加の参加者を提供できます。

| チャット参加者 | 説明 |
|------------------|-------------|
| `@github` | `@github`参加者を使用して、GitHubリポジトリ、Issue、プルリクエストなどについて質問します。[利用可能なGitHubスキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)について詳しくはリンク先を参照してください。<br/>例: `@github What are all of the open PRs assigned to me?`, `@github Show me the recent merged PRs from @dancing-mona` |
| `@terminal` | `@terminal`参加者を使用して、統合ターミナルやシェル コマンドについて質問します。<br/>例: `@terminal list the 5 largest files in this workspace` |
| `@vscode` | `@vscode`参加者を使用して、VS Code機能、設定、VS Code拡張機能APIについて質問します。<br/>例: `@vscode how to enable  word wrapping?` |
| `@workspace` | `@workspace`参加者を使用して、現在のワークスペースについて質問します。<br/>例: `@workspace how is authentication implemented?` |

## エージェントを使用する

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用すると、自然言語で高レベルのタスクを指定し、AIが要求を自律的に推論して、必要な作業を計画し、コードベースに変更を適用できます。エージェントは、コード編集とツール呼び出しを組み合わせて、指定したタスクを達成します。要求を処理する際に、編集とツールの結果を監視し、発生した問題を解決するために反復します。

| 操作 | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.openAgent)` | チャットビューでエージェントの使用に切り替えます。 |
| Tools (<i class="codicon codicon-tools"></i>) | エージェント使用時に利用可能なツールを構成します。組み込みツール、MCPサーバー、拡張機能提供のツールから選択します。 |
| Auto-approve tools _(Experimental)_ | エージェント使用時に[すべてのツールの自動承認](/docs/copilot/chat/chat-tools.md#auto-approve-all-tools)を有効化します(`setting(chat.tools.autoApprove)`)。 |
| Auto-approve terminal commands _(Experimental)_ | エージェント使用時に[ターミナル コマンドの自動承認](/docs/copilot/chat/chat-tools.md#automatically-approve-terminal-commands)を有効化します(`setting(chat.tools.terminal.autoApprove)`)。 |
| MCP | [MCPサーバー](/docs/copilot/customization/mcp-servers.md)を構成して、エージェントの機能とツールを拡張します。 |

> **ヒント**
>
> * エージェント使用時に追加ツールを加えて、機能を拡張します。
> * カスタム エージェントを構成して、たとえば読み取り専用の計画モードを実装するなど、エージェントの動作を定義します。
> * カスタム指示を定義して、コードの生成方法や構成方法をエージェントにガイドします。

## 計画

VS Codeチャットの[plan agent](/docs/copilot/chat/chat-planning.md)を使用すると、複雑なコーディング タスクを開始する前に、詳細な実装計画を作成できます。承認済みの計画を実装エージェントに引き渡して、コーディングを開始します。

| 操作 | 説明 |
|--------|-------------|
| Plan agent | チャットビューのエージェント ドロップダウンから**Plan**エージェントを選択して、複雑なコーディング タスクの詳細な実装計画を作成します。 |
| Todo list (Experimental) | ツール ピッカーで`todos`ツールを有効化して、todoリストで複雑なタスクの進捗を追跡します。 |

## チャット体験をカスタマイズする

コーディング スタイル、ツール、開発者ワークフローに合った応答を生成できるように、チャット体験をカスタマイズします。VS Codeでチャット体験をカスタマイズする方法はいくつかあります。

* [カスタム指示](/docs/copilot/customization/custom-instructions.md): コード生成、コードレビューの実施、コミットメッセージの生成などのタスク向けに、共通のガイドラインやルールを定義します。カスタム指示は、AIがどのような条件で動作すべきか(タスクを_どのように_行うか)を記述します。

* [再利用可能なプロンプト ファイル](/docs/copilot/customization/prompt-files.md): コード生成やコードレビューなどの一般的なタスク向けに、再利用可能なプロンプトを定義します。プロンプト ファイルは、チャットで直接実行できるスタンドアロンのプロンプトです。実行するタスク(_何を_すべきか)を記述します。

* [カスタム エージェント](/docs/copilot/customization/custom-agents.md): チャットの動作、使用できるツール、コードベースとのやり取り方法を定義します。各チャット プロンプトはエージェントの境界内で実行され、要求ごとにツールや指示を構成する必要はありません。

> **ヒント**
>
> * 言語ごとの指示を定義して、各言語でより正確な生成コードを得ます。
> * 指示をワークスペースに保存して、チームと簡単に共有します。
> * 一般的なタスク向けに再利用可能なプロンプト ファイルを定義して、時間を節約し、チーム メンバーがすばやく開始できるようにします。

## エディターのAI機能

エディターでコーディングしている間、Copilotを使用して入力に応じたインライン提案を生成できます。インラインチャットを呼び出して、コーディングの流れを保ったまま質問したり、Copilotから支援を受けたりできます。たとえば、関数やメソッドのユニット テストを生成するようCopilotに依頼できます。[インライン提案](/docs/copilot/ai-powered-suggestions.md)と[インラインチャット](/docs/copilot/chat/inline-chat.md)について詳しくは、ドキュメントを参照してください。

| 操作 | 説明 |
|--------|-------------|
| インライン提案 | エディターで入力を開始すると、コーディング スタイルに一致し、既存コードを考慮した[インライン提案](/docs/copilot/ai-powered-suggestions.md)が表示されます。 |
| コード コメント | コード コメントに指示を書いて、インライン提案のプロンプトを提供します。<br/>例: `# write a calculator class with methods for add, subtract, and multiply. Use static methods.` |
| `kb(inlinechat.start)` | エディターのインラインチャットを開始して、エディターから直接チャット要求を送信します。自然言語を使用し、チャット変数とスラッシュコマンドを参照してコンテキストを提供します。 |
| `kb(editor.action.rename)` | コード内のシンボルを名前変更する際に、AI搭載の提案を取得します。 |
| コンテキスト メニュー アクション | エディターのコンテキスト メニューを使用して、コードの説明、テストの生成、コードのレビューなど、一般的なAIアクションにアクセスします。エディターを右クリックしてコンテキスト メニューを開き、**Generate Code**を選択します。 |
| コードアクション(電球) | エディターでコードアクション(電球)を選択して、コードのlintまたはコンパイラーエラーを修正します。 |

> **ヒント**
>
> * 意味のあるメソッド名や関数名を使用して、より良いインライン提案をより早く得ます。
> * コード ブロックを選択してインラインチャットのプロンプト範囲を絞り込むか、ファイルやシンボルを添付して関連コンテキストを追加します。
> * エディターのコンテキスト メニュー オプションを使用して、一般的なAI搭載アクションにエディターから直接アクセスします。

## ソース コントロールとIssue

AIを使用してコミットとプルリクエストの変更を分析し、コミットメッセージやプルリクエストの説明の提案を得られます。

| 操作 | 説明 |
|--------|-------------|
| `#changes` | 現在のソース コントロールの変更を、チャットプロンプトのコンテキストとして追加します。 |
| コンテキストとしてのコミット | ソース コントロール履歴のコミットを、チャットプロンプトのコンテキストとして追加します。 |
| コミット メッセージ | ソース コントロール コミット内の現在の変更に対するコミット メッセージを生成します。 |
| マージ競合(Experimental) | [AIでGitのマージ競合を解決する](/docs/sourcecontrol/overview#resolve-merge-conflicts-with-ai-experimental)ための支援を得ます。 |
| プルリクエストの説明 | プルリクエストの変更に対応するプルリクエストのタイトルと説明を生成します。 |
| `@github` | チャットで`@github`参加者を使用して、リポジトリ全体のIssue、プルリクエストなどについて質問します。[利用可能なGitHubスキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)について詳しくはリンク先を参照してください。<br/>例: `@github What are all of the open PRs assigned to me?`, `@github Show me the recent merged pr's from @dancing-mona`  |

## コードをレビューする(experimental)

AIを使用してコード ブロックの簡易レビューを行う、またはワークスペースの未コミット変更のレビューを実行できます。レビューのフィードバックはエディターにコメントとして表示され、提案を適用できます。

| 操作 | 説明 |
|--------|-------------|
| **Review Selection** _(Preview)_ | コード ブロックを選択し、エディターのコンテキスト メニューから**Generate Code** > **Review**を選択して、簡易レビューを実行します。 |
| **Code Review** | ソース コントロール ビューで**Code Review**ボタンを選択して、未コミット変更全体のより深いレビューを実行します。 |

## 検索と設定

検索ビューでセマンティックに関連する検索結果を取得する、または設定エディターでの設定検索の支援を受けます。

| 操作 | 説明 |
|--------|-------------|
| 設定検索 | 設定エディターにセマンティック検索結果を含めます(`setting(workbench.settings.showAISearchToggle)`)。 |
| セマンティック検索 _(Preview)_ | 検索ビューにセマンティック検索結果を含めます(`setting(search.searchView.semanticSearchBehavior)`)。 |

## テストを生成する

VS Codeでは、チャット内のスラッシュコマンドを使用して、コードベース内の関数やメソッドのテストを生成できます。スラッシュコマンドは、チャット プロンプトで使用できる一般的なタスクのショートハンド表記です。`/`に続けてコマンド名を入力してスラッシュコマンドを使用します。

| 操作 | 説明 |
|--------|-------------|
| `/tests` | エディター内のすべて、または選択したメソッド/関数のみのテストを生成します。生成されたテストは既存のテスト ファイルに追記されるか、新しいテスト ファイルが作成されます。  |
| `/setupTests` | コードのテスト フレームワークのセットアップ支援を受けます。適切なテスト フレームワークの推奨、セットアップと構成の手順、VS Codeテスト拡張機能の提案を取得します。   |
| `/fixTestFailure` | 失敗しているテストの修正方法について、Copilotに提案を求めます。 |
| テスト カバレッジ _(Experimental)_ | まだテストでカバーされていない関数やメソッドのテストを生成します。[詳細はこちら](https://code.visualstudio.com/updates/v1_93#_generate-tests-based-on-test-coverage-experimental)。 |

> **ヒント**
>
> * 使用するテスト フレームワークやライブラリの詳細を提示します。

## デバッグと問題の修正

Copilotを使用してコーディングの問題を修正したり、VS Codeでのデバッグ セッションの構成と開始の支援を受けたりできます。

| 操作 | 説明 |
|--------|-------------|
| `/fix` | コード ブロックの修正方法、またはコード内のコンパイラー/ lintエラーの解決方法について、Copilotに提案を求めます。たとえば、解決できないNode.jsパッケージ名の修正支援などです。 |
| `/fixTestFailure` | 失敗しているテストの修正方法について、Copilotに提案を求めます。 |
| `/startDebugging` _(Experimental)_ | `launch.json`デバッグ構成ファイルを生成し、チャットビューから[デバッグ セッションを開始](/docs/copilot/guides/debug-with-copilot.md)します。 |
| `copilot-debug` command | [プログラムをデバッグ](/docs/copilot/guides/debug-with-copilot.md)するのに役立つターミナル コマンドです。実行コマンドの前に付けて、そのコマンドのデバッグ セッションを開始します(例: `copilot-debug python foo.py`)。 |

> **ヒント**
>
> * 必要な修正の種類(メモリ使用量やパフォーマンスの最適化など)に関する追加情報を提供します。
> * エディターで、コードの問題修正の提案を示すCopilotコードアクションに注目します。

## 新しいプロジェクトをスキャフォールドする

Copilotは、プロジェクト構造のスキャフォールドを生成して新しいプロジェクト作成を支援したり、要件に基づいてノートブックを生成したりできます。

| 操作 | 説明 |
|--------|-------------|
| Agent | [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用し、自然言語プロンプトで新しいプロジェクトまたはファイルを作成します。例: `Create a svelte web application to track my tasks`。 |
| `/new` | チャットビューで`/new`コマンドを使用して、新しいプロジェクトまたは新しいファイルをスキャフォールドします。必要なプロジェクト/ファイルの種類を自然言語で説明し、作成前にスキャフォールド内容をプレビューします。<br/>例: `/new Express app using typescript and svelte` |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して、要件に基づいて新しいJupyterノートブックを生成します。ノートブックに含める内容を自然言語で説明します。<br/>例: `/newNotebook get census data and preview key insights with Seaborn`。 |

## ターミナル

シェル コマンドや、ターミナルでコマンドを実行する際のエラー解決方法について支援を受けます。

| 操作 | 説明 |
|--------|-------------|
| `kb(inlinechat.start)` | ターミナルのインラインチャットを開始し、シェル コマンドやターミナルについて自然言語で質問します。<br/>例: `how many cores on this machine?` |
| `@terminal` | チャットビューで`@terminal`参加者を使用して、統合ターミナルやシェル コマンドについて質問します。<br/>例: `@terminal list the 5 largest files in this workspace` |
| `@terminal /explain` | チャットビューで`/explain`コマンドを使用して、ターミナルの内容を説明します。<br/>例: `@terminal /explain top shell command` |

## Pythonとノートブックのサポート

Native Python REPLおよびJupyterノートブックでのPythonプログラミング タスクの支援を受けるために、チャットを使用できます。

| 操作 | 説明 |
|--------|-------------|
| <i class="codicon codicon-sparkle"></i> Generate<br/>`kb(inlinechat.start)` | ノートブックでインラインチャットを開始して、コード ブロックまたはMarkdownブロックを生成します。 |
| `#` | Jupyterカーネルの変数をチャットプロンプトに添付して、より関連性の高い応答を得ます。 |
| Native REPL + `kb(inlinechat.start)` | Native Python REPLでインラインチャットを開始し、生成されたコマンドを実行します。 |
| `kb(workbench.action.chat.open)` | **チャットビュー**を開き、エージェントを使用してノートブック編集を行います。 |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して、要件に基づいて新しいJupyterノートブックを生成します。ノートブックに含める内容を自然言語で説明します。<br/>例: `/newNotebook get census data and preview key insights with Seaborn`。 |

## 次のステップ

* [チュートリアル: VS CodeのAI機能を始める](/docs/copilot/getting-started.md)
