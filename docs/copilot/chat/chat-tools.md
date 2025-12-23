---
ContentId: 8f2c4a1d-9e3b-4c5f-a7d8-6b9c2e4f1a3d
DateApproved: 12/10/2025
MetaDescription: VS Codeでチャットを拡張するために、組み込みツール、MCPツール、拡張機能ツールを使って専用の機能を利用する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# チャットでツールを使用する

ツールは、コードの検索、コマンドの実行、Webコンテンツの取得、APIの呼び出しなどの特定のタスクを達成するための専用機能で、Visual Studio Codeのチャットを拡張します。VS Codeは3種類のツール(組み込みツール、Model Context Protocol (MCP)ツール、拡張機能ツール)をサポートしています。

この記事では、VS Codeで利用できるツールの種類、チャットプロンプトでの使い方、ツールの呼び出しと承認を管理する方法について説明します。

<video src="../images/chat-tools/chat-tools-picker.mp4" title="チャットのツールピッカーでツールを選択して構成する方法を示すビデオ。" autoplay loop controls muted poster="../images/chat-tools/chat-tools-picker.png"></video>

## ツールの種類

VS Codeは、チャットで使用できる3種類のツールをサポートしています:

<details>
<summary>組み込みツール</summary>

VS Codeには、チャットで自動的に利用できる包括的な組み込みツールセットが用意されています。これらのツールは一般的な開発タスクをカバーしており、ワークスペース内での作業に最適化されています。

組み込みツールはインストールや構成を必要とせず、チャットを使い始めるとすぐに利用できます。

組み込みツールの完全な一覧と説明については、[チャットツールのリファレンス](/docs/copilot/reference/copilot-vscode-features.md#chat-tools)を参照してください。

</details>

<details>
<summary>MCP tools</summary>

Model Context Protocol (MCP)は、統一されたインターフェイスを通じてAIモデルが外部ツールやサービスを使用できるようにするオープンスタンダードです。MCPサーバーは、チャットに追加の機能を提供するためにVS Codeへ追加できるツールを提供します。

チャットでMCPサーバーのツールを使用する前に、MCPサーバーをインストールして構成する必要があります。MCPサーバーはローカルマシン上で実行することも、リモートでホストすることもできます。

[VS CodeでMCPサーバーを構成する](/docs/copilot/customization/mcp-servers.md)を参照してください。

</details>

<details>
<summary>拡張機能ツール</summary>

VS Code拡張機能は、エディターと深く統合するツールを提供できます。拡張機能ツールはLanguage Model Tools APIを使用し、VS Code拡張機能APIの全範囲にアクセスしながら専用機能を提供します。

拡張機能ツールは、それらを提供する拡張機能をインストールすると自動的に利用できます。ユーザーは拡張機能自体のインストール以外に、別途インストールや構成を行う必要はありません。

拡張機能ツールを作成したい開発者は、[Language Model Tools APIガイド](/api/extension-guides/ai/tools.md)を参照してください。

</details>

## チャットでツールを有効にする

チャットでツールを使用する前に、チャットビューでツールを有効にする必要があります。ツールピッカーを使うことで、リクエストごとにツールを有効または無効にできます。さらにツールを追加するには、[MCPサーバーをインストール](/docs/copilot/customization/mcp-servers.md)するか、ツールを提供する[拡張機能](/docs/getstarted/extensions.md)をインストールします。

> [!TIP]
> 結果を向上させるために、プロンプトに関連するツールのみを選択してください。

To access the tools picker:

1. チャットビューを開き、エージェントピッカーから**Agent**を選択します。

1. チャット入力欄の**Configure Tools**ボタンを選択します。

    ![チャットビューのスクリーンショット。チャット入力欄のConfigure Toolsボタンが強調表示されている。](../images/chat-tools/agent-mode-select-tools.png)

1. ツールを選択または選択解除して、現在のリクエストで利用できるツールを制御します。

    検索ボックスを使ってツールの一覧をフィルターできます。

[プロンプトファイル](/docs/copilot/customization/prompt-files.md)や[カスタムエージェント](/docs/copilot/customization/custom-agents.md)でチャットをカスタマイズする場合、特定のプロンプトまたはモードで使用できるツールを指定できます。[ツールリストの優先順位](/docs/copilot/customization/custom-agents.md#tool-list-priority)の詳細を参照してください。

## プロンプトでツールを使用する

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、エージェントはプロンプトとリクエストのコンテキストに基づいて、有効になっているツールの中から使用するツールを自動的に判断します。エージェントはタスクを達成するために必要に応じて関連するツールを自律的に選択し、呼び出します。

また、プロンプトで`#`に続けてツール名を入力することで、ツールを明示的に参照できます。これは、特定のツールが使用されることを確実にしたい場合に便利です。チャット入力欄に`#`を入力すると、組み込みツール、インストール済みサーバーのMCPツール、拡張機能ツール、ツールセットなど、利用可能なツールの一覧が表示されます。

**ツール参照を明示する例:**

* `"Summarize the content from #fetch https://code.visualstudio.com/updates"`
* `"How does routing work in Next.js? #githubRepo vercel/next.js"`
* `"Fix the issues in #problems"`
* `"Explain the authentication flow #codebase"`

一部のツールは、プロンプト内でパラメーターを直接受け取ります。たとえば、`#fetch`にはURLが必要で、`#githubRepo`にはリポジトリ名が必要です。

> [!TIP]
> 既定では、ツール呼び出しの詳細はチャットの会話内で折りたたまれています。チャット内のツール要約行を選択すると展開でき、または`setting(chat.agent.thinking.collapsedTools)`設定(実験段階)で既定の動作を変更できます。

## ツールの承認

一部のツールは実行前にあなたの承認が必要です。これは、ツールがファイルや環境を変更する操作を行ったり、悪意のあるツール出力を通じてプロンプトインジェクション攻撃を試みたりできるためのセキュリティ対策です。

ツールに承認が必要な場合、ツールの詳細を表示する確認ダイアログが表示されます。ツールを承認する前に情報を注意深く確認してください。ツールは1回のみ、現在のセッション、現在のワークスペース、または今後のすべての呼び出しに対して承認できます。

![ツールの詳細と承認オプションを示すツール確認ダイアログのスクリーンショット。](../images/chat-tools/chat-approve-tool.png)

ツールやエージェントのアクションにより、ファイルが変更される可能性があります。ワークスペースで意図しない[機密ファイルの編集](/docs/copilot/chat/review-code-edits.md#edit-sensitive-files)を防ぐ方法について確認してください。

> [!IMPORTANT]
> 特にファイルを変更するツール、コマンドを実行するツール、外部サービスにアクセスするツールを承認する前には、必ずツールパラメーターを注意深く確認してください。VS CodeでAIを使用する際の[セキュリティに関する考慮事項](/docs/copilot/security.md)を参照してください。

### ツールの自動承認を有効または無効にする(実験段階)

既定では、任意のツールを自動的に承認することを選択できます。意図しない承認を防ぐために、`setting(chat.tools.eligibleForAutoApproval)`設定で特定のツールの自動承認を無効にできます。値を`false`に設定すると、そのツールは常に手動承認が必要になります。

組織はデバイス管理ポリシーを使用して、特定のツールに手動承認を強制することもできます。詳細は[エンタープライズドキュメント](/docs/setup/enterprise.md)を参照してください。

### URLの承認

`fetch`ツールのようにツールがURLへアクセスしようとする場合、悪意のあるコンテンツや予期しないコンテンツから保護するために2段階の承認プロセスが使用されます。VS CodeはチャットビューでURLの詳細を含む確認ダイアログを表示し、レビューを求めます。

* **事前承認: URLへのリクエストを承認する**

    このステップにより、接続先のドメインを信頼できることを確認し、機密データが信頼できないサイトへ送信されるのを防げます。

    ![URLの詳細と承認オプションを示すURL承認ダイアログのスクリーンショット。](../images/chat-tools/chat-approve-url.png)

    1回のみ承認するか、特定のURLまたはドメインへの今後のリクエストを自動的に承認するかを選択できます。自動承認を選択しても、結果をレビューする必要性には影響しません。**Allow requests to**を選択すると、そのURLまたはドメインに対して事前承認と事後承認の両方を構成することを選択できます。

    > [!NOTE]
    > 事前承認は["Trusted Domains"機能](/docs/editing/editingevolved.md#_outgoing-link-protection)を尊重します。ドメインがそこに一覧表示されている場合、そのドメインへのリクエストは自動的に承認され、応答のレビューステップは延期されます。

* **事後承認: URLから取得した応答コンテンツを承認する**

    このステップにより、取得したコンテンツがチャットに追加されたり他のツールに渡されたりする前にレビューすることが保証され、潜在的なプロンプトインジェクション攻撃を防ぎます。

    たとえば、GitHub.comのようなよく知られたサイトからコンテンツを取得するリクエストを承認するかもしれません。しかし、Issueの説明やコメントなどのコンテンツはユーザー生成であるため、モデルの挙動を操作する可能性のある有害な内容が含まれている可能性があります。

    1回のみ承認するか、特定のURLまたはドメインからの今後の応答を自動的に承認するかを選択できます。

    > [!IMPORTANT]
    > 事後承認のステップは"Trusted Domains"機能とは連動しておらず、常にレビューが必要です。これは、通常は信頼するドメイン上の信頼できないコンテンツによる問題を防ぐためのセキュリティ対策です。

`setting(chat.tools.urls.autoApprove)`設定は、自動承認するURLパターンを保存するために使用されます。設定値は、リクエストと応答の両方に対する自動承認を有効/無効にするブール値、またはより細かく制御するための`approveRequest`と`approveResponse`プロパティを持つオブジェクトのいずれかです。完全一致URL、globパターン、またはワイルドカードを使用できます。

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

### ツール確認をリセットする

保存されたツール承認をすべてクリアするには、コマンドパレット(`kb(workbench.action.showCommands)`)で**Chat: Reset Tool Confirmations**コマンドを使用します。

## ツールパラメーターを編集する

ツールが実行される前に、入力パラメーターをレビューして編集できます:

1. ツール確認ダイアログが表示されたら、ツール名の横にあるシェブロンを選択して詳細を展開します。

1. 必要に応じてツールの入力パラメーターを編集します。

1. **Allow**を選択して、変更したパラメーターでツールを実行します。

## ターミナルコマンド

エージェントはタスクを達成するためのワークフローの一部として、ターミナルコマンドを使用する場合があります。エージェントがターミナルコマンドを実行すると決定した場合、組み込みのターミナルツールを使用してVS Code内の統合ターミナルで実行します。

チャットの会話内で、エージェントは実行したコマンドを表示します。コマンドの横にある**Show Output**(`>`)を選択すると、コマンドの出力をチャット内にインラインで表示できます。**Show Terminal**を選択すると、統合ターミナルで完全な出力を表示することもできます。

![チャットに表示されたターミナルコマンド出力のスクリーンショット。](../images/chat-tools/terminal-command-output.png)

実験段階の`setting(chat.tools.terminal.outputLocation)`設定を使用して、ターミナルコマンド出力を表示する場所(チャット内インライン、統合ターミナル)を構成できます。

ターミナルペインでは、エージェントがチャットセッションで使用したターミナルの一覧を確認できます。ターミナル一覧のチャットアイコンで、エージェントのターミナルを区別することもできます。

![複数のエージェントターミナルが表示された統合ターミナルのスクリーンショット。](../images/chat-tools/agent-terminals-in-terminal-pane.png)

### ターミナルコマンドを自動的に承認する

`setting(chat.tools.terminal.autoApprove)`設定を使用して、どのターミナルコマンドを自動的に承認するかを構成できます。許可するコマンドと拒否するコマンドの両方を指定できます:

* コマンドを`true`に設定すると自動的に承認します
* コマンドを`false`に設定すると常に承認が必要になります
* パターンを`/`文字で囲むことで正規表現を使用できます

例:

```jsonc
{
  // Allow the `mkdir` command
  "mkdir": true,
  // Allow `git status` and commands starting with `git show`
  "/^git (status|show\\b.*)$/": true,

  // Block the `del` command
  "del": false,
  // Block any command containing "dangerous"
  "/dangerous/": false
}
```

既定では、パターンは個々のサブコマンドに対してマッチします。コマンドを自動承認するには、すべてのサブコマンドが`true`のエントリにマッチし、かつ`false`のエントリにマッチしない必要があります。

高度なシナリオでは、`matchCommandLine`プロパティを持つオブジェクト構文を使用して、個々のサブコマンドではなく完全なコマンドラインに対してマッチさせます。

関連する設定:

* `setting(chat.tools.terminal.enableAutoApprove)`: permanently disable auto-approve functionality
* `setting(chat.tools.terminal.blockDetectedFileWrites)` (experimental): detection of file writes (experimental)
* `setting(chat.tools.terminal.ignoreDefaultAutoApproveRules)` (experimental): disable all default rules (both allow and block), giving full control over all rules.

> [!CAUTION]
> ターミナルコマンドの自動承認は、_ベストエフォート_の保護を提供し、エージェントが悪意を持って行動していないことを前提としています。ターミナルの自動承認を有効にすると、一部のコマンドがすり抜ける可能性があるため、プロンプトインジェクションから自分自身を守ることが重要です。検出が破綻する可能性がある例をいくつか示します:
>
> * VS CodeはPowerShellとbashのtree sitter文法を使用してサブコマンドを抽出するため、これらの文法が検出できない場合はパターンも検出されません。
> * zshやfishの文法がないため、VS Codeはbashの文法を使用しており、その結果、一部のサブコマンドは検出されません。
> * ファイル書き込みの検出は現在最小限であるため、ファイル編集のエージェントツールでは不可能なファイル書き込みをターミナルで行える可能性があります。

## ツールセットでツールをグループ化する

ツールセットは、プロンプトで単一のエンティティとして参照できるツールのコレクションです。ツールセットは、関連するツールを整理し、チャットプロンプト、[プロンプトファイル](/docs/copilot/customization/prompt-files.md)、[カスタムチャットエージェント](/docs/copilot/customization/custom-agents.md)で使いやすくするのに役立ちます。一部の組み込みツールは、`#edit`や`#search`などの事前定義されたツールセットの一部です。

### ツールセットを作成する

ツールセットを作成するには:

1. コマンドパレットから**Chat: Configure Tool Sets**コマンドを実行し、**Create new tool sets file**を選択します。

    代わりに、チャットビューで**Configure Chat** > **Tool Sets** > **Create new tool sets file**を選択します。

    ![チャットビューとConfigure Chatメニューを示すスクリーンショット。Configure Chatボタンが強調表示されている。](../images/customization/configure-chat-instructions.png)

1. 開いた`.jsonc`ファイルでツールセットを定義します。

    ツールセットは次の構造になります:

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

    * `tools`: ツール名の配列(組み込みツール、MCPツール、または拡張機能ツール)
    * `description`: ツールピッカーに表示される簡単な説明
    * `icon`: ツールセットのアイコン([Product Icon Reference](/api/references/icons-in-labels.md)を参照)

### ツールセットを使用する

プロンプトで`#`に続けてツールセット名を入力して、ツールセットを参照します:

* `"Analyze the codebase for security issues #reader"`
* `"Where is the DB connection string defined? #search"`

ツールピッカーでは、ツールセットは関連ツールの折りたたみ可能なグループとして利用できます。ツールセット全体を選択または選択解除することで、複数の関連ツールを一度にすばやく有効化または無効化できます。

## よくある質問

### どのツールが利用可能かを知るにはどうすればよいですか?

チャット入力欄に`#`を入力すると、利用可能なツールの一覧が表示されます。チャットのツールピッカーを使用して、アクティブなツールの一覧を表示および管理することもできます。

### "Cannot have more than 128 tools per request."というエラーが表示されます

チャットリクエストでは、一度に最大128個のツールを有効にできます。リクエストあたり128個を超えたというエラーが表示される場合:

* チャットビューでツールピッカーを開き、いくつかのツール、またはMCPサーバー全体の選択を解除して数を減らします。

* または、`setting(github.copilot.chat.virtualTools.threshold)`設定で仮想ツールを有効にして、大規模なツールセットを自動的に管理します。

### エージェントがターミナルシェルとしてCommand Promptを使用しないのはなぜですか?

エージェントは、cmdの場合を除き、ターミナルの既定として構成されているシェルを使用します。これは、Command Promptでは[shell integration](https://code.visualstudio.com/docs/terminal/shell-integration)がサポートされていないためで、エージェントがターミナル内部で起きていることを把握できる範囲が非常に限られることを意味します。コマンドの実行開始や終了に関する直接的なシグナルを得る代わりに、エージェントはタイムアウトやターミナルがアイドル状態になるのを監視することに依存して継続する必要があります。これにより、遅く不安定な体験につながります。

それでも`setting(chat.tools.terminal.terminalProfile.windows)`設定でエージェントがCommand Promptを使用するように構成できますが、PowerShellを使用する場合と比べて体験は劣ります。

```json
"chat.tools.terminal.terminalProfile.windows": {
  "path": "C:\\WINDOWS\\System32\\cmd.exe"
}
```

### すべてのツールとターミナルコマンドを自動的に承認できますか?

> [!CAUTION]
> この設定は、潜在的に破壊的な操作を含むすべての手動承認を無効にします。重要なセキュリティ保護が取り除かれ、攻撃者がマシンを侵害しやすくなります。影響を理解している場合にのみこの設定を有効にしてください。詳細は[セキュリティドキュメント](/docs/copilot/security.md)を参照してください。
>
> ユーザー確認のプロンプトなしにすべてのツールとターミナルコマンドを実行できるようにするには、`chat.tools.global.autoApprove`設定を有効にします。この設定はすべてのワークスペースに対してグローバルに適用されます!

### ツールとチャット参加者の違いは何ですか?

チャット参加者は、チャットでドメイン固有の質問ができるようにする専門アシスタントです。チャット参加者は、チャットリクエストを渡すと残りを引き受けてくれるドメインエキスパートだと考えるとよいでしょう。

ツールは、エージェントフローの一部として呼び出され、特定のタスクに貢献して実行します。1つのチャットリクエストに複数のツールを含められますが、一度にアクティブにできるチャット参加者は1つだけです。

### 自分のツールを作成できますか?

はい。ツールは2つの方法で作成できます:

* [Language Model Tools API](/api/extension-guides/ai/tools.md)を使用してツールを提供する**VS Code拡張機能を開発する**
* ツールを提供する**MCPサーバーを作成する**。[MCP開発者ガイド](/docs/copilot/guides/mcp-developer-guide.md)を参照してください

## 関連リソース

* [チャットツールのリファレンス](/docs/copilot/reference/copilot-vscode-features.md#chat-tools)
* [VS CodeでAIを使用する際のセキュリティに関する考慮事項](/docs/copilot/security.md)
