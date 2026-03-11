---
ContentId: f9b2c4e3-8a7d-4e1f-b5c3-2d9a6f8e4b71
DateApproved: 3/9/2026
MetaDescription: Visual Studio Codeでエージェントプラグインを発見、インストール、管理して、事前にパッケージ化されたコマンド、スキル、エージェント、フック、MCPサーバーでGitHub Copilotを拡張する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- copilot
- agents
- plugins
- marketplace
- customization
- ai
- skills
- hooks
- mcp
---
# VS Codeのエージェントプラグイン（プレビュー）

エージェントプラグインは、Visual Studio Codeのプラグインマーケットプレイスから発見およびインストールできるチャットカスタマイズの事前パッケージ化されたバンドルです。単一のプラグインは、スラッシュコマンド、[エージェントスキル](/docs/copilot/customization/agent-skills.md)、[カスタムエージェント](/docs/copilot/customization/custom-agents.md)、[フック](/docs/copilot/customization/hooks.md)、および[MCPサーバー](/docs/copilot/customization/mcp-servers.md)の任意の組み合わせを提供できます。

プラグインはローカルで定義されたカスタマイズとともに動作します。プラグインをインストールすると、そのコマンド、スキル、エージェント、フック、およびMCPサーバーがチャットに表示されます。

> [!NOTE]
> エージェントプラグインは現在プレビュー中です。`setting(chat.plugins.enabled)`設定でエージェントプラグイン機能を有効または無効にします。

## プラグインが提供する機能

エージェントプラグインは、以下のカスタマイズタイプの1つ以上をバンドルできます。

* **スラッシュコマンド**: チャットで`/`を使用して呼び出すことができる追加コマンド
* **スキル**: 指示、スクリプト、リソースをオンデマンドで読み込む[エージェントスキル](/docs/copilot/customization/agent-skills.md)
* **エージェント**: 特化したペルソナとツール構成を持つ[カスタムエージェント](/docs/copilot/customization/custom-agents.md)
* **フック**: エージェントのライフサイクルポイントでシェルコマンドを実行する[フック](/docs/copilot/customization/hooks.md)
* **MCPサーバー**: 外部ツール統合用の[MCPサーバー](/docs/copilot/customization/mcp-servers.md)

たとえば、テストプラグインには、スクリプト付きの`test-runner`スキル、読み取り専用ツール付きの`test-reviewer`エージェント、テストレポートダッシュボード用のMCPサーバーが含まれる場合があります。プラグインディレクトリ構造は次のようになります。

```text
my-testing-plugin/
    plugin.json              # Plugin metadata and configuration
    skills/
        test-runner/
            SKILL.md             # Testing skill instructions
            run-tests.sh         # Supporting script
    agents/
        test-reviewer.agent.md # Code review agent
    hooks/
        post-test.json         # Hook to run after tests
```

インストールすると、プラグイン提供カスタマイズがローカルで定義されたカスタマイズとともに表示されます。たとえば、プラグインからのスキルは**スキルの構成**メニューに表示され、プラグインからのMCPサーバーはMCPサーバーリストに表示されます。

> [!CAUTION]
> プラグインには、マシン上でコードを実行するフックとMCPサーバーが含まれる場合があります。特にコミュニティマーケットプレイスからのプラグインの場合は、インストール前にプラグイン内容と発行者を確認してください。

## プラグインを発見してインストール

VS Codeは、エージェントプラグインを参照および管理するための拡張機能サイドバーの専用ビューを提供します。

### 利用可能なプラグインの参照

1. 拡張機能ビュー（`kb(workbench.view.extensions)`）を開き、検索フィールドに`@agentPlugins`を入力します。

        または、拡張機能サイドバーの**その他のアクション**（3つの点）アイコンを選択して、**ビュー** > **エージェントプラグイン**を選択します。

1. 構成されたマーケットプレイスから利用可能なプラグインのリストを参照します。

        ![拡張機能サイドバーでエージェントプラグインを参照するスクリーンショット。](../images/agent-plugins/extensions-view.png)

1. **インストール**を選択してユーザープロファイルにプラグインをインストールします。

### インストール済みプラグインの表示

拡張機能サイドバーの**エージェントプラグイン - インストール済み**ビューは、インストール済みのプラグインを表示します。このビューから、プラグインを有効、無効、またはアンインストールできます。

![拡張機能サイドバーの「エージェントプラグイン - インストール済み」ビューのスクリーンショット。](../images/agent-plugins/installed-plugins.png)

チャットビューから**ギアアイコン** > **プラグイン**を選択して、インストール済みプラグインを管理することもできます。

## プラグインマーケットプレイスの構成

デフォルトでは、VS Codeは[copilot-plugins](https://github.com/github/copilot-plugins)および[awesome-copilot](https://github.com/github/awesome-copilot/)からプラグインを発見します。`setting(chat.plugins.marketplaces)`設定を使用して、追加のマーケットプレイスを追加できます。

マーケットプレイスはプラグイン定義を含むGitリポジトリです。これらはいくつかの形式で参照できます。

* **短縮形**: パブリックGitHubリポジトリの`owner/repo`。たとえば、`anthropics/claude-code`。
* **HTTPSgitリモート**: `.git`で終わる完全なURL。たとえば、`https://github.com/anthropics/claude-code.git`。
* **SCPスタイルのgitリモート**: SSHスタイルの参照。たとえば、`git@github.com:anthropics/claude-code.git`。
* **ファイルURI**: ディスク上にすでにクローンされているマーケットプレイスリポジトリへの`file:///`パス。

プライベートリポジトリもサポートされています。パブリック検索が失敗した場合、VS Codeはリポジトリを直接クローンするようにフォールバックします。

```json
// settings.json
"chat.plugins.marketplaces": [
        "anthropics/claude-code"
]
```

## ローカルプラグインの使用

プラグインを手動でクローンまたはダウンロードした場合、`setting(chat.plugins.paths)`設定で登録できます。この設定は、ローカルプラグインディレクトリパスを有効または無効状態にマップします。

```json
// settings.json
"chat.plugins.paths": {
        "/path/to/my-plugin": true,
        "/path/to/another-plugin": false
}
```

プラグインを有効にするには値を`true`に設定するか、登録したまま無効に保つには`false`に設定します。

## 関連リソース

* [GitHub Copilot CLIのプラグインの検索とインストール](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing)
* [エージェントスキルの使用](/docs/copilot/customization/agent-skills.md)
* [MCPサーバーの追加と管理](/docs/copilot/customization/mcp-servers.md)
* [ライフサイクル自動化用のフックの使用](/docs/copilot/customization/hooks.md)
* [カスタムエージェントの作成](/docs/copilot/customization/custom-agents.md)

