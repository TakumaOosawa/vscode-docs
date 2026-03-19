---
ContentId: a3e1f7c2-8d4b-4f9a-b6e5-2c8d3f1a9b7e
DateApproved: 3/9/2026
MetaDescription: MCP サーバー構成形式、コマンド、および Visual Studio Code の設定に関するリファレンス。
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

この記事では、MCP サーバー構成ファイル形式、関連コマンド、および VS Code の設定に関するリファレンスを提供します。MCP サーバーの追加と管理の詳細については、「[MCP サーバーの追加と管理](/docs/copilot/customization/mcp-servers.md)」を参照してください。

## 構成ファイル

MCP サーバー構成は、`mcp.json` JSON ファイルに保存されます。このファイルはワークスペース（`.vscode/mcp.json`）または[ユーザープロファイル](/docs/configure/profiles.md)に配置できます。VS Code は構成ファイルの IntelliSense を提供します。

### 構成の構造

構成ファイルには、主に 2 つのセクションがあります:

* **`"servers": {}`**: サーバー名をその構成にマップするオブジェクト。各キーはサーバー名で、値はサーバー構成オブジェクトです。サーバータイプに応じて、異なるフィールドが必須です。

* **`"inputs": []`**: API キーなどの機密情報の入力変数定義の任意配列。

サーバー構成で[定義済み変数](/docs/reference/variables-reference.md)を使用できます。たとえば、ワークスペースフォルダを参照する場合は（`${workspaceFolder}`）。

### 標準入出力（stdio）サーバー

標準入出力ストリームを通じて通信するサーバーに対して、この構成を使用します。これはローカル実行の MCP サーバーで最も一般的なタイプです。

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|----------|
| `type` | はい | サーバー接続タイプ | `"stdio"` |
| `command` | はい | サーバー実行可能ファイルを起動するコマンド。システムパスで利用可能であるか、完全パスを含む必要があります。 | `"npx"`、`"node"`、`"python"`、`"docker"` |
| `args` | いいえ | コマンドに渡される引数の配列 | `["server.py", "--port", "3000"]` |
| `env` | いいえ | サーバーの環境変数 | `{"API_KEY": "${input:api-key}"}` |
| `envFile` | いいえ | より多くの変数を読み込むための環境ファイルのパス | `"${workspaceFolder}/.env"` |
| `sandboxEnabled` | いいえ | サーバーをサンドボックス環境で実行します。macOS と Linux でのみサポートされています。 | `true` |
| `sandbox` | いいえ | サンドボックス サーバーのファイルシステムとネットワークアクセスルール。`sandboxEnabled` が `true` の場合にのみ適用されます。「[サンドボックス構成](#sandbox-configuration)」を参照してください。 | `{"filesystem": {...}, "network": {...}}` |

> [!NOTE]
> stdio サーバーで Docker を使用する場合、デタッチオプション（`-d`）を使用しないでください。サーバーは VS Code と通信するためにフォアグラウンドで実行する必要があります。

<details>
<summary>ローカルサーバー構成例</summary>

この例は、`npx` を使用した基本的なローカル MCP サーバーの最小限の構成を示しています:

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

ローカル実行の stdio MCP サーバーのサンドボックスを有効にして、ファイルシステムとネットワークへのアクセスを制限できます。サンドボックス化されたサーバーは、明示的に許可したファイルシステムパスとネットワークドメインのみにアクセスできます。サンドボックスは macOS と Linux でのみ利用可能です。

サーバーのサンドボックスを有効にするには、その構成で `"sandboxEnabled": true` を設定します。次に、`sandbox` オブジェクトを使用してファイルシステムとネットワークアクセスルールを定義します。サンドボックス化されたサーバーが現在のルールが許可していないアクセスが必要な場合は、サーバー出力でエラーメッセージを確認し、`sandbox` 構成を更新してください。

> [!NOTE]
> サンドボックスが有効な場合、ツール確認は自動承認されます。サーバーが制御された環境で実行されるためです。

`sandbox` オブジェクトは、次のプロパティをサポートしています:

| プロパティ | 型 | 説明 |
|----------|------|-------------|
| `filesystem.allowWrite` | string[] | サーバーが書き込みを許可されているファイルパス。 |
| `filesystem.denyRead` | string[] | サーバーが読み取りを許可されていないファイルパス。 |
| `filesystem.denyWrite` | string[] | サーバーが書き込みを許可されていないファイルパス。 |
| `network.allowedDomains` | string[] | サーバーがアクセスを許可されているドメイン。ワイルドカード（例：`*.example.com`）がサポートされています。 |
| `network.deniedDomains` | string[] | サーバーがアクセスを許可されていないドメイン。 |

ファイルシステムパス値で[定義済み変数](/docs/reference/variables-reference.md)（`${workspaceFolder}` など）を使用できます。

<details>
<summary>サンドボックス構成例</summary>

この例はサンドボックスを有効にし、ワークスペースへの書き込みアクセスを許可し、`.ssh` ディレクトリへの読み取りアクセスを拒否し、特定のドメインへのネットワークアクセスを許可しています:

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

### HTTP とサーバー送信イベント（SSE）サーバー

HTTP を通じて通信するサーバーに対して、この構成を使用します。VS Code は最初に HTTP ストリーム トランスポートを試し、HTTP がサポートされていない場合は SSE にフォールバックします。

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|----------|
| `type` | はい | サーバー接続タイプ | `"http"`、`"sse"` |
| `url` | はい | サーバーの URL | `"http://localhost:3000"`、`"https://api.example.com/mcp"` |
| `headers` | いいえ | 認証または構成用の HTTP ヘッダー | `{"Authorization": "Bearer ${input:api-token}"}` |

ネットワークで利用可能なサーバーに加えて、VS Code は `unix:///path/to/server.sock` または Windows では `pipe:///pipe/named-pipe` の形式でソケットまたはパイプパスを指定することによって、Unix ソケットまたは Windows 名前付きパイプで HTTP トラフィックをリッスンしている MCP サーバーに接続できます。`unix:///tmp/server.sock#/mcp/subpath` などの URL フラグメントを使用してサブパスを指定できます。

<details>
<summary>リモート サーバー構成例</summary>

この例は、認証なしのリモート MCP サーバーの最小限の構成を示しています:

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

入力変数を使用すると、構成値のプレースホルダーを定義でき、API キーやパスワードなどの機密情報をサーバー構成に直接ハードコードする必要がなくなります。

`${input:variable-id}` を使用して入力変数を参照する場合、VS Code はサーバーが初めて起動するときに値を要求します。その後、値は後続の使用のために安全に保存されます。VS Code の[入力変数](/docs/reference/variables-reference.md#input-variables)について詳しく説明しています。

**入力変数プロパティ:**

| フィールド | 必須 | 説明 | 例 |
|-------|----------|-------------|---------|
| `type` | はい | 入力プロンプトのタイプ | `"promptString"` |
| `id` | はい | サーバー構成で参照する一意の識別子 | `"api-key"`、`"database-url"` |
| `description` | はい | ユーザーフレンドリーなプロンプト テキスト | `"GitHub Personal Access Token"` |
| `password` | いいえ | 入力を非表示にします（デフォルト: false） | API キーとパスワードの場合は`true` |

<details>
<summary>入力変数を使用したサーバー構成例</summary>

この例は、API キーが必要なローカル サーバーを構成しています:

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

サーバー構成に `dev` キーを追加することで、MCP サーバーの_開発モード_を有効にできます。これは 2 つのプロパティを持つオブジェクトです:

* `watch`: ファイル変更を監視して MCP サーバーを再起動するファイル glob パターン。
* `debug`: MCP サーバーでデバッガーをセットアップできます。現在、VS Code は Node.js と Python MCP サーバーのデバッグをサポートしています。

MCP Dev Guide の[MCP 開発モード](/api/extension-guides/ai/mcp.md#mcp-development-mode-in-vs-code)について詳しく説明しています。

### サーバーの命名規則

MCP サーバーを定義する際は、サーバー名に対して以下の命名規則に従ってください:

* サーバー名に camelCase を使用します。例：「uiTesting」または「githubIntegration」
* 空白または特殊文字の使用を避けてください
* 競合を避けるために、各サーバーに一意の名前を使用してください
* 「github」や「database」など、サーバーの機能またはブランドを反映した説明的な名前を使用してください

## コマンド

次の表に、コマンド パレット（`kb(workbench.action.showCommands)`）で利用可能な MCP 関連のコマンドをリストアップしています。

| コマンド | 説明 |
|---------|-------------|
| **MCP: Add Server** | ワークスペースまたはユーザープロファイルに新しい MCP サーバーを追加します。 |
| **MCP: Browse MCP Servers** | Extensions ビューで MCP サーバー ギャラリーを開きます。 |
| **MCP: Browse Resources** | MCP サーバーに提供されるリソースを参照します。 |
| **MCP: Install Server from Manifest** | MCP マニフェスト ファイルから MCP サーバーをインストールします。 |
| **MCP: List Servers** | すべての構成済み MCP サーバーをリストアップし、開始、停止、再起動、出力表示などのアクションを実行します。 |
| **MCP: Open Remote User Configuration** | リモート環境の `mcp.json` ファイルを開きます。 |
| **MCP: Open User Configuration** | ユーザープロファイルの `mcp.json` ファイルを開きます。 |
| **MCP: Open Workspace Folder MCP Configuration** | ワークスペースの `.vscode/mcp.json` ファイルを開きます。 |
| **MCP: Reset Cached Tools** | MCP サーバーのキャッシュされたツールリストをクリアします。サーバーのツールが変更された場合に使用します。 |
| **MCP: Reset Trust** | MCP サーバーの信頼の決定をリセットし、次の起動時に再確認が必要になります。 |
| **MCP: Show Installed Servers** | インストール済みの MCP サーバーすべてのリストを表示します。 |

## 設定

VS Code AI 設定の完全なリストは、「[AI 設定リファレンス](/docs/copilot/reference/copilot-settings.md)」を参照してください。以下は MCP サーバーに固有の設定です。

| 設定 | 説明 |
|---------|-------------|
| `setting(chat.mcp.access)` | VS Code で使用できる MCP サーバーを管理します。 |
| `setting(chat.mcp.discovery.enabled)` | 他のアプリケーションから MCP サーバー構成を自動検出するように構成します。 |
| `setting(chat.mcp.autostart)`（実験的） | 構成の変更が検出されたときに、MCP サーバーを自動的に起動します。 |
| `setting(chat.mcp.serverSampling)` | MCP サーバーに公開されているモデルを構成します（バックグラウンドでリクエストを作成）。 |
| `setting(chat.mcp.apps.enabled)`（実験的） | MCP サーバーによって提供される豊富なユーザー インターフェイス（MCP Apps）を有効にするか無効にするかを設定します。 |

## 関連リソース

* [MCP サーバーの追加と管理](/docs/copilot/customization/mcp-servers.md)
* [Model Context Protocol ドキュメント](https://modelcontextprotocol.io/)
* [MCP Dev Guide](/docs/copilot/guides/mcp-developer-guide.md)

