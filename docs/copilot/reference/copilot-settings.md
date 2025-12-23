---
ContentId: 7b232695-cbbe-4f3f-a625-abc7a5e6496c
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeにおけるGitHub Copilotの構成設定の概要。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeにおけるGitHub Copilotの設定リファレンス

この記事では、Visual Studio CodeにおけるGitHub Copilotの構成設定を一覧で紹介します。VS Codeでの設定の一般的な使い方については、[ユーザー設定とワークスペース設定](/docs/configure/settings.md)を参照してください。

チームは、VS CodeでのCopilotの改善と新機能の追加に継続的に取り組んでいます。一部の機能はまだ試験段階です。ぜひ試して、[Issues](https://github.com/microsoft/vscode/issues)でフィードバックを共有してください。[VS Codeの機能ライフサイクル](/docs/configure/settings.md#feature-lifecycle)の詳細も確認できます。

> [!TIP]
> Copilotのサブスクリプションがまだない場合は、[Copilot Free plan](https://github.com/github-copilot/signup)にサインアップするとCopilotを無料で利用でき、インライン提案とチャット操作に月ごとの上限が適用されます。

## 一般設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.commandCenter.enabled)`<br/>VS Codeのタイトルバーにチャットメニューを表示するかどうかを制御します。 | `true` |
| `setting(workbench.settings.showAISearchToggle)`<br/>設定エディターでAIによる設定検索を有効にします。 | `true` |
| `setting(workbench.commandPalette.experimental.askChatLocation)` _(Experimental)_<br/>コマンドパレットがチャットの質問を行う場所を制御します。 | `"chatView"` |
| `setting(search.searchView.semanticSearchBehavior)` _(Preview)_<br/>検索ビューでセマンティック検索を実行するタイミングを構成します: 手動(既定)、テキスト検索結果が見つからない場合、または常に。 | `"manual"` |
| `setting(search.searchView.keywordSuggestions)` _(Preview)_<br/>検索ビューにキーワード候補を表示するかどうかを制御します。 | `false` |

## コード編集の設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.editor.enableCodeActions)`<br/>利用可能な場合にCopilotコマンドをコードアクションとして表示するかどうかを制御します。 | `true` |
| `setting(github.copilot.renameSuggestions.triggerAutomatically)`<br/>シンボルの名前変更候補を生成します。 | `true` |
| `setting(github.copilot.enable)`<br/>指定した[言語](/docs/languages/identifiers.md)のインライン提案を有効または無効にします。 | `{ "*": true, "plaintext": false, "markdown": false, "scminput": false }` |
| `setting(github.copilot.nextEditSuggestions.enabled)`<br/>[次の編集の提案](/docs/copilot/ai-powered-suggestions.md#next-edit-suggestions)(NES)を有効にします。 | `true` |
| `setting(editor.inlineSuggest.edits.allowCodeShifting)`<br/>提案を表示するためにNESがコードをシフトできるかどうかを構成します。 | `"always"` |
| `setting(editor.inlineSuggest.edits.renderSideBySide)`<br/>可能であればNESが大きな提案を並べて表示できるか、またはCopilot NESが関連するコードの下に常に大きな提案を表示するかを構成します。 | `"auto"` |
| `setting(github.copilot.nextEditSuggestions.fixes)`<br/>診断(波線)に基づく次の編集の提案を有効にします。例: インポートの不足。 | `true` |
| `setting(editor.inlineSuggest.minShowDelay)`<br/>インライン提案を表示するまでに待機する時間(ミリ秒)。 | `0` |

## チャットの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.localeOverride)`<br/>`en`や`fr`など、チャット応答のロケールを指定します。 | `"auto"` |
| `setting(github.copilot.chat.useProjectTemplates)`<br/>`/new`を使用する際に、関連するGitHubプロジェクトをスタータープロジェクトとして使用します。 | `true` |
| `setting(github.copilot.chat.scopeSelection)`<br/>`/explain`を使用し、アクティブなエディターに選択範囲がない場合に、特定のシンボルスコープを求めるかどうか。 | `false` |
| `setting(github.copilot.chat.terminalChatLocation)`<br/>ターミナルからのチャットクエリを開く場所を制御します。 | `"chatView"` |
| `setting(chat.detectParticipant.enabled)`<br/>チャットビューでのチャット参加者検出を有効にします。 | `true` |
| `setting(chat.checkpoints.enabled)` <br/>チャットの[チェックポイント](/docs/copilot/chat/chat-checkpoints.md)を有効または無効にします。 | `true` |
| `setting(chat.checkpoints.showFileChanges)` <br/>各チャットリクエストの最後に、ファイル変更の概要を表示します。 | `false` |
| `setting(chat.editRequests)`<br/>[以前のチャットリクエストの編集](/docs/copilot/chat/chat-checkpoints.md#edit-a-previous-chat-request)を有効または無効にします。 | `"inline"` |
| `setting(chat.editor.fontFamily)`<br/>チャットのコードブロックで使用するフォントファミリー。 | `"default"` |
| `setting(chat.editor.fontSize)`<br/>チャットのコードブロックで使用するフォントサイズ(ピクセル)。 | `14` |
| `setting(chat.editor.fontWeight)`<br/>チャットのコードブロックで使用するフォントの太さ。 | `"default"` |
| `setting(chat.editor.lineHeight)`<br/>チャットのコードブロックで使用する行の高さ(ピクセル)。 | `0` |
| `setting(chat.editor.wordWrap)`<br/>チャットのコードブロックでの行の折り返しを切り替えます。 | `"off"` |
| `setting(chat.editing.confirmEditRequestRemoval)`<br/>編集を元に戻す前に確認を求めます。 | `true` |
| `setting(chat.editing.confirmEditRequestRetry)`<br/>直前の編集のやり直しを行う前に確認を求めます。 | `true` |
| `setting(chat.editing.autoAcceptDelay)`<br/>提案された編集を自動的に受け入れるまでの遅延を構成します。0を指定すると自動受け入れは無効になります。 | `0` |
| `setting(chat.fontFamily)`<br/>チャット内のMarkdownコンテンツのフォントファミリー。 | `"default"` |
| `setting(chat.fontSize)`<br/>チャット内のMarkdownコンテンツのフォントサイズ(ピクセル)。 | `13` |
| `setting(chat.notifyWindowOnConfirmation)`<br/>ユーザー入力が必要な場合にOS通知ウィンドウを表示するかどうかを有効または無効にします。 | `true` |
| `setting(chat.notifyWindowOnResponseReceived)`<br/>チャット応答を受信した際にOS通知ウィンドウを表示するかどうかを有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.autoReplyToPrompts)` <br/>ターミナルのプロンプトに既定の回答で自動的に返信します。 | `false` |
| `setting(chat.tools.terminal.terminalProfile.<platform>)`<br/>各プラットフォームでチャットのターミナルコマンドに使用するターミナルプロファイルを構成します。 | `""` |
| `setting(chat.useAgentsMdFile)` <br/>`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用することを有効または無効にします。 | `true` |
| `setting(chat.math.enabled)` _(Preview)_<br/>チャットで[KaTeX](https://katex.org)による数式レンダリングを有効または無効にします。 | `false` |
| `setting(chat.viewTitle.enabled)` _(Preview)_<br/>チャットヘッダーに現在のチャットセッションのタイトルを表示します。 | `true` |
| `setting(github.copilot.chat.codesearch.enabled)` _(Preview)_<br/>プロンプトで`#codebase`を使用すると、Copilotが編集対象として関連ファイルを自動的に検出します。 | `false` |
| `setting(chat.emptyState.history.enabled)` _(Experimental)_<br/>チャットビューの空の状態で最近のチャット履歴を表示します。 | `false` |
| `setting(chat.sendElementsToChat.enabled)` _(Experimental)_<br/>Simple Browserからの要素をコンテキストとしてチャットビューに送信することを有効にします。 | `true` |
| `setting(chat.useNestedAgentsMdFiles)` _(Experimental)_<br/>ワークスペースのサブフォルダーにある`AGENTS.md`ファイルをチャットリクエストのコンテキストとして使用することを有効または無効にします。 | `false` |
| `setting(github.copilot.chat.customOAIModels)` _(Experimental)_<br/>チャット用のOpenAI互換のカスタムモデルを構成します。 | `[]` |
| `setting(github.copilot.chat.edits.suggestRelatedFilesFromGitHistory)` _(Experimental)_<br/>チャットコンテキストでgit履歴から関連ファイルを提案します。 | `true` |

## エージェントの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.agent.enabled:true)`<br/>エージェントの使用を有効または無効にします(VS Code 1.99以降が必要)。 | `true` |
| `setting(chat.agent.maxRequests)`<br/>Copilotがエージェントを使用して行えるリクエストの最大数。 | `25` |
| `setting(github.copilot.chat.agent.autoFix)`<br/>生成されたコード変更の問題を自動的に診断し、修正します。 | `true` |
| `setting(chat.mcp.access)`<br/>VS Codeで使用できるModel Context Protocol(MCP)サーバーを管理します。 | `true` |
| `setting(chat.mcp.discovery.enabled)`<br/>他のアプリケーションからMCPサーバー構成を自動検出する機能を構成します。 | `false` |
| `setting(chat.tools.terminal.autoApprove)` <br/>[エージェント使用時に自動承認されるターミナルコマンド](/docs/copilot/chat/chat-tools.md#automatically-approve-terminal-commands)を制御します。コマンドは`true`(自動承認)または`false`(承認が必要)に設定できます。正規表現はパターンを`/`文字で囲むことで使用できます。 | `{ "rm": false, "rmdir": false, "del": false, "kill": false, "curl": false, "wget": false, "eval": false, "chmod": false, "chown": false, "/^Remove-Item\\b/i": false }` |
| `setting(chat.tools.terminal.enableAutoApprove)` <br/>ターミナルコマンドの自動承認を有効または無効にします。 | `true` |
| `setting(chat.tools.terminal.ignoreDefaultAutoApproveRules)` <br/>ターミナルコマンドの既定の自動承認ルールを無視します。 | `false` |
| `setting(chat.tools.global.autoApprove)`<br/>すべてのツールを自動承認します。この設定は[重要なセキュリティ保護を無効化](/docs/copilot/security.md)します。 | `false` |
| `setting(chat.tools.urls.autoApprove)` <br/>[自動承認されるURLリクエストと応答](/docs/copilot/chat/chat-tools.md#url-approval)を制御します。 | `[]` |
| `setting(chat.agent.thinking.collapsedTools)` _(Experimental)_<br/>チャット会話でツール呼び出しの詳細を既定で折りたたむか展開するかを構成します。 | `always` |
| `setting(chat.agent.thinkingStyle)` _(Experimental)_<br/>チャットで思考トークンをどのように表示するかを構成します。 | `fixedScrolling` |
| `setting(chat.customAgentInSubagent.enabled)` _(Experimental)_<br/>[サブエージェント](/docs/copilot/chat/chat-sessions.md#context-isolated-subagents)でカスタムエージェントを使用することを有効にします。 | `false` |
| `setting(chat.mcp.autoStart)` _(Experimental)_<br/>MCP構成の変更が検出されたときにMCPサーバーを自動的に起動します。 | `newAndOutdated` |
| `setting(chat.tools.eligibleForAutoApproval)` _(Experimental)_<br/>エージェントが使用する前に手動承認が必要なツールを構成します。 | `[]` |
| `setting(chat.tools.terminal.blockDetectedFileWrites)` _(Experimental)_<br/>ファイル書き込みを行うターミナルコマンドに対してユーザー承認を要求します。 | `outsideWorkspace` |
| `setting(chat.useAgentSkills)` _(Experimental)_<br/>VS Codeで[エージェントスキル](/docs/copilot/customization/agent-skills.md)のサポートを有効にします。 | `false` |
| `setting(github.copilot.chat.newWorkspaceCreation.enabled)` _(Experimental)_<br/>チャットで新しいワークスペースをスキャフォールドするツールを有効にします。 | `true` |
| `setting(github.copilot.chat.agent.thinkingTool:true)` _(Experimental)_<br/>エージェント使用時に思考ツールを有効にします。 | `false` |
| `setting(github.copilot.chat.cli.customAgents.enabled)` _(Experimental)_<br/>GitHubのバックグラウンドエージェントセッションからカスタムエージェントを使用することを有効にします。 | `false` |
| `setting(github.copilot.chat.summarizeAgentConversationHistory.enabled)` _(Experimental)_<br/>コンテキストウィンドウがいっぱいになったときに、エージェント会話履歴を自動的に要約します。 | `true` |
| `setting(github.copilot.chat.virtualTools.threshold)` _(Experimental)_<br/>このツール数を超えると仮想ツールが使用されます。仮想ツールは、類似するツールのセットをまとめ、モデルがオンデマンドで有効化できるようにします。これにより、チャットリクエストあたり128ツールの制限を超えられます。 | `128` |

## エージェントセッション

[Agentsビュー](/docs/copilot/agents/overview.md)は、ローカルのチャット会話とリモートのコーディングエージェントセッションの両方を管理するための集中管理場所を提供します。このビューにより、複数のAIセッションを同時に扱い、進捗を追跡し、長時間実行されるタスクを効率的に管理できます。

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.viewSessions.orientation)` <br/>チャットビューでエージェントセッション一覧をどのように表示するかを構成します。 | `auto` |
| `setting(chat.agentSessionsViewLocation)` _(Preview)_<br/>専用のAgentsビューを有効または無効にします。 | `disabled` |

## インラインチャットの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(inlineChat.finishOnType)`<br/>変更領域の外で入力すると、エディターのインラインチャットセッションを終了します。 | `false` |
| `setting(inlineChat.holdToSpeech)`<br/>エディターのインラインチャットのキーボードショートカット(`kb(inlineChat.start)`)を押し続けると、音声認識が自動的に有効になります。 | `true` |
| `setting(editor.inlineSuggest.syntaxHighlightingEnabled)`<br/>インライン提案の構文ハイライトを表示します。 | `true` |
| `setting(inlineChat.lineEmptyHint)` _(Experimental)_<br/>空行でエディターのインラインチャットのヒントを表示します。 | `false` |
| `setting(inlineChat.lineNaturalLanguageHint)` _(Experimental)_<br/>行の大部分が単語で構成されている場合、直ちにエディターのインラインチャットをトリガーします。 | `true` |
| `setting(github.copilot.chat.editor.temporalContext.enabled)` _(Experimental)_<br/>最近表示および編集したファイルを、エディターのインラインチャットのコンテキストに含めます。 | `false` |

## コードレビューの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.reviewSelection.enabled)` _(Preview)_<br/>エディターで選択したテキストに対するAIコードレビューを有効にします。 | `true` |
| `setting(github.copilot.chat.reviewSelection.instructions)` _(Preview)_<br/>現在のエディター選択範囲をAIでレビューするリクエストに追加されるカスタム指示。 | `[]` |

## カスタム指示の設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.instructionsFilesLocations)` <br/>カスタム指示ファイルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ファイルパスのglobパターンをサポートします。 | `{ ".github/instructions": true }` |
| `setting(github.copilot.chat.codeGeneration.useInstructionFiles)`<br/>`.github/copilot-instructions.md`のカスタム指示をチャットリクエストに自動的に追加します。 | `true` |
| `setting(github.copilot.chat.commitMessageGeneration.instructions)` _(Experimental)_<br/>AIでコミットメッセージを生成するためのカスタム指示。 | `[]` |
| `setting(github.copilot.chat.pullRequestDescriptionGeneration.instructions)` _(Experimental)_<br/>AIでPull Requestのタイトルと説明を生成するためのカスタム指示。 | `[]` |

## 再利用可能なプロンプトファイルの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(chat.promptFilesLocations)` <br/>プロンプトファイルを検索する場所。相対パスはワークスペースのルートフォルダーから解決されます。ファイルパスのglobパターンをサポートします。 | `{ ".github/prompts": true }` |
| `setting(chat.promptFilesRecommendations)` <br/>新しいチャットセッションを開く際のプロンプトファイルの推奨を有効または無効にします。プロンプトファイル名とbooleanまたはwhen句のキー/値ペアのリスト。 | `[]` |

## デバッグの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.startDebugging.enabled)` _(Preview)_<br/>チャットビューで実験的な`/startDebugging`インテントを有効にし、デバッグ構成を生成します。 | `true` |
| `setting(github.copilot.chat.copilotDebugCommand.enabled)` _(Preview)_<br/>`copilot-debug`ターミナルコマンドを有効にします。 | `true` |

## テストの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(github.copilot.chat.generateTests.codeLens)` _(Experimental)_<br/>現在のテストカバレッジ情報でカバーされていないシンボルに対して、**Generate tests**のコードレンズを表示します。 | `false` |
| `setting(github.copilot.chat.setupTests.enabled)` _(Experimental)_<br/>`/tests`生成で実験的な`/setupTests`インテントとプロンプトを有効にします。 | `true` |

## ノートブックの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(notebook.experimental.generate)` _(Experimental)_<br/>ノートブックのインラインチャットでコードセルを作成するための**Generate**アクションを有効にします。 | `true` |
| `setting(github.copilot.chat.edits.newNotebook.enabled)` _(Experimental)_<br/>編集モードで新しいノートブックファイルを作成するためのノートブックツールを有効にします。 | `true` |
| `setting(github.copilot.chat.notebook.followCellExecution.enabled)` _(Experimental)_<br/>現在実行中のセルをエディターに表示します。 | `false` |

## アクセシビリティの設定

| 設定と説明 | 既定値 |
|------------------------|---------------|
| `setting(inlineChat.accessibleDiffView)`<br/>インラインチャットが変更内容についてアクセシブルな差分ビューアーもレンダリングするかどうか。 | `"auto"` |
| `setting(accessibility.signals.chatRequestSent)`<br/>チャットリクエストが行われたときに、シグナル(音(オーディオキュー)および/またはアナウンス(アラート))を再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.chatResponseReceived)`<br/>応答を受信したときに音/オーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatEditModifiedFile)`<br/>チャット編集によりファイルが変更されたときに音/オーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.chatUserActionRequired)`<br/>ユーザーがチャットで操作を行う必要があるときに音/オーディオキューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.signals.lineHasInlineSuggestion)`<br/>カーソルがインライン提案のある行にあるときに音/オーディオキューを再生します。 | `{ "sound": "auto" }` |
| `setting(accessibility.signals.nextEditSuggestion)`<br/>次の編集の提案が利用可能なときに音/オーディオキューを再生します。 | `{ "sound": "auto", "announcement": "auto" }` |
| `setting(accessibility.verboseChatProgressUpdates)`<br/>チャットのアクティビティについて詳細な更新を提供します。 | `true` |
| `setting(accessibility.verbosity.inlineChat)`<br/>インラインエディターのチャットのアクセシビリティヘルプメニューへのアクセス方法、および入力にフォーカスがあるときに機能の使い方を説明するヒントをアラートで知らせる方法についての情報を提供します。 | `true` |
| `setting(accessibility.verbosity.inlineCompletions)`<br/>インライン提案のホバーとAccessible Viewへのアクセス方法についての情報を提供します。 | `true` |
| `setting(accessibility.verbosity.panelChat)`<br/>チャット入力にフォーカスがあるときにチャットヘルプメニューへアクセスする方法についての情報を提供します。 | `true` |
| `setting(accessibility.voice.keywordActivation)`<br/>キーワードフレーズ'Hey Code'が認識されて音声チャットセッションを開始するかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.autoSynthesize)`<br/>音声が入力として使用されたときに、テキスト応答を自動的に読み上げるかどうかを制御します。 | `"off"` |
| `setting(accessibility.voice.speechTimeout)`<br/>話すのをやめた後に音声認識が有効のままになる時間(ミリ秒)。 | `1200` |

## 関連リソース

* [VS CodeにおけるCopilot機能の概要をすばやく確認する](/docs/copilot/reference/copilot-vscode-features.md)
