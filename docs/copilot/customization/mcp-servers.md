---
ContentId: 7c550054-4ade-4665-b368-215798c48673
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeのGitHub Copilotを使用してModel Context Protocol（MCP）サーバーを追加および管理する方法について説明します。
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

[Model Context Protocol（MCP）](https://modelcontextprotocol.io/)は、AIモデルを外部ツールやサービスに接続するためのオープン標準です。Visual Studio Codeでは、MCPサーバーはファイル操作、データベース、外部APIなどのタスク用の[ツール](/docs/copilot/agents/agent-tools.md)を提供します。MCPサーバーは[リソース、プロンプト、インタラクティブアプリ](#その他のmcp機能)も提供できます。

MCPがAIカスタマイズフレームワークにどう適合するかについては、[カスタマイズの概念](/docs/copilot/concepts/customization.md#mcp)および[ツールの概念](/docs/copilot/concepts/tools.md)を参照してください。

この記事では、MCPサーバーの追加、設定、管理方法について説明します。チャットでのツールの使用方法については、[エージェントでツールを使用する](/docs/copilot/agents/agent-tools.md)を参照してください。

> [!TIP]
> [チャットカスタマイズエディター](/docs/copilot/customization/overview.md#chat-customizations-editor)（プレビュー）を使用して、すべてのチャットカスタマイズを1つの場所で検索、作成、管理できます。コマンドパレットから**Chat: Open Chat Customizations**を実行します。

## クイックスタート：チャットでMCPサーバーを使用する

次の手順に従って、MCPサーバーをインストールし、そのツールをチャットで使用します。この例では、[Playwright](https://github.com/microsoft/playwright-mcp)MCPサーバーを使用してブラウザーでWebページと対話します。

1. 拡張機能ビュー（`kb(workbench.view.extensions)`）を開き、検索フィールドに`@mcp playwright`と入力します。

1. **インストール**を選択して、Playwright MCPサーバーをユーザープロファイルにインストールします。

1. プロンプトが表示されたら、サーバーを信頼して開始することを確認します。VS Codeはサーバーのツールを検出し、チャットで利用可能にします。

1. チャットビュー（`kb(workbench.action.chat.open)`）を開き、Playwrightツールを使用するプロンプトを入力します。例えば：

    ```prompt
    code.visualstudio.comにアクセスして、クッキーバナーを拒否し、ホームページのスクリーンショットをください。
    ```

    VS CodeはPlaywrightツールを呼び出してブラウザーでページを開き、スクリーンショットを取得します。各ツール呼び出しを確認するよう求められる場合があります。

> [!TIP]
> チャット入力の**ツールを設定**ボタンを選択すると、Playwright MCPサーバーの利用可能なすべてのツールが表示され、特定のツールのオン/オフを切り替えられます。

## MCPサーバーを追加する

MCPサーバーギャラリーからMCPサーバーをインストールするには：

1. 拡張機能ビュー（`kb(workbench.view.extensions)`）を開き、検索フィールドに`@mcp`と入力します。ギャラリーの利用可能なMCPサーバーのリストが表示されます。

1. MCPサーバーをユーザープロファイルまたはワークスペースにインストールできます：

    * ユーザープロファイルにインストールするには、**インストール**を選択します。

    * ワークスペースにインストールするには、MCPサーバーを右クリックして**ワークスペースにインストール**を選択します。これにより、ワークスペースの`.vscode/mcp.json`ファイルが更新されます。

1. MCPサーバーの詳細を表示するには、リストのMCPサーバーを選択して詳細ページを開きます。

> [!CAUTION]
> ローカルMCPサーバーはマシン上で任意のコードを実行できます。[信頼できるソース](#mcpサーバーの信頼)からのみサーバーを追加し、開始する前に発行者とサーバー設定を確認してください。VS CodeでAIを使用するための[セキュリティドキュメント](/docs/copilot/security.md)を読んで、その含意をご理解ください。

### `mcp.json`ファイルを設定する

`mcp.json`ファイルを編集してMCPサーバーを手動で設定できます。このファイルには2つの場所があります：

* **ワークスペース**：プロジェクトで`.vscode/mcp.json`を作成または開きます。このファイルをソース管理に含めて、MCPサーバー設定をチームと共有します。
* **ユーザープロファイル**：**MCP: Open User Configuration**コマンドを実行して、[ユーザープロファイル](/docs/configure/profiles.md)フォルダーの`mcp.json`ファイルを開きます。ここで設定されたサーバーはすべてのワークスペースで利用可能です。複数のプロファイルを使用する場合、各プロファイルに独自のMCPサーバー設定を設定できます。

コマンドパレット（`kb(workbench.action.showCommands)`）から**MCP: Add Server**を実行して、ガイド付きフローでサーバーを追加することもできます。その際に**Workspace**または**Global**をターゲットとして選択できます。

> [!IMPORTANT]
> APIキーなどの機密情報をハードコーディングしないでください。代わりに[入力変数](/docs/copilot/reference/mcp-configuration.md#入力変数機密データ)または環境ファイルを使用してください。

次の例は、リモートMCPサーバーとローカルMCPサーバーを設定する`mcp.json`ファイルを示しています：

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

VS Codeは設定ファイル用のIntelliSenseを提供しています。完全な設定スキーマとフィールドリファレンスについては、[MCP設定リファレンス](/docs/copilot/reference/mcp-configuration.md)を参照してください。

> [!NOTE]
> MCPサーバーはそれらが設定されている場所で実行されます。ユーザープロファイルのサーバーはローカルで実行されます。[リモート](/docs/remote/remote-overview.md)に接続していて、サーバーをリモートマシンで実行したい場合は、ワークスペース設定またはリモートユーザー設定（**MCP: Open Remote User Configuration**）で定義してください。

### MCPサーバーを追加するその他のオプション

<details>
<summary>開発コンテナーにMCPサーバーを追加する</summary>

MCPサーバーは`devcontainer.json`ファイルを通じてDev Containersで設定できます。これにより、MCPサーバー設定をコンテナ化された開発環境の一部として含めることができます。

Dev ContainerでMCPサーバーを設定するには、`customizations.vscode.mcp`セクションにサーバー設定を追加します：

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

開発コンテナーが作成されると、VS CodeはMCPサーバー設定をリモート`mcp.json`ファイルに自動的に書き込み、コンテナ化された開発環境で利用可能にします。

</details>

<details>
<summary>MCPサーバーを自動的に検出する</summary>

VS CodeはClaude Desktopなどの他のアプリケーションからMCPサーバー設定を自動的に検出および再利用できます。

`setting(chat.mcp.discovery.enabled)`設定を使用して、MCP サーバー設定を検出対象とする1つ以上のツールを選択できます。

</details>

<details>
<summary>コマンドラインからMCPサーバーをインストールする</summary>

VS Codeコマンドラインインターフェースを使用して、MCPサーバーをユーザープロファイルまたはワークスペースに追加することもできます。

ユーザープロファイルにMCPサーバーを追加するには、`--add-mcp`VS Codeコマンドラインオプションを使用し、JSONサーバー設定を`{\"name\":\"server-name\",\"command\":...}`の形式で指定します。

```bash
code --add-mcp "{\"name\":\"my-server\",\"command\": \"uvx\",\"args\": [\"mcp-server-fetch\"]}"
```

</details>

## その他のMCP機能

ツール以外に、MCPサーバーは以下の機能を提供できます：

| 機能 | 説明 | 使用方法 |
|------------|-------------|------------|
| **リソース** | ファイル、データベーステーブル、APIレスポンスなど、MCPサーバーのデータをプロンプトのコンテキストとしてアクセスします。リソースはチャットリクエストに接続する読み取り専用コンテキストを提供します。 | チャットビューで**コンテキストを追加**>**MCPリソース**を選択します。**MCP: Browse Resources**コマンドを使用することもできます。 |
| **プロンプト** | MCPサーバーの事前設定されたプロンプトテンプレートを使用して、一般的なタスクを標準化します。各MCPサーバーはその機能に応じた独自のプロンプトセットを公開できます。 | チャット入力に`/<MCPサーバー>.<プロンプト>`と入力します。 |
| **MCPアプリ** | フォーム、ビジュアライゼーション、ドラッグアンドドロップリストなどのインタラクティブUIコンポーネントをディスプリイ上に直接レンダリング取得します。MCPアプリはテキストレスポンス以上のリッチなインタラクションを実現します。詳細は[MCP Appsブログ記事](https://code.visualstudio.com/blogs/2026/01/26/mcp-apps-support)を参照してください。 | MCPサーバーがサポートしている場合、MCPアプリはインラインで表示されます。 |

## MCPサーバーのサンドボックス化

macOSおよびLinuxでは、ローカルで実行されているstdio MCPサーバーのサンドボックス化を有効にして、ファイルシステムとネットワークへのアクセスを制限できます。サンドボックス化されたサーバーは分離環境で実行され、明示的に許可したファイルパスとネットワークドメインのみにアクセスできます。

サーバーのサンドボックス化を有効にするには、`mcp.json`ファイルのサーバー設定で`"sandboxEnabled": true`に設定します。`sandbox`オブジェクトを追加して特定のファイルシステムおよびネットワークルールをカスタマイズできます。

次の例は、ローカルMCPサーバーのサンドボックス化を有効にし、ワークスペースのファイルへの書き込みと特定のAPIドメインへのアクセスのみに制限する方法を示しています：

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

サンドボックス化が有効な場合、サーバーからのツール呼び出しは制御環境で実行されるため、自動承認されます。

完全なサンドボックス設定スキーマについては、[サンドボックス設定](/docs/copilot/reference/mcp-configuration.md#サンドボックス設定)リファレンスを参照してください。

> [!NOTE]
> サンドボックス化は現在Windowsでは利用できません。

## MCPサーバーを管理する

VS Codeはサーバーの開始/停止、ログの表示、アンインストール、キャッシュされたツールのクリアなど、MCPサーバーを管理するするための複数のオプションを提供します。

| 方法 | 説明 | |
|--------|-------------|---|
| **拡張機能ビュー** | **MCPサーバー - インストール済み**セクションのサーバーを右クリックするか、歯車アイコンを選択します。 | ![拡張機能ビューのMCPサーバーを示すスクリーンショット。](../images/mcp-servers/extensions-view-mcp-servers.png) |
| **`mcp.json`エディター** | 設定ファイルを開きインラインアクション（コードレンズ）を使用します。**MCP: Open User Configuration**または**MCP: Open Workspace Folder Configuration**を使用してファイルを開きます。 | ![サーバーを管理するレンズを含むMCPサーバー設定。](../images/mcp-servers/mcp-server-config-lenses.png) |
| **コマンドパレット** | **MCP: List Servers**を実行してサーバーを選択し、アクションを選択します。 | ![コマンドパレットのMCPサーバーアクションを示すスクリーンショット。](../images/mcp-servers/mcp-list-servers-actions.png) |

## VS CodeでMCPサーバーへのアクセスを集中管理する

組織はGitHubポリシーを使用してMCPサーバーへのアクセスを集中管理できます。詳細は[MCPサーバーのエンタープライズ管理](/docs/enterprise/ai-settings.md#mcpサーバーアクセスを設定する)を参照してください。

## MCPサーバーを自動的に開始する

MCPサーバーを追加するか設定を変更する場合、VS Codeはサーバーを（再）起動して提供するツールを検出する必要があります。

`setting(chat.mcp.autoStart)`設定（実験的機能）を使用して、設定変更が検出されたときにMCPサーバーを自動的に再起動するようVS Codeを設定できます。

## MCPサーバーの信頼

MCPサーバーをワークスペースに追加するか設定を変更する場合、サーバーを開始する前にサーバーとその機能を信頼することを確認する必要があります。VS Codeはサーバーを初回起動するときに、サーバーを信頼することを確認するダイアログを表示します。ダイアログのMCPサーバーへのリンクを選択して、設定を確認します。

![MCPサーバー信頼プロンプトを示すスクリーンショット。](../images/mcp-servers/mcp-server-trust-dialog.png)

MCPサーバーを信頼しない場合は、サーバーが起動せず、チャットリクエストはサーバーが提供するツールを使用せずに続行されます。

MCPサーバーの信頼をリセットするには、コマンドパレットから**MCP: Reset Trust**コマンドを実行します。

> [!WARNING]
> `mcp.json`ファイルからMCPサーバーを直接開始する場合、サーバー設定を信頼することを求めるプロンプトが表示されません。

## デバイス間でMCP設定を同期する

[設定同期](/docs/configure/settings-sync.md)が有効になっている場合、MCPサーバー設定を含む設定と設定をデバイス間で同期できます。これにより、一貫性のある開発環境を維持し、すべてのデバイスで同じMCPサーバーにアクセスできます。

設定同期でMCPサーバー設定を同期するには：

1. コマンドパレットから**Settings Sync: Configure**コマンドを実行します

1. 同期設定リストの**MCPサーバー**オプションを有効にします

## MCPサーバーのトラブルシューティングとデバッグ

### MCP出力ログ

VS CodeがMCPサーバーの問題に遭遇すると、チャットビューにエラーインジケーターが表示されます。

![MCPサーバーエラー](../images/mcp-servers/mcp-error-loading-tool.png)

チャットビューのエラー通知を選択してから、**出力を表示**オプションを選択することでサーバーログを表示します。または、コマンドパレットから**MCP: List Servers**を実行してサーバーを選択してから、**出力を表示**を選択します。

![MCPサーバーエラー出力](../images/mcp-servers/mcp-server-error-output.png)

## よくある質問

<details>
<summary>Dockerを使用する際、MCPサーバーが起動しません</summary>

コマンド引数が正しく、コンテナーが分離モード（`-d`オプション）で実行されていないことを確認してください。MCPサーバー出力でエラーメッセージを確認することもできます（[トラブルシューティング](#mcpサーバーのトラブルシューティングとデバッグ)を参照）。

</details>

## 関連リソース

* [MCP設定リファレンス](/docs/copilot/reference/mcp-configuration.md)
* [エージェントでツールを使用する](/docs/copilot/agents/agent-tools.md)
* [Model Context Protocolドキュメント](https://modelcontextprotocol.io/)
* [VS CodeのMCPアプリサポート](https://code.visualstudio.com/blogs/2026/01/26/mcp-apps-support)
* [エージェントプラグインを検出および管理する](/docs/copilot/customization/agent-plugins.md)

