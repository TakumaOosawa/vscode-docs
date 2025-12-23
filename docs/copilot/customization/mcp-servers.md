---
ContentId: 7c550054-4ade-4665-b368-215798c48673
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotと一緒にModel Context Protocol(MCP)サーバーを構成して使用する方法を説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでMCPサーバーを使用する

Model Context Protocol(MCP)は、AIモデルが統一されたインターフェイスを通じて外部ツールやサービスを使用できるようにするオープン標準です。VS Codeでは、MCPサーバーがファイル操作、データベース、外部APIとのやり取りなどのタスク向けの[ツール](/docs/copilot/chat/chat-tools.md)を提供します。

MCPサーバーは、VS Codeでチャットをツールで拡張する3つの方法の1つです。ほかの方法として、組み込みツールと拡張機能が提供するツールがあります。[ツールの種類](/docs/copilot/chat/chat-tools.md#types-of-tools)を確認してください。

この記事では、Visual Studio CodeでMCPサーバーを設定し、その機能を使用する方法を説明します。

<details>
<summary>MCPの仕組みは何ですか?</summary>

MCPはクライアントサーバーアーキテクチャに従います。

* **MCPクライアント**(VS Codeなど)がMCPサーバーに接続し、AIモデルの代わりにアクションを要求します。
* **MCPサーバー**が、明確に定義されたインターフェイスを通じて特定の機能を公開する1つ以上のツールを提供します。
* **Model Context Protocol**が、ツールの検出、呼び出し、応答処理を含む、クライアントとサーバー間の通信メッセージ形式を定義します。

たとえば、ファイルシステムMCPサーバーは、ファイルやディレクトリの読み取り、書き込み、検索のツールを提供できます。GitHubのMCPサーバーは、リポジトリの一覧表示、プルリクエストの作成、Issueの管理のツールを提供します。MCPサーバーはローカルマシンで実行することも、リモートでホストすることもできます。VS Codeはどちらの構成もサポートします。

このやり取りを標準化することで、MCPはAIモデルごととツールごとに個別の統合を作る必要をなくします。これにより、ワークスペースに新しいMCPサーバーを追加するだけで、AIアシスタントの機能を拡張できます。[Model Context Protocol仕様](https://modelcontextprotocol.io/)を確認してください。

</details>

<details>
<summary>VS CodeでサポートされるMCP機能</summary>

VS Codeは、次のMCP機能をサポートします。

* [トランスポート](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports):
    * ローカルの標準入出力(`stdio`)
    * ストリーミング可能なHTTP(`http`)
    * Server-sent events(`sse`): 旧式サポートです。

* [機能](https://modelcontextprotocol.io/specification/2025-06-18#features):
    * ツール
    * プロンプト
    * リソース
    * Elicitation
    * サンプリング
    * 認証
    * サーバー指示
    * [ルート](https://modelcontextprotocol.io/docs/concepts/roots)

</details>

> [!NOTE]
> VS CodeのMCPサポートは、VS Code 1.102以降で一般提供(一般公開)されています。

## 前提条件

* 最新バージョンの[Visual Studio Code](/download)をインストールします。
* [Copilot](/docs/copilot/setup.md)にアクセスできる必要があります。

## MCPサーバーを追加する

> [!CAUTION]
> ローカルのMCPサーバーは、マシン上で任意のコードを実行できます。信頼できるソースのサーバーだけを追加し、開始する前に発行元とサーバー構成を確認してください。VS Codeは、MCPサーバーを初めて起動するときに、[MCPサーバーを信頼する](#mcp-server-trust)かどうかの確認を求めます。影響を理解するには、VS CodeでAIを使用するための[セキュリティドキュメント](/docs/copilot/security.md)を確認してください。

### GitHub MCPサーバーレジストリからMCPサーバーを追加する

VS Codeの拡張機能ビューから、[GitHub MCPサーバーレジストリ](https://github.com/mcp)からMCPサーバーを直接インストールできます。MCPサーバーは、[ユーザープロファイル](/docs/configure/profiles.md)または現在のワークスペースにインストールできます。

拡張機能ビューからGitHub MCPサーバーレジストリにあるMCPサーバーをインストールするには、次の手順を行います。

1. `setting(chat.mcp.gallery.enabled)`設定で、MCPサーバーギャラリーを有効にします。

1. 拡張機能ビューを開きます(`kb(workbench.view.extensions)`)。

1. 検索フィールドに`@mcp`と入力してMCPサーバーの一覧を表示するか、コマンドパレットから**MCP: Browse Servers**コマンドを実行します。

    VS Codeは[GitHub MCPサーバーレジストリ](https://github.com/mcp)からMCPサーバーの一覧を取得します。

1. MCPサーバーをインストールするには、次のいずれかを行います。

    * ユーザープロファイルの場合: **Install**を選択します。

    * ワークスペースの場合: MCPサーバーを右クリックして**Install in Workspace**を選択します。

1. MCPサーバーの詳細を表示するには、一覧でMCPサーバーを選択します。

### MCPサーバーを追加するほかの方法

VS CodeでMCPサーバーを追加する方法はほかにもあります。

<details>
<summary>ワークスペースの`mcp.json`ファイルにMCPサーバーを追加する</summary>

特定のプロジェクト向けにMCPサーバーを構成する場合は、`.vscode/mcp.json`ファイルでワークスペースにサーバー構成を追加できます。これにより、同じMCPサーバー構成をプロジェクトチームと共有できます。

> [!IMPORTANT]
> 入力変数または環境ファイルを使用して、APIキーなどの機密情報や資格情報をハードコーディングしないようにしてください。

ワークスペースにMCPサーバーを追加するには、次の手順を行います。

1. ワークスペースに`.vscode/mcp.json`ファイルを作成します。

1. エディターの**Add Server**ボタンを選択して、新しいサーバーのテンプレートを追加します。VS CodeはMCPサーバー構成ファイル向けのIntelliSenseを提供します。

    次の例では、GitHubのリモートMCPサーバーを構成する方法を示します。[VS CodeのMCP構成形式](#configuration-format)を確認してください。

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

1. 代わりに、コマンドパレットから**MCP: Add Server**コマンドを実行し、追加するMCPサーバーの種類を選択してサーバー情報を指定します。次に、**Workspace**を選択して、サーバーをワークスペースの`.vscode/mcp.json`ファイルに追加します。

</details>

<details>
<summary>ユーザー構成にMCPサーバーを追加する</summary>

すべてのワークスペース向けにMCPサーバーを構成するには、ユーザー[プロファイル](/docs/configure/profiles.md)にサーバー構成を追加できます。これにより、同じサーバー構成を複数プロジェクトで再利用できます。

ユーザー構成にMCPサーバーを追加するには、次のいずれかを行います。

* コマンドパレットから**MCP: Add Server**コマンドを実行し、サーバー情報を指定してから、**Global**を選択してサーバー構成をプロファイルに追加します。

* 代わりに、**MCP: Open User Configuration**コマンドを実行します。これにより、ユーザープロファイル内の`mcp.json`ファイルが開きます。その後、手動でサーバー構成をファイルに追加できます。

複数のVS Code[プロファイル](/docs/configure/profiles.md)を使用している場合は、アクティブなプロファイルに基づいてMCPサーバー構成を切り替えられます。たとえば、[Playwright MCPサーバー](https://github.com/microsoft/playwright-mcp)はWeb開発用プロファイルに構成し、Python開発用プロファイルには構成しないようにできます。

MCPサーバーは、構成した場所で実行されます。[リモート](/docs/remote/remote-overview.md)に接続していて、リモートマシン上でサーバーを実行したい場合は、リモート設定(**MCP: Open Remote User Configuration**)またはワークスペース設定で定義する必要があります。ユーザー設定で定義したMCPサーバーは、常にローカルで実行されます。

</details>

<details>
<summary>dev containerにMCPサーバーを追加する</summary>

MCPサーバーは、`devcontainer.json`ファイルを通じてDev Containersで構成できます。これにより、コンテナー化された開発環境の一部としてMCPサーバー構成を含められます。

Dev ContainerでMCPサーバーを構成するには、サーバー構成を`customizations.vscode.mcp`セクションに追加します。

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

Dev Containerが作成されると、VS CodeはMCPサーバー構成をリモートの`mcp.json`ファイルに自動で書き込み、コンテナー化された開発環境で使用できるようにします。

</details>

<details>
<summary>MCPサーバーを自動的に検出する</summary>

VS Codeは、Claude DesktopなどのほかのアプリケーションからMCPサーバー構成を自動的に検出して再利用できます。

自動検出は`setting(chat.mcp.discovery.enabled)`設定で構成します。MCPサーバー構成を検出する対象として、1つ以上のツールを選択します。

</details>

<details>
<summary>コマンドラインからMCPサーバーをインストールする</summary>

VS Codeのコマンドラインインターフェイスを使って、ユーザープロファイルまたはワークスペースにMCPサーバーを追加することもできます。

ユーザープロファイルにMCPサーバーを追加するには、VS Codeのコマンドラインオプション`--add-mcp`を使用し、`{\"name\":\"server-name\",\"command\":...}`の形式でJSONサーバー構成を指定します。

```bash
code --add-mcp "{\"name\":\"my-server\",\"command\": \"uvx\",\"args\": [\"mcp-server-fetch\"]}"
```

</details>

## チャットでMCPツールを使用する

MCPサーバーを追加すると、そのサーバーが提供するツールをチャットで使用できます。MCPツールはVS Codeのほかのツールと同様に動作します。エージェントの使用時に自動的に呼び出されるほか、プロンプトで明示的に参照することもできます。

チャットでMCPツールを使用するには、次の手順を行います。

1. **Chat**ビューを開きます(`kb(workbench.action.chat.open)`)。

1. ツールピッカーを開き、エージェントに使用を許可するツールを選択します。MCPツールはMCPサーバーごとにグループ化されています。

    > [!TIP]
    > [カスタムプロンプト](/docs/copilot/customization/prompt-files.md)または[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成する場合も、使用できるMCPツールを指定できます。

1. エージェントを使用している場合、ツールはプロンプトに基づいて必要に応じて自動的に呼び出されます。

    たとえば、GitHub MCPサーバーをインストールしてから、「List my GitHub issues」と依頼します。

    ![エージェント使用時のMCPツール呼び出しを示すChatビューのスクリーンショット。](../images/mcp-servers/chat-agent-mode-tool-invocation.png)

1. `#`の後にツール名を入力して、MCPツールを明示的に参照することもできます。

1. 求められたら、ツール呼び出しを確認して承認します。

    ![チャットで表示されるMCPツール確認ダイアログのスクリーンショット。](../images/mcp-servers/mcp-tool-confirmation.png)

ツール承認の管理方法、ツールピッカーの使用方法、ツールセットの作成方法などは、[チャットでツールを使用する](/docs/copilot/chat/chat-tools.md)を確認してください。

### キャッシュされたMCPツールをクリアする

VS CodeがMCPサーバーを初めて起動するとき、サーバーの機能とツールを検出します。その後、[これらのツールをチャットで使用](#use-mcp-tools-in-chat)できます。VS Codeは、MCPサーバーのツール一覧をキャッシュします。キャッシュされたツールをクリアするには、コマンドパレットで**MCP: Reset Cached Tools**コマンドを使用します。

## MCPリソースを使用する

MCPサーバーは、チャットプロンプトのコンテキストとして使用できるリソースへの直接アクセスを提供できます。たとえば、ファイルシステムMCPサーバーはファイルやディレクトリへのアクセスを提供できます。また、データベースMCPサーバーはデータベーステーブルへのアクセスを提供できます。

MCPサーバーからリソースをチャットプロンプトに追加するには、次の手順を行います。

1. Chatビューで、**Add Context** > **MCP Resources**を選択します。

1. 一覧からリソースの種類を選択し、必要に応じてリソース入力パラメーターを指定します。

    ![GitHub MCPサーバーが提供するリソース種類を示すMCPリソースQuick Pickのスクリーンショット。](../images/mcp-servers/mcp-resources-quick-pick.png)

MCPサーバーで使用できるリソースの一覧を表示するには、**MCP: Browse Resources**コマンドを使用します。または、**MCP: List Servers** > **Browse Resources**コマンドを使用して、特定のサーバーのリソースを表示します。

MCPツールは、応答の一部としてリソースを返す場合があります。**Save**を選択するか、リソースをエクスプローラービューにドラッグアンドドロップして、これらのリソースを表示またはワークスペースに保存できます。

## MCPプロンプトを使用する

MCPサーバーは、よくあるタスク向けの事前構成済みプロンプトを提供できます。これらはスラッシュコマンドでチャットから呼び出せます。チャットでMCPプロンプトを呼び出すには、チャット入力欄に`/`を入力し、その後に`mcp.servername.promptname`形式でプロンプト名を入力します。

MCPプロンプトは、追加の入力パラメーターを求める場合があります。

![追加の入力パラメーターを求めるダイアログとMCPプロンプト呼び出しを示すChatビューのスクリーンショット。](../images/mcp-servers/mcp-prompt-invocation.png)

## 関連ツールをツールセットにまとめる

MCPサーバーを追加するほど、ツール一覧が長くなる可能性があります。関連するツールをツールセットにまとめることで、管理と参照を簡単にできます。

[ツールセットの作成と使用](/docs/copilot/chat/chat-tools.md#group-tools-with-tool-sets)を確認してください。

## インストール済みのMCPサーバーを管理する

インストール済みのMCPサーバーに対して、サーバーの開始と停止、サーバーログの表示、サーバーのアンインストールなど、さまざまな操作を実行できます。

MCPサーバーに対してこれらの操作を実行するには、次のいずれかの方法を使用します。

* **MCP SERVERS - INSTALLED**セクションでサーバーを右クリックするか、歯車アイコンを選択します。

    ![拡張機能ビューに表示されるMCPサーバーのスクリーンショット。](../images/mcp-servers/extensions-view-mcp-servers.png)

* `mcp.json`構成ファイルを開き、エディター内(コードレンズ)でアクションにアクセスします。

    ![サーバー管理用のレンズを含むMCPサーバー構成。](../images/mcp-servers/mcp-server-config-lenses.png)

    MCPサーバー構成にアクセスするには、**MCP: Open User Configuration**または**MCP: Open Workspace Folder Configuration**コマンドを使用します。

* コマンドパレットから**MCP: List Servers**コマンドを実行し、サーバーを選択します。

    ![コマンドパレットでMCPサーバーのアクションを示すスクリーンショット。](../images/mcp-servers/mcp-list-servers-actions.png)

### MCPサーバーを自動的に開始する

MCPサーバーを追加したり構成を変更したりした場合、VS Codeはサーバーが提供するツールを検出するためにサーバーを(再)起動する必要があります。

`setting(chat.mcp.autostart)`設定(実験的)を使用すると、構成の変更が検出されたときにVS CodeがMCPサーバーを自動的に再起動するように構成できます。

代わりに、Chatビューから手動でMCPサーバーを再起動するか、[MCPサーバー一覧](#manage-installed-mcp-servers)から再起動アクションを選択します。

![ChatビューのRefreshボタンを示すスクリーンショット。](../images/mcp-servers/chat-view-mcp-refresh.png)

## MCPサーバーを見つける

MCPはまだ比較的新しい標準であり、エコシステムは急速に進化しています。より多くの開発者がMCPを採用するにつれて、プロジェクトに統合できるサーバーやツールはさらに増えると予想されます。

[GitHub MCPサーバーレジストリ](https://github.com/mcp)は、開始地点として最適です。VS Codeの拡張機能ビューからレジストリに直接アクセスできます。

MCPの[公式サーバーリポジトリ](https://github.com/modelcontextprotocol/servers)には、MCPの汎用性を示す公式サーバーとコミュニティ提供のサーバーがあります。ファイルシステム操作、データベース操作、Webサービスなど、さまざまな機能のサーバーを探索できます。

VS Code拡張機能は、MCPサーバーを提供し、拡張機能のインストールプロセスの一部として構成することもできます。MCPサーバーサポートを提供する拡張機能は、[Visual Studio Marketplace](https://marketplace.visualstudio.com/VSCode)で確認してください。

## MCPサーバーの信頼

MCPサーバーは、マシン上で任意のコードを実行できます。信頼できるソースのサーバーだけを追加し、開始する前に発行元とサーバー構成を確認してください。影響を理解するには、VS CodeでAIを使用するための[セキュリティドキュメント](/docs/copilot/security.md)を確認してください。

ワークスペースにMCPサーバーを追加したり構成を変更したりした場合は、起動する前にサーバーとその機能を信頼することを確認する必要があります。VS Codeは、サーバーを初めて起動するときに、サーバーを信頼するかどうかを確認するダイアログを表示します。ダイアログ内のMCPサーバーへのリンクを選択すると、別ウィンドウでMCPサーバー構成を確認できます。

![MCPサーバー信頼プロンプトのスクリーンショット。](../images/mcp-servers/mcp-server-trust-dialog.png)

サーバーを信頼しない場合、サーバーは起動されず、チャット要求はサーバーが提供するツールを使用せずに続行されます。

MCPサーバーの信頼をリセットするには、コマンドパレットから**MCP: Reset Trust**コマンドを実行します。

> [!NOTE]
> `mcp.json`ファイルからMCPサーバーを直接起動する場合は、サーバー構成を信頼するかどうかの確認は表示されません。

## デバイス間でMCPサーバーを同期する

[Settings Sync](/docs/configure/settings-sync.md)を有効にすると、MCPサーバー構成を含む設定と構成をデバイス間で同期できます。これにより、一貫した開発環境を維持し、すべてのデバイスで同じMCPサーバーにアクセスできます。

Settings SyncでMCPサーバー同期を有効にするには、コマンドパレットから**Settings Sync: Configure**コマンドを実行し、同期する構成の一覧に**MCP Servers**が含まれていることを確認します。

## 構成形式

MCPサーバーはJSONファイル(`mcp.json`)で構成します。このファイルでは、サーバー定義と、機密データ向けの省略可能な入力変数という2つの主要セクションを定義します。

MCPサーバーは、異なるトランスポート方法で接続できます。サーバーの通信方法に基づいて、適切な構成を選択してください。

### 構成の構造

構成ファイルには2つの主要セクションがあります。

* **`"servers": {}`**: MCPサーバーとその構成の一覧を含みます。
* **`"inputs": []`**: APIキーなどの機密情報向けの省略可能なプレースホルダーです。

サーバー構成では[定義済み変数](/docs/reference/variables-reference.md)を使用できます。たとえば、ワークスペースフォルダーを参照するには(`${workspaceFolder}`)を使用します。

### Standard I/O(stdio)サーバー

この構成は、標準入出力ストリームを通じて通信するサーバーに使用します。これは、ローカルで実行するMCPサーバーで最も一般的な種類です。

| Field | Required | Description | Examples |
|-------|----------|-------------|----------|
| `type` | Yes | サーバー接続の種類 | `"stdio"` |
| `command` | Yes | サーバー実行ファイルを起動するコマンドです。システムのパス上にあるか、完全なパスを含む必要があります。 | `"npx"`, `"node"`, `"python"`, `"docker"` |
| `args` | No | コマンドに渡す引数の配列 | `["server.py", "--port", "3000"]` |
| `env` | No | サーバーの環境変数 | `{"API_KEY": "${input:api-key}"}` |
| `envFile` | No | 追加の変数を読み込む環境ファイルへのパス | `"${workspaceFolder}/.env"` |

> [!NOTE]
> stdioサーバーでDockerを使用する場合は、デタッチオプション(`-d`)を使用しないでください。サーバーはVS Codeと通信するためにフォアグラウンドで実行する必要があります。

<details>
<summary>ローカルサーバー構成の例</summary>

この例では、`npx`を使用する基本的なローカルMCPサーバーの最小構成を示します。

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

### HTTPとServer-Sent Events(SSE)サーバー

この構成は、HTTPで通信するサーバーに使用します。VS Codeは最初にHTTP Streamトランスポートを試し、HTTPがサポートされていない場合はSSEにフォールバックします。

| Field | Required | Description | Examples |
|-------|----------|-------------|----------|
| `type` | Yes | サーバー接続の種類 | `"http"`, `"sse"` |
| `url` | Yes | サーバーのURL | `"http://localhost:3000"`, `"https://api.example.com/mcp"` |
| `headers` | No | 認証または構成向けのHTTPヘッダー | `{"Authorization": "Bearer ${input:api-token}"}` |

ネットワーク経由で利用できるサーバーに加えて、VS Codeは、UnixソケットまたはWindowsの名前付きパイプでHTTPトラフィックを待ち受けるMCPサーバーにも接続できます。接続するには、`unix:///path/to/server.sock`の形式、またはWindowsでは`pipe:///pipe/named-pipe`の形式でソケットまたはパイプのパスを指定します。`unix:///tmp/server.sock#/mcp/subpath`のようにURLフラグメントを使用してサブパスを指定できます。

<details>
<summary>リモートサーバー構成の例</summary>

この例では、認証なしのリモートMCPサーバーの最小構成を示します。

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

### 機密データ向けの入力変数

入力変数を使用すると、構成値のプレースホルダーを定義できます。これにより、APIキーやパスワードなどの機密情報をサーバー構成に直接ハードコーディングする必要がなくなります。

`${input:variable-id}`を使用して入力変数を参照すると、サーバーの初回起動時にVS Codeが値の入力を求めます。その値はその後の使用のために安全に保存されます。VS Codeの[入力変数](/docs/reference/variables-reference.md#input-variables)を確認してください。

**入力変数のプロパティ:**

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| `type` | Yes | 入力プロンプトの種類 | `"promptString"` |
| `id` | Yes | サーバー構成で参照する一意の識別子 | `"api-key"`, `"database-url"` |
| `description` | Yes | ユーザー向けのプロンプトテキスト | `"GitHub Personal Access Token"` |
| `password` | No | 入力した値を非表示にします(既定: false) | APIキーとパスワードでは`true` |

<details>
<summary>入力変数を使用するサーバー構成の例</summary>

この例では、APIキーが必要なローカルサーバーを構成します。

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

### サーバー名の命名規則

MCPサーバーを定義する場合は、サーバー名について次の命名規則に従ってください。

* サーバー名は、"uiTesting"や"githubIntegration"のようにcamelCaseを使用します。
* 空白や特殊文字を使用しないでください。
* 競合を避けるため、サーバーごとに一意の名前を使用してください。
* "github"や"database"のように、サーバーの機能またはブランドを反映する説明的な名前を使用してください。

## MCPサーバーのトラブルシューティングとデバッグ

### MCP出力ログ

VS CodeがMCPサーバーで問題を検出すると、Chatビューにエラーインジケーターが表示されます。

![MCP Server Error](../images/mcp-servers/mcp-error-loading-tool.png)

Chatビューでエラー通知を選択し、**Show Output**オプションを選択してサーバーログを表示します。代わりに、コマンドパレットから**MCP: List Servers**を実行し、サーバーを選択してから**Show Output**を選択します。

![MCP Server Error Output](../images/mcp-servers/mcp-server-error-output.png)

### MCPサーバーをデバッグする

MCPサーバー構成に`dev`キーを追加することで、MCPサーバーの_開発モード_を有効にできます。これは次の2つのプロパティを持つオブジェクトです。

* `watch`: ファイル変更を監視し、MCPサーバーを再起動するためのファイルglobパターンです。
* `debug`: MCPサーバーでデバッガーを設定できます。現在、VS CodeはNode.jsとPythonのMCPサーバーのデバッグをサポートします。

MCP開発ガイドで[VS CodeのMCP開発モード](/api/extension-guides/ai/mcp.md#mcp-development-mode-in-vs-code)を確認してください。

## MCPアクセスを一元管理する

組織は、GitHubポリシーを通じてMCPサーバーへのアクセスを一元管理できます。[MCPサーバーのエンタープライズ管理](/docs/setup/enterprise.md#configure-mcp-server-access)を確認してください。

## よくある質問

### 使用するMCPツールを制御できますか?

* エージェントを使用しているときにChatビューで**Tools**ボタンを選択し、必要に応じて特定のツールのオンとオフを切り替えます。
* **Add Context**ボタンを使用するか、`#`を入力して、プロンプトに特定のツールを追加します。
* さらに高度に制御するには、`.github/copilot-instructions.md`を使用してツール使用を細かく調整できます。

### Dockerを使用しているときにMCPサーバーが起動しません

コマンド引数が正しいことと、コンテナーがデタッチモード(`-d`オプション)で実行されていないことを確認します。MCPサーバー出力にエラーメッセージがないかを確認することもできます([トラブルシューティング](#troubleshoot-and-debug-mcp-servers)を参照してください)。

### "Cannot have more than 128 tools per request."というエラーが出ます

モデルの制約により、チャット要求で同時に有効にできるツールは最大128です。128を超えるツールを選択している場合は、Chatビューのツールピッカーで一部のツールまたはサーバー全体の選択を解除してツール数を減らすか、仮想ツールが有効になっていることを確認してください(`setting(github.copilot.chat.virtualTools.threshold)`)。

![Chatビューでチャット入力のToolsアイコンを強調表示し、有効なツールを選択できるツールQuick Pickを示すスクリーンショット。](../images/mcp-servers/agent-mode-select-tools.png)

## 関連リソース

* [Model Context Protocolドキュメント](https://modelcontextprotocol.io/)
* [Model Context Protocolサーバーリポジトリ](https://github.com/modelcontextprotocol/servers)
* [VS Codeチャットでエージェントを使用する](/docs/copilot/chat/copilot-chat.md#built-in-agents)---
ContentId: 7c550054-4ade-4665-b368-215798c48673
DateApproved: 12/10/2025
MetaDescription: Learn how to configure and use Model Context Protocol (MCP) servers with GitHub Copilot in Visual Studio Code.
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# Use MCP servers in VS Code

Model Context Protocol (MCP) is an open standard that lets AI models use external tools and services through a unified interface. In VS Code, MCP servers provide [tools](/docs/copilot/chat/chat-tools.md) for tasks like file operations, databases, or interacting with external APIs.

MCP servers are one of three ways to extend chat with tools in VS Code, alongside built-in tools and extension-contributed tools. Learn more about [types of tools](/docs/copilot/chat/chat-tools.md#types-of-tools).

This article guides you through setting up MCP servers and using their capabilities in Visual Studio Code.

<details>
<summary>How does MCP work?</summary>

MCP follows a client-server architecture:

* **MCP clients** (like VS Code) connect to MCP servers and request actions on behalf of the AI model
* **MCP servers** provide one or more tools that expose specific functionalities through a well-defined interface
* **Model Context Protocol** defines the message format for communication between clients and servers, including tool discovery, invocation, and response handling

For example, a file system MCP server might provide tools for reading, writing, or searching files and directories. GitHub's MCP server offers tools to list repositories, create pull requests, or manage issues. MCP servers can run locally on your machine or be hosted remotely, and VS Code supports both configurations.

By standardizing this interaction, MCP eliminates the need for custom integrations between each AI model and each tool. This allows you to extend your AI assistant's capabilities by simply adding new MCP servers to your workspace. Learn more about the [Model Context Protocol specification](https://modelcontextprotocol.io/).

</details>

<details>
<summary>Supported MCP capabilities in VS Code</summary>

VS Code supports the following MCP capabilities:

* [Transports](https://modelcontextprotocol.io/specification/2025-06-18/basic/transports):
    * Local standard input/output (`stdio`)
    * Streamable HTTP (`http`)
    * Server-sent events (`sse`) - legacy support.

* [Features](https://modelcontextprotocol.io/specification/2025-06-18#features):
    * Tools
    * Prompts
    * Resources
    * Elicitation
    * Sampling
    * Authentication
    * Server instructions
    * [Roots](https://modelcontextprotocol.io/docs/concepts/roots)

</details>

> [!NOTE]
> MCP support in VS Code is generally available starting from VS Code 1.102.

## Prerequisites

* Install the latest version of [Visual Studio Code](/download)
* Access to [Copilot](/docs/copilot/setup.md)

## Add an MCP server

> [!CAUTION]
> Local MCP servers can run arbitrary code on your machine. Only add servers from trusted sources, and review the publisher and server configuration before starting it. VS Code prompts you to confirm that you [trust the MCP server](#mcp-server-trust) when you start an MCP server for the first time. Read the [Security documentation](/docs/copilot/security.md) for using AI in VS Code to understand the implications.

### Add an MCP server from the GitHub MCP server registry

You can install an MCP server directly from the [GitHub MCP server registry](https://github.com/mcp) via the Extensions view in VS Code. You can choose to install the MCP server either in your [user profile](/docs/configure/profiles.md) or in the current workspace.

To install an MCP server from the Extensions view:

1. Enable the MCP server gallery with the `setting(chat.mcp.gallery.enabled)` setting.

1. Open the Extensions view (`kb(workbench.view.extensions)`)

1. Enter `@mcp` in the search field to show the list of MCP servers or run the **MCP: Browse Servers** command from the Command Palette.

    VS Code retrieves the list of MCP servers from the [GitHub MCP server registry](https://github.com/mcp).

1. To install an MCP server:

    * In your user profile: select **Install**

    * In your workspace: right-click the MCP server and select **Install in Workspace**

1. To view the MCP server details, select the MCP server in the list.

### Other options to add an MCP server

You have several other options to add an MCP server in VS Code:

<details>
<summary>Add an MCP server to a workspace `mcp.json` file</summary>

If you want to configure MCP servers for a specific project, you can add the server configuration to your workspace in the `.vscode/mcp.json` file. This allows you to share the same MCP server configuration with your project team.

> [!IMPORTANT]
> Make sure to avoid hardcoding sensitive information like API keys and other credentials by using input variables or environment files.

To add an MCP server to your workspace:

1. Create a `.vscode/mcp.json` file in your workspace.

1. Select the **Add Server** button in the editor to add a template for a new server. VS Code provides IntelliSense for the MCP server configuration file.

    The following example shows how to configure the GitHub remote MCP server. Learn more about the [MCP configuration format in VS Code](#configuration-format).

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

1. Alternatively, run the **MCP: Add Server** command from the Command Palette, choose the type of MCP server to add and provide the server information. Next, select **Workspace** to add the server to the `.vscode/mcp.json` file in your workspace.

</details>

<details>
<summary>Add an MCP server to your user configuration</summary>

To configure an MCP server for all your workspaces, you can add the server configuration to your user [profile](/docs/configure/profiles.md). This enables you to reuse the same server configuration across multiple projects.

To add an MCP server to your user configuration:

* Run the **MCP: Add Server** command from the Command Palette, provide the server information, and then select **Global** to add the server configuration to your profile.

* Alternatively, run the **MCP: Open User Configuration** command, which opens the `mcp.json` file in your user profile. You can then manually add the server configuration to the file.

When you use multiple VS Code [profiles](/docs/configure/profiles.md), this allows you to switch between different MCP server configurations based on your active profile. For example, the [Playwright MCP server](https://github.com/microsoft/playwright-mcp) could be configured in a web development profile, but not in a Python development profile.

MCP servers are executed wherever they're configured. If you're connected to a [remote](/docs/remote/remote-overview.md) and want a server to run on the remote machine, it should be defined in your remote settings (**MCP: Open Remote User Configuration**) or in the workspace's settings. MCP servers defined in your user settings are always executed locally.

</details>

<details>
<summary>Add an MCP server to a dev container</summary>

MCP servers can be configured in Dev Containers through the `devcontainer.json` file. This allows you to include MCP server configurations as part of your containerized development environment.

To configure MCP servers in a Dev Container, add the server configuration to the `customizations.vscode.mcp` section:

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

When the Dev Container is created, VS Code automatically writes the MCP server configurations to the remote `mcp.json` file, making them available in your containerized development environment.

</details>

<details>
<summary>Automatically discover MCP servers</summary>

VS Code can automatically detect and reuse MCP server configurations from other applications, such as Claude Desktop.

Configure autodiscovery with the `setting(chat.mcp.discovery.enabled)` setting. Select one or more tools from which to discover MCP server configuration from those tools.

</details>

<details>
<summary>Install an MCP server from the command line</summary>

You can also use the VS Code command-line interface to add an MCP server to your user profile or to a workspace.

To add an MCP server to your user profile, use the `--add-mcp` VS Code command line option, and provide the JSON server configuration in the form `{\"name\":\"server-name\",\"command\":...}`.

```bash
code --add-mcp "{\"name\":\"my-server\",\"command\": \"uvx\",\"args\": [\"mcp-server-fetch\"]}"
```

</details>

## Use MCP tools in chat

Once you have added an MCP server, you can use the tools it provides in chat. MCP tools work like other tools in VS Code: they can be automatically invoked when using agents or explicitly referenced in your prompts.

To use MCP tools in chat:

1. Open the **Chat** view (`kb(workbench.action.chat.open)`).

1. Open the tool picker to select which tools the agent is allowed to use. MCP tools are grouped per MCP server.

    > [!TIP]
    > When you create [custom prompts](/docs/copilot/customization/prompt-files.md) or [custom agents](/docs/copilot/customization/custom-agents.md), you can also specify which MCP tools can be used.

1. When using agents, tools are automatically invoked as needed based on your prompt.

    For example, install the GitHub MCP server and then ask "List my GitHub issues".

    ![Screenshot of the Chat view, showing an MCP tool invocation when using agents.](../images/mcp-servers/chat-agent-mode-tool-invocation.png)

1. You can also explicitly reference MCP tools by typing `#` followed by the tool name.

1. Review and approve tool invocations when prompted.

    ![Screenshot of the MCP tool confirmation dialog in chat.](../images/mcp-servers/mcp-tool-confirmation.png)

Learn more about [using tools in chat](/docs/copilot/chat/chat-tools.md), including how to manage tool approvals, use the tool picker, and create tool sets.

### Clear cached MCP tools

When VS Code starts the MCP server for the first time, it discovers the server's capabilities and tools. You can then [use these tools in chat](#use-mcp-tools-in-chat). VS Code caches the list of tools for an MCP server. To clear the cached tools, use the **MCP: Reset Cached Tools** command in the Command Palette.

## Use MCP resources

MCP servers can give direct access to resources that you can use as context in your chat prompts. For example, a file system MCP server can let you access files and directories, or a database MCP server might provide access to database tables.

To add a resource from an MCP server to your chat prompt:

1. In the Chat view, select **Add Context** > **MCP Resources**

1. Select a resource type from the list and provide optional resource input parameters.

    ![Screenshot of the MCP resource Quick Pick, showing resource types provided by the GitHub MCP server.](../images/mcp-servers/mcp-resources-quick-pick.png)

To view the list of available resources for an MCP server, use the **MCP: Browse Resources** command or use the **MCP: List Servers** > **Browse Resources** command to view resources for a specific server.

MCP tools can return resources as part of their response. You can view or save these resources to your workspace by selecting **Save** or by dragging and dropping the resource to the Explorer view.

## Use MCP prompts

MCP servers can provide preconfigured prompts for common tasks that you can invoke in chat with a slash command. To invoke an MCP prompt in chat, type `/` in the chat input field, followed by the prompt name, formatted as `mcp.servername.promptname`.

Optionally, the MCP prompt might ask you for extra input parameters.

![Screenshot of the Chat view, showing an MCP prompt invocation and a dialog asking for additional input parameters.](../images/mcp-servers/mcp-prompt-invocation.png)

## Group related tools in a tool set

As you add more MCP servers, the list of tools can become long. You can group related tools into a tool set to make them easier to manage and reference.

Learn more about how to [create and use tool sets](/docs/copilot/chat/chat-tools.md#group-tools-with-tool-sets).

## Manage installed MCP servers

You can perform various actions on the installed MCP servers, such as starting or stopping a server, viewing the server logs, uninstalling the server, and more.

To perform these actions on an MCP server, use either of these options:

* Right-click a server in the **MCP SERVERS - INSTALLED** section or select the gear icon

    ![Screenshot showing the MCP servers in the Extensions view.](../images/mcp-servers/extensions-view-mcp-servers.png)

* Open the `mcp.json` configuration file and access the actions inline in the editor (code lenses)

    ![MCP server configuration with lenses to manage server.](../images/mcp-servers/mcp-server-config-lenses.png)

    Use the **MCP: Open User Configuration** or **MCP: Open Workspace Folder Configuration** commands to access the MCP server configuration.

* Run the **MCP: List Servers** command from the Command Palette and select a server

    ![Screenshot showing the actions for an MCP server in the Command Palette.](../images/mcp-servers/mcp-list-servers-actions.png)

### Automatically start MCP servers

When you add an MCP server or change its configuration, VS Code needs to (re)start the server to discover the tools it provides.

You can configure VS Code to automatically restart the MCP server when configuration changes are detected by using the `setting(chat.mcp.autostart)` setting (Experimental).

Alternatively, manually restart the MCP server from the Chat view, or by selecting the restart action from the [MCP server list](#manage-installed-mcp-servers).

![Screenshot showing the Refresh button in the Chat view.](../images/mcp-servers/chat-view-mcp-refresh.png)

## Find MCP servers

MCP is still a relatively new standard, and the ecosystem is rapidly evolving. As more developers adopt MCP, you can expect to see an increasing number of servers and tools available for integration with your projects.

The [GitHub MCP server registry](https://github.com/mcp) is a great starting point. You can access the registry directly from the Extensions view in VS Code.

MCP's [official server repository](https://github.com/modelcontextprotocol/servers) provides official, and community-contributed servers that showcase MCP's versatility. You can explore servers for various functionalities, such as file system operations, database interactions, and web services.

VS Code extensions can also contribute MCP servers and configure them as part of the extension's installation process. Check the [Visual Studio Marketplace](https://marketplace.visualstudio.com/VSCode) for extensions that provide MCP server support.

## MCP server trust

MCP servers can run arbitrary code on your machine. Only add servers from trusted sources, and review the publisher and server configuration before starting it. Read the [Security documentation](/docs/copilot/security.md) for using AI in VS Code to understand the implications.

When you add an MCP server to your workspace or change its configuration, you need to confirm that you trust the server and its capabilities before starting it. VS Code shows a dialog to confirm that you trust the server when you start a server for the first time. Select the link to MCP server in the dialog to review the MCP server configuration in a separate window.

![Screenshot showing the MCP server trust prompt.](../images/mcp-servers/mcp-server-trust-dialog.png)

If you don't trust the server, it is not started, and chat requests continue without using the tools provided by the server.

You can reset trust for your MCP servers by running the **MCP: Reset Trust** command from the Command Palette.

> [!NOTE]
> If you start the MCP server directly from the `mcp.json` file, you are not prompted to trust the server configuration.

## Synchronize MCP servers across devices

With [Settings Sync](/docs/configure/settings-sync.md) enabled, you can synchronize settings and configurations across devices, including MCP server configurations. This allows you to maintain a consistent development environment and access the same MCP servers on all your devices.

To enable MCP server synchronization with Settings Sync, run the **Settings Sync: Configure** command from the Command Palette, and ensure that **MCP Servers** is included in the list of synchronized configurations.

## Configuration format

MCP servers are configured using a JSON file (`mcp.json`) that defines two main sections: server definitions and optional input variables for sensitive data.

MCP servers can connect using different transport methods. Choose the appropriate configuration based on how your server communicates.

### Configuration structure

The configuration file has two main sections:

* **`"servers": {}`** - Contains the list of MCP servers and their configurations
* **`"inputs": []`** - Optional placeholders for sensitive information like API keys

You can use [predefined variables](/docs/reference/variables-reference.md) in the server configuration, for example to refer to the workspace folder (`${workspaceFolder}`).

### Standard I/O (stdio) servers

Use this configuration for servers that communicate through standard input and output streams. This is the most common type for locally-run MCP servers.

| Field | Required | Description | Examples |
|-------|----------|-------------|----------|
| `type` | Yes | Server connection type | `"stdio"` |
| `command` | Yes | Command to start the server executable. Must be available on your system path or contain its full path. | `"npx"`, `"node"`, `"python"`, `"docker"` |
| `args` | No | Array of arguments passed to the command | `["server.py", "--port", "3000"]` |
| `env` | No | Environment variables for the server | `{"API_KEY": "${input:api-key}"}` |
| `envFile` | No | Path to an environment file to load more variables | `"${workspaceFolder}/.env"` |

> [!NOTE]
> When using Docker with stdio servers, don't use the detach option (`-d`). The server must run in the foreground to communicate with VS Code.

<details>
<summary>Example local server configuration</summary>

This example shows the minimal configuration for a basic, local MCP server using `npx`:

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

### HTTP and Server-Sent Events (SSE) servers

Use this configuration for servers that communicate over HTTP. VS Code first tries the HTTP Stream transport and falls back to SSE if HTTP is not supported.

| Field | Required | Description | Examples |
|-------|----------|-------------|----------|
| `type` | Yes | Server connection type | `"http"`, `"sse"` |
| `url` | Yes | URL of the server | `"http://localhost:3000"`, `"https://api.example.com/mcp"` |
| `headers` | No | HTTP headers for authentication or configuration | `{"Authorization": "Bearer ${input:api-token}"}` |

In addition to servers available over the network, VS Code can connect to MCP servers listening for HTTP traffic on Unix sockets or Windows named pipes by specifying the socket or pipe path in the form `unix:///path/to/server.sock` or `pipe:///pipe/named-pipe` on Windows. You can specify subpaths by using a URL fragment, such as `unix:///tmp/server.sock#/mcp/subpath`.

<details>
<summary>Example remote server configuration</summary>

This example shows the minimal configuration for a remote MCP server without authentication:

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

### Input variables for sensitive data

Input variables let you define placeholders for configuration values, avoiding the need to hardcode sensitive information like API keys or passwords directly in the server configuration.

When you reference an input variable using `${input:variable-id}`, VS Code prompts you for the value when the server starts for the first time. The value is then securely stored for subsequent use. Learn more about [input variables](/docs/reference/variables-reference.md#input-variables) in VS Code.

**Input variable properties:**

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| `type` | Yes | Type of input prompt | `"promptString"` |
| `id` | Yes | Unique identifier to reference in server config | `"api-key"`, `"database-url"` |
| `description` | Yes | User-friendly prompt text | `"GitHub Personal Access Token"` |
| `password` | No | Hide typed input (default: false) | `true` for API keys and passwords |

<details>
<summary>Example server configuration with input variables</summary>

This example configures a local server that requires an API key:

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

### Server naming conventions

When defining MCP servers, follow these naming conventions for the server name:

* Use camelCase for the server name, such as "uiTesting" or "githubIntegration"
* Avoid using whitespace or special characters
* Use a unique name for each server to avoid conflicts
* Use a descriptive name that reflects the server's functionality or brand, such as "github" or "database"

## Troubleshoot and debug MCP servers

### MCP output log

When VS Code encounters an issue with an MCP server, it shows an error indicator in the Chat view.

![MCP Server Error](../images/mcp-servers/mcp-error-loading-tool.png)

Select the error notification in the Chat view, and then select the **Show Output** option to view the server logs. Alternatively, run **MCP: List Servers** from the Command Palette, select the server, and then choose **Show Output**.

![MCP Server Error Output](../images/mcp-servers/mcp-server-error-output.png)

### Debug an MCP server

You can enable _development mode_ for MCP servers by adding a `dev` key to the MCP server configuration. This is an object with two properties:

* `watch`: A file glob pattern to watch for files change that will restart the MCP server.
* `debug`: Enables you to set up a debugger with the MCP server. Currently, VS Code supports debugging Node.js and Python MCP servers.

Learn more about [MCP development mode](/api/extension-guides/ai/mcp.md#mcp-development-mode-in-vs-code) in the MCP Dev Guide.

## Centrally control MCP access

Organizations can centrally manage access to MCP servers via GitHub policies. Learn more about [enterprise management of MCP servers](/docs/setup/enterprise.md#configure-mcp-server-access).

## Frequently asked questions

### Can I control which MCP tools are used?

* Select the **Tools** button in the Chat view when using agents, and toggle specific tools on/off as needed.
* Add specific tools to your prompt by using the **Add Context** button or by typing `#`.
* For more advanced control, you can use `.github/copilot-instructions.md` to fine-tune tool usage.

### The MCP server is not starting when using Docker

Verify that the command arguments are correct and that the container is not running in detached mode (`-d` option). You can also check the MCP server output for any error messages (see [Troubleshooting](#troubleshoot-and-debug-mcp-servers)).

### I'm getting an error that says "Cannot have more than 128 tools per request."

A chat request can have a maximum of 128 tools enabled at a time due to model constraints. If you have more than 128 tools selected, reduce the number of tools by deselecting some tools or whole servers in the tools picker in the Chat view, or ensure that virtual tools are enabled (`setting(github.copilot.chat.virtualTools.threshold)`).

![Screenshot showing the Chat view, highlighting the Tools icon in the chat input and showing the tools Quick Pick where you can select which tools are active.](../images/mcp-servers/agent-mode-select-tools.png)

## Related resources

* [Model Context Protocol Documentation](https://modelcontextprotocol.io/)
* [Model Context Protocol Server repository](https://github.com/modelcontextprotocol/servers)
* [Use agents in VS Code chat](/docs/copilot/chat/copilot-chat.md#built-in-agents)
