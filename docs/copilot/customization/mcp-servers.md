---
ContentId: 7c550054-4ade-4665-b368-215798c48673
DateApproved: 01/08/2026
MetaDescription: Visual Studio CodeのGitHub CopilotでModel Context Protocol (MCP)サーバーを構成して使用する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでMCPサーバーを使用する

Model Context Protocol (MCP)は、AIモデルが統一されたインターフェースを通じて外部のツールやサービスを使用できるようにするオープン標準です。VS Codeでは、MCPサーバーはファイル操作、データベース、外部APIとの対話などのタスクのための[ツール](/docs/copilot/chat/chat-tools.md)を提供します。

MCPサーバーは、組み込みツールや拡張機能が提供するツールと並んで、VS Codeのチャットをツールで拡張する3つの方法のうちの1つです。[ツールの種類](/docs/copilot/chat/chat-tools.md#types-of-tools)について詳しくはこちらをご覧ください。

この記事では、Visual Studio CodeでMCPサーバーを設定し、その機能を使用する方法について説明します。

> [!IMPORTANT]
> 組織によっては、VS CodeでのMCPサーバーの使用を無効にしていたり、使用できるMCPサーバーを制限していたりする場合があります。詳細については、管理者に問い合わせてください。

<details>
<summary>MCPの仕組み</summary>

MCPはクライアントサーバーアーキテクチャに従います。

* **MCPクライアント**（VS Codeなど）は、MCPサーバーに接続し、AIモデルに代わってアクションを要求します
* **MCPサーバー**は、明確に定義されたインターフェースを通じて特定の機能を公開する1つ以上のツールを提供します
* **Model Context Protocol**は、ツールの検出、呼び出し、応答処理など、クライアントとサーバー間の通信のためのメッセージ形式を定義します

たとえば、ファイルシステムMCPサーバーは、ファイルやディレクトリの読み取り、書き込み、検索を行うためのツールを提供する場合があります。GitHubのMCPサーバーは、リポジトリの一覧表示、プルリクエストの作成、Issueの管理を行うためのツールを提供します。MCPサーバーはローカルマシン上で実行することも、リモートでホストすることもでき、VS Codeは両方の構成をサポートしています。

この対話を標準化することで、MCPは各AIモデルと各ツール間のカスタム統合の必要性を排除します。これにより、ワークスペースに新しいMCPサーバーを追加するだけで、AIアシスタントの機能を拡張できます。[Model Context Protocol仕様](https://modelcontextprotocol.io/)の詳細については、こちらをご覧ください。

</details>

<details>
<summary>VS CodeでサポートされているMCP機能</summary>

VS Codeは以下のMCP機能をサポートしています。

* [トランスポート](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports):
    * ローカル標準入出力 (`stdio`)
    * ストリーム可能なHTTP (`http`)
    * Server-sent events (`sse`) - レガシーサポート。

* [機能](https://modelcontextprotocol.io/specification/2025-06-18#features):
    * ツール
    * プロンプト
    * リソース
    * Elicitation
    * サンプリング
    * 認証
    * サーバーの指示
    * [ルート](https://modelcontextprotocol.io/docs/concepts/roots)

</details>

> [!NOTE]
> VS CodeでのMCPサポートは、VS Code 1.102から一般提供されています。

## 前提条件

* [Visual Studio Code](/download)の最新バージョンをインストールする
* [Copilot](/docs/copilot/setup.md)へのアクセス

## MCPサーバーを追加する

> [!CAUTION]
> ローカルMCPサーバーは、マシン上で任意のコードを実行できます。信頼できるソースからのサーバーのみを追加し、起動する前にパブリッシャーとサーバー構成を確認してください。VS Codeは、初めてMCPサーバーを起動するときに、[MCPサーバーを信頼する](#mcp-server-trust)かどうかを確認するプロンプトを表示します。影響を理解するために、VS CodeでのAI使用に関する[セキュリティドキュメント](/docs/copilot/security.md)をお読みください。

### GitHub MCPサーバーレジストリからMCPサーバーを追加する

VS Codeの拡張機能ビューを介して、[GitHub MCPサーバーレジストリ](https://github.com/mcp)から直接MCPサーバーをインストールできます。MCPサーバーは、[ユーザープロファイル](/docs/configure/profiles.md)または現在のワークスペースのいずれかにインストールすることを選択できます。

拡張機能ビューからMCPサーバーをインストールするには:

1. `setting(chat.mcp.gallery.enabled)`設定でMCPサーバーギャラリーを有効にします。

1. 拡張機能ビュー (`kb(workbench.view.extensions)`) を開きます

1. 検索フィールドに`@mcp`と入力してMCPサーバーのリストを表示するか、コマンドパレットから**MCP: Browse Servers**コマンドを実行します。

    VS Codeは[GitHub MCPサーバーレジストリ](https://github.com/mcp)からMCPサーバーのリストを取得します。

1. MCPサーバーをインストールするには:

    * ユーザープロファイルの場合: **インストール**を選択します

    * ワークスペースの場合: MCPサーバーを右クリックし、**ワークスペースにインストール**を選択します

1. MCPサーバーの詳細を表示するには、リストでMCPサーバーを選択します。

### MCPサーバーを追加するその他のオプション

VS CodeでMCPサーバーを追加するには、他にもいくつかのオプションがあります。

<details>
<summary>ワークスペースの`mcp.json`ファイルにMCPサーバーを追加する</summary>

特定のプロジェクト用にMCPサーバーを構成する場合は、サーバー構成をワークスペースの`.vscode/mcp.json`ファイルに追加できます。これにより、同じMCPサーバー構成をプロジェクトチームと共有できます。

> [!IMPORTANT]
> 入力変数や環境ファイルを使用して、APIキーやその他の資格情報などの機密情報をハードコーディングしないようにしてください。

ワークスペースにMCPサーバーを追加するには:

1. ワークスペースに`.vscode/mcp.json`ファイルを作成します。

1. エディターの**Add Server**ボタンを選択して、新しいサーバーのテンプレートを追加します。VS CodeはMCPサーバー構成ファイルに対してIntelliSenseを提供します。

    次の例は、GitHubリモートMCPサーバーを構成する方法を示しています。[VS CodeでのMCP構成形式](#configuration-format)の詳細については、こちらをご覧ください。

    ```json
    {
        "servers": {
            "github-mcp": {
                "type": "http",
                "url": "https://api.githubcopilot.com/mcp"
            }
        }
    }
    ```

1. または、コマンドパレットから**MCP: Add Server**コマンドを実行し、追加するMCPサーバーの種類を選択し、サーバー情報を提供します。次に、**Workspace**を選択して、ワークスペースの`.vscode/mcp.json`ファイルにサーバーを追加します。

</details>

<details>
<summary>ユーザー構成にMCPサーバーを追加する</summary>

すべてのワークスペースに対してMCPサーバーを構成するには、サーバー構成をユーザー[プロファイル](/docs/configure/profiles.md)に追加できます。これにより、複数のプロジェクト間で同じサーバー構成を再利用できます。

ユーザー構成にMCPサーバーを追加するには:

* コマンドパレットから**MCP: Add Server**コマンドを実行し、サーバー情報を提供した後、**Global**を選択してサーバー構成をプロファイルに追加します。

* または、`mcp.json`ファイルをユーザープロファイルで開く**MCP: Open User Configuration**コマンドを実行します。その後、手動でサーバー構成をファイルに追加できます。

複数のVS Code[プロファイル](/docs/configure/profiles.md)を使用する場合、これにより、アクティブなプロファイルに基づいてさまざまなMCPサーバー構成を切り替えることができます。たとえば、[Playwright MCPサーバー](https://github.com/microsoft/playwright-mcp)はWeb開発プロファイルで構成されますが、Python開発プロファイルでは構成されません。

MCPサーバーは、構成されている場所で実行されます。[リモート](/docs/remote/remote-overview.md)に接続していて、リモートマシン上でサーバーを実行したい場合は、リモート設定 (**MCP: Open Remote User Configuration**) またはワークスペースの設定で定義する必要があります。ユーザー設定で定義されたMCPサーバーは常にローカルで実行されます。

</details>

<details>
<summary>開発コンテナーにMCPサーバーを追加する</summary>

MCPサーバーは、`devcontainer.json`ファイルを通じて開発コンテナーで構成できます。これにより、コンテナー化された開発環境の一部としてMCPサーバー構成を含めることができます。

開発コンテナーでMCPサーバーを構成するには、`customizations.vscode.mcp`セクションにサーバー構成を追加します。

```json
{
    "image": "mcr.microsoft.com/devcontainers/typescript-node:latest",
    "customizations": {
        "vscode": {
            "mcp": {
                "servers": {
                    "playwright": {
                        "command": "npx",
                        "args": ["-y", "@microsoft/mcp-server-playwright"]
                    }
                }
            }
        }
    }
}
```

開発コンテナーが作成されると、VS Codeは自動的にMCPサーバー構成をリモート`mcp.json`ファイルに書き込み、コンテナー化された開発環境で使用できるようにします。

</details>

<details>
<summary>MCPサーバーを自動的に検出する</summary>

VS Codeは、Claude Desktopなどの他のアプリケーションからMCPサーバー構成を自動的に検出して再利用できます。

`setting(chat.mcp.discovery.enabled)`設定で自動検出を構成します。MCPサーバー構成を検出するツールを1つ以上選択します。

</details>

<details>
<summary>コマンドラインからMCPサーバーをインストールする</summary>

VS Codeコマンドラインインターフェイスを使用して、ユーザープロファイルまたはワークスペースにMCPサーバーを追加することもできます。

ユーザープロファイルにMCPサーバーを追加するには、`--add-mcp` VS Codeコマンドラインオプションを使用し、`{\"name\":\"server-name\",\"command\":...}`という形式でJSONサーバー構成を提供します。

```bash
code --add-mcp "{\"name\":\"my-server\",\"command\": \"uvx\",\"args\": [\"mcp-server-fetch\"]}"
```

</details>

## チャットでMCPツールを使用する

MCPサーバーを追加したら、そのサーバーが提供するツールをチャットで使用できます。MCPツールはVS Codeの他のツールと同様に機能します。つまり、エージェントの使用時に自動的に呼び出されるか、プロンプトで明示的に参照できます。

チャットでMCPツールを使用するには:

1. **チャット**ビューを開きます (`kb(workbench.action.chat.open)`)。

1. ツールピッカーを開き、エージェントが使用できるツールを選択します。MCPツールはMCPサーバーごとにグループ化されています。

    > [!TIP]
    > [カスタムプロンプト](/docs/copilot/customization/prompt-files.md)または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成するときに、使用できるMCPツールを指定することもできます。

1. エージェントを使用する場合、プロンプトに基づいて必要に応じてツールが自動的に呼び出されます。

    たとえば、GitHub MCPサーバーをインストールしてから、「GitHubのIssueを一覧表示して」と尋ねます。

    ![エージェント使用時のMCPツール呼び出しを示すチャットビューのスクリーンショット。](../images/mcp-servers/chat-agent-mode-tool-invocation.png)

1. `#`の後にツール名を入力して、MCPツールを明示的に参照することもできます。

1. プロンプトが表示されたら、ツールの呼び出しを確認して承認します。

    ![チャットでのMCPツール確認ダイアログのスクリーンショット。](../images/mcp-servers/mcp-tool-confirmation.png)

ツールの承認の管理、ツールピッカーの使用、ツールセットの作成など、[チャットでのツールの使用](/docs/copilot/chat/chat-tools.md)について詳しくはこちらをご覧ください。

### キャッシュされたMCPツールをクリアする

VS Codeが初めてMCPサーバーを起動すると、サーバーの機能とツールが検出されます。その後、[これらのツールをチャットで使用](#use-mcp-tools-in-chat)できるようになります。VS CodeはMCPサーバーのツールのリストをキャッシュします。キャッシュされたツールをクリアするには、コマンドパレットの**MCP: Reset Cached Tools**コマンドを使用します。

## MCPリソースを使用する

MCPサーバーは、チャットプロンプトでコンテキストとして使用できるリソースへの直接アクセスを提供できます。たとえば、ファイルシステムMCPサーバーではファイルやディレクトリにアクセスでき、データベースMCPサーバーではデータベーステーブルへのアクセスを提供できます。

MCPサーバーからチャットプロンプトにリソースを追加するには:

1. チャットビューで、**コンテキストの追加** > **MCPリソース**を選択します

1. リストからリソースタイプを選択し、オプションのリソース入力パラメーターを指定します。

    ![GitHub MCPサーバーによって提供されるリソースタイプを示すMCPリソースクイックピックのスクリーンショット。](../images/mcp-servers/mcp-resources-quick-pick.png)

MCPサーバーで使用可能なリソースのリストを表示するには、**MCP: Browse Resources**コマンドを使用するか、**MCP: List Servers** > **Browse Resources**コマンドを使用して特定のサーバーのリソースを表示します。

MCPツールは、応答の一部としてリソースを返すことができます。**保存**を選択するか、エクスプローラービューにリソースをドラッグアンドドロップすることで、これらのリソースを表示またはワークスペースに保存できます。

## MCPプロンプトを使用する

MCPサーバーは、スラッシュコマンドを使用してチャットで呼び出すことができる一般的なタスク用の事前構成済みプロンプトを提供できます。チャットでMCPプロンプトを呼び出すには、チャット入力フィールドに`/`と入力し、`mcp.servername.promptname`という形式でプロンプト名を入力します。

オプションで、MCPプロンプトは追加の入力パラメーターを求める場合があります。

![MCPプロンプトの呼び出しと追加の入力パラメーターを求めるダイアログを示すチャットビューのスクリーンショット。](../images/mcp-servers/mcp-prompt-invocation.png)

## 関連ツールをツールセットにグループ化する

MCPサーバーを追加すると、ツールのリストが長くなる可能性があります。関連するツールをツールセットにグループ化すると、管理や参照が容易になります。

[ツールセットを使用したツールのグループ化](/docs/copilot/chat/chat-tools.md#group-tools-with-tool-sets)の方法について詳しくはこちらをご覧ください。

## インストールされているMCPサーバーを管理する

サーバーの起動や停止、サーバーログの表示、サーバーのアンインストールなど、インストールされているMCPサーバーに対してさまざまなアクションを実行できます。

MCPサーバーでこれらのアクションを実行するには、次のいずれかのオプションを使用します:

* **MCP SERVERS - INSTALLED**セクションでサーバーを右クリックするか、歯車アイコンを選択します

    ![拡張機能ビューにMCPサーバーを表示するスクリーンショット。](../images/mcp-servers/extensions-view-mcp-servers.png)

* `mcp.json`構成ファイルを開き、エディター内のアクション（コードレンズ）にアクセスします

    ![サーバーを管理するためのレンズを備えたMCPサーバー構成。](../images/mcp-servers/mcp-server-config-lenses.png)

    MCPサーバー構成にアクセスするには、**MCP: Open User Configuration**または**MCP: Open Workspace Folder Configuration**コマンドを使用します。

* コマンドパレットから**MCP: List Servers**コマンドを実行し、サーバーを選択します

    ![コマンドパレットでのMCPサーバーに対するアクションを示すスクリーンショット。](../images/mcp-servers/mcp-list-servers-actions.png)

### MCPサーバーを自動的に起動する

MCPサーバーを追加したり、その構成を変更したりすると、VS Codeは提供されるツールを検出するためにサーバーを（再）起動する必要があります。

`setting(chat.mcp.autostart)`設定（実験的）を使用して、構成の変更が検出されたときにMCPサーバーを自動的に再起動するようにVS Codeを構成できます。

または、チャットビューから手動でMCPサーバーを再起動するか、[MCPサーバーリスト](#manage-installed-mcp-servers)から再起動アクションを選択します。

![チャットビューの更新ボタンを示すスクリーンショット。](../images/mcp-servers/chat-view-mcp-refresh.png)

## MCPサーバーを見つける

MCPはまだ比較的新しい標準であり、エコシステムは急速に進化しています。より多くの開発者がMCPを採用するにつれて、プロジェクトとの統合に使用できるサーバーやツールが増えることが予想されます。

[GitHub MCPサーバーレジストリ](https://github.com/mcp)は、手始めとして最適です。レジストリには、VS Codeの拡張機能ビューから直接アクセスできます。

MCPの[公式サーバーリポジトリ](https://github.com/modelcontextprotocol/servers)では、MCPの汎用性を示す公式およびコミュニティ提供のサーバーが提供されています。ファイルシステム操作、データベース対話、Webサービスなど、さまざまな機能のサーバーを探索できます。

VS Code拡張機能もMCPサーバーを提供し、拡張機能のインストールプロセスの一部として構成できます。MCPサーバーサポートを提供する拡張機能については、[Visual Studio Marketplace](https://marketplace.visualstudio.com/VSCode)を確認してください。

## MCPサーバーの信頼

MCPサーバーは、マシン上で任意のコードを実行できます。信頼できるソースからのサーバーのみを追加し、起動する前にパブリッシャーとサーバー構成を確認してください。影響を理解するために、VS CodeでのAI使用に関する[セキュリティドキュメント](/docs/copilot/security.md)をお読みください。

ワークスペースにMCPサーバーを追加したり、その構成を変更したりする場合は、サーバーを起動する前に、サーバーとその機能を信頼することを確認する必要があります。VS Codeは、初めてサーバーを起動するときに、サーバーを信頼することを確認するダイアログを表示します。ダイアログ内のMCPサーバーへのリンクを選択して、別のウィンドウでMCPサーバー構成を確認します。

![MCPサーバー信頼プロンプトを示すスクリーンショット。](../images/mcp-servers/mcp-server-trust-dialog.png)

サーバーを信頼しない場合、サーバーは起動されず、チャット要求はサーバーが提供するツールを使用せずに続行されます。

コマンドパレットから**MCP: Reset Trust**コマンドを実行することで、MCPサーバーの信頼をリセットできます。

> [!NOTE]
> `mcp.json`ファイルから直接MCPサーバーを起動した場合、サーバー構成を信頼するかどうかは求められません。

## デバイス間でMCPサーバーを同期する

[設定の同期](/docs/configure/settings-sync.md)を有効にすると、MCPサーバー構成を含む設定と構成をデバイス間で同期できます。これにより、一貫した開発環境を維持し、すべてのデバイスで同じMCPサーバーにアクセスできます。

設定の同期でMCPサーバーの同期を有効にするには、コマンドパレットから**Settings Sync: Configure**コマンドを実行し、同期された構成のリストに**MCP Servers**が含まれていることを確認します。

## 構成形式

MCPサーバーは、サーバー定義と機密データ用のオプションの入力変数という2つのメインセクションを定義するJSONファイル（`mcp.json`）を使用して構成されます。

MCPサーバーは、さまざまなトランスポートメソッドを使用して接続できます。サーバーの通信方法に基づいて適切な構成を選択してください。

### 構成構造

構成ファイルには、次の2つの主要なセクションがあります。

* **`"servers": {}`** - MCPサーバーとその構成のリストが含まれます
* **`"inputs": []`** - APIキーなどの機密情報のオプションのプレースホルダー

サーバー構成では、たとえばワークスペースフォルダー（`${workspaceFolder}`）を参照するために、[事前定義された変数](/docs/reference/variables-reference.md)を使用できます。

### 標準I/O (stdio) サーバー

標準入出力ストリームを介して通信するサーバーには、この構成を使用します。これは、ローカルで実行されるMCPサーバーの最も一般的なタイプです。

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|----------|
| `type` | はい | サーバー接続タイプ | `"stdio"` |
| `command` | はい | サーバー実行可能ファイルを起動するコマンド。システムパスで使用可能であるか、フルパスを含める必要があります。 | `"npx"`, `"node"`, `"python"`, `"docker"` |
| `args` | いいえ | コマンドに渡される引数の配列 | `["server.py", "--port", "3000"]` |
| `env` | いいえ | サーバーの環境変数 | `{"API_KEY": "${input:api-key}"}` |
| `envFile` | いいえ | より多くの変数をロードするための環境ファイルへのパス | `"${workspaceFolder}/.env"` |

> [!NOTE]
> stdioサーバーでDockerを使用する場合、detachオプション（`-d`）を使用しないでください。VS Codeと通信するには、サーバーをフォアグラウンドで実行する必要があります。

<details>
<summary>ローカルサーバー構成の例</summary>

この例は、`npx`を使用した基本的なローカルMCPサーバーの最小構成を示しています。

```json
{
    "servers": {
        "memory": {
            "command": "npx",
            "args": [
            "-y",
            "@modelcontextprotocol/server-memory"
            ]
        }
    }
}
```

</details>

### HTTPおよびServer-Sent Events (SSE) サーバー

HTTP経由で通信するサーバーには、この構成を使用します。VS Codeは最初にHTTPストリームトランスポートを試み、HTTPがサポートされていない場合はSSEにフォールバックします。

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|----------|
| `type` | はい | サーバー接続タイプ | `"http"`, `"sse"` |
| `url` | はい | サーバーのURL | `"http://localhost:3000"`, `"https://api.example.com/mcp"` |
| `headers` | いいえ | 認証または構成用のHTTPヘッダー | `{"Authorization": "Bearer ${input:api-token}"}` |

ネットワーク経由で使用可能なサーバーに加えて、VS Codeは、UnixソケットまたはWindows名前付きパイプ上のHTTPトラフィックをリッスンするMCPサーバーに接続できます。これを行うには、`unix:///path/to/server.sock`またはWindowsの場合は`pipe:///pipe/named-pipe`という形式でソケットまたはパイプのパスを指定します。`unix:///tmp/server.sock#/mcp/subpath`などのURLフラグメントを使用してサブパスを指定できます。

<details>
<summary>リモートサーバー構成の例</summary>

この例は、認証なしのリモートMCPサーバーの最小構成を示しています。

```json
{
    "servers": {
        "context7": {
            "type": "http",
            "url": "https://mcp.context7.com/mcp"
        }
    }
}
```

</details>

### 機密データの入力変数

入力変数を使用すると、構成値のプレースホルダーを定義でき、APIキーやパスワードなどの機密情報をサーバー構成に直接ハードコーディングする必要がなくなります。

`${input:variable-id}`を使用して入力変数を参照すると、サーバーが初めて起動するときに、VS Codeは値の入力を求めます。値は、その後の使用のために安全に保存されます。VS Codeの[入力変数](/docs/reference/variables-reference.md#input-variables)の詳細については、こちらをご覧ください。

**入力変数のプロパティ:**

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|---------|
| `type` | はい | 入力プロンプトのタイプ | `"promptString"` |
| `id` | はい | サーバー構成で参照するための一意の識別子 | `"api-key"`, `"database-url"` |
| `description` | はい | ユーザーフレンドリーなプロンプトテキスト | `"GitHub Personal Access Token"` |
| `password` | いいえ | 入力された入力を非表示にする (デフォルト: false) | `true` for API keys and passwords |

<details>
<summary>入力変数を使用したサーバー構成の例</summary>

この例では、APIキーを必要とするローカルサーバーを構成します。

```json
{
    "inputs": [
        {
            "type": "promptString",
            "id": "perplexity-key",
            "description": "Perplexity API Key",
            "password": true
        }
    ],
    "servers": {
        "perplexity": {
            "type": "stdio",
            "command": "npx",
            "args": [
                "-y",
                "server-perplexity-ask"
            ],
            "env": {
                "PERPLEXITY_API_KEY": "${input:perplexity-key}"
            }
        }
    }
}
```

</details>

### サーバーの命名規則

MCPサーバーを定義するときは、サーバー名について次の命名規則に従ってください。

* `"uiTesting"や"githubIntegration"など、サーバー名にはキャメルケースを使用する
* 空白や特殊文字を使用しない
* 競合を避けるために、各サーバーに一意の名前を使用する
* `"github"や"database"など、サーバーの機能やブランドを反映したわかりやすい名前を使用する

## MCPサーバーのトラブルシューティングとデバッグ

### MCP出力ログ

VS CodeがMCPサーバーで問題が発生した場合、チャットビューにエラーインジケーターが表示されます。

![MCPサーバーエラー](../images/mcp-servers/mcp-error-loading-tool.png)

チャットビューでエラー通知を選択し、**Show Output**オプションを選択してサーバーログを表示します。または、コマンドパレットから**MCP: List Servers**を実行し、サーバーを選択してから**Show Output**を選択します。

![MCPサーバーエラー出力](../images/mcp-servers/mcp-server-error-output.png)

### MCPサーバーをデバッグする

MCPサーバー構成に`dev`キーを追加することで、MCPサーバーの_開発モード_を有効にできます。これは、次の2つのプロパティを持つオブジェクトです。

* `watch`: ファイルの変更を監視してMCPサーバーを再起動するファイルglobパターン。
* `debug`: MCPサーバーでデバッガを設定できるようにします。現在、VS CodeはNode.jsおよびPython MCPサーバーのデバッグをサポートしています。

MCP開発ガイドの[VS CodeでのMCP開発モード](/api/extension-guides/ai/mcp.md#mcp-development-mode-in-vs-code)の詳細については、こちらをご覧ください。

## MCPアクセスを一元管理する

組織は、GitHubポリシーを介してMCPサーバーへのアクセスを一元管理できます。[MCPサーバーのエンタープライズ管理](/docs/enterprise/ai-settings.md#configure-mcp-server-access)の詳細については、こちらをご覧ください。

## よくある質問

### 使用するMCPツールを制御できますか?

* エージェントを使用するときにチャットビューの**Tools**ボタンを選択し、必要に応じて特定のツールをオン/オフに切り替えます。
* **コンテキストの追加**ボタンを使用するか、`#`を入力して、特定のツールをプロンプトに追加します。
* より高度な制御を行うには、`.github/copilot-instructions.md`を使用してツールの使用を微調整できます。

### Docker使用時にMCPサーバーが起動しない

コマンド引数が正しいことと、コンテナーがデタッチモード（`-d`オプション）で実行されていないことを確認してください。また、MCPサーバーの出力でエラーメッセージを確認することもできます（[トラブルシューティング](#troubleshoot-and-debug-mcp-servers)を参照）。

### "Cannot have more than 128 tools per request." というエラーが表示されます。

モデルの制約により、チャットリクエストでは一度に最大128個のツールを有効にできます。選択しているツールが128個を超える場合は、チャットビューのツールピッカーでいくつかのツールまたはサーバー全体の選択を解除してツールの数を減らすか、仮想ツールが有効になっていること（`setting(github.copilot.chat.virtualTools.threshold)`）を確認してください。

![チャット入力のツールアイコンを強調表示し、アクティブなツールを選択できるツールクイックピックを示すチャットビューのスクリーンショット。](../images/mcp-servers/agent-mode-select-tools.png)

## 関連リソース

* [Model Context Protocolドキュメント](https://modelcontextprotocol.io/)
* [Model Context Protocolサーバーリポジトリ](https://github.com/modelcontextprotocol/servers)
* [VS Codeチャットでエージェントを使用する](/docs/copilot/chat/copilot-chat.md#built-in-agents)
