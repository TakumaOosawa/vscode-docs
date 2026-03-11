---
ContentId: 7b232695-cbbe-4f3f-a625-abc7a5e6496c
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeのGitHub Copilotの設定について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeのGitHub Copilot設定リファレンス

このリファレンスでは、Visual Studio CodeのGitHub Copilotの設定をリストアップしています。VS Codeの設定の操作に関する一般的な情報については、[ユーザーとワークスペース設定](/docs/configure/settings.md)を参照してください。

Copilot in VS Codeは継続的に改善され、新機能が追加されています。いくつかの機能はまだ実験的です。試してみて、[GitHubの問題](https://github.com/microsoft/vscode/issues)でフィードバックを共有してください。[VS Codeの機能ライフサイクル](/docs/configure/settings.md#feature-lifecycle)について詳しくは、こちらをご覧ください。

> [!TIP]
> Copilotのサブスクリプションをまだ持っていない場合は、[Copilot無料プラン](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で使用でき、月単位でインライン候補とチャットインタラクションの制限を受けます。

##一般設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.commandCenter.enabled)`<br/>VS Codeのタイトルバーでチャットメニューを表示するかどうかを制御します。 | `true` |
| `setting(workbench.settings.showAISearchToggle)`<br/>設定エディターでAIで設定を検索できるようにします。 | `true` |
| `setting(workbench.commandPalette.experimental.askChatLocation)` _(実験的)_<br/>コマンドパレットがチャットの質問をする場所を制御します。 | `"chatView"` |
| `setting(search.searchView.semanticSearchBehavior)` _(プレビュー)_<br/>検索ビューでセマンティック検索を実行するタイミングを設定します: 手動(デフォルト)、テキスト検索結果が見つからない場合、常に。 | `"manual"` |
| `setting(search.searchView.keywordSuggestions)` _(プレビュー)_<br/>検索ビューでキーワード候補を表示するかどうかを制御します。 | `false` |

##コード編集設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.editor.enableCodeActions)`<br/>利用可能な場合、Copilotコマンドをコードアクションとして表示するかどうかを制御します。 | `true` |
| `setting(github.copilot.renameSuggestions.triggerAutomatically)`<br/>シンボル名前変更候補を生成します。 | `true` |
| `setting(github.copilot.enable)`<br/>指定した[言語](/docs/languages/identifiers.md)のインライン候補を有効または無効にします。 | `{ "*": true, "plaintext": false, "markdown": false, "scminput": false }` |
| `setting(github.copilot.nextEditSuggestions.enabled)`<br/>[次の編集候補](/docs/copilot/ai-powered-suggestions.md#next-edit-suggestions)(NES)を有効にします。 | `true` |
| `setting(editor.inlineSuggest.edits.allowCodeShifting)`<br/>NESが候補を表示するためにコードをシフトできるかどうかを設定します。 | `"always"` |
| `setting(editor.inlineSuggest.edits.renderSideBySide)`<br/>NESが可能な場合に大きな候補を並べて表示できるか、またはCopilot NESが常に関連するコードの下に大きな候補を表示するかを設定します。 | `"auto"` |
| `setting(github.copilot.nextEditSuggestions.fixes)`<br/>診断に基づいて次の編集候補を有効にします(スクイグル)。例えば、インポートが不足しています。 | `true` |
| `setting(editor.inlineSuggest.minShowDelay)`<br/>インライン候補を表示する前に待機する時間(ミリ秒)。 | `0` |

##チャット設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.localeOverride)`<br/>チャットレスポンスのロケールを指定します。例:`en`または`fr`。 | `"auto"` |
| `setting(github.copilot.chat.useProjectTemplates)`<br/>`/new`を使う際に、関連するGitHubプロジェクトをスタータープロジェクトとして使用します。 | `true` |
| `setting(github.copilot.chat.scopeSelection)`<br/>`/explain`を使う際に、アクティブなエディターに選択範囲がない場合、特定のシンボルスコープに対してプロンプトを表示するかどうか。 | `false` |
| `setting(github.copilot.chat.terminalChatLocation)`<br/>ターミナルからのチャットクエリを開く場所を制御します。 | `"chatView"` |
| `setting(chat.detectParticipant.enabled)`<br/>チャットビューでチャット参加者検出を有効にします。 | `true` |
| `setting(chat.checkpoints.enabled)` <br/>チャット内の[チェックポイント](/docs/copilot/chat/chat-checkpoints.md)を有効または無効にします。 | `true` |
| `setting(chat.checkpoints.showFileChanges)` <br/>各チャットリクエストの終了時にファイル変更の概要を表示します。 | `false` |
| `setting(chat.editRequests)`<br/>[以前のチャットリクエストを編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)できるように有効または無効にします。 | `"inline"` |
| `setting(chat.editor.fontFamily)`<br/>チャットコードブロックのフォントファミリー。 | `"default"` |
| `setting(chat.editor.fontSize)`<br/>チャットコードブロックのフォントサイズ(ピクセル)。 | `14` |
| `setting(chat.editor.fontWeight)`<br/>チャットコードブロックのフォントの太さ。 | `"default"` |
| `setting(chat.editor.lineHeight)`<br/>チャットコードブロックの行の高さ(ピクセル)。 | `0` |
| `setting(chat.editor.wordWrap)`<br/>チャットコードブロックで行を折り返すことができるようにします。 | `"off"` |
| `setting(chat.editing.confirmEditRequestRemoval)`<br/>編集を取り消す前に確認を要求します。 | `true` |
| `setting(chat.editing.confirmEditRequestRetry)`<br/>最後の編集をやり直す前に確認を要求します。 | `true` |
| `setting(chat.editing.autoAcceptDelay)`<br/>提案された編集が自動的に受け入れられる遅延時間を設定します。無効にするには0を使用します。 | `0` |
| `setting(chat.fontFamily)`<br/>チャットのMarkdownコンテンツのフォントファミリー。 | `"default"` |
| `setting(chat.fontSize)`<br/>チャットのMarkdownコンテンツのフォントサイズ(ピクセル)。 | `13` |
| `setting(chat.notifyWindowOnConfirmation)`<br/>ユーザーの入力が必要な場合にOS通知を表示するタイミングを設定します: `off`で通知を表示しない、`windowNotFocused`(デフォルト)でVS Codeウィンドウがフォーカスされていないときのみ通知を表示、`always`で常に通知を表示します。 | `"windowNotFocused"` |
| `setting(chat.notifyWindowOnResponseReceived)`<br/>チャットレスポンスを受け取ったときにOS通知を表示するタイミングを設定します: `off`で通知を表示しない、`windowNotFocused`(デフォルト)でVS Codeウィンドウがフォーカスされていないときのみ通知を表示、`always`で常に通知を表示します。 | `"windowNotFocused"` |
| `setting(chat.requestQueuing.defaultAction)`<br/>リクエスト実行中に**送信**ボタンのデフォルトアクションを設定します: `queue`でメッセージをキューに追加、`steer`で現在のリクエストを譲歩します。 | `"queue"` |
| `setting(chat.tools.terminal.autoReplyToPrompts)` <br/>ターミナルプロンプトにデフォルトの応答を自動的に返します。 | `false` |
| `setting(chat.tools.terminal.terminalProfile.<platform>)`<br/>各プラットフォームでチャットターミナルコマンドに使用するターミナルプロファイルを設定します。 | `""` |
| `setting(chat.hookFilesLocations)` _(プレビュー)_ <br/>追加の[フックファイルロケーション](/docs/copilot/customization/hooks.md#hook-file-locations)を設定します。フォルダーへのパス(すべての`*.json`ファイルを読み込む)または`.json`ファイルへの直接パスを指定します。相対パスとチルダパスのみがサポートされています。 | `{}` |
| `setting(chat.useCustomAgentHooks)` _(プレビュー)_ <br/>カスタムエージェントフロントマターで定義された[エージェントスコープフック](/docs/copilot/customization/hooks.md#agentscoped-hooks)を有効にします。有効になっている場合、`.agent.md`ファイルのフックはそのエージェントがアクティブな場合のみ実行されます。 | `false` |
| `setting(chat.useAgentsMdFile)` <br/>`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用するかどうかを有効または無効にします。 | `true` |
| `setting(chat.math.enabled)` <br/>チャット内で[KaTeX](https://katex.org)を使用した数学レンダリングを有効または無効にします。 | `false` |
| `setting(chat.viewTitle.enabled)` _(プレビュー)_<br/>チャットヘッダーに現在のチャットセッションのタイトルを表示します。 | `true` |
| `setting(github.copilot.chat.codesearch.enabled)` _(プレビュー)_<br/>プロンプトで`#codebase`を使う場合、Copilotは関連ファイルを自動的に検出して編集できます。 | `false` |
| `setting(chat.emptyState.history.enabled)` _(実験的)_<br/>チャットビューの空の状態で最近のチャット履歴を表示します。 | `false` |
| `setting(chat.sendElementsToChat.enabled)` _(実験的)_<br/>[統合ブラウザー](/docs/debugtest/integrated-browser.md)からチャットビューにコンテキストとして要素を送信できるようにします。 | `true` |
| `setting(workbench.browser.enableChatTools)` _(実験的)_<br/>[ブラウザーツール](/docs/debugtest/integrated-browser.md#browser-tools-for-agents)を有効にして、エージェントが統合ブラウザー内のページと相互作用できるようにします。 | `false` |
| `setting(chat.useNestedAgentsMdFiles)` _(実験的)_<br/>ワークスペースのサブフォルダーの`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用するかどうかを有効または無効にします。 | `false` |
| `setting(github.copilot.chat.customOAIModels)` _(実験的)_<br/>チャット用のカスタムOpenAI互換モデルを設定します。 | `[]` |
| `setting(github.copilot.chat.edits.suggestRelatedFilesFromGitHistory)` _(実験的)_<br/>チャットコンテキストでgit履歴から関連ファイルを提案します。 | `true` |

##エージェント設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.agent.enabled:true)`<br/>エージェントの使用を有効または無効にします(VS Code 1.99以降が必要)。 | `true` |
| `setting(chat.agent.maxRequests)`<br/>Copilotがエージェントを使用して実行できるリクエストの最大数。 | `25` |
| `setting(github.copilot.chat.agent.autoFix)`<br/>生成されたコード変更の問題を自動的に診断して修正します。 | `true` |
| `setting(chat.mcp.access)`<br/>どのモデルコンテキストプロトコル(MCP)サーバーをVS Codeで使用できるかを管理します。 | `true` |
| `setting(chat.mcp.discovery.enabled)`<br/>他のアプリケーションからMCPサーバー構成の自動検出を設定します。 | `false` |
| `setting(chat.mcp.serverSampling)`<br/>MCPサーバーに公開されるモデルを設定します。 | `{}` |
| `setting(chat.mcp.apps.enabled)` _(実験的)_<br/>MCPサーバーが提供するリッチユーザーインターフェース(MCPアプリ)を有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.autoApprove)` <br/>エージェントを使う際に自動的に承認される[ターミナルコマンド](/docs/copilot/agents/agent-tools.md#automatically-approve-terminal-commands)を制御します。コマンドは`true`(自動承認)または`false`(承認が必要)に設定できます。`/`で囲まれたパターンを使用して正規表現を使用できます。 | `{ "rm": false, "rmdir": false, "del": false, "kill": false, "curl": false, "wget": false, "eval": false, "chmod": false, "chown": false, "/^Remove-Item\\b/i": false }` |
| `setting(chat.tools.terminal.enableAutoApprove)` <br/>ターミナルコマンドの自動承認を有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.enforceTimeoutFromModel)` _(実験的)_<br/>エージェントが指定するタイムアウト値を適用するかどうかを制御します。有効にすると、エージェントは指定された期間後にコマンドのトラッキングを停止し、これまで収集した出力を返します。 | `true` |
| `setting(chat.tools.terminal.ignoreDefaultAutoApproveRules)` <br/>ターミナルコマンドのデフォルト自動承認ルールを無視します。 | `false` |
| `setting(chat.tools.global.autoApprove)`<br/>すべてのツールを自動的に承認します - この設定は[重要なセキュリティ保護を無効にします](/docs/copilot/security.md)。 | `false` |
| `setting(chat.autopilot.enabled)` _(実験的)_<br/>[オートパイロット権限レベル](/docs/copilot/agents/agent-tools.md#permission-levels)が権限ピッカーで利用可能かどうかを制御します。有効にすると、オートパイロットはすべてのツール呼び出しを自動承認し、タスクが完了するまで継続します。 | `true` |
| `setting(chat.tools.urls.autoApprove)` <br/>どの[URLリクエストとレスポンスが自動的に承認されるか](/docs/copilot/agents/agent-tools.md#url-approval)を制御します。 | `[]` |
| `setting(chat.agent.thinking.collapsedTools)` _(実験的)_<br/>ツール呼び出しの詳細がチャット会話でデフォルトで折りたたまれているか拡張されているかを設定します。 | `always` |
| `setting(chat.agent.thinkingStyle)` _(実験的)_<br/>シンキングトークンをチャットでどのように表示するかを設定します。 | `fixedScrolling` |
| `setting(chat.mcp.autoStart)` _(実験的)_<br/>MCP設定の変更が検出されたときにMCPサーバーを自動的に開始します。 | `newAndOutdated` |
| `setting(chat.tools.eligibleForAutoApproval)` _(実験的)_<br/>エージェントが使用する前に手動承認が必要なツールを設定します。 | `[]` |
| `setting(chat.tools.terminal.blockDetectedFileWrites)` _(実験的)_<br/>ファイル書き込みを実行するターミナルコマンドについてはユーザーの承認が必要です。 | `outsideWorkspace` |
| `setting(chat.tools.terminal.sandbox.enabled)` _(実験的)_<br/>エージェントが実行した[ターミナルコマンドのサンドボックス化](/docs/copilot/agents/agent-tools.md#sandbox-terminal-commands-experimental)を有効にします(macOSおよびLinuxのみ)。有効にすると、コマンドは自動承認され、ファイルシステムとネットワークアクセスが制限されます。 | `false` |
| `setting(chat.tools.terminal.sandbox.linuxFileSystem)` _(実験的)_<br/>Linuxでサンドボックス化されたターミナルコマンドのファイルシステムアクセスルールを設定します。`allowWrite`、`denyWrite`、および`denyRead`プロパティをサポートしています。 | `{}` |
| `setting(chat.tools.terminal.sandbox.macFileSystem)` _(実験的)_<br/>macOSでサンドボックス化されたターミナルコマンドのファイルシステムアクセスルールを設定します。`allowWrite`、`denyWrite`、および`denyRead`プロパティをサポートしています。 | `{}` |
| `setting(chat.tools.terminal.sandbox.network)` _(実験的)_<br/>サンドボックス化されたターミナルコマンドのネットワークアクセスルールを設定します。許可されたドメインを指定する`allowedDomains`と[信頼できるドメイン](/docs/editing/editingevolved.md#outgoing-link-protection)リストのドメインを含める`allowTrustedDomains`をサポートしています。 | `{}` |
| `setting(github.copilot.chat.newWorkspaceCreation.enabled)` _(実験的)_<br/>チャットで新しいワークスペースをスキャフォールディングするためのツールを有効にします。 | `true` |
| `setting(github.copilot.chat.agent.thinkingTool:true)` _(実験的)_<br/>エージェントを使用する場合、シンキングツールを有効にします。 | `false` |
| `setting(github.copilot.chat.summarizeAgentConversationHistory.enabled)` _(実験的)_<br/>コンテキストウィンドウが満杯の場合、エージェント会話履歴を自動的に要約します。 | `true` |
| `setting(github.copilot.chat.virtualTools.threshold)` _(実験的)_<br/>仮想ツールを使用する必要があるツール数。仮想ツールは同様のツールセットをまとめて、モデルがオンデマンドで起動できるようにします。チャットリクエストの128個のツール制限を超えることができます。 | `128` |

##エージェントセッション

[エージェント表示](/docs/copilot/agents/overview.md)は、ローカルチャット会話とリモートコーディングエージェントセッションの両方を管理するための一元化された場所を提供します。このビューでは、複数のAIセッションを同時に処理し、その進捗をトラッキングし、長時間実行されるタスクを効率的に管理できます。

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(workbench.startupEditor)` <br/>VS Codeウェルカムページをエージェントセッションのエントリーポイントとして機能するように設定します。`agentSessionsWelcomePage`に設定して、最近のセッション、埋め込みチャット、クイックアクションを含む[VS Codeウェルカムページ](/docs/copilot/chat/chat-sessions.md#vs-code-welcome-page)を表示します。 | N/A |
| `setting(chat.viewSessions.enabled)` <br/>チャットビューにエージェントセッションリストを表示します。 | `true` |
| `setting(chat.agentsControl.enabled)` _(実験的)_<br/>コマンドセンターで[エージェント状態インジケーター](/docs/copilot/agents/overview.md#agent-status-indicator-experimental)を有効にします。未読およびセッション内バッジを表示します。 | `true` |
| `setting(chat.agentsControl.clickBehavior)` _(実験的)_<br/>エージェント状態インジケーターでチャットアイコンを選択するときの動作を設定します。 | `"cycle"`(Insiders)<br/>`"default"`(Stable) |
| `setting(chat.unifiedAgentsBar.enabled)` _(実験的)_<br/>コマンドセンター検索ボックスを統合チャットおよび検索コントロールに置き換えます。 | `false` |

##インラインチャット設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(inlineChat.defaultModel)`<br/>エディターのインラインチャット用のデフォルト言語モデルを設定します。選択したモデルはセッション中は保持されますが、VS Codeが再読み込みされた後はこの設定されたデフォルトにリセットされます。 | N/A |
| `setting(inlineChat.renderMode)` _(実験的)_<br/>インラインチャットの表示方法を設定します。`hover`: フローティングオーバーレイでインラインチャットを表示、`zone`: エディターで専用ゾーンでインラインチャットを表示します。 | `"hover"` |
| `setting(inlineChat.finishOnType)`<br/>変更された領域の外にテキストを入力したときにエディターのインラインチャットセッションを完了します。 | `false` |
| `setting(inlineChat.holdToSpeech)`<br/>エディタのインラインチャットキーボードショートカット(`kb(inlineChat.start)`)を押し続けると、音声認識が自動的に有効になります。 | `true` |
| `setting(editor.inlineSuggest.syntaxHighlightingEnabled)`<br/>インライン候補に対して構文ハイライトを表示します。 | `true` |
| `setting(inlineChat.affordance)` _(実験的)_<br/>テキストを選択するときに視覚的なヒントを表示して、インラインチャットを開始できるようにします。`off`: ヒントなし、`gutter`: 行番号領域に表示、`editor`: カーソル位置で電球表示。 | `"off"` |
| `setting(inlineChat.lineEmptyHint)` _(実験的)_<br/>空の行でエディターのインラインチャットのヒントを表示します。 | `false` |
| `setting(inlineChat.lineNaturalLanguageHint)` _(実験的)_<br/>行がほぼ単語で構成されるとすぐに、エディターのインラインチャットをトリガーします。 | `true` |
| `setting(github.copilot.chat.editor.temporalContext.enabled)` _(実験的)_<br/>最近表示および編集したファイルをエディターのインラインチャットのコンテキストに含めます。 | `false` |

##コードレビュー設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.reviewSelection.enabled)` _(プレビュー)_<br/>エディターテキスト選択のAIを使用したコードレビューを有効にします。 | `true` |
| `setting(github.copilot.chat.reviewSelection.instructions)` _(プレビュー)_<br/>現在のエディター選択をAIでレビューするリクエストに追加されるカスタム命令。 | `[]` |

##カスタム命令設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.instructionsFilesLocations)` <br/>カスタム命令ファイルを検索する場所。各フォルダーは再帰的に検索され、サブディレクトリーが含まれます。相対パスはワークスペースのルートフォルダーから解決されます。ファイルパスのグロブパターンをサポートしています。 | `{ ".github/instructions": true, "~/.claude/rules": false" }` |
| `setting(chat.includeApplyingInstructions)`<br/>マッチング`applyTo`パターンを使用して命令ファイルをチャットリクエストに自動的に追加します。 | `true` |
| `setting(chat.includeReferencedInstructions)`<br/>Markdownリンク経由で参照される命令ファイルをチャットリクエストに自動的に追加します。 | `false` |
| `setting(github.copilot.chat.codeGeneration.useInstructionFiles)`<br/>`.github/copilot-instructions.md`からカスタム命令をチャットリクエストに自動的に追加します。 | `true` |
| `setting(github.copilot.chat.commitMessageGeneration.instructions)` _(実験的)_<br/>AIでコミットメッセージを生成するためのカスタム命令。 | `[]` |
| `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` _(実験的)_<br/>AIでプルリクエストのタイトルと説明を生成するためのカスタム命令。 | `[]` |

##再利用可能なプロンプトファイル設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.promptFilesLocations)` <br/>プロンプトファイルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ファイルパスのグロブパターンをサポートしています。 | `{ ".github/prompts": true }` |
| `setting(chat.promptFilesRecommendations)` <br/>新しいチャットセッションを開くときのプロンプトファイル推奨を有効または無効にします。プロンプトファイル名とブール値またはwhenクローゼのキー値ペアのリスト。 | `[]` |

##カスタムエージェント設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.agentFilesLocations)` <br/>カスタムエージェントファイルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ユーザー固有のパスに対して、ホームディレクトリ拡張(`~`)をサポートしています。 | `{ ".github/agents": true }` |
| `setting(chat.customAgentInSubagent.enabled)` _(実験的)_<br/>カスタムエージェントを[サブエージェント](/docs/copilot/agents/subagents.md)で使用できるようにします。 | `false` |
| `setting(github.copilot.chat.cli.customAgents.enabled)` _(実験的)_<br/>GitHubバックグラウンドエージェントセッションからカスタムエージェントを使用できるようにします。 | `false` |

##エージェントスキル設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.useAgentSkills)` <br/>VS Codeで[エージェントスキル](/docs/copilot/customization/agent-skills.md)のサポートを有効にします。 | `true` |
| `setting(chat.agentSkillsLocations)` <br/>エージェントスキルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ユーザー固有のパスに対して、ホームディレクトリ拡張(`~`)をサポートしています。 | `"chat.agentSkillsLocations": { ".github/skills": true,".claude/skills": true,"~/.copilot/skills": true,"~/.claude/skills": true}` |

##デバッグ設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.startDebugging.enabled)` _(プレビュー)_<br/>チャットビューで実験的な`/startDebugging`インテントを有効にして、デバッグ構成を生成します。 | `true` |
| `setting(github.copilot.chat.copilotDebugCommand.enabled)` _(プレビュー)_<br/>`copilot-debug`ターミナルコマンドを有効にします。 | `true` |

##テスト設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.generateTests.codeLens)` _(実験的)_<br/>現在のテストカバレッジ情報でカバーされていないシンボルの**テストを生成**コードレンズを表示します。 | `false` |
| `setting(github.copilot.chat.setupTests.enabled)` _(実験的)_<br/>実験的な`/setupTests`インテントと`/tests`生成時のプロンプトを有効にします。 | `true` |

##ノートブック設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(notebook.experimental.generate)` _(実験的)_<br/>ノートブックのインラインチャットでコードセルを作成するための**生成**アクションを有効にします。 | `true` |
| `setting(github.copilot.chat.edits.newNotebook.enabled)` _(実験的)_<br/>編集モード(非推奨)でノートブックツールを有効にして、新しいノートブックファイルを作成します。 | `true` |
| `setting(github.copilot.chat.notebook.followCellExecution.enabled)` _(実験的)_<br/>エディターで現在実行中のセルを表示します。 | `false` |

##アクセシビリティー設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(inlineChat.accessibleDiffView)`<br/>インラインチャットの変更に対してアクセシビリティー対応の差分ビューアーをレンダリングするかどうか。 | `"auto"` |
| `setting(accessibility.signals.chatRequestSent)`<br/>チャットリクエストが送信されたときに、信号(音声キュー)または発表(アラート)を再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.chatResponseReceived)`<br/>レスポンスを受け取ったときに音声/音声キューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatEditModifiedFile)`<br/>ファイルがチャット編集で変更されたときに音声/音声キューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatUserActionRequired)`<br/>ユーザーがチャットでアクションを実施する必要がある場合に音声/音声キューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.lineHasInlineSuggestion)`<br/>カーソルがインライン候補を含む行にある場合に音声/音声キューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.nextEditSuggestion)`<br/>次の編集候補が利用可能な場合に音声/音声キューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.verboseChatProgressUpdates)`<br/>チャット活動に関する詳細な更新を提供します。 | `true` |
| `setting(accessibility.verbosity.inlineChat)`<br/>インラインエディターチャットアクセシビリティーヘルプメニューにアクセスする方法についての情報を提供し、入力がフォーカスされてときに機能の使用方法を説明するヒントでアラートします。 | `true` |
| `setting(accessibility.verbosity.inlineCompletions)`<br/>インライン候補ホバーとアクセシビリティービューにアクセスする方法についての情報を提供します。 | `true` |
| `setting(accessibility.verbosity.panelChat)`<br/>チャット入力がフォーカスされている場合に、チャットヘルプメニューにアクセスする方法についての情報を提供します。 | `true` |
| `setting(accessibility.voice.keywordActivation)`<br/>キーワードフレーズ「HeyCode」を認識してボイスチャットセッションを開始するかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.autoSynthesize)`<br/>音声が入力として使用された場合に、テキストレスポンスを自動的に大声で読み上げるかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.speechTimeout)`<br/>音声音声認識が、あなたが話すのを止めた後にアクティブなままになる期間(ミリ秒)。 | `1200` |

##関連リソース

* [VS CodeのCopilot機能の概要をご覧ください](/docs/copilot/reference/copilot-vscode-features.md)

