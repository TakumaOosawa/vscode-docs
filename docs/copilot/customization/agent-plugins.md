---
ContentId: f9b2c4e3-8a7d-4e1f-b5c3-2d9a6f8e4b71
DateApproved: 3/9/2026
MetaDescription: VS Code のエージェントプラグインを検出、インストール、管理して、事前パッケージ化されたコマンド、スキル、エージェント、フック、MCP サーバーで GitHub Copilot を拡張する方法について説明します。
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
# VS Code のエージェントプラグイン (プレビュー)

エージェントプラグインは、Visual Studio Code のプラグインマーケットプレイスから検出してインストールできるチャットカスタマイズのあらかじめパッケージ化されたバンドルです。単一のプラグインは、スラッシュコマンド、[エージェントスキル](/docs/copilot/customization/agent-skills.md)、[カスタムエージェント](/docs/copilot/customization/custom-agents.md)、[フック](/docs/copilot/customization/hooks.md)、[MCP サーバー](/docs/copilot/customization/mcp-servers.md)の任意の組み合わせを提供できます。

プラグインはローカルで定義されたカスタマイズと並行して機能します。プラグインをインストールすると、そのコマンド、スキル、エージェント、フック、MCP サーバーがチャットに表示されます。

> [!NOTE]
> エージェントプラグインは現在プレビュー中です。`setting(chat.plugins.enabled)`設定でエージェントプラグインのサポートを有効または無効にします。

## プラグインが提供するもの

エージェントプラグインは、次のカスタマイズタイプの1つ以上をバンドルできます。

* **スラッシュコマンド**: チャット内で`/`を使用して呼び出せる追加コマンド
* **スキル**: 指定、スクリプト、オンデマンド読み込みリソース付きの[エージェントスキル](/docs/copilot/customization/agent-skills.md)
* **エージェント**: 専門的なペルソナとツール構成を備えた[カスタムエージェント](/docs/copilot/customization/custom-agents.md)
* **フック**: エージェントライフサイクルポイントでシェルコマンドを実行する[フック](/docs/copilot/customization/hooks.md)
* **MCP サーバー**: 外部ツール統合用の[MCP サーバー](/docs/copilot/customization/mcp-servers.md)

例えば、テストプラグインは、スクリプト付きの`test-runner`スキル、読み取り専用ツール付きの`test-reviewer`エージェント、テストレポートダッシュボード用の MCP サーバーを含む場合があります。プラグインディレクトリ構造は次のようになります。

```text
my-testing-plugin/
    plugin.json              # プラグインメタデータと構成
    skills/
        test-runner/
            SKILL.md             # テストスキルの指定
            run-tests.sh         # サポートスクリプト
    agents/
        test-reviewer.agent.md # コードレビューエージェント
    hooks/
        post-test.json         # テスト後に実行するフック
```

インストール後、プラグイン提供のカスタマイズはローカルで定義されたカスタマイズと一緒に表示されます。例えば、プラグインのスキルは**スキルを構成**メニューに表示され、プラグインの MCP サーバーは MCP サーバーリストに表示されます。

> [!CAUTION]
> プラグインのマシン上でコードを実行するフックと MCP サーバーを含めることができます。インストール前に、特にコミュニティマーケットプレイスのプラグインについて、プラグインのコンテンツと公開元を確認してください。

## プラグインを検出してインストール

VS Code は、エージェントプラグインを参照および管理するための専用ビューを [拡張機能] サイドバーに提供します。

### 利用可能なプラグインを参照

1. [拡張機能] ビュー (`kb(workbench.view.extensions)`)を開き、検索フィールドに`@agentPlugins`と入力します。

        または、[拡張機能] サイドバーの**その他のアクション**(3つのドット)アイコンを選択し、**ビュー** > **エージェントプラグイン**を選択します。

1. 構成されたマーケットプレイスから利用可能なプラグインのリストを参照します。

        ![拡張機能サイドバーでエージェントプラグインを参照してするスクリーンショット。](../images/agent-plugins/extensions-view.png)

1. **インストール**を選択してユーザープロファイルにプラグインをインストールします。

### インストール済みプラグインを表示

[拡張機能] サイドバーの**エージェントプラグイン - インストール済み**ビューには、インストール済みのプラグインが表示されます。このビューから、プラグインを有効、無効、またはアンインストールできます。

![拡張機能サイドバーの [エージェントプラグイン - インストール済み] ビューのスクリーンショット。](../images/agent-plugins/installed-plugins.png)

[チャット] ビューから、**ギアアイコン** > **プラグイン**を選択して、インストール済みプラグインを管理することもできます。

## プラグインマーケットプレイスを構成

デフォルトでは、VS Code は[copilot-plugins](https://github.com/github/copilot-plugins)および[awesome-copilot](https://github.com/github/awesome-copilot/)からプラグインを検出します。`setting(chat.plugins.marketplaces)`設定で追加のマーケットプレイスを追加できます。

マーケットプレイスは、プラグイン定義を含む Git リポジトリです。いくつかの形式で参照できます。

* **短縮形**: 公開 GitHub リポジトリの`owner/repo`。例:`anthropics/claude-code`。
* **HTTPS git リモート**: `.git`で終わる完全な URL。例:`https://github.com/anthropics/claude-code.git`。
* **SCP スタイルの git リモート**: SSH スタイルの参照。例:`git@github.com:anthropics/claude-code.git`。
* **ファイル URI**: ディスク上に既にクローンされているマーケットプレイスリポジトリへの`file:///`パス。

プライベートリポジトリもサポートされています。公開検索に失敗した場合、VS Code はリポジトリを直接クローンします。

```json
// settings.json
"chat.plugins.marketplaces": [
        "anthropics/claude-code"
]
```

## ローカルプラグインを使用

プラグインを手動でクローンまたはダウンロードした場合は、`setting(chat.plugins.paths)`設定を使用して登録できます。この設定は、ローカルプラグインディレクトリパスを有効または無効状態にマップします。

```json
// settings.json
"chat.plugins.paths": {
        "/path/to/my-plugin": true,
        "/path/to/another-plugin": false
}
```

プラグインを有効にする場合は値を`true`に設定するか、登録したままにして無効にする場合は`false`に設定します。

## 関連リソース

* [GitHub Copilot CLI のプラグインを見つけてインストール](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing)
* [エージェントスキルを使用](/docs/copilot/customization/agent-skills.md)
* [MCP サーバーを追加および管理](/docs/copilot/customization/mcp-servers.md)
* [ライフサイクル自動化にフックを使用](/docs/copilot/customization/hooks.md)
* [カスタムエージェントを作成](/docs/copilot/customization/custom-agents.md)

