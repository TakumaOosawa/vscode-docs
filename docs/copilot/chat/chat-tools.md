---
ContentId: 8f2c4a1d-9e3b-4c5f-a7d8-6b9c2e4f1a3d
DateApproved: 01/08/2026
MetaDescription: 組み込みツール、MCPツール、および拡張機能ツールを使用して、VS Codeのチャットを専門的な機能で拡張する方法を説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# チャットでツールを使用する

ツールは、コードの検索、コマンドの実行、Webコンテンツの取得、APIの呼び出しなど、特定のタスクを実行するための専門的な機能でVisual Studio Codeのチャットを拡張します。VS Codeは、組み込みツール、Model Context Protocol (MCP) ル、および拡張機能ツールの3種類のツールをサポートしています。

この記事では、VS Codeで使用可能なさまざまな種類のツール、チャットプロンプトでそれらを使用する方法、およびツールの呼び出しと承認を管理する方法について説明します。

<video src="../images/chat-tools/chat-tools-picker.mp4" title="Video showing how to select and configure tools in the chat tools picker." autoplay loop controls muted poster="../images/chat-tools/chat-tools-picker.png"></video>

## ツールの種類

VS Codeは、チャットで使用できる3種類のツールをサポートしています。

<details>
<summary>組み込みツール</summary>

VS Codeは、チャットで自動的に利用可能な包括的な組み込みツールのセットを提供します。これらのツールは一般的な開発タスクをカバーし、ワークスペース内での作業に最適化されています。

組み込みツールはインストールや構成を必要とせず、チャットの使用を開始するとすぐに利用できます。

組み込みツールの完全なリストとその説明については、[チャットツールリファレンス](/docs/copilot/reference/copilot-vscode-features.md#chat-tools)を参照してください。

</details>

<details>
<summary>MCPツール</summary>

Model Context Protocol (MCP) は、AIモデルが統合インターフェイスを通じて外部ツールやサービスを使用できるようにするオープンスタンダードです。MCPサーバーは、VS Codeに追加してチャットを追加機能で拡張できるツールを提供します。

チャットでツールを使用する前に、MCPサーバーをインストールして構成する必要があります。MCPサーバーは、ローカルマシンで実行することも、リモートでホストすることもできます。

[VS CodeでのMCPサーバーの構成](/docs/copilot/customization/mcp-servers.md)について詳しくはこちらをご覧ください。

> [!IMPORTANT]
> 組織でVS CodeでのMCPサーバーの使用が無効になっているか、使用できるMCPサーバーが制限されている可能性があります。詳細については管理者に問い合わせてください。

</details>

<details>
<summary>拡張機能ツール</summary>

VS Code拡張機能は、エディターと深く統合されたツールを提供できます。拡張機能ツールは、Language Model Tools APIを使用して、VS Code拡張機能APIの全範囲にアクセスしながら専門的な機能を提供します。

拡張機能ツールは、それらを提供する拡張機能をインストールすると自動的に利用可能になります。ユーザーは、拡張機能自体のインストール以外に個別のインストールや構成を行う必要はありません。

拡張機能ツールの作成を検討している開発者は、[Language Model Tools APIガイド](/api/extension-guides/ai/tools.md)を参照してください。

</details>

## チャットのツールを有効にする

チャットでツールを使用する前に、チャットビューでそれらを有効にする必要があります。ツールピッカーを使用して、リクエストごとにツールを有効または無効にできます。ツールを提供する[MCPサーバーをインストールする](/docs/copilot/customization/mcp-servers.md)か、[拡張機能をインストールする](/docs/getstarted/extensions.md)ことで、さらにツールを追加できます。

> [!TIP]
> 結果を改善するために、プロンプトに関連するツールのみを選択してください。

ツールピッカーにアクセスするには：

1. チャットビューを開き、エージェントピッカーから**Agent**を選択します。

1. チャット入力フィールドの**Configure Tools**ボタンを選択します。

    ![Screenshot showing the Chat view, highlighting the Configure Tools button in the chat input.](../images/chat-tools/agent-mode-select-tools.png)

1. 現在のリクエストで使用可能なツールを制御するために、ツールを選択または選択解除します。

    検索ボックスを使用してツールのリストをフィルタリングします。

[プロンプトファイル](/docs/copilot/customization/prompt-files.md)または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を使用してチャットをカスタマイズする場合、特定のプロンプトまたはモードで使用可能なツールを指定できます。[ツールリストの優先順位](/docs/copilot/customization/custom-agents.md#tool-list-priority)について詳しくはこちらをご覧ください。

## プロンプトでツールを使用する

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、エージェントはプロンプトとリクエストのコンテキストに基づいて、有効なツールから使用するツールを自動的に決定します。エージェントは、タスクを達成するために必要に応じて関連するツールを自律的に選択して呼び出します。

`#`の後にツール名を入力することで、プロンプト内でツールを明示的に参照することもできます。これは、特定のツールが確実に使用されるようにしたい場合に便利です。チャット入力フィールドに`#`と入力すると、組み込みツール、インストールされたサーバーからのMCPツール、拡張機能ツール、およびツールセットを含む、使用可能なツールのリストが表示されます。

**明示的なツール参照の例:**

* `"Summarize the content from #fetch https://code.visualstudio.com/updates"`
* `"How does routing work in Next.js? #githubRepo vercel/next.js"`
* `"Fix the issues in #problems"`
* `"Explain the authentication flow #codebase"`

一部のツールは、プロンプトで直接パラメーターを受け入れます。たとえば、`#fetch`にはURLが必要で、`#githubRepo`にはリポジトリ名が必要です。

> [!TIP]
> デフォルトでは、ツール呼び出しの詳細はチャットの会話内で折りたたまれています。チャット内のツール概要行を選択して展開するか、`setting(chat.agent.thinking.collapsedTools)`設定（試験的機能）でデフォルトの動作を変更できます。

## ツールの承認

一部のツールは、実行する前に承認が必要です。これは、ツールがファイルを変更したり、環境を変更したり、悪意のあるツールの出力を通じてプロンプトインジェクション攻撃を試みたりする可能性があるため、セキュリティ対策として行われます。

ツールが承認を必要とする場合、ツールの詳細を示す確認ダイアログが表示されます。ツールを承認する前に情報を注意深く確認してください。ツールの承認は、1回のみ、現在のセッション、現在のワークスペース、または将来のすべての呼び出しに対して行うことができます。

![Screenshot of a tool confirmation dialog showing tool details and approval options.](../images/chat-tools/chat-approve-tool.png)

ツールやエージェントのアクションによってファイルが変更される場合があります。ワークスペース内の[機密ファイルへの誤った編集](/docs/copilot/chat/review-code-edits.md#edit-sensitive-files)を防ぐ方法については、こちらをご覧ください。

> [!IMPORTANT]
> 特にファイルを変更したり、コマンドを実行したり、外部サービスにアクセスしたりするツールの場合は、承認する前に必ずツールのパラメーターを注意深く確認してください。VS CodeでのAIの使用に関する[セキュリティ上の考慮事項](/docs/copilot/security.md)を参照してください。

### ツールの自動承認を有効または無効にする（試験的機能）

デフォルトでは、任意のツールを自動的に承認することを選択できます。誤った承認を防ぐために、`setting(chat.tools.eligibleForAutoApproval)`設定を使用して、特定のツールの自動承認を無効にすることができます。そのツールの手動承認を常に要求するには、値を`false`に設定します。

組織は、デバイス管理ポリシーを使用して特定ツールの手動承認を強制することもできます。詳細については、[Enterpriseドキュメント](/docs/enterprise/ai-settings.md)をご覧ください。

### URLの承認

`fetch`ツールなどでツールがURLにアクセスしようとすると、悪意のあるコンテンツや予期しないコンテンツからユーザーを保護するために、2段階の承認プロセスが使用されます。VS Codeのチャットビューに、確認のためのURLの詳細を含む確認ダイアログが表示されます。

* **事前承認：URLへのリクエストの承認**

    このステップにより、アクセスしようとしているドメインが信頼できるものであることを確認し機密データが信頼できないサイトに送信されるのを防ぐことができます。

    ![Screenshot of a URL approval dialog showing URL details and approval options.](../images/chat-tools/chat-approve-url.png)

    1回限りの承認、または特定のURLやドメインへの将来のリクエストを自動的に承認するオプションがあります。自動承認を選択しても、結果を確認する必要性に影響はありません。**Allow requests to**を選択すると、URLまたはドメインに対して事前承認と事後承認の両方を構成することを選択できます。

    > [!NOTE]
    > 事前承認は["Trusted Domains"機能](/docs/editing/editingevolved.md#_outgoing-link-protection)を尊重します。ドメインがそこにリストされている場合、そのドメインへのリクエストは自動的に承認され、応答の確認ステップは延期されます。

* **事後承認：URLから取得した応答コンテンツの承認**

    このステップにより、取得したコンテンツがチャットに追加されたり他のツールに渡されたりする前に確認し、潜在的なプロンプトインジェクション攻撃を防ぐことができます。

    たとえば、GitHub.comなどの有名なサイトからのコンテンツの取得リクエストを承認するとします。しかし、課題の説明やコメントなどのコンテンツはユーザー生成のものであるため、モデルの動作を操作する可能性のある有害なコンテンツが含まれている可能性があります。

    1回限りの承認、または特定のURLやドメインからの将来の応答を自動的に承認するオプションがあります。

    > [!IMPORTANT]
    > 事後承認ステップは"Trusted Domains"機能とはリンクしておらず、常に確認が必要です。これは、信頼できるドメイン上の信頼できないコンテンツによる問題を防ぐためのセキュリティ対策です。

`setting(chat.tools.urls.autoApprove)`設定は、自動承認URLパターンを保存するために使用されます。設定値は、リクエストとレスポンスの両方の自動承認を有効または無効にするブール値か、詳細な制御のための`approveRequest`および`approveResponse`プロパティを持つオブジェクトのいずれかです。完全なURL、globパターン、またはワイルドカードを使用できます。

URL自動承認の例:

```jsonc
{
"chat.tools.urls.autoApprove": {
    "https://www.example.com": false,
    "https://*.contoso.com/*": true,
    "https://example.com/api/*": {
        "approveRequest": true,
        "approveResponse": false
    }
}
```

### ツール確認のリセット

保存されたすべてのツールの承認をクリアするには、コマンドパレット（`kb(workbench.action.showCommands)`）で**Chat: Reset Tool Confirmations**コマンドを使用します。

## ツールパラメーターの編集

ツールを実行する前に、入力パラメーターを確認して編集できます：

1. ツール確認ダイアログが表示されたら、ツール名の横にあるシェブロンを選択して詳細を展開します。

1. 必要に応じてツール入力パラメーターを編集します。

1. 変更したパラメーターでツールを実行するには、**Allow**を選択します。

## ターミナルコマンド

エージェントは、タスクを達成するためのワークフローの一部としてターミナルコマンドを使用する場合があります。エージェントがターミナルコマンドを実行することを決定すると、組み込みのターミナルツールを使用して、VS Code内の統合ターミナルでそれらを実行します。

チャットの会話では、エージェントが実行したコマンドが表示されます。コマンドの横にある**Show Output**（`>`）を選択すると、チャット内でインラインでコマンドの出力を表示できます。また、**Show Terminal**を選択して、統合ターミナルで完全な出力を表示することもできます。

![Screenshot showing terminal command output in chat.](../images/chat-tools/terminal-command-output.png)

試験的な`setting(chat.tools.terminal.outputLocation)`設定を使用して、ターミナルコマンドの出力が表示される場所（チャット内のインライン、または統合ターミナル）を構成します。

ターミナルペインでは、エージェントがチャットセッションで使用したターミナルのリストを確認できます。また、ターミナルリスト内のチャットアイコンによってエージェントのターミナルを区別することもできます。

![Screenshot showing the integrated terminal with multiple agent terminals.](../images/chat-tools/agent-terminals-in-terminal-pane.png)

### ターミナルコマンドの自動承認

`setting(chat.tools.terminal.autoApprove)`設定を使用して、自動的に承認されるターミナルコマンドを構成できます。許可されるコマンドと拒否されるコマンドの両方を指定できます：

* コマンドを自動的に承認するには`true`に設定します
* 常に承認を要求するには`false`に設定します
* パターンを`/`文字で囲むことで正規表現を使用します

例:

```jsonc
{
  // `mkdir`コマンドを許可
  "mkdir": true,
  // `git status`および`git show`で始まるコマンドを許可
  "/^git (status|show\\b.*)$/": true,

  // `del`コマンドをブロック
  "del": false,
  // "dangerous"を含む任意のコマンドをブロック
  "/dangerous/": false
}
```

デフォルトでは、パターンは個々のサブコマンドに対して照合されます。コマンドが自動承認されるには、すべてのサブコマンドが`true`エントリと一致する必要があり、`false`エントリと一致してはなりません。

高度なシナリオの場合、個々のサブコマンドではなく完全なコマンドラインに対して照合するために、`matchCommandLine`プロパティを持つオブジェクト構文を使用します。

関連する設定:

* `setting(chat.tools.terminal.enableAutoApprove)`: 自動承認機能を完全に無効にします
* `setting(chat.tools.terminal.blockDetectedFileWrites)`（試験的機能）: ファイル書き込みの検出（試験的機能）
* `setting(chat.tools.terminal.ignoreDefaultAutoApproveRules)`（試験的機能）: すべてのデフォルトルール（許可とブロックの両方）を無効にし、すべてのルールを完全に制御できるようにします。

> [!CAUTION]
> ターミナルコマンドの自動承認は_ベストエフォート_の保護を提供し、エージェントが悪意を持って行動していないことを前提としています。ターミナルの自動承認を有効にする場合は、一部のコマンドがすり抜ける可能性があるため、プロンプトインジェクションから身を守ることが重要です。検出が失敗する可能性がある例をいくつか示します：
>
> * VS CodeはPowerShellおよびbash tree-sitter文法を使用してサブコマンドを抽出するため、これらの文法がパターンを検出しない場合、パターンは検出されません。
> * VS Codeは、zshやfishの文法がないためbash文法を使用しており、一部のサブコマンドは検出されません。
> * ファイル書き込みの検出は現在最小限であるため、ファイル編集エージェントツールを使用することでは不可能なファイルへの書き込みが、ターミナルで可能になる場合があります。
> * 引用符の連結などのさまざまな手法によって、自動承認を回避することが可能です。たとえば、`find -exec`は通常ブロックされますが、同じことを行う`find -e"x"ec`はブロックされません。
>
> プロンプトインジェクションの可能性がある場合、または高リスクな環境にいる場合は、サンドボックス化またはコンテナー内でのVS Codeの実行を検討する必要があります。

## ツールセットでツールをグループ化する

ツールセットは、プロンプトで単一のエンティティとして参照できるツールのコレクションです。ツールセットを使用すると、関連するツールを整理し、チャットプロンプト、[プロンプトファイル](/docs/copilot/customization/prompt-files.md)、および[カスタムチャットエージェント](/docs/copilot/customization/custom-agents.md)で使いやすくすることができます。一部の組み込みツールは、`#edit`や`#search`などの事前定義されたツールセットの一部です。

### ツールセットの作成

ツールセットを作成するには：

1. コマンドパレットから**Chat: Configure Tool Sets**コマンドを実行し、**Create new tool sets file**を選択します。

    または、チャットビューで**Configure Chat**を選択 > **Tool Sets** > **Create new tool sets file**を選択します。

    ![Screenshot showing the Chat view and Configure Chat menu, highlighting the Configure Chat button.](../images/customization/configure-chat-instructions.png)

1. 開いた`.jsonc`ファイルでツールセットを定義します。

    ツールセットは次の構造を持ちます：

    ```json
    {
        "reader": {
            "tools": [
                "changes",
                "codebase",
                "problems",
                "usages"
            ],
            "description": "Tools for reading and gathering context",
            "icon": "book"
        }
    }
    ```

    ツールセットのプロパティ:

    * `tools`: ツール名の配列（組み込みツール、MCPツール、または拡張機能ツール）
    * `description`: ツールピッカーに表示される簡単な説明
    * `icon`: ツールセットのアイコン（[製品アイコンリファレンス](/api/references/icons-in-labels.md)を参照）

### ツールセットの使用

`#`の後にツールセット名を入力して、プロンプトでツールセットを参照します：

* `"Analyze the codebase for security issues #reader"`
* `"Where is the DB connection string defined? #search"`

ツールピッカーでは、ツールセットは関連するツールの折りたたみ可能なグループとして利用可能です。ツールセット全体を選択または選択解除して、複数の関連ツールを一度にすばやく有効または無効にすることができます。

## よくある質問

### どのツールが利用可能かを確認するにはどうすればよいですか？

チャット入力フィールドに`#`と入力すると、利用可能なすべてのツールのリストが表示されます。チャット内のツールピッカーを使用して、アクティブなツールのリストを表示および管理することもできます。

### "Cannot have more than 128 tools per request."というエラーが表示されます。

チャットリクエストでは、一度に最大128個のツールを有効にできます。リクエストあたり128個のツールを超えているというエラーが表示された場合は、次のようにします：

* チャットビューのツールピッカーを開き、いくつかのツールまたはMCPサーバー全体を選択解除して数を減らします。

* または、`setting(github.copilot.chat.virtualTools.threshold)`設定で仮想ツールを有効にして、大規模なツールセットを自動的に管理します。

### エージェントがターミナルシェルとしてコマンドプロンプトを使用しないのはなぜですか？

エージェントは、cmdの場合を除き、ターミナルのデフォルトとして構成したシェルを使用します。これは、コマンドプロンプトでは[シェル統合](https://code.visualstudio.com/docs/terminal/shell-integration)がサポートされていないためで、エージェントはターミナル内で何が起こっているかをほとんど把握できません。コマンドがいつ実行されているか、または実行が完了したかについての直接的なシグナルを取得する代わりに、エージェントはタイムアウトに依存し、ターミナルがアイドル状態になるのを監視して続行する必要があります。これにより、遅く不安定なエクスペリエンスになります。

`setting(chat.tools.terminal.terminalProfile.windows)`設定を使用してエージェントがコマンドプロンプトを使用するように構成することはできますが、PowerShellを使用する場合と比較して劣ったエクスペリエンスになります。

```json
"chat.tools.terminal.terminalProfile.windows": {
  "path": "C:\\WINDOWS\\System32\\cmd.exe"
}
```

### すべてのツールとターミナルコマンドを自動的に承認できますか？

> [!CAUTION]
> この設定は、潜在的に破壊的なアクションを含むすべての手動承認を無効にします。重要なセキュリティ保護を削除し、攻撃者がマシンを侵害しやすくします。影響を理解している場合にのみ、この設定を有効にしてください。詳細については[セキュリティドキュメント](/docs/copilot/security.md)を参照してください。
>
> ユーザーの確認を求めずにすべてのツールとターミナルコマンドの実行を許可するには、`chat.tools.global.autoApprove`設定を有効にします。この設定は、すべてのワークスペースにグローバルに適用されます！

### ツールとチャット参加者の違いは何ですか？

チャット参加者は、チャットでドメイン固有の質問をすることができる専門のアシスタントです。チャット参加者は、チャットリクエストを渡すと残りの処理を行ってくれるドメインの専門家であると想像してください。

ツールは、エージェントフローの一部として呼び出され、特定のタスクに貢献し実行します。単一のチャットリクエストに複数のツールを含めることができますが、一度にアクティブにできるチャット参加者は1つだけです。

### 独自のツールを作成できますか？

はい。ツールは次の2つの方法で作成できます：

* [Language Model Tools API](/api/extension-guides/ai/tools.md)を使用してツールを提供する**VS Code拡張機能を開発する**
* ツールを提供する**MCPサーバーを作成する**。[MCP開発者ガイド](/docs/copilot/guides/mcp-developer-guide.md)を参照してください

## 関連リソース

* [チャットツールリファレンス](/docs/copilot/reference/copilot-vscode-features.md#chat-tools)
* [VS CodeでのAIの使用に関するセキュリティ上の考慮事項](/docs/copilot/security.md)
