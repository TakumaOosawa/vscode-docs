---
ContentId: 7b232695-cbbe-4f3f-a625-abc7a5e6496c
DateApproved: 01/08/2026
MetaDescription: Visual Studio CodeでのGitHub Copilotの構成設定の概要。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでのGitHub Copilot設定リファレンス

この記事では、Visual Studio CodeでのGitHub Copilotの構成設定の一覧を示します。VS Codeでの設定の操作に関する一般的な情報については、[ユーザーとワークスペースの設定](/docs/configure/settings.md)を参照してください。

チームは、VS CodeでのCopilotの改善と新機能の追加に継続的に取り組んでいます。一部の機能はまだ実験的なものです。ぜひお試しいただき、[issue](https://github.com/microsoft/vscode/issues)でフィードバックをお寄せください。[VS Codeの機能ライフサイクル](/docs/configure/settings.md#feature-lifecycle)に関する詳細情報もご覧ください。

> [!TIP]
> Copilotサブスクリプションをまだお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップして、インライン候補やチャットのやり取りの月間制限付きでCopilotを無料で使用できます。

## 一般設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.commandCenter.enabled)`<br/>VS Codeタイトルバーにチャットメニューを表示するかどうかを制御します。 | `true` |
| `setting(workbench.settings.showAISearchToggle)`<br/>設定エディターでAIを使用した設定の検索を有効にします。 | `true` |
| `setting(workbench.commandPalette.experimental.askChatLocation)` _(実験的)_<br/>コマンドパレットがチャットの質問をする場所を制御します。 | `"chatView"` |
| `setting(search.searchView.semanticSearchBehavior)` _(プレビュー)_<br/>検索ビューでセマンティック検索を実行するタイミングを構成します：手動（デフォルト）、テキスト検索結果が見つからない場合、または常に。 | `"manual"` |
| `setting(search.searchView.keywordSuggestions)` _(プレビュー)_<br/>検索ビューにキーワードの候補を表示するかどうかを制御します。 | `false` |

## コード編集設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.editor.enableCodeActions)`<br/>利用可能な場合にCopilotコマンドをコードアクションとして表示するかどうかを制御します。 | `true` |
| `setting(github.copilot.renameSuggestions.triggerAutomatically)`<br/>シンボルの名前変更候補を生成します。 | `true` |
| `setting(github.copilot.enable)`<br/>指定された[言語](/docs/languages/identifiers.md)のインライン候補を有効または無効にします。 | `{ "*": true, "plaintext": false, "markdown": false, "scminput": false }` |
| `setting(github.copilot.nextEditSuggestions.enabled)`<br/>[Next Edit Suggestions](/docs/copilot/ai-powered-suggestions.md#next-edit-suggestions) (NES)を有効にします。 | `true` |
| `setting(editor.inlineSuggest.edits.allowCodeShifting)`<br/>候補を表示するためにNESがコードをシフトできるかどうかを構成します。 | `"always"` |
| `setting(editor.inlineSuggest.edits.renderSideBySide)`<br/>可能な場合にNESが大きな候補をサイドバイサイドで表示できるか、Copilot NESが常に関連するコードの下に大きな候補を表示するかを構成します。 | `"auto"` |
| `setting(github.copilot.nextEditSuggestions.fixes)`<br/>診断（波線）に基づいたNext Edit Suggestionsを有効にします。例えば、欠落しているインポートなど。 | `true` |
| `setting(editor.inlineSuggest.minShowDelay)`<br/>インライン候補を表示する前に待機する時間（ミリ秒）。 | `0` |

## チャット設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.localeOverride)`<br/>`en`や`fr`など、チャット応答のロケールを指定します。 | `"auto"` |
| `setting(github.copilot.chat.useProjectTemplates)`<br/>`/new`を使用する際、関連するGitHubプロジェクトをスタータープロジェクトとして使用します。 | `true` |
| `setting(github.copilot.chat.scopeSelection)`<br/>`/explain`を使用し、アクティブなエディターに選択がない場合、特定のシンボルスコープを求めるプロンプトを表示するかどうか。 | `false` |
| `setting(github.copilot.chat.terminalChatLocation)`<br/>ターミナルからのチャットクエリを開く場所を制御します。 | `"chatView"` |
| `setting(chat.detectParticipant.enabled)`<br/>チャットビューでのチャット参加者の検出を有効にします。 | `true` |
| `setting(chat.checkpoints.enabled)` <br/>チャットでの[チェックポイント](/docs/copilot/chat/chat-checkpoints.md)を有効または無効にします。 | `true` |
| `setting(chat.checkpoints.showFileChanges)` <br/>各チャットリクエストの最後にファイルの変更概要を表示します。 | `false` |
| `setting(chat.editRequests)`<br/>[以前のチャットリクエストの編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)を有効または無効にします。 | `"inline"` |
| `setting(chat.editor.fontFamily)`<br/>チャットコードブロックのフォントファミリー。 | `"default"` |
| `setting(chat.editor.fontSize)`<br/>チャットコードブロックのフォントサイズ（ピクセル単位）。 | `14` |
| `setting(chat.editor.fontWeight)`<br/>チャットコードブロックのフォントの太さ。 | `"default"` |
| `setting(chat.editor.lineHeight)`<br/>チャットコードブロックの行の高さ（ピクセル単位）。 | `0` |
| `setting(chat.editor.wordWrap)`<br/>チャットコードブロックの折り返しを切り替えます。 | `"off"` |
| `setting(chat.editing.confirmEditRequestRemoval)`<br/>編集を取り消す前に確認を求めます。 | `true` |
| `setting(chat.editing.confirmEditRequestRetry)`<br/>最後の編集のやり直しを実行する前に確認を求めます。 | `true` |
| `setting(chat.editing.autoAcceptDelay)`<br/>提案された編集が自動的に受け入れられるまでの遅延時間を構成します。0を使用すると自動受け入れが無効になります。 | `0` |
| `setting(chat.fontFamily)`<br/>チャット内のMarkdownコンテンツのフォントファミリー。 | `"default"` |
| `setting(chat.fontSize)`<br/>チャット内のMarkdownコンテンツのフォントサイズ（ピクセル単位）。 | `13` |
| `setting(chat.notifyWindowOnConfirmation)`<br/>ユーザー入力が必要な場合にOSの通知ウィンドウを表示するかどうかを有効または無効にします。 | `true` |
| `setting(chat.notifyWindowOnResponseReceived)`<br/>チャット応答を受信したときにOSの通知ウィンドウを表示するかどうかを有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.autoReplyToPrompts)` <br/>既定の回答でターミナルプロンプトに自動的に返信します。 | `false` |
| `setting(chat.tools.terminal.terminalProfile.<platform>)`<br/>各プラットフォームでチャットターミナルコマンドに使用するターミナルプロファイルを構成します。 | `""` |
| `setting(chat.useAgentsMdFile)` <br/>チャットリクエストのコンテキストとして`AGENTS.md`ファイルを使用することを有効または無効にします。 | `true` |
| `setting(chat.math.enabled)` _(プレビュー)_<br/>チャットでの[KaTeX](https://katex.org)による数式レンダリングを有効または無効にします。 | `false` |
| `setting(chat.viewTitle.enabled)` _(プレビュー)_<br/>チャットヘッダーに現在のチャットセッションのタイトルを表示します。 | `true` |
| `setting(github.copilot.chat.codesearch.enabled)` _(プレビュー)_<br/>プロンプトで`#codebase`を使用すると、Copilotは編集対象の関連ファイルを自動的に検出します。 | `false` |
| `setting(chat.emptyState.history.enabled)` _(実験的)_<br/>チャットビューの空の状態に最近のチャット履歴を表示します。 | `false` |
| `setting(chat.sendElementsToChat.enabled)` _(実験的)_<br/>シンプルブラウザーからチャットビューに要素をコンテキストとして送信することを有効にします。 | `true` |
| `setting(chat.useNestedAgentsMdFiles)` _(実験的)_<br/>ワークスペースのサブフォルダーにある`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用することを有効または無効にします。 | `false` |
| `setting(github.copilot.chat.customOAIModels)` _(実験的)_<br/>チャット用のカスタムOpenAI互換モデルを構成します。 | `[]` |
| `setting(github.copilot.chat.edits.suggestRelatedFilesFromGitHistory)` _(実験的)_<br/>チャットコンテキストでgit履歴から関連ファイルを提案します。 | `true` |

## エージェント設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.agent.enabled:true)`<br/>エージェントの使用を有効または無効にします（VS Code 1.99以降が必要）。 | `true` |
| `setting(chat.agent.maxRequests)`<br/>Copilotがエージェントを使用して行えるリクエストの最大数。 | `25` |
| `setting(github.copilot.chat.agent.autoFix)`<br/>生成されたコード変更の問題を自動的に診断して修正します。 | `true` |
| `setting(chat.mcp.access)`<br/>VS Codeで使用できるModel Context Protocol (MCP)サーバーを管理します。 | `true` |
| `setting(chat.mcp.discovery.enabled)`<br/>他のアプリケーションからのMCPサーバー構成の自動検出を構成します。 | `false` |
| `setting(chat.tools.terminal.autoApprove)` <br/>エージェントの使用時に[自動承認されるターミナルコマンド](/docs/copilot/chat/chat-tools.md#automatically-approve-terminal-commands)を制御します。コマンドは`true`（自動承認）または`false`（承認が必要）に設定できます。`/`文字でパターンを囲むことで正規表現を使用できます。 | `{ "rm": false, "rmdir": false, "del": false, "kill": false, "curl": false, "wget": false, "eval": false, "chmod": false, "chown": false, "/^Remove-Item\\b/i": false }` |
| `setting(chat.tools.terminal.enableAutoApprove)` <br/>ターミナルコマンドの自動承認を有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.ignoreDefaultAutoApproveRules)` <br/>ターミナルコマンドのデフォルトの自動承認ルールを無視します。 | `false` |
| `setting(chat.tools.global.autoApprove)`<br/>すべてのツールを自動的に承認します - この設定は[重要なセキュリティ保護を無効にします](/docs/copilot/security.md)。 | `false` |
| `setting(chat.tools.urls.autoApprove)` <br/>[自動承認されるURLリクエストとレスポンス](/docs/copilot/chat/chat-tools.md#url-approval)を制御します。 | `[]` |
| `setting(chat.agent.thinking.collapsedTools)` _(実験的)_<br/>チャット会話でツール呼び出しの詳細をデフォルトで折りたたむか展開するかを構成します。 | `always` |
| `setting(chat.agent.thinkingStyle)` _(実験的)_<br/>チャットで思考トークンをどのように表示するかを構成します。 | `fixedScrolling` |
| `setting(chat.customAgentInSubagent.enabled)` _(実験的)_<br/>[サブエージェント](/docs/copilot/chat/chat-sessions.md#context-isolated-subagents)を使用したカスタムエージェントの使用を有効にします。 | `false` |
| `setting(chat.mcp.autoStart)` _(実験的)_<br/>MCP構成の変更が検出されたときにMCPサーバーを自動的に起動します。 | `newAndOutdated` |
| `setting(chat.tools.eligibleForAutoApproval)` _(実験的)_<br/>エージェントによって使用される前に手動承認が必要なツールを構成します。 | `[]` |
| `setting(chat.tools.terminal.blockDetectedFileWrites)` _(実験的)_<br/>ファイルの書き込みを実行するターミナルコマンドについてユーザーの承認を要求します。 | `outsideWorkspace` |
| `setting(chat.useAgentSkills)` _(実験的)_<br/>VS Codeでの[エージェントスキル](/docs/copilot/customization/agent-skills.md)のサポートを有効にします。 | `false` |
| `setting(github.copilot.chat.newWorkspaceCreation.enabled)` _(実験的)_<br/>チャットで新しいワークスペースをスキャフォールディングするためのツールを有効にします。 | `true` |
| `setting(github.copilot.chat.agent.thinkingTool:true)` _(実験的)_<br/>エージェントを使用する際に思考ツールを有効にします。 | `false` |
| `setting(github.copilot.chat.cli.customAgents.enabled)` _(実験的)_<br/>GitHubバックグラウンドエージェントセッションからのカスタムエージェントの使用を有効にします。 | `false` |
| `setting(github.copilot.chat.summarizeAgentConversationHistory.enabled)` _(実験的)_<br/>コンテキストウィンドウがいっぱいになったときにエージェントの会話履歴を自動的に要約します。 | `true` |
| `setting(github.copilot.chat.virtualTools.threshold)` _(実験的)_<br/>仮想ツールを使用するツール数のしきい値。仮想ツールは類似したツールのセットをグループ化し、モデルがオンデマンドでそれらをアクティブ化できるようにします。チャットリクエストの128ツールの制限を超えることができます。 | `128` |

## エージェントセッション

[エージェントビュー](/docs/copilot/agents/overview.md)は、ローカルのチャット会話とリモートのコーディングエージェントセッションの両方を管理するための一元化された場所を提供します。このビューを使用すると、複数のAIセッションを同時に操作し、進捗状況を追跡し、長時間実行されるタスクを効率的に管理できます。

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.viewSessions.orientation)` <br/>チャットビューでのエージェントセッションリストの表示方法を構成します。 | `auto` |
| `setting(chat.viewSessions.enabled)` <br/>チャットビューにエージェントセッションリストを表示します。 | `true` |

## インラインチャット設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(inlineChat.finishOnType)`<br/>変更された領域の外側で入力すると、エディターのインラインチャットセッションを終了します。 | `false` |
| `setting(inlineChat.holdToSpeech)`<br/>エディターのインラインチャットのキーボードショートカット（`kb(inlineChat.start)`）を押し続けると、音声認識が自動的に有効になります。 | `true` |
| `setting(editor.inlineSuggest.syntaxHighlightingEnabled)`<br/>インライン候補の構文ハイライトを表示します。 | `true` |
| `setting(inlineChat.lineEmptyHint)` _(実験的)_<br/>空行にエディターのインラインチャットのヒントを表示します。 | `false` |
| `setting(inlineChat.lineNaturalLanguageHint)` _(実験的)_<br/>行のほとんどが単語で構成されている場合、すぐにエディターのインラインチャットをトリガーします。 | `true` |
| `setting(github.copilot.chat.editor.temporalContext.enabled)` _(実験的)_<br/>エディターのインラインチャットのコンテキストに、最近表示および編集したファイルを含めます。 | `false` |

## コードレビュー設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.reviewSelection.enabled)` _(プレビュー)_<br/>エディターのテキスト選択に対するAIによるコードレビューを有効にします。 | `true` |
| `setting(github.copilot.chat.reviewSelection.instructions)` _(プレビュー)_<br/>現在のエディター選択をAIでレビューするリクエストに追加されるカスタム指示。 | `[]` |

## カスタム指示設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.instructionsFilesLocations)` <br/>カスタム指示ファイルを検索する場所。相対パスは、ワークスペースのルートフォルダーから解決されます。ファイルパスのglobパターンをサポートします。 | `{ ".github/instructions": true }` |
| `setting(github.copilot.chat.codeGeneration.useInstructionFiles)`<br/>チャットリクエストに`.github/copilot-instructions.md`からのカスタム指示を自動的に追加します。 | `true` |
| `setting(github.copilot.chat.commitMessageGeneration.instructions)` _(実験的)_<br/>AIでコミットメッセージを生成するためのカスタム指示。 | `[]` |
| `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` _(実験的)_<br/>AIでプルリクエストのタイトルと説明を生成するためのカスタム指示。 | `[]` |

## 再利用可能なプロンプトファイル設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(chat.promptFilesLocations)` <br/>プロンプトファイルを検索する場所。相対パスは、ワークスペースのルートフォルダーから解決されます。ファイルパスのglobパターンをサポートします。 | `{ ".github/prompts": true }` |
| `setting(chat.promptFilesRecommendations)` <br/>新しいチャットセッションを開くときのプロンプトファイルの推奨事項を有効または無効にします。プロンプトファイル名とブール値またはwhen句のキーと値のペアのリスト。 | `[]` |

## デバッグ設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.startDebugging.enabled)` _(プレビュー)_<br/>チャットビューでの実験的な`/startDebugging`インテントを有効にして、デバッグ構成を生成します。 | `true` |
| `setting(github.copilot.chat.copilotDebugCommand.enabled)` _(プレビュー)_<br/>`copilot-debug`ターミナルコマンドを有効にします。 | `true` |

## テスト設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(github.copilot.chat.generateTests.codeLens)` _(実験的)_<br/>現在のテストカバレッジ情報でカバーされていないシンボルに対して**テストの生成**コードレンズを表示します。 | `false` |
| `setting(github.copilot.chat.setupTests.enabled)` _(実験的)_<br/>実験的な`/setupTests`インテントと`/tests`生成でのプロンプトを有効にします。 | `true` |

## ノートブック設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(notebook.experimental.generate)` _(実験的)_<br/>ノートブックのインラインチャットでコードセルを作成するための**生成**アクションを有効にします。 | `true` |
| `setting(github.copilot.chat.edits.newNotebook.enabled)` _(実験的)_<br/>編集モードでノートブックツールを有効にして、新しいノートブックファイルを作成します。 | `true` |
| `setting(github.copilot.chat.notebook.followCellExecution.enabled)` _(実験的)_<br/>現在実行中のセルをエディターに表示します。 | `false` |

## アクセシビリティ設定

| 設定と説明 | デフォルト |
|------------------------|---------------|
| `setting(inlineChat.accessibleDiffView)`<br/>インラインチャットがその変更のためのアクセシブルな差分ビューアーもレンダリングするかどうか。 | `"auto"` |
| `setting(accessibility.signals.chatRequestSent)`<br/>チャットリクエストが行われたときにシグナル（サウンド（オーディオキュー）やアナウンス（アラート））を再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.chatResponseReceived)`<br/>応答を受信したときにサウンド/オーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatEditModifiedFile)`<br/>チャットの編集によってファイルが変更されたときにサウンド/オーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatUserActionRequired)`<br/>ユーザーがチャットでアクションを実行する必要があるときにサウンド/オーディオキューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.lineHasInlineSuggestion)`<br/>カーソルがインライン候補のある行にあるときにサウンド/オーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.nextEditSuggestion)`<br/>Next Edit Suggestionsが利用可能なときにサウンド/オーディオキューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.verboseChatProgressUpdates)`<br/>チャットアクティビティに関する詳細な更新を提供します。 | `true` |
| `setting(accessibility.verbosity.inlineChat)`<br/>入力がフォーカスされているときに、インラインエディターチャットのアクセシビリティヘルプメニューにアクセスする方法と、機能の使用方法を説明するヒントを含むアラートに関する情報を提供します。 | `true` |
| `setting(accessibility.verbosity.inlineCompletions)`<br/>インライン候補のホバーとアクセシブルビューにアクセスする方法に関する情報を提供します。 | `true` |
| `setting(accessibility.verbosity.panelChat)`<br/>チャット入力がフォーカスされているときにチャットヘルプメニューにアクセスする方法に関する情報を提供します。 | `true` |
| `setting(accessibility.voice.keywordActivation)`<br/>音声チャットセッションを開始するためにキーワードフレーズ'Hey Code'を認識するかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.autoSynthesize)`<br/>入力として音声が使用されたときに、テキスト応答を自動的に読み上げるかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.speechTimeout)`<br/>話すのを止めた後に音声認識がアクティブなままである時間（ミリ秒）。 | `1200` |

## 関連リソース

* [VS CodeでのCopilot機能の概要](/docs/copilot/reference/copilot-vscode-features.md)
