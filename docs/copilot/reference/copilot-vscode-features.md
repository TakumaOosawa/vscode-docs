---
ContentId: de6f9f68-7dd5-4de3-a210-3db57882384b
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeのAI機能の概要を素早く把握できます。GitHub Copilotは、より少ない労力でより速くコードを作成するためのAI搭載機能を提供します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでのGitHub Copilotチートシート

Visual Studio CodeのGitHub Copilotは、より少ない労力でより速くコードを作成するためのAI搭載機能を提供します。このチートシートでは、Visual Studio CodeにおけるGitHub Copilotの機能の概要を説明します。

> [!TIP]
> Copilotのサブスクリプションをまだお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)に登録することで無料でCopilotを利用でき、毎月一定数のインライン提案とチャット対話を活用できます。

## 基本的なキーボードショートカット

* `kb(workbench.panel.chat)` - チャットビューを開く
* `kb(workbench.action.chat.startVoiceChat)` - チャットビューで音声チャットプロンプトを入力する
* `kb(workbench.action.chat.newChat)` - チャットビューで新しいチャットセッションを開始する
* `kb(workbench.action.chat.openAgent)` - チャットビューでエージェントの使用に切り替える
* `kb(inlineChat.start)` - エディターまたはターミナルでインラインチャットを開始する
* `kb(workbench.action.chat.startVoiceChat)` (長押し) - インライン音声チャットを開始する
* `kb(editor.action.inlineSuggest.commit)` - インライン提案を受け入れるか、次の編集提案に移動する
* `kb(editor.action.inlineSuggest.hide)` - インライン提案を閉じる

## VS CodeでのAIへのアクセス

* 自然言語を使用してチャット会話を開始する
    * チャットビュー (`kb(workbench.action.chat.open)`): セカンダリサイドバーで進行中のチャット会話を維持する
    * エディターまたはターミナルのインラインチャット (`kb(inlineChat.start)`): 作業の流れの中で質問する
    * クイックチャット (`kb(workbench.action.quickchat.toggle)`): 現在のタスクを離れることなく簡単な質問をする

* [エディター](/docs/copilot/ai-powered-suggestions.md)でのAI
    * インライン提案: 入力中に提案を取得し、`kb(editor.action.inlineSuggest.commit)`を押して提案を受け入れる
    * エディターのコンテキストメニューアクション: コードの説明や修正、テストの生成、テキスト選択範囲のレビューなど、一般的なAIアクションにアクセスする
    * コードアクション: エディターのコードアクション（電球アイコン）を使用し、Lintやコンパイルのエラーを修正する

* VS Code全体でのタスク固有の[スマートアクション](/docs/copilot/copilot-smart-actions.md)
    * コミットメッセージおよびプルリクエストのタイトルと説明を生成する
    * テストエラーを修正する
    * セマンティックファイル検索の提案

## VS Codeでのチャット体験

自然言語によるチャット会話を開始して、コーディングタスクの支援を受けます。たとえば、コードブロックやプログラミングの概念の説明、コードのリファクタリング、新機能の実装などを依頼できます。[Copilot Chat](/docs/copilot/chat/copilot-chat.md)の使用に関する詳細情報を確認してください。

| アクション | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.open)` | セカンダリサイドバーで[チャットビュー](/docs/copilot/chat/copilot-chat.md)を開きます。 |
| `kb(inlinechat.start)` | [インラインチャット](/docs/copilot/chat/inline-chat.md)を開始して、エディターまたはターミナルでチャットを開きます。 |
| `kb(workbench.action.quickchat.toggle)` | ワークフローを中断することなく[クイックチャット](/docs/copilot/chat/copilot-chat.md)を開きます。 |
| `kb(workbench.action.chat.newChat)` | チャットビューで新しいチャットセッションを開始します。 |
| `kb(workbench.action.chat.toggleAgentMode)` | チャットビューで異なる[エージェント](/docs/copilot/customization/custom-agents.md)を切り替えます。 |
| `kb(workbench.action.chat.openModelPicker)` | チャット用の[異なるAIモデルを選択](/docs/copilot/customization/language-models.md)するためのモデルピッカーを表示します。 |
| `Add Context...` | さまざまなタイプの[コンテキストをチャットプロンプト](/docs/copilot/chat/copilot-chat-context.md)に添付します。 |
| `/`-command | 一般的なタスクには[スラッシュコマンド](#slash-commands)を使用するか、[再利用可能なチャットプロンプト](/docs/copilot/customization/overview.md)を呼び出します。 |
| `#`-mention | 一般的なツールやチャット変数を参照して、プロンプト内で[コンテキストを提供](/docs/copilot/chat/copilot-chat-context.md)します。 |
| `@`-mention | [チャット参加者](#chat-participants)を参照して、ドメイン固有のリクエストを処理します。 |
| 編集 (<i class="codicon codicon-pencil"></i>) | [以前のチャットプロンプトを編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)し、変更を元に戻します。 |
| 履歴 (<i class="codicon codicon-history"></i>) | チャットセッションの履歴にアクセスします。 |
| 音声 (<i class="codicon codicon-mic"></i>) | 音声（音声チャット）を使用してチャットプロンプトを入力します。チャットの応答が読み上げられます。 |
| [KaTeX](https://katex.org) | チャットの応答で数式をレンダリングします。`setting(chat.math.enabled)`で有効にします。数式を右クリックすると、ソース式をコピーできます。 |

> **ヒント**
>
> * `#`-mentionを使用して、チャットプロンプトにコンテキストを追加します。
> * `/`コマンドと`@`参加者を使用して、より正確で関連性の高い回答を得ます。
> * 具体的かつシンプルにし、フォローアップの質問をして最良の結果を得ます。
> * ニーズに合ったエージェントを選択します: 質問、編集、エージェント、またはカスタムエージェントの作成。

## プロンプトにコンテキストを追加する

[チャットプロンプトにコンテキスト](/docs/copilot/chat/copilot-chat-context.md)を提供することで、より関連性の高い回答を得られます。ファイル、シンボル、エディターの選択範囲、ソース管理のコミット、テストの失敗など、さまざまなコンテキストタイプから選択できます。

| アクション | 説明 |
|--------|-------------|
| **Add Context** | クイックピックを開き、チャットプロンプトに関連するコンテキストを選択します。ワークスペースファイル、シンボル、現在のエディターの選択範囲、ターミナルの選択範囲など、さまざまなコンテキストタイプから選択できます。 |
| ファイルをドラッグ＆ドロップ | エクスプローラーや検索ビューからファイルをドラッグ＆ドロップするか、エディタータブをチャットビューにドラッグします。 |
| フォルダーをドラッグ＆ドロップ | フォルダーをチャットビューにドラッグ＆ドロップして、その中のファイルを添付します。 |
| 問題をドラッグ＆ドロップ | 「問題」パネルから項目をドラッグ＆ドロップします。 |
| `#<file\|folder\|symbol>` | `#`に続けてファイル、フォルダー、またはシンボル名を入力し、チャットコンテキストとして追加します。 |
| `#`-mention | `#`に続けて[チャットツール](#chat-tools)を入力し、特定のコンテキストタイプまたはツールを追加します。 |

## チャットツール

チャットで[ツール](/docs/copilot/chat/chat-tools.md)を使用して、ユーザーリクエストの処理中に専門的なタスクを実行します。そのようなタスクの例としては、ディレクトリ内のファイルの一覧表示、ワークスペース内のファイルの編集、ターミナルコマンドの実行、ターミナルからの出力の取得などがあります。

VS Codeは組み込みツールを提供しており、[MCPサーバー](/docs/copilot/customization/mcp-servers.md)や[拡張機能](/api/extension-guides/ai/tools.md)のツールを使用してチャットを拡張できます。[ツールの種類](/docs/copilot/chat/chat-tools.md#types-of-tools)について詳しくはこちらをご覧ください。

次の表は、VS Codeの組み込みツールの一覧です。

| チャット変数/ツール | 説明 |
|--------|-------------|
| `#changes` | ソース管理の変更リスト。 |
| `#codebase` | 現在のワークスペースでコード検索を実行し、チャットプロンプトに関連するコンテキストを自動的に検索します。 |
| `#createAndRunTask` | ワークスペースに新しい[タスク](/docs/debugtest/tasks.md)を作成して実行します。 |
| `#createDirectory` | ワークスペースに新しいディレクトリを作成します。 |
| `#createFile` | ワークスペースに新しいファイルを作成します。 |
| `#edit` (ツールセット) | ワークスペース内の変更を有効にします。 |
| `#editFiles` | ワークスペース内のファイルに編集を適用します。 |
| `#editNotebook` | ノートブックに編集を加えます。 |
| `#extensions` | VS Code拡張機能を検索して質問します。例: "Python #extensions を使い始めるには?" |
| `#fetch` | 指定されたWebページからコンテンツを取得します。例: "Summarize #fetch code.visualstudio.com/updates." |
| `#fileSearch` | globパターンを使用してワークスペース内のファイルを検索し、そのパスを返します。 |
| `#getNotebookSummary` | ノートブックのセルとその詳細のリストを取得します。 |
| `#getProjectSetupInfo` | さまざまなタイプのプロジェクトをスキャフォールディングするための手順と構成を提供します。 |
| `#getTaskOutput` | ワークスペースで[タスク](/docs/debugtest/tasks.md)を実行した出力を取得します。 |
| `#getTerminalOutput` | ワークスペースでターミナルコマンドを実行した出力を取得します。 |
| `#githubRepo` | GitHubリポジトリでコード検索を実行します。例: "what is a global snippet #githubRepo microsoft/vscode." |
| `#installExtension` | VS Code拡張機能をインストールします。 |
| `#listDirectory` | ワークスペース内のディレクトリにあるファイルを一覧表示します。 |
| `#new` | デバッグおよび実行構成が事前に構成された新しいVS Codeワークスペースをスキャフォールディングします。 |
| `#newJupyterNotebook` | 説明に基づいて新しいJupyterノートブックをスキャフォールディングします。 |
| `#newWorkspace` | 新しいワークスペースを作成します。 |
| `#openSimpleBrowser` | 組み込みのSimple Browserを開き、ローカルにデプロイされたWebアプリをプレビューします。 |
| `#problems` | **問題**パネルからのワークスペースの問題や課題をコンテキストとして追加します。コードの修正やデバッグ中に役立ちます。 |
| `#readFile` | ワークスペース内のファイルの内容を読み取ります。 |
| `#readNotebookCellOutput` | ノートブックセルの実行結果を読み取ります。 |
| `#runCell` | ノートブックセルを実行します。 |
| `#runCommands` (ツールセット) | ターミナルでのコマンド実行と出力の読み取りを有効にします。 |
| `#runInTerminal` | 統合ターミナルでシェルコマンドを実行します。 |
| `#runNotebooks` (ツールセット) | ノートブックセルの実行を有効にします。 |
| `#runTask` | ワークスペース内の既存の[タスク](/docs/debugtest/tasks.md)を実行します。 |
| `#runTasks` (ツールセット) | ワークスペースでの[タスク](/docs/debugtest/tasks.md)の実行と出力の読み取りを有効にします。 |
| `#runSubagent` | 分離された[サブエージェントコンテキスト](/docs/copilot/chat/chat-sessions.md#subagents)でタスクを実行します。メインエージェントスレッドのコンテキスト管理を改善するのに役立ちます。 |
| `#runTests` | ワークスペースで[単体テスト](/docs/debugtest/testing.md)を実行します。 |
| `#runVscodeCommand` | VS Codeコマンドを実行します。例: "Enable zen mode #runVscodeCommand." |
| `#search` (ツールセット) | 現在のワークスペース内のファイルの検索を有効にします。 |
| `#searchResults` | 検索ビューから検索結果を取得します。 |
| `#selection` | 現在のエディターの選択範囲を取得します（テキストが選択されている場合のみ利用可能）。 |
| `#terminalLastCommand` | 最後に実行されたターミナルコマンドとその出力を取得します。 |
| `#terminalSelection` | 現在のターミナルの選択範囲を取得します。 |
| `#testFailure` | 単体テストの失敗情報を取得します。[テスト](/docs/debugtest/testing.md)の実行や診断に役立ちます。 |
| `#textSearch` | ファイル内のテキストを検索します。 |
| `#todos` | Todoリストを使用して、チャットリクエストの実装と進行状況を追跡します。 |
| `#usages` | "すべての参照を検索"、"実装へ移動"、および"定義へ移動"の組み合わせ。 |
| `#VSCodeAPI` | VS Codeの機能と拡張機能の開発について質問します。 |

## スラッシュコマンド

スラッシュコマンドは、チャット内の特定の機能へのショートカットです。これらを使用して、問題の修正、テストの生成、コードの説明などのアクションを素早く実行できます。

| スラッシュコマンド | 説明 |
|---------------|-------------|
| `/doc` | エディターのインラインチャットからコードのドキュメントコメントを生成します。 |
| `/explain` | コードブロック、ファイル、またはプログラミングの概念を説明します。 |
| `/fix` | コードブロックの修正、またはコンパイラやLintのエラー解決を依頼します。 |
| `/tests` | エディター内のすべて、または選択されたメソッドや関数のテストを生成します。 |
| `/setupTests` | コードのテストフレームワークのセットアップに関するヘルプを取得します。関連するテストフレームワークの推奨、セットアップと構成の手順、およびVS Codeテスト拡張機能の提案を取得します。 |
| `/clear` | チャットビューで新しいチャットセッションを開始します。 |
| `/new` | 新しいVS Codeワークスペースまたはファイルをスキャフォールディングします。自然言語を使用して必要なプロジェクト/ファイルの種類を記述し、作成前にスキャフォールディングされたコンテンツをプレビューします。 |
| `/newNotebook` | 要件に基づいて新しいJupyterノートブックをスキャフォールディングします。自然言語を使用して、ノートブックに含めるべき内容を記述します。 |
| `/search` | 検索ビューの検索クエリを生成します。検索したい内容を自然言語で記述します。 |
| `/startDebugging` | `launch.json`デバッグ構成ファイルを生成し、チャットビューからデバッグセッションを開始します。 |
| `/<prompt name>` | チャットで[再利用可能なプロンプト](/docs/copilot/customization/prompt-files.md)を実行します。 |

## チャット参加者

チャット参加者を使用して、チャット内でドメイン固有のリクエストを処理します。チャット参加者には`@`というプレフィックスが付き、特定のトピックについて質問するために使用できます。VS Codeには、`@github`、`@terminal`、`@vscode`などの組み込みチャット参加者が用意されており、拡張機能によって追加の参加者を提供することもできます。

| チャット参加者 | 説明 |
|------------------|-------------|
| `@github` | `@github`参加者を使用して、GitHubリポジトリ、課題、プルリクエストなどについて質問します。[利用可能なGitHubスキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)についての詳細を確認してください。<br/>例: `@github What are all of the open PRs assigned to me?`, `@github Show me the recent merged PRs from @dancing-mona` |
| `@terminal` | `@terminal`参加者を使用して、統合ターミナルまたはシェルコマンドについて質問します。<br/>例: `@terminal list the 5 largest files in this workspace` |
| `@vscode` | `@vscode`参加者を使用して、VS Codeの機能、設定、およびVS Code拡張APIについて質問します。<br/>例: `@vscode how to enable  word wrapping?` |
| `@workspace` | `@workspace`参加者を使用して、現在のワークスペースについて質問します。<br/>例: `@workspace how is authentication implemented?` |

## エージェントを使用する

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、自然言語を使用して高レベルのタスクを指定し、AIにリクエストを自律的に推論させ、必要な作業を計画させ、コードベースに変更を適用させることができます。エージェントは、コード編集とツール呼び出しを組み合わせて、指定されたタスクを達成します。リクエストを処理する際、編集とツールの結果を監視し、発生した問題を解決するために反復処理を行います。

| アクション | 説明 |
|--------|-------------|
| `kb(workbench.action.chat.openAgent)` | チャットビューでエージェントの使用に切り替える |
| ツール (<i class="codicon codicon-tools"></i>) | エージェントを使用するときに利用可能なツールを構成します。組み込みツール、MCPサーバー、および拡張機能が提供するツールから選択します。 |
| ツールの自動承認 _(実験的機能)_ | エージェントを使用するときに[すべてのツールの自動承認](/docs/copilot/chat/chat-tools.md#auto-approve-all-tools)を有効にします (`setting(chat.tools.autoApprove)`)。 |
| ターミナルコマンドの自動承認 _(実験的機能)_ | エージェントを使用するときに[ターミナルコマンドの自動承認](/docs/copilot/chat/chat-tools.md#automatically-approve-terminal-commands)を有効にします (`setting(chat.tools.terminal.autoApprove)`)。 |
| MCP | [MCPサーバー](/docs/copilot/customization/mcp-servers.md)を構成して、エージェントの機能とツールを拡張します。 |

> **ヒント**
>
> * エージェントを使用する際に追加のツールを追加して、その機能を拡張します。
> * カスタムエージェントを構成して、エージェントの動作方法を定義します。たとえば、読み取り専用の計画モードを実装するなどです。
> * コードの生成方法や構造化方法についてエージェントをガイドするためのカスタム指示を定義します。

## 計画 (Planning)

VS Codeチャットで[Planエージェント](/docs/copilot/chat/chat-planning.md)を使用して、複雑なコーディングタスクを開始する前に詳細な実装計画を作成します。承認された計画を実装エージェントに引き継いでコーディングを開始します。

| アクション | 説明 |
|--------|-------------|
| Planエージェント | チャットビューのエージェントドロップダウンから**Plan**エージェントを選択して、複雑なコーディングタスクの詳細な実装計画を作成します。 |
| Todoリスト (実験的機能) | ツールピッカーで`todos`ツールを有効にして、Todoリストで複雑なタスクの進行状況を追跡します。 |

## チャット体験をカスタマイズする

コーディングスタイル、ツール、開発者のワークフローに合わせて回答を生成するように、チャット体験をカスタマイズします。VS Codeでチャット体験をカスタマイズするには、いくつかの方法があります。

* [カスタム指示](/docs/copilot/customization/custom-instructions.md): コード生成、コードレビューの実行、コミットメッセージの生成などのタスクに関する一般的なガイドラインやルールを定義します。カスタム指示は、AIが動作すべき条件（タスクを*どのように*実行すべきか）を記述します。

* [再利用可能なプロンプトファイル](/docs/copilot/customization/prompt-files.md): コード生成やコードレビューの実行などの一般的なタスクの再利用可能なプロンプトを定義します。プロンプトファイルは、チャットで直接実行できるスタンドアロンのプロンプトです。これらは実行するタスク（*何を*すべきか）を記述します。

* [カスタムエージェント](/docs/copilot/customization/custom-agents.md): チャットの動作方法、使用できるツール、コードベースとの対話方法を定義します。各チャットプロンプトは、リクエストごとにツールや指示を構成することなく、エージェントの境界内で実行されます。

> **ヒント**
>
> * 言語固有の指示を定義して、各言語でより正確な生成コードを取得します。
> * 指示をワークスペースに保存して、チームと簡単に共有します。
> * 一般的なタスクの再利用可能なプロンプトファイルを定義して、時間を節約し、チームメンバーがすぐに開始できるようにします。

## エディターのAI機能

エディターでコーディングしているときに、Copilotを使用して入力中​​にインライン提案を生成できます。インラインチャットを呼び出して質問したり、Copilotから支援を受けたりしながら、コーディングの流れを維持できます。たとえば、関数やメソッドの単体テストを生成するようにCopilotに依頼します。[インライン提案](/docs/copilot/ai-powered-suggestions.md)と[インラインチャット](/docs/copilot/chat/inline-chat.md)の詳細をご覧ください。

| アクション | 説明 |
|--------|-------------|
| インライン提案 | エディターで入力を開始し、コーディングスタイルに一致し、既存のコードを考慮した[インライン提案](/docs/copilot/ai-powered-suggestions.md)を取得します。 |
| コードコメント | コードコメントに指示を書くことで、インライン提案のプロンプトを提供します。<br/>例: `# write a calculator class with methods for add, subtract, and multiply. Use static methods.` |
| `kb(inlinechat.start)` | エディターのインラインチャットを開始して、エディターから直接チャットリクエストを送信します。自然言語を使用し、チャット変数やスラッシュコマンドを参照してコンテキストを提供します。 |
| `kb(editor.action.rename)` | コード内のシンボルの名前を変更するときに、AIを利用した提案を取得します。 |
| コンテキストメニューアクション | エディターのコンテキストメニューを使用して、コードの説明、テストの生成、コードのレビューなど、一般的なAIアクションにアクセスします。エディターで右クリックしてコンテキストメニューを開き、**コードの生成 (Generate Code)** を選択します。 |
| コードアクション（電球アイコン） | エディターでコードアクション（電球アイコン）を選択して、コード内のLintやコンパイルのエラーを修正します。 |

> **ヒント**
>
> * 意味のあるメソッド名や関数名を使用して、より良いインライン提案を素早く取得します。
> * コードブロックを選択してインラインチャットプロンプトのスコープを設定するか、ファイルやシンボルを添付して関連するコンテキストを添付します。
> * エディターのコンテキストメニューオプションを使用して、エディターから直接一般的なAI機能のアクションにアクセスします。

## ソース管理と課題

AIを使用して、コミットやプルリクエストの変更を分析し、コミットメッセージやプルリクエストの説明についての提案を提供します。

| アクション | 説明 |
|--------|-------------|
| `#changes` | チャットプロンプトに現在のソース管理の変更をコンテキストとして追加します。 |
| コミットをコンテキストとして使用 | ソース管理履歴からコミットをチャットプロンプトのコンテキストとして追加します。 |
| コミットメッセージ | ソース管理コミットでの現在の変更に対するコミットメッセージを生成します。 |
| マージ競合 (実験的機能) | [AIを使用したGitマージ競合の解決](/docs/sourcecontrol/overview#resolve-merge-conflicts-with-ai-experimental)に関するヘルプを取得します。 |
| プルリクエストの説明 | プルリクエストの変更に対応するプルリクエストのタイトルと説明を生成します。 |
| `@github` | チャットで`@github`参加者を使用して、リポジトリ全体の課題、プルリクエストなどについて質問します。[利用可能なGitHubスキル](https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide#currently-available-skills)についての詳細を確認してください。<br/>例: `@github What are all of the open PRs assigned to me?`, `@github Show me the recent merged pr's from @dancing-mona` |

## コードレビュー (実験的機能)

AIを使用して、コードブロックの迅速なレビューパスを実行したり、ワークスペース内のコミットされていない変更のレビューを実行したりします。レビューのフィードバックはエディターにコメントとして表示され、そこで提案を適用できます。

| アクション | 説明 |
|--------|-------------|
| **選択範囲のレビュー (Review Selection)** _(プレビュー)_ | コードブロックを選択し、エディターのコンテキストメニューから**コードの生成 (Generate Code)** > **レビュー (Review)** を選択して、素早いレビューパスを実行します。 |
| **コードレビュー** | ソース管理ビューの**コードレビュー (Code Review)** ボタンを選択して、すべてのコミットされていない変更の詳細なレビューを行います。 |

## 検索と設定

検索ビューで関連性の高い検索結果を取得したり、設定エディターで設定の検索を支援したりします。

| アクション | 説明 |
|--------|-------------|
| 設定検索 | 設定エディターにセマンティック検索結果を含めます (`setting(workbench.settings.showAISearchToggle)`)。 |
| セマンティック検索 _(プレビュー)_ | 検索ビューにセマンティック検索結果を含めます (`setting(search.searchView.semanticSearchBehavior)`)。 |

## テストを生成する

VS Codeは、チャットでスラッシュコマンドを使用して、コードベース内の関数やメソッドのテストを生成できます。スラッシュコマンドは、チャットプロンプトで使用できる一般的なタスクの短縮表記です。`/`の後にコマンド名を入力して、スラッシュコマンドを使用します。

| アクション | 説明 |
|--------|-------------|
| `/tests` | エディター内のすべて、または選択されたメソッドや関数のテストを生成します。生成されたテストは、既存のテストファイルに追加されるか、新しいテストファイルが作成されます。 |
| `/setupTests` | コードのテストフレームワークのセットアップに関するヘルプを取得します。関連するテストフレームワークの推奨、セットアップと構成の手順、およびVS Codeテスト拡張機能の提案を取得します。 |
| `/fixTestFailure` | Copilotに、失敗したテストの修正方法についての提案を依頼します。 |
| テストカバレッジ _(実験的機能)_ | まだテストでカバーされていない関数やメソッドのテストを生成します。[詳細情報](https://code.visualstudio.com/updates/v1_93#_generate-tests-based-on-test-coverage-experimental)を取得してください。 |

> **ヒント**
>
> * 使用するテストフレームワークまたはライブラリに関する詳細を提供します。

## デバッグと問題の修正

Copilotを使用して、コーディングの問題を修正したり、VS Codeでのデバッグセッションの構成と開始を支援したりします。

| アクション | 説明 |
|--------|-------------|
| `/fix` | Copilotに、コードブロックの修正方法、またはコード内のコンパイラやLintのエラーを解決する方法についての提案を依頼します。たとえば、解決されていないNode.jsパッケージ名の修正を支援するなどです。 |
| `/fixTestFailure` | Copilotに、失敗したテストの修正方法についての提案を依頼します。 |
| `/startDebugging` _(実験的機能)_ | `launch.json`デバッグ構成ファイルを生成し、チャットビューから[デバッグセッションを開始](/docs/copilot/guides/debug-with-copilot.md)します。 |
| `copilot-debug` コマンド | [プログラムをデバッグ](/docs/copilot/guides/debug-with-copilot.md)するのに役立つターミナルコマンドです。実行コマンドの前にプレフィックスを付けて、デバッグセッションを開始します（例: `copilot-debug python foo.py`）。 |

> **ヒント**
>
> * メモリ消費やパフォーマンスの最適化など、必要な修正の種類に関する追加情報を提供します。
> * コード内の問題を修正するための提案を示す、エディター内のCopilotコードアクションに注目してください。

## 新しいプロジェクトのスキャフォールディング

Copilotは、プロジェクト構造のスキャフォールディング（雛形）を生成して新しいプロジェクトを作成したり、要件に基づいてノートブックを生成したりするのに役立ちます。

| アクション | 説明 |
|--------|-------------|
| エージェント | [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)と自然言語プロンプトを使用して、新しいプロジェクトまたはファイルを作成します。例えば、`Create a svelte web application to track my tasks`。 |
| `/new` | チャットビューで`/new`コマンドを使用して、新しいプロジェクトまたは新しいファイルをスキャフォールディングします。自然言語を使用して必要なプロジェクト/ファイルの種類を記述し、作成前にスキャフォールディングされたコンテンツをプレビューします。<br/>例: `/new Express app using typescript and svelte` |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して、要件に基づいて新しいJupyterノートブックを生成します。自然言語を使用して、ノートブックに含めるべき内容を記述します。<br/>例: `/newNotebook get census data and preview key insights with Seaborn`. |

## ターミナル

シェルコマンドや、ターミナルでコマンドを実行する際のエラー解決について支援を受けます。

| アクション | 説明 |
|--------|-------------|
| `kb(inlinechat.start)` | ターミナルのインラインチャットを開始して、自然言語を使用してシェルコマンドやターミナルについて質問します。<br/>例: `how many cores on this machine?` |
| `@terminal` | チャットビューで`@terminal`参加者を使用して、統合ターミナルまたはシェルコマンドについて質問します。<br/>例: `@terminal list the 5 largest files in this workspace` |
| `@terminal /explain` | チャットビューで`/explain`コマンドを使用して、ターミナルからの内容を説明します。<br/>例: `@terminal /explain top shell command` |

## Pythonとノートブックのサポート

チャットを使用して、ネイティブPython REPLやJupyterノートブックでのPythonプログラミングタスクを支援できます。

| アクション | 説明 |
|--------|-------------|
| <i class="codicon codicon-sparkle"></i> 生成<br/>`kb(inlinechat.start)` | ノートブックでインラインチャットを開始して、コードブロックまたはMarkdownブロックを生成します。 |
| `#` | チャットプロンプトにJupyterカーネルからの変数を添付して、より関連性の高い回答を得ます。 |
| ネイティブREPL + `kb(inlinechat.start)` | ネイティブPython REPLでインラインチャットを開始し、生成されたコマンドを実行します。 |
| `kb(workbench.action.chat.open)` | **チャットビュー**を開き、エージェントを使用してノートブックの編集を行います。 |
| `/newNotebook` | チャットビューで`/newNotebook`コマンドを使用して、要件に基づいて新しいJupyterノートブックを生成します。自然言語を使用して、ノートブックに含めるべき内容を記述します。<br/>例: `/newNotebook get census data and preview key insights with Seaborn`. |

## 次のステップ

* [チュートリアル: VS CodeのAI機能を使ってみる](/docs/copilot/getting-started.md)
