---
ContentId: 7b232695-cbbe-4f3f-a625-abc7a5e6496c
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeのGitHub Copilotの設定リファレンスです。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeのGitHub Copilot設定リファレンス

このページではVisual Studio CodeのGitHub Copilotの設定オプションについて説明します。VS Codeでの設定全般については、[ユーザーとワークスペースの設定](/docs/configure/settings.md)を参照してください。

チームはCopilot in VS Codeの改善と新機能の追加に継続的に取り組んでいます。一部の機能はまだ実験段階です。ぜひ試してみて、[GitHubのIssue](https://github.com/microsoft/vscode/issues)でフィードバックをお聞かせください。[VS Codeの機能ライフサイクル](/docs/configure/settings.md#feature-lifecycle)の詳細をご覧ください。

> [!TIP]
> まだCopilotサブスクリプションを持っていない場合は、[Copilot Free プラン](https://github.com/github-copilot/signup)にサインアップして、無料でCopilotを使用できます。月間のインラインサジェストとチャット操作に制限があります。

## 一般的な設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.commandCenter.enabled)`<br/>VS Codeのタイトルバーにチャットメニューを表示するかどうかを制御します。 | `true` |
| `setting(workbench.settings.showAISearchToggle)`<br/>設定エディターでAIを使用した設定検索を有効にします。 | `true` |
| `setting(workbench.commandPalette.experimental.askChatLocation)` _(実験段階)_<br/>コマンドパレットがチャット質問をどこに表示するかを制御します。 | `"chatView"` |
| `setting(search.searchView.semanticSearchBehavior)` _(プレビュー)_<br/>検索ビューでセマンティック検索を実行するタイミングを設定します。手動(既定)、テキスト検索が結果を返さない場合、常になど。 | `"manual"` |
| `setting(search.searchView.keywordSuggestions)` _(プレビュー)_<br/>検索ビューにキーワード提案を表示するかどうかを制御します。 | `false` |

## コード編集設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.editor.enableCodeActions)`<br/>利用可能な場合、Copilotコマンドをコードアクションとして表示するかどうかを制御します。 | `true` |
| `setting(github.copilot.renameSuggestions.triggerAutomatically)`<br/>シンボルの名前変更の提案を生成します。 | `true` |
| `setting(github.copilot.enable)`<br/>指定された[言語](/docs/languages/identifiers.md)のインラインサジェストを有効または無効にします。 | `{ "*": true, "plaintext": false, "markdown": false, "scminput": false }` |
| `setting(github.copilot.nextEditSuggestions.enabled)`<br/>[次の編集タスク](/docs/copilot/ai-powered-suggestions.md#next-edit-suggestions)(NES)を有効にします。 | `true` |
| `setting(editor.inlineSuggest.edits.allowCodeShifting)`<br/>NESがサジェストを表示するためにコードをシフトできるかどうかを設定します。 | `"always"` |
| `setting(editor.inlineSuggest.edits.renderSideBySide)`<br/>NESがより大きなサジェストを側に並べて表示できるか、またはCopilot NESが常により大きなサジェストを関連するコードの下に表示するかを設定します。 | `"auto"` |
| `setting(github.copilot.nextEditSuggestions.fixes)`<br/>診断(波線)に基づいて次の編集タスクを有効にします。例えば、不足しているインポートなど。 | `true` |
| `setting(editor.inlineSuggest.minShowDelay)`<br/>インラインサジェストを表示する前に待機する時間(ミリ秒単位)。 | `0` |

## チャット設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.localeOverride)`<br/>チャット応答のロケールを指定します。例えば`en`または`fr`。 | `"auto"` |
| `setting(github.copilot.chat.useProjectTemplates)`<br/>`/new`を使用する際に、関連するGitHubプロジェクトをスタータープロジェクトとして使用します。 | `true` |
| `setting(github.copilot.chat.scopeSelection)`<br/>`/explain`を使用して、アクティブなエディターに選択がない場合に特定のシンボルスコープを提示するかどうかを指定します。 | `false` |
| `setting(github.copilot.chat.terminalChatLocation)`<br/>ターミナルからのチャットクエリをどこで開くかを制御します。 | `"chatView"` |
| `setting(chat.detectParticipant.enabled)`<br/>チャットビューでチャット参加者の検出を有効にします。 | `true` |
| `setting(chat.checkpoints.enabled)` <br/>チャットで[チェックポイント](/docs/copilot/chat/chat-checkpoints.md)を有効または無効にします。 | `true` |
| `setting(chat.checkpoints.showFileChanges)` <br/>各チャットリクエストの最後にファイル変更のサマリーを表示します。 | `false` |
| `setting(chat.editRequests)`<br/>[前のチャットリクエストの編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)を有効または無効にします。 | `"inline"` |
| `setting(chat.editor.fontFamily)`<br/>チャットコードブロックのフォント族。 | `"default"` |
| `setting(chat.editor.fontSize)`<br/>チャットコードブロックのフォントサイズ(ピクセル)。 | `14` |
| `setting(chat.editor.fontWeight)`<br/>チャットコードブロックのフォントウェイト。 | `"default"` |
| `setting(chat.editor.lineHeight)`<br/>チャットコードブロックの行の高さ(ピクセル)。 | `0` |
| `setting(chat.editor.wordWrap)`<br/>チャットコードブロックの空行を切り替えます。 | `"off"` |
| `setting(chat.editing.confirmEditRequestRemoval)`<br/>編集を取り消す前に確認を求めます。 | `true` |
| `setting(chat.editing.confirmEditRequestRetry)`<br/>最後の編集のやり直しを実行する前に確認を求めます。 | `true` |
| `setting(chat.editing.autoAcceptDelay)`<br/>提案された編集が自動的に受け入れられる遅延を設定します。自動受け入れを無効にするには0を使用します。 | `0` |
| `setting(chat.fontFamily)`<br/>チャットのMarkdownコンテンツのフォント族。 | `"default"` |
| `setting(chat.fontSize)`<br/>チャットのMarkdownコンテンツのフォントサイズ(ピクセル)。 | `13` |
| `setting(chat.notifyWindowOnConfirmation)`<br/>ユーザー入力が必要な場合のOS通知表示タイミングを設定します。`off`は通知を表示しません。`windowNotFocused`(既定)はVS Codeウィンドウがフォーカスされていない場合にのみ通知を表示します。`always`は常に通知を表示します。 | `"windowNotFocused"` |
| `setting(chat.notifyWindowOnResponseReceived)`<br/>チャット応答を受け取った場合のOS通知表示タイミングを設定します。`off`は通知を表示しません。`windowNotFocused`(既定)はVS Codeウィンドウがフォーカスされていない場合にのみ通知を表示します。`always`は常に通知を表示します。 | `"windowNotFocused"` |
| `setting(chat.requestQueuing.defaultAction)`<br/>リクエストが進行中の**送信**ボタンのデフォルトアクションを設定します。`queue`はメッセージをキューに追加します。`steer`は現在のリクエストをイールドするよう通知します。 | `"queue"` |
| `setting(chat.tools.terminal.autoReplyToPrompts)` <br/>ターミナルプロンプトにデフォルトの答えで自動的に返信します。 | `false` |
| `setting(chat.tools.terminal.terminalProfile.<platform>)`<br/>各プラットフォームでチャットターミナルコマンドに使用するターミナルプロフィールを設定します。 | `""` |
| `setting(chat.hookFilesLocations)` _(プレビュー)_ <br/>追加の[フックファイルの場所](/docs/copilot/customization/hooks.md#hook-file-locations)を設定します。フォルダへのパス(すべての`*.json`ファイルを読み込みます)または`.json`ファイルへの直接パスを指定します。相対パスと~記号付きパスのみがサポートされています。 | `{}` |
| `setting(chat.useCustomAgentHooks)` _(プレビュー)_ <br/>カスタムエージェントのフロントマターに定義された[エージェント スコープ フック](/docs/copilot/customization/hooks.md#agentscoped-hooks)を有効にします。有効にすると、`.agent.md`ファイル内のフックはそのエージェントがアクティブなときのみ実行されます。 | `false` |
| `setting(chat.useAgentsMdFile)` <br/>`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用するかどうかを有効または無効にします。 | `true` |
| `setting(chat.math.enabled)` <br/>チャットの[KaTeX](https://katex.org)での数式レンダリングを有効または無効にします。 | `false` |
| `setting(chat.viewTitle.enabled)` _(プレビュー)_<br/>現在のチャットセッションのタイトルをチャットヘッダーに表示します。 | `true` |
| `setting(github.copilot.chat.codesearch.enabled)` _(プレビュー)_<br/>プロンプトで`#codebase`を使用する場合、Copilotは編集するための関連ファイルを自動的に検出します。 | `false` |
| `setting(chat.emptyState.history.enabled)` _(実験段階)_<br/>チャットビューの空の状態で最近のチャット履歴を表示します。 | `false` |
| `setting(chat.sendElementsToChat.enabled)` _(実験段階)_<br/>[統合ブラウザー](/docs/debugtest/integrated-browser.md)からチャットビューにコンテキストとして要素を送信できるようにします。 | `true` |
| `setting(workbench.browser.enableChatTools)` _(実験段階)_<br/>エージェントが統合ブラウザー内のページと相互作用できるようにする[ブラウザーツール](/docs/debugtest/integrated-browser.md#browser-tools-for-agents)を有効にします。 | `false` |
| `setting(chat.useNestedAgentsMdFiles)` _(実験段階)_<br/>ワークスペースのサブフォルダ内の`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用するかどうかを有効または無効にします。 | `false` |
| `setting(github.copilot.chat.customOAIModels)` _(実験段階)_<br/>チャット用にカスタムOpenAI互換モデルを設定します。 | `[]` |
| `setting(github.copilot.chat.edits.suggestRelatedFilesFromGitHistory)` _(実験段階)_<br/>チャットコンテキストでgit履歴から関連ファイルを提案します。 | `true` |

## エージェント設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.agent.enabled:true)`<br/>エージェントの使用を有効または無効にします(VS Code 1.99以降が必要)。 | `true` |
| `setting(chat.agent.maxRequests)`<br/>Copilotがエージェントを使用して実行できるリクエストの最大数。 | `25` |
| `setting(github.copilot.chat.agent.autoFix)`<br/>生成されたコード変更の問題を自動的に診断して修正します。 | `true` |
| `setting(chat.mcp.access)`<br/>VS Codeでどのモデルコンテキストプロトコル(MCP)サーバーを使用できるかを管理します。 | `true` |
| `setting(chat.mcp.discovery.enabled)`<br/>他のアプリケーションからのMCPサーバー構成の自動検出を設定します。 | `false` |
| `setting(chat.mcp.serverSampling)`<br/>MCPサーバーに公開されるモデルを設定します。 | `{}` |
| `setting(chat.mcp.apps.enabled)` _(実験段階)_<br/>MCPサーバーが提供するリッチユーザーインターフェースであるMCPアプリを有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.autoApprove)` <br/>[エージェントを使用する場合に自動承認される](/docs/copilot/agents/agent-tools.md#automatically-approve-terminal-commands)ターミナルコマンドを制御します。コマンドは`true`(自動承認)または`false`(承認が必要)に設定できます。正規表現は`/`文字で囲むことで使用できます。 | `{ "rm": false, "rmdir": false, "del": false, "kill": false, "curl": false, "wget": false, "eval": false, "chmod": false, "chown": false, "/^Remove-Item\\b/i": false }` |
| `setting(chat.tools.terminal.enableAutoApprove)` <br/>ターミナルコマンドの自動承認を有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.enforceTimeoutFromModel)` _(実験段階)_<br/>エージェントが指定したターミナルコマンドのタイムアウト値を強制するかどうかを制御します。有効にすると、エージェントは指定の期間の後にコマンドの追跡を停止し、それまでに収集した出力を返します。 | `true` |
| `setting(chat.tools.terminal.ignoreDefaultAutoApproveRules)` <br/>ターミナルコマンドのデフォルト自動承認ルールを無視します。 | `false` |
| `setting(chat.tools.global.autoApprove)`<br/>すべてのツールを自動的に承認します。この設定では[重要なセキュリティ保護が無効になります](/docs/copilot/security.md)。 | `false` |
| `setting(chat.autopilot.enabled)` _(実験段階)_<br/>[Autopilot権限レベル](/docs/copilot/agents/agent-tools.md#permission-levels)が権限ピッカーで利用可能かどうかを制御します。有効にすると、Autopilotはすべてのツール呼び出しを自動承認し、タスクが完了するまで継続します。 | `true` |
| `setting(chat.tools.urls.autoApprove)` <br/>[自動承認されるURLリクエストとレスポンス](/docs/copilot/agents/agent-tools.md#url-approval)を制御します。 | `[]` |
| `setting(chat.agent.thinking.collapsedTools)` _(実験段階)_<br/>チャット会話でツール呼び出しの詳細がデフォルトで折りたたまれているか展開されているかを設定します。 | `always` |
| `setting(chat.agent.thinkingStyle)` _(実験段階)_<br/>考えるトークンをチャットで表示する方法を設定します。 | `fixedScrolling` |
| `setting(chat.mcp.autoStart)` _(実験段階)_<br/>MCP設定の変更が検出されたときにMCPサーバーを自動的に開始します。 | `newAndOutdated` |
| `setting(chat.tools.eligibleForAutoApproval)` _(実験段階)_<br/>エージェントが使用する前に手動承認が必要なツールを設定します。 | `[]` |
| `setting(chat.tools.terminal.blockDetectedFileWrites)` _(実験段階)_<br/>ファイル書き込みを実行するターミナルコマンドの場合、ユーザー承認が必要です。 | `outsideWorkspace` |
| `setting(chat.tools.terminal.sandbox.enabled)` _(実験段階)_<br/>エージェントが実行するターミナルコマンドの[サンドボックス化](/docs/copilot/agents/agent-tools.md#sandbox-terminal-commands-experimental)を有効にします(macOSおよびLinuxのみ)。有効にすると、コマンドは自動承認され、ファイルシステムとネットワークアクセスが制限されます。 | `false` |
| `setting(chat.tools.terminal.sandbox.linuxFileSystem)` _(実験段階)_<br/>Linuxでのサンドボックス化されたターミナルコマンドのファイルシステムアクセスルールを設定します。`allowWrite`、`denyWrite`、`denyRead`プロパティをサポートしています。 | `{}` |
| `setting(chat.tools.terminal.sandbox.macFileSystem)` _(実験段階)_<br/>macOSでのサンドボックス化されたターミナルコマンドのファイルシステムアクセスルールを設定します。`allowWrite`、`denyWrite`、`denyRead`プロパティをサポートしています。 | `{}` |
| `setting(chat.tools.terminal.sandbox.network)` _(実験段階)_<br/>サンドボックス化されたターミナルコマンドのネットワークアクセスルールを設定します。許可されたドメインを指定する`allowedDomains`と、[信頼できるドメイン](/docs/editing/editingevolved.md#outgoing-link-protection)リストのドメインを含める`allowTrustedDomains`をサポートしています。 | `{}` |
| `setting(github.copilot.chat.newWorkspaceCreation.enabled)` _(実験段階)_<br/>チャットで新しいワークスペースをスキャフォールディングするためのツールを有効にします。 | `true` |
| `setting(github.copilot.chat.agent.thinkingTool:true)` _(実験段階)_<br/>エージェントを使用する場合に考えるツールを有効にします。 | `false` |
| `setting(github.copilot.chat.summarizeAgentConversationHistory.enabled)` _(実験段階)_<br/>コンテキストウィンドウがいっぱいになった場合、エージェント会話履歴を自動的に要約します。 | `true` |
| `setting(github.copilot.chat.virtualTools.threshold)` _(実験段階)_<br/>仮想ツールを使用する必要があるツール数。仮想ツールは同様のツールセットをグループ化し、モデルがオンデマンドで有効にできるようにします。チャットリクエストあたり128ツールの制限を超えて使用できます。 | `128` |

## エージェントセッション

[エージェントビュー](/docs/copilot/agents/overview.md)は、ローカルチャット会話とリモートコーディングエージェントセッションの両方を管理するための一元的な場所を提供します。このビューを使用して、複数のAIセッションを同時に操作でき、進捗を追跡し、長時間実行されるタスクを効率的に管理できます。

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(workbench.startupEditor)` <br/>VS Codeのウェルカムページをエージェントセッションのエントリーポイントとして機能するように設定します。`agentSessionsWelcomePage`に設定すると、[VS Codeのウェルカムページ](/docs/copilot/chat/chat-sessions.md#vs-code-welcome-page)が最近のセッション、埋め込みチャット、クイックアクションと共に表示されます。 | N/A |
| `setting(chat.viewSessions.enabled)` <br/>チャットビューにエージェントセッションリストを表示します。 | `true` |
| `setting(chat.agentsControl.enabled)` _(実験段階)_<br/>コマンドセンターで[エージェントステータスインジケーター](/docs/copilot/agents/overview.md#agent-status-indicator-experimental)を有効にします。未読および進行中のセッションバッジを表示します。 | `true` |
| `setting(chat.agentsControl.clickBehavior)` _(実験段階)_<br/>エージェントステータスインジケーターでチャットアイコンをクリックしたときの動作を設定します。 | `"cycle"` (Insiders)<br/>`"default"` (Stable) |
| `setting(chat.unifiedAgentsBar.enabled)` _(実験段階)_<br/>コマンドセンター検索ボックスを統合チャットと検索コントロールに置き換えます。 | `false` |

## インラインチャット設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(inlineChat.defaultModel)`<br/>エディターインラインチャットのデフォルト言語モデルを設定します。選択したモデルはセッション中は保持されますが、VS Codeを再度読み込むとこの設定されたデフォルトにリセットされます。 | N/A |
| `setting(inlineChat.renderMode)` _(実験段階)_<br/>インラインチャットの表示方法を設定します。`hover`:フローティングオーバーレイでインラインチャットを表示、`zone`:エディターの専用ゾーンでインラインチャットを表示。 | `"hover"` |
| `setting(inlineChat.finishOnType)`<br/>変更されたリージョンの外でタイプしたとき、エディターインラインチャットセッションを終了します。 | `false` |
| `setting(inlineChat.holdToSpeech)`<br/>エディターインラインチャットキーボードショートカット(`kb(inlineChat.start)`)を押し続けると、音声認識が自動的に有効になります。 | `true` |
| `setting(editor.inlineSuggest.syntaxHighlightingEnabled)`<br/>インラインサジェストに構文強調表示を表示します。 | `true` |
| `setting(inlineChat.affordance)` _(実験段階)_<br/>テキストを選択するときに視覚的なヒントを表示して、インラインチャットを開始するのに役立ちます。`off`:ヒントなし、`gutter`:行番号領域に表示、`editor`:カーソル位置に電球で表示。 | `"off"` |
| `setting(inlineChat.lineEmptyHint)` _(実験段階)_<br/>空の行でエディターインラインチャットのヒントを表示します。 | `false` |
| `setting(inlineChat.lineNaturalLanguageHint)` _(実験段階)_<br/>行がほぼ単語で構成されるとすぐに、エディターインラインチャットをトリガーします。 | `true` |
| `setting(github.copilot.chat.editor.temporalContext.enabled)` _(実験段階)_<br/>最近表示および編集されたファイルをエディターインラインチャットのコンテキストに含めます。 | `false` |

## コードレビュー設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.reviewSelection.enabled)` _(プレビュー)_<br/>エディターテキスト選択に対するAIコードレビューを有効にします。 | `true` |
| `setting(github.copilot.chat.reviewSelection.instructions)` _(プレビュー)_<br/>現在のエディター選択のAIレビューをリクエストするときに追加されるカスタム指示。 | `[]` |

## カスタム指示設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.instructionsFilesLocations)` <br/>カスタム指示ファイルを検索する場所。各フォルダはサブディレクトリを含めて再帰的に検索されます。相対パスはワークスペースのルートフォルダーから解決されます。ファイルパスのグロブパターンをサポートしています。 | `{ ".github/instructions": true, "~/.claude/rules": false" }` |
| `setting(chat.includeApplyingInstructions)`<br/>マッチングする`applyTo`パターンを持つ指示ファイルをチャットリクエストに自動的に追加します。 | `true` |
| `setting(chat.includeReferencedInstructions)`<br/>Markdownリンク経由で参照される指示ファイルをチャットリクエストに自動的に追加します。 | `false` |
| `setting(github.copilot.chat.codeGeneration.useInstructionFiles)`<br/>`.github/copilot-instructions.md`からカスタム指示をチャットリクエストに自動的に追加します。 | `true` |
| `setting(github.copilot.chat.commitMessageGeneration.instructions)` _(実験段階)_<br/>AIでコミットメッセージを生成するためのカスタム指示。 | `[]` |
| `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` _(実験段階)_<br/>AIでプルリクエストのタイトルと説明を生成するためのカスタム指示。 | `[]` |

## 再利用可能なプロンプトファイル設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.promptFilesLocations)` <br/>プロンプトファイルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ファイルパスのグロブパターンをサポートしています。 | `{ ".github/prompts": true }` |
| `setting(chat.promptFilesRecommendations)` <br/>新しいチャットセッションを開くときのプロンプトファイル推奨を有効または無効にします。プロンプトファイル名と論理値またはwhen句のキーと値のペアのリスト。 | `[]` |

## カスタムエージェント設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.agentFilesLocations)` <br/>カスタムエージェントファイルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ユーザー固有のパスの場合、ホームディレクトリの拡張(`~`)をサポートしています。 | `{ ".github/agents": true }` |
| `setting(chat.customAgentInSubagent.enabled)` _(実験段階)_<br/>[サブエージェント](/docs/copilot/agents/subagents.md)でカスタムエージェントの使用を有効にします。 | `false` |
| `setting(github.copilot.chat.cli.customAgents.enabled)` _(実験段階)_<br/>GitHubバックグラウンドエージェントセッションからカスタムエージェントを使用できるようにします。 | `false` |

## エージェントスキル設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.useAgentSkills)` <br/>VS Codeで[エージェントスキル](/docs/copilot/customization/agent-skills.md)のサポートを有効にします。 | `true` |
| `setting(chat.agentSkillsLocations)` <br/>エージェントスキルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ユーザー固有のパスの場合、ホームディレクトリの拡張(`~`)をサポートしています。 | `"chat.agentSkillsLocations": { ".github/skills": true,".claude/skills": true,"~/.copilot/skills": true,"~/.claude/skills": true}` |

## デバッグ設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.startDebugging.enabled)` _(プレビュー)_<br/>チャットビューで実験的な`/startDebugging`インテントを有効にして、デバッグ設定を生成します。 | `true` |
| `setting(github.copilot.chat.copilotDebugCommand.enabled)` _(プレビュー)_<br/>`copilot-debug`ターミナルコマンドを有効にします。 | `true` |

## テスト設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.generateTests.codeLens)` _(実験段階)_<br/>現在のテストカバレッジ情報でカバーされていないシンボルの**テストの生成**コードレンズを表示します。 | `false` |
| `setting(github.copilot.chat.setupTests.enabled)` _(実験段階)_<br/>実験的な`/setupTests`インテントと`/tests`生成でのプロンプト表示を有効にします。 | `true` |

## ノートブック設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(notebook.experimental.generate)` _(実験段階)_<br/>ノートブックインラインチャットでコードセルを作成するための**生成**アクションを有効にします。 | `true` |
| `setting(github.copilot.chat.edits.newNotebook.enabled)` _(実験段階)_<br/>編集モード(非推奨)のノートブックツールを有効にして、新しいノートブックファイルを作成します。 | `true` |
| `setting(github.copilot.chat.notebook.followCellExecution.enabled)` _(実験段階)_<br/>現在実行中のセルをエディターに表示します。 | `false` |

## アクセシビリティ設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(inlineChat.accessibleDiffView)`<br/>インラインチャットがその変更のアクセシブルなDiffビューアーもレンダリングするかどうかを指定します。 | `"auto"` |
| `setting(accessibility.signals.chatRequestSent)`<br/>チャットリクエストが作成されると、シグナル(オーディオキュー)またはアナウンスメント(アラート)を再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.chatResponseReceived)`<br/>応答が受け取られると、音またはオーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatEditModifiedFile)`<br/>ファイルがチャット編集で変更されると、音またはオーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatUserActionRequired)`<br/>ユーザーがチャットでアクションを実行する必要がある場合、音またはオーディオキューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.lineHasInlineSuggestion)`<br/>カーソルがインラインサジェストを持つ行にある場合、音またはオーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.nextEditSuggestion)`<br/>次の編集タスクが利用可能な場合、音またはオーディオキューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.verboseChatProgressUpdates)`<br/>チャットアクティビティについて詳細な更新を提供します。 | `true` |
| `setting(accessibility.verbosity.inlineChat)`<br/>インラインエディターチャットアクセシビリティヘルプメニューにアクセスする方法に関する情報を提供し、入力がフォーカスされたときの機能の使用方法を説明するヒント付きアラートを提供します。 | `true` |
| `setting(accessibility.verbosity.inlineCompletions)`<br/>インラインサジェストホバーとアクセシブルビューにアクセスする方法に関する情報を提供します。 | `true` |
| `setting(accessibility.verbosity.panelChat)`<br/>チャット入力がフォーカスされたときにチャットヘルプメニューにアクセスする方法に関する情報を提供します。 | `true` |
| `setting(accessibility.voice.keywordActivation)`<br/>音声チャットセッションを開始するための'Hey Code'というキーワードフレーズが認識されるかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.autoSynthesize)`<br/>音声が入力として使用された場合、テキスト応答を自動的に音声で読み上げるかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.speechTimeout)`<br/>音声認識の話し終わった後もアクティブなままの時間(ミリ秒単位)。 | `1200` |

## 関連リソース

* [VS Codeで利用可能なCopilot機能のクイックオーバービュー](/docs/copilot/reference/copilot-vscode-features.md)

