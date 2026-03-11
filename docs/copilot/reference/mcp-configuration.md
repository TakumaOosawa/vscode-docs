---
ContentId: a3e1f7c2-8d4b-4f9a-b6e5-2c8d3f1a9b7e
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeのMCPサーバー構成形式、コマンド、設定のリファレンス。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- mcp
- model context protocol
- mcp.json
- configuration
- sandbox
- tools
- copilot
- reference
- ai
---
# MCP構成リファレンス

このアーティクルでは、MCPサーバー構成ファイル形式、関連するコマンド、およびVS Codeの設定に関するリファレンスを提供します。MCPサーバーの追加と管理については、[MCPサーバーの追加と管理](/docs/copilot/customization/mcp-servers.md)を参照してください。

## 構成ファイル

MCPサーバー構成は`mcp.json`JSONファイルに保存されます。このファイルはワークスペース(`.vscode/mcp.json`)または[ユーザープロファイル](/docs/configure/profiles.md)内に配置できます。VS Codeは構成ファイルのIntelliSenseを提供します。

### 構成構造

構成ファイルには2つのメインセクションがあります:

* **`"servers": {}`**: サーバー名をそれぞれの構成にマッピングするオブジェクト。各キーはサーバー名で、値はサーバー構成オブジェクトです。サーバータイプに応じて、異なるフィールドが必要になります。

* **`"inputs": []`**: APIキーなどの機密情報の入力変数定義のオプション配列。

サーバー構成で[定義済み変数](/docs/reference/variables-reference.md)を使用できます。たとえば、ワークスペースフォルダー(`${workspaceFolder}`)を参照します。

### 標準I/O(stdio)サーバー

標準入出力ストリームを介して通信するサーバーにこの構成を使用します。これはローカルで実行されるMCPサーバーの最も一般的なタイプです。

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|----------|
| `type` | はい | サーバー接続タイプ | `"stdio"` |
| `command` | はい | サーバー実行可能ファイルを開始するコマンド。システムパスで利用可能であるか、完全なパスを含む必要があります。 | `"npx"`、`"node"`、`"python"`、`"docker"` |
| `args` | いいえ | コマンドに渡される引数の配列 | `["server.py", "--port", "3000"]` |
| `env` | いいえ | サーバーの環境変数 | `{"API_KEY": "${input:api-key}"}` |
| `envFile` | いいえ | より多くの変数を読み込むための環境ファイルへのパス | `"${workspaceFolder}/.env"` |
| `sandboxEnabled` | いいえ | サーバーをサンドボックス環境で実行します。macOSとLinuxでのみサポートされています。 | `true` |
| `sandbox` | いいえ | サンドボックスサーバーのファイルシステムおよびネットワークアクセスルール。`sandboxEnabled`が`true`の場合にのみ適用されます。[サンドボックス構成](#サンドボックス構成)を参照してください。 | `{"filesystem": {...}, "network": {...}}` |

> [!NOTE]
> stdioサーバーでDockerを使用する場合、デタッチオプション(`-d`)を使用しないでください。サーバーはVS Codeと通信するためにフォアグラウンドで実行される必要があります。

<details>
<summary>例:ローカルサーバー構成</summary>

この例は、`npx`を使用した基本的なローカルMCPサーバーの最小限の構成を示しています:

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

### サンドボックス構成

ローカルで実行されるstdioMCPサーバーのサンドボックスを有効にして、ファイルシステムおよびネットワークへのアクセスを制限できます。サンドボックスサーバーは、明確に許可したファイルシステムパスおよびネットワークドメインのみにアクセスできます。サンドボックスはmacOSおよびLinuxでのみ利用可能です。

サーバーのサンドボックスを有効にするには、その構成で`"sandboxEnabled": true`を設定します。次に、`sandbox`オブジェクトを使用してファイルシステムおよびネットワークアクセスルールを定義します。サンドボックスサーバーが現在のルールで許可していないアクセスが必要な場合は、サーバー出力でエラーメッセージを確認し、`sandbox`構成を更新します。

> [!NOTE]
> サンドボックスが有効になっている場合、サーバーは制御された環境で実行されるため、ツール確認は自動承認されます。

`sandbox`オブジェクトは以下のプロパティをサポートします:

| プロパティ | 型 | 説明 |
|----------|------|-------------|
| `filesystem.allowWrite` | string[] | サーバーが書き込みを許可されるファイルパス。 |
| `filesystem.denyRead` | string[] | サーバーが読み取りを許可されないファイルパス。 |
| `filesystem.denyWrite` | string[] | サーバーが書き込みを許可されないファイルパス。 |
| `network.allowedDomains` | string[] | サーバーがアクセスを許可されるドメイン。ワイルドカード(`*.example.com`など)がサポートされています。 |
| `network.deniedDomains` | string[] | サーバーがアクセスを許可されないドメイン。 |

ファイルシステムパス値で`${workspaceFolder}`などの[定義済み変数](/docs/reference/variables-reference.md)を使用できます。

<details>
<summary>例:サンドボックス構成</summary>

この例はサンドボックスを有効にし、ワークスペースへの書き込みアクセスを許可し、`.ssh`ディレクトリへの読み取りアクセスを拒否し、特定のドメインへのネットワークアクセスを許可します:

```json
{
    "servers": {
        "myServer": {
            "type": "stdio",
            "command": "npx",
            "args": ["-y", "@example/mcp-server"],
            "sandboxEnabled": true,
            "sandbox": {
                "filesystem": {
                    "allowWrite": ["${workspaceFolder}"],
                    "denyRead": ["${userHome}/.ssh"]
                },
                "network": {
                    "allowedDomains": ["api.example.com", "*.cdn.example.com"]
                }
            }
        }
    }
}
```

</details>

### HTTPおよびServer-Sent Events(SSE)サーバー

HTTPを介して通信するサーバーにこの構成を使用します。VS CodeはまずHTTP Streamトランスポートを試し、HTTPがサポートされていない場合はSSEにフォールバックします。

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|----------|
| `type` | はい | サーバー接続タイプ | `"http"`、`"sse"` |
| `url` | はい | サーバーのURL | `"http://localhost:3000"`、`"https://api.example.com/mcp"` |
| `headers` | いいえ | 認証または構成用のHTTPヘッダー | `{"Authorization": "Bearer ${input:api-token}"}` |

ネットワーク経由で利用可能なサーバーに加えて、VS CodeはUnixソケットまたはWindowsナイプドパイプでHTTPトラフィックをリッスンしているMCPサーバーに接続できます。`unix:///path/to/server.sock`または`pipe:///pipe/named-pipe`の形式でソケットまたはパイプパスを指定します。`unix:///tmp/server.sock#/mcp/subpath`などのURLフラグメントを使用してサブパスを指定できます。

<details>
<summary>例:リモートサーバー構成</summary>

この例は、認証なしでリモートMCPサーバーの最小限の構成を示しています:

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

入力変数を使用すると、構成値のプレースホルダーを定義でき、APIキーやパスワードなどの機密情報をサーバー構成に直接ハードコードする必要がなくなります。

`${input:variable-id}`を使用して入力変数を参照すると、サーバーが初めて起動するときにVS Codeは値の入力を促します。値は後続の使用のために安全に保存されます。VS Codeの[入力変数](/docs/reference/variables-reference.md#input-variables)について詳しく学びます。

**入力変数プロパティ:**

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|---------|
| `type` | はい | 入力プロンプトのタイプ | `"promptString"` |
| `id` | はい | サーバー構成で参照する一意の識別子 | `"api-key"`、`"database-url"` |
| `description` | はい | ユーザーフレンドリーなプロンプトテキスト | `"GitHub Personal Access Token"` |
| `password` | いいえ | 入力テキストを隠す(デフォルト:false) | `true` APIキーおよびパスワード用 |

<details>
<summary>例:入力変数を使用したサーバー構成</summary>

この例は、APIキーを必要とするローカルサーバーを構成します:

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

### 開発モード

サーバー構成に`dev`キーを追加することで、MCPサーバーの_開発モード_を有効にできます。これは2つのプロパティを持つオブジェクトです:

* `watch`:MCPサーバーを再起動するファイル変更を監視するファイルグロブパターン。
* `debug`:MCPサーバーでデバッガーをセットアップできます。現在、VS CodeはNode.jsおよびPythonMCPサーバーのデバッグをサポートしています。

MCPDev Guideの[MCP開発モード](/api/extension-guides/ai/mcp.md#mcp-development-mode-in-vs-code)について詳しく学びます。

### サーバーの命名規則

MCPサーバーを定義するときは、サーバー名について次の命名規則に従います:

* サーバー名にはcamelCaseを使用します(例:「uiTesting」または「githubIntegration」)
* 空白または特殊文字を使用しないでください
* 競合を避けるために、各サーバーに一意の名前を使用してください
* サーバーの機能またはブランドを反映する説明的な名前を使用してください(例:「github」または「database」)

## コマンド

次の表に、コマンドパレット(`kb(workbench.action.showCommands)`)で利用可能なMCP関連コマンドを示します。

| コマンド | 説明 |
|---------|-------------|
| **MCP:サーバーの追加** | ワークスペースまたはユーザープロファイルに新しいMCPサーバーを追加します。 |
| **MCP:MCPサーバーの参照** | 拡張機能ビューでMCPサーバーギャラリーを開きます。 |
| **MCP:リソースの参照** | MCPサーバーが提供するリソースを参照します。 |
| **MCP:マニフェストからサーバーをインストール** | MCPマニフェストファイルからMCPサーバーをインストールします。 |
| **MCP:サーバーのリスト** | すべての構成されたMCPサーバーをリストし、起動、停止、再起動、出力表示などのアクションを実行します。 |
| **MCP:リモートユーザー構成を開く** | リモート環境の`mcp.json`ファイルを開きます。 |
| **MCP:ユーザー構成を開く** | ユーザープロファイルの`mcp.json`ファイルを開きます。 |
| **MCP:ワークスペースフォルダーMCP構成を開く** | ワークスペースの`.vscode/mcp.json`ファイルを開きます。 |
| **MCP:キャッシュされたツールをリセット** | MCPサーバーのツールのキャッシュされたリストをクリアします。サーバーのツールが変更されたときにこれを使用します。 |
| **MCP:信頼をリセット** | MCPサーバーの信頼決定をリセットし、次の起動時に再確認が必要になります。 |
| **MCP:インストール済みサーバーを表示** | インストール済みのすべてのMCPサーバーのリストを表示します。 |

## 設定

VS Code AI設定の完全なリストについては、[AI設定リファレンス](/docs/copilot/reference/copilot-settings.md)を参照してください。次の設定はMCPサーバーに固有のものです。

| 設定 | 説明 |
|---------|-------------|
| `setting(chat.mcp.access)` | VS Codeで使用できるMCPサーバーを管理します。 |
| `setting(chat.mcp.discovery.enabled)` | 他のアプリケーションからのMCPサーバー構成の自動検出を構成します。 |
| `setting(chat.mcp.autostart)`(試験的) | 構成の変更が検出されたときにMCPサーバーを自動的に起動します。 |
| `setting(chat.mcp.serverSampling)` | MCPサーバーに公開されるモデルを構成します(背景でリクエストを行う)。 |
| `setting(chat.mcp.apps.enabled)`(試験的) | MCPサーバーが提供するリッチユーザーインターフェースであるMCPアプリを有効または無効にします。 |

## 関連リソース

* [MCPサーバーの追加と管理](/docs/copilot/customization/mcp-servers.md)
* [Model Context Protocolドキュメント](https://modelcontextprotocol.io/)
* [MPDev Guide](/docs/copilot/guides/mcp-developer-guide.md)

