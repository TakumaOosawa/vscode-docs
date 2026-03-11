---
ContentId: 7c550054-4ade-4665-b368-215798c48673
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用してModel Context Protocol(MCP)サーバーを追加および管理する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- mcp
- model context protocol
- tools
- copilot
- ai
- agents
- chat
- customization
- api
---
# VS CodeでMCPサーバーを追加および管理する

[Model Context Protocol(MCP)](https://modelcontextprotocol.io/)は、AIモデルを外部ツールおよびサービスに接続するためのオープンスタンダードです。Visual Studio Codeでは、MCPサーバーはファイル操作、データベース、外部APIなどのタスク用の[ツール](/docs/copilot/agents/agent-tools.md)を提供します。MCPサーバーは、[リソース、プロンプト、インタラクティブアプリ](#other-mcp-capabilities)も提供できます。

MCPがAIカスタマイズフレームワークにどのように適合するかについては、[カスタマイズの概念](/docs/copilot/concepts/customization.md#mcp)および[ツールの概念](/docs/copilot/concepts/tools.md)を参照してください。

この記事では、MCPサーバーを追加、構成、管理する方法について説明します。チャットでのツールの使用方法については、[エージェントでツールを使用する](/docs/copilot/agents/agent-tools.md)を参照してください。

> [!TIP]
> [チャットカスタマイズエディター](/docs/copilot/customization/overview.md#chat-customizations-editor)(プレビュー)を使用して、すべてのチャットカスタマイズを一か所で検出、作成、管理できます。コマンドパレットから**Chat: Open Chat Customizations**を実行してください。

## クイックスタート: チャットでMCPサーバーを使用する

次の手順に従ってMCPサーバーをインストールし、チャットでそのツールを使用してください。この例では、[Playwright](https://github.com/microsoft/playwright-mcp)MCPサーバーを使用してブラウザーを通じてWebページと対話します。

1. 拡張機能ビュー(`kb(workbench.view.extensions)`)を開き、検索フィールドに`@mcp playwright`と入力します。

1. **インストール**を選択して、Playwright MCPサーバーをユーザープロファイルにインストールします。

1. プロンプトが表示されたら、サーバーの起動を信頼することを確認します。VS Codeはサーバーのツールを検出し、チャットで利用可能にします。

1. チャットビュー(`kb(workbench.action.chat.open)`)を開き、Playwrightツールを使用するプロンプトを入力します。例:

    ```prompt
    Go to code.visualstudio.com, decline the cookie banner, and give me a screenshot of the homepage.
    ```

    VS Codeがplaywrightツールを呼び出してページをブラウザーで開き、スクリーンショットを撮ります。各ツール呼び出しを確認するよう求められる場合があります。

> [!TIP]
> チャット入力の**ツールを構成**ボタンをクリックして、Playwright MCPサーバーで利用可能なすべてのツールを表示し、特定のツールのオン/オフを切り替えます。

## MCPサーバーを追加する

MCPサーバーギャラリーからMCPサーバーをインストールするには:

1. 拡張機能ビュー(`kb(workbench.view.extensions)`)を開き、検索フィールドに`@mcp`と入力します。これにより、ギャラリーで利用可能なMCPサーバーのリストが表示されます。

1. MCPサーバーをユーザープロファイルまたはワークスペースにインストールできます:

    * ユーザープロファイルにインストールするには、**インストール**を選択します。

    * ワークスペースにインストールするには、MCPサーバーを右クリックして**ワークスペースにインストール**を選択します。これにより、ワークスペース内の`.vscode/mcp.json`ファイルが更新されます。

1. MCPサーバーの詳細を表示するには、リスト内のMCPサーバーを選択して詳細ページを開きます。

> [!CAUTION]
> ローカルMCPサーバーはマシン上で任意のコードを実行できます。[信頼できるソース](#mcp-server-trust)からのみサーバーを追加し、起動前にパブリッシャーとサーバー構成を確認してください。VS CodeでAIを使用する場合の影響を理解するために、[セキュリティドキュメント](/docs/copilot/security.md)を読んでください。

### `mcp.json`ファイルを構成する

`mcp.json`ファイルを編集してMCPサーバーを手動で構成できます。このファイルには2つの場所があります:

* **ワークスペース**: プロジェクトで`.vscode/mcp.json`を作成または開きます。このファイルをソース管理に含めて、MCPサーバー構成をチーム全体と共有できます。
* **ユーザープロファイル**: **MCP: Open User Configuration**コマンドを実行して、[ユーザープロファイル](/docs/configure/profiles.md)フォルダーの`mcp.json`ファイルを開きます。ここで構成されたサーバーは、すべてのワークスペースで利用可能です。複数のプロファイルを使用する場合、各プロファイルは独自のMCPサーバー構成を持つことができます。

コマンドパレット(`kb(workbench.action.showCommands)`)で**MCP: Add Server**を実行して、ガイド付きフローでサーバーを追加することもでき、ターゲットとして**ワークスペース**または**グローバル**を選択できます。

> [!IMPORTANT]
> APIキーなどの機密情報をハードコードしないでください。代わりに[入力変数](/docs/copilot/reference/mcp-configuration.md#input-variables-for-sensitive-data)または環境ファイルを使用してください。

次の例は、リモートMCPサーバーとローカルMCPサーバーを構成する`mcp.json`ファイルを示しています:

```json
{
    "servers": {
        "github": {
            "type": "http",
            "url": "https://api.githubcopilot.com/mcp"
        },
        "playwright": {
            "command": "npx",
            "args": ["-y", "@microsoft/mcp-server-playwright"]
        }
    }
}
```

VS Codeは構成ファイルのIntelliSenseを提供します。完全な構成スキーマとフィールドリファレンスについては、[MCP構成リファレンス](/docs/copilot/reference/mcp-configuration.md)を参照してください。

> [!NOTE]
> MCPサーバーは構成されている場所で実行されます。ユーザープロファイル内のサーバーはローカルで動作します。[リモート](/docs/remote/remote-overview.md)に接続していて、サーバーをリモートマシンで実行したい場合は、ワークスペース設定またはリモートユーザー設定(**MCP: Open Remote User Configuration**)で定義してください。

### MCPサーバーを追加する他のオプション

<details>
<summary>MCPサーバーをdeveloper containerに追加する</summary>

MCPサーバーは、`devcontainer.json`ファイルを通じてDev Containerで構成できます。これにより、MCPサーバー構成をコンテナ化された開発環境の一部として含めることができます。

Dev ContainerでMCPサーバーを構成するには、`customizations.vscode.mcp`セクションにサーバー構成を追加します:

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

Dev Containerが作成されると、VS Codeは自動的にMCPサーバー構成をリモート`mcp.json`ファイルに書き込み、コンテナ化された開発環境で利用可能にします。

</details>

<details>
<summary>MCPサーバーを自動的に検出する</summary>

VS Codeはその他のアプリケーション(Claude Desktopなど)からMCPサーバー構成を自動的に検出および再利用できます。

`setting(chat.mcp.discovery.enabled)`設定により、MCPサーバーの設定を検出するためのツールを1つ以上選択できます。

</details>

<details>
<summary>コマンドラインからMCPサーバーをインストールする</summary>

VS Codeコマンドラインインターフェースを使用してMCPサーバーをユーザープロファイルまたはワークスペースに追加することもできます。

MCPサーバーをユーザープロファイルに追加するには、`--add-mcp`VS Codeコマンドラインオプションを使用し、JSON サーバー構成を`{\"name\":\"server-name\",\"command\":...}`の形式で提供します。

```bash
code --add-mcp "{\"name\":\"my-server\",\"command\": \"uvx\",\"args\": [\"mcp-server-fetch\"]}"
```

</details>

## その他のMCP機能

ツール以外に、MCPサーバーは他の機能を提供できます:

| 機能 | 説明 | 使用方法 |
|------------|-------------|------------|
| **リソース** | ファイル、データベーステーブル、APIレスポンスなど、MCPサーバーからのデータをプロンプト内のコンテキストとしてアクセスします。リソースは、チャトリクエストに添付する読み取り専用コンテキストを提供します。 | チャットビューで**コンテキストを追加**> **MCPリソース**を選択します。**MCP: Browse Resources**コマンドも使用できます。 |
| **プロンプト** | MCPサーバーから事前に構成されたプロンプトテンプレートを使用して一般的なタスクを標準化します。各MCPサーバーは、その機能に合わせた独自のプロンプトセットを公開できます。 | チャット入力に`/<MCPサーバー>.<プロンプト>`と入力します。 |
| **MCPアプリ** | フォーム、ビジュアライゼーション、ドラッグアンドドロップリストなどのインタラクティブUIコンポーネントをチャットに直接レンダリングされます。MCPアプリはテキストレスポンスを超えたより豊かなインタラクションを実現します。詳細は、[MCPアプリブログポスト](https://code.visualstudio.com/blogs/2026/01/26/mcp-apps-support)を参照してください。 | MCPアプリはMCPサーバーがそれらをサポートする場合、インラインで表示されます。 |

## MCPサーバーのサンドボックス化

macOSおよびLinuxでは、ローカルで実行されるstdio MCPサーバーのサンドボックス化を有効にして、ファイルシステムおよびネットワークへのアクセスを制限できます。サンドボックス化されたサーバーは分離された環境で実行され、明示的に許可したファイルパスおよびネットワークドメインにのみアクセスできます。

サーバーのサンドボックス化を有効にするには、`mcp.json`ファイルのサーバー構成で`"sandboxEnabled": true`を設定します。`sandbox`オブジェクトを追加して特定のファイルシステムおよびネットワークルールでサンドボックスの制限をさらにカスタマイズできます。

次の例は、ローカルMCPサーバーのサンドボックス化を有効にし、ワークスペース内のファイルへの書き込みおよび特定のAPIドメインへのアクセスのみに制限する方法を示しています:

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
                    "allowWrite": ["${workspaceFolder}"]
                },
                "network": {
                    "allowedDomains": ["api.example.com"]
                }
            }
        }
    }
}
```

サンドボックス化が有効な場合、サーバーからのツール呼び出しは制御された環境で実行されるため、自動承認されます。

完全なサンドボックス構成スキーマについては、[サンドボックス構成](/docs/copilot/reference/mcp-configuration.md#sandbox-configuration)リファレンスを参照してください。

> [!NOTE]
> サンドボックス化は現在Windowsで利用できません。

## MCPサーバーを管理する

VS Codeはサーバーの開始または停止、ログの表示、アンインストール、キャッシュされたツールのクリアなど、MCPサーバーを管理するための複数のオプションを提供します。

| 方法 | 説明 | |
|--------|-------------|---|
| **拡張機能ビュー** | **MCP SERVERS - INSTALLED**セクションでサーバーを右クリックするか、ギアアイコンを選択します。 | ![拡張機能ビューのMCPサーバーを示すスクリーンショット。](../images/mcp-servers/extensions-view-mcp-servers.png) |
| **`mcp.json`エディター** | 構成ファイルを開き、インラインアクション(コードレンズ)を使用します。**MCP: Open User Configuration**または**MCP: Open Workspace Folder Configuration**を使用してファイルを開きます。 | ![サーバーを管理するレンズを含むMCPサーバー構成。](../images/mcp-servers/mcp-server-config-lenses.png) |
| **コマンドパレット** | **MCP: List Servers**を実行してサーバーを選択し、アクションを選択します。 | ![コマンドパレットのMCPサーバーのアクションを示すスクリーンショット。](../images/mcp-servers/mcp-list-servers-actions.png) |

## VS CodeでMCPサーバーへのアクセスを一元管理する

組織はGitHubポリシーを通じてMCPサーバーへのアクセスを一元的に管理できます。[MCPサーバーのエンタープライズ管理](/docs/enterprise/ai-settings.md#configure-mcp-server-access)について詳細を学びます。

## MCPサーバーを自動的に起動する

MCPサーバーを追加するか、その構成を変更する場合、VS Codeはサーバーを(再)起動して、それが提供するツールを検出する必要があります。

`setting(chat.mcp.autoStart)`設定(実験的)を使用して、構成変更が検出されたときにVS CodeがMCPサーバーを自動的に再起動するように構成できます。

## MCPサーバーの信頼

ワークスペースにMCPサーバーを追加するか、その構成を変更する場合、サーバーを起動する前にサーバーとその機能を信頼することを確認する必要があります。VS Codeはサーバーを初めて起動するときにサーバーを信頼していることを確認するダイアログを表示します。ダイアログで、MCPサーバーへのリンクを選択して、その構成を確認してください。

![MCPサーバーの信頼プロンプトを示すスクリーンショット。](../images/mcp-servers/mcp-server-trust-dialog.png)

MCPサーバーを信頼しない場合、サーバーは起動されず、チャトリクエストはサーバーが提供するツールを使用せずに続行されます。

**MCP: Reset Trust**コマンドをコマンドパレットから実行してMCPサーバーの信頼をリセットできます。

> [!WARNING]
> `mcp.json`ファイルから直接MCPサーバーを起動する場合、サーバーの構成を信頼するよう求められません。

## デバイス間でMCP構成を同期する

[設定同期](/docs/configure/settings-sync.md)を有効にすると、MCPサーバー構成を含む設定と構成をデバイス間で同期できます。これにより、一貫した開発環境を維持し、すべてのデバイスで同じMCPサーバーにアクセスできます。

設定同期でMCPサーバー構成を同期するには:

1. コマンドパレットから**Settings Sync: Configure**コマンドを実行します

1. 同期構成のリストで**MCPサーバー**オプションを有効にします

## MCPサーバーのトラブルシューティングとデバッグ

### MCPの出力ログ

VS CodeがMCPサーバーで問題が発生すると、チャットビューではエラー指標が表示されます。

![MCPサーバーエラー](../images/mcp-servers/mcp-error-loading-tool.png)

チャットビューのエラー通知を選択してから、**出力を表示**オプションを選択してサーバーログを表示します。または、コマンドパレットから**MCP: List Servers**を実行して、サーバーを選択してから、**出力を表示**を選択します。

![MCPサーバーエラー出力](../images/mcp-servers/mcp-server-error-output.png)

## よくある質問

<details>
<summary>Dockerを使用している場合、MCPサーバーが開始されない</summary>

コマンド引数が正しいことと、コンテナーが切り離されたモード(`-d`オプション)で実行されていないことを確認してください。MCPサーバー出力でエラーメッセージを確認することもできます([トラブルシューティング](#troubleshoot-and-debug-mcp-servers)を参照)。

</details>

## 関連リソース

* [MCP構成リファレンス](/docs/copilot/reference/mcp-configuration.md)
* [エージェントでツールを使用する](/docs/copilot/agents/agent-tools.md)
* [Model Context Protocol Documentation](https://modelcontextprotocol.io/)
* [VS CodeのMCPアプリのサポート](https://code.visualstudio.com/blogs/2026/01/26/mcp-apps-support)
* [エージェントプラグインを検出および管理する](/docs/copilot/customization/agent-plugins.md)

