---
ContentId: 557a7e74-f77e-488d-90ea-fd2cfecfffda
DateApproved: 12/10/2025
MetaDescription: VS CodeでのGitHub Copilotチャットの開始。チャットへのアクセス方法や、自然言語を使用してコードを作成し、コードベースを理解し、問題を解決する方法について学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでチャットを始める

Visual Studio Codeのチャットを使用すると、自然言語を使用してAIによるコーディング支援を受けることができます。コードに関する質問、複雑なロジックの理解、新機能の生成、バグの修正など、すべて対話型インターフェイスを通じて行うことができます。

この記事では、VS Codeでさまざまなチャットエクスペリエンスにアクセスする方法、最初のプロンプトを送信する方法、より良い結果を得るための効果的なプロンプトを作成する方法、およびワークフローに合わせてチャットをカスタマイズする方法について説明します。

## VS Codeでチャットにアクセスする

VS Codeには、AIチャット会話を開始する3つの方法があり、それぞれ異なるワークフローやタスクに最適化されています。各チャットエクスペリエンスにアクセスするには、VS Codeタイトルバーのチャットメニューまたは対応するキーボードショートカットを使用します。

![VS CodeコマンドセンターのCopilot Chatメニューのスクリーンショット](images/copilot-chat/copilot-chat-menu-command-center.png)

<details>
<summary>チャットビュー</summary>

kb(workbench.action.chat.open)を押して、専用のサイドパネルでチャットビューを開きます。チャット用に大きなワークスペースが必要な場合は、チャットメニューから**新しいチャットエディター**を選択してエディタータブとして開くか、**新しいチャットウィンドウ**を選択して別のウィンドウとして開くことができます。

**チャットビューの用途:**

* 継続的なマルチターンチャット会話
* 質問をする、ファイル間でコード編集を行う、または自律的なコーディングワークフローを開始するために、異なる[エージェント](#switch-between-agents)を切り替える
* 複数のファイルにまたがる機能の作業
* 複雑な変更の計画と実装

![チャットビューのスクリーンショット](images/copilot-chat/chat-view.png)

</details>

<details>
<summary>インラインチャット</summary>

kb(inlineChat.start)を押して、エディターまたはターミナルで直接チャット会話を開始します。

**インラインチャットの用途:**

* 作業している場所で直接インライン提案を取得する
* 現在のコンテキストでコードを理解する
* ターミナルコマンドと出力に関するヘルプを取得する

![インラインチャットのスクリーンショット](images/copilot-chat/inline-chat.png)

</details>

<details>
<summary>クイックチャット</summary>

kb(workbench.action.quickchat.toggle)を押して、軽量のチャットオーバーレイを開きます。

**クイックチャットの用途:**

* 拡張会話を必要としない簡単な質問
* 現在のビューを変更せずに回答を取得する
* 作業に集中したまま情報を検索する

![クイックチャットのスクリーンショット](images/copilot-chat/quick-chat.png)

</details>

> [!TIP]
> `code chat`コマンドを使用して、コマンドラインから直接チャットを開始できます。詳細については、[VS Codeコマンドラインドキュメント](/docs/configure/command-line.md#start-chat-from-the-command-line)を参照してください。

## 最初のチャットプロンプトを送信する

VS Codeでチャットがどのように機能するかを確認するために、基本的な電卓アプリを作成してみましょう。

1. kb(workbench.action.chat.open)を押すか、VS Codeタイトルバーから**Chat**を選択してチャットビューを開きます。

1. エージェントピッカーから**Agent**を選択します。

    エージェントを使用すると、チャットは何を行う必要があるかを自律的に判断し、ワークスペースに必要な変更を加えます。

1. チャット入力フィールドに次のプロンプトを入力し、kb(workbench.action.chat.submit)を押して送信します。

    ```prompt
    HTML、CSS、JavaScriptを使用して基本的な電卓アプリを作成する
    ```

    エージェントは変更をワークスペースに直接適用し、依存関係のインストールやビルドスクリプトの実行などのためにターミナルコマンドを実行する場合もあります。

1. エディターで、[提案された変更を確認](/docs/copilot/chat/review-code-edits.md)し、保持するか破棄するかを選択します。

1. フォローアップの質問をしてアプリを強化します。たとえば、次のように質問できます。

    ```prompt
    ダークモードの切り替えを追加する
    ```

    または

    ```prompt
    モダンなデザインでスタイルを設定する
    ```

    会話を続けると、VS Codeはチャットプロンプトと応答の履歴をコンテキストとして使用します。このコンテキストにより、チャットとマルチターン会話を行い、結果を調整および改善できます。

> [!TIP]
> 音声入力を使用してVS Codeのチャットと対話します。詳細については、[チャットでの音声入力の使用](/docs/configure/accessibility/voice.md)を参照してください。

## さまざまな言語モデルを探索する

VS Codeには、さまざまなタスクに最適化された、選択可能な言語モデルが用意されています。高速なコーディングタスク用に設計されたモデルもあれば、複雑な推論や計画に優れたモデルもあります。

言語モデルを変更するには、チャット入力フィールドのモデルピッカーを使用して、ニーズに最も合ったモデルを選択します。

![利用可能なモデルのドロップダウンリストを示す、チャットビューの言語モデルピッカーのスクリーンショット](images/copilot-chat/chat-model-picker.png)

他のモデルプロバイダーからモデルを追加して、チャットで使用することもできます。[他のプロバイダーのモデルを使用する](/docs/copilot/customization/language-models.md)方法の詳細をご覧ください。

> [!NOTE]
> 利用可能なモデルのリストは、Copilotサブスクリプションによって異なる場合があり、時間の経過とともに変更される可能性があります。[利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)の詳細については、GitHub Copilotドキュメントを参照してください。

## エージェントを切り替える

エージェントを使用すると、チャットは特定のタスクに最適化された別の役割やペルソナを引き受けることができます。チャットセッション中にいつでもエージェントを切り替えることができます。

1. チャットビューを開きます(kb(workbench.action.chat.open))。

1. エージェントピッカーから目的のエージェントを選択します。

    ![異なるエージェントオプションを表示する、エージェントピッカーが展開されたチャットビューを示すスクリーンショット](../images/customization/chat-mode-dropdown.png)

### 組み込みエージェント

VS Codeには、**Agent**、**Plan**、**Ask**、**Edit**の4つの組み込みエージェントが用意されています。より専門的なワークフローのために、独自の[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成することもできます。

<details>
<summary>Agent</summary>

Agentは、ターミナルコマンドやツールの実行を必要とする可能性のある、高レベルの要件に基づく複雑なコーディングタスクに最適化されています。AIは自律的に動作し、関連するコンテキストと編集するファイルを決定し、必要な作業を計画し、問題が発生した場合は繰り返し解決します。

VS Codeはエディターに変更を直接適用し、エディターオーバーレイコントロールを使用して、提案された編集間を移動して確認できます。エージェントは、さまざまなタスクを実行するために複数の[ツール](/docs/copilot/chat/chat-tools.md)を呼び出す場合があります。

MCPサーバーを追加するか、ツールを提供する拡張機能をインストールすることで、[追加ツールを使用してチャットをカスタマイズ](/docs/copilot/chat/chat-tools.md)できます。

Agentでチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=agent) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=agent)

### エージェントを使い始める

> [!TIP]
> バックグラウンドエージェントやクラウドエージェントなど、さまざまなエージェントタイプの操作を示すハンズオンチュートリアルについては、[エージェントチュートリアル](/docs/copilot/agents/agents-tutorial.md)を参照してください。

ローカルエージェントセッションを開始するには:

1. チャットビューのエージェントピッカーから**Agent**を選択します。

1. チャット入力フィールドに高レベルのプロンプトを入力します。たとえば、次のように質問できます。

    ```prompt
    OAuth2とJWTを使用したユーザー認証システムを実装する
    ```

    または

    ```prompt
    このプロジェクトのCI/CDパイプラインをセットアップする
    ```

1. ツールピッカーを使用して[ツールを有効化](/docs/copilot/chat/chat-tools.md)し、エージェントに機能を追加します。

1. **送信**を選択するか、kb(workbench.action.chat.submit)を押してプロンプトを送信します。

1. エージェントがリクエストを処理する際に、コードの変更とツールの呼び出しを確認して承認します。

    > [!TIP]
    > VS Codeは、ワークスペース構成設定や環境設定などの機密ファイルへの不注意な編集を防ぐのに役立ちます。詳細については、[機密ファイルの編集](/docs/copilot/chat/review-code-edits.md#edit-sensitive-files)を参照してください。

</details>

<details>
<summary>Plan</summary>

Planエージェントは、コーディングタスクの構造化された実装計画を作成するために最適化されています。実装前に複雑な機能や変更を小さく管理しやすいステップに分解したい場合は、Planエージェントを使用します。

Planエージェントは、必要なステップの概要を説明する詳細な計画を生成し、タスクを包括的に理解するための確認質問をします。その後、その計画を実装エージェントに渡すか、ガイドとして使用できます。

Planでチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=plan) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=plan)

### Planエージェントを使い始める

1. チャット入力フィールドに高レベルのプロンプトを入力します。たとえば、次のように質問できます。

    ```prompt
    アプリケーションを更新して多言語ロカライズをサポートする
    ```

    または

    ```prompt
    検索機能をアプリケーションに追加する
    ```

1. チャットビューのエージェントピッカーから**Plan**を選択します。

1. **送信**を選択するか、kb(workbench.action.chat.submit)を押してプロンプトを送信します。

1. 必要に応じて確認質問に答えたり、計画を修正したりします。

1. **実装を開始(Start Implementation)**を選択して、計画を実装エージェントに渡します。

</details>

<details>
<summary>Ask</summary>

Askは、コードベース、コーディング、および一般的な技術概念に関する質問に答えるために最適化されています。何かがどのように機能するかを理解したい場合、アイデアを探求したい場合、またはコーディングタスクのヘルプが必要な場合は、Askを使用します。複数のファイルにまたがる大きな変更や、より複雑なコーディングタスクの場合は、エージェントの使用を検討してください。

応答には、コードベースに個別に適用できるコードブロックが含まれる場合があります。これは、単一ファイル内の小さな編集に適しています。コードブロックをコードベースに適用するには、コードブロックの上にカーソルを置き、**エディターに適用**ボタンを選択します。

Askでチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=ask) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=ask)

### Askを使い始める

1. チャット入力フィールドにプロンプトを入力します。たとえば、次のように質問できます。

    ```prompt
    Reactで検索機能を実装する3つの方法を提供する
    ```

    または

    ```prompt
    このプロジェクトのDB接続はどこで構成されていますか? #codebase
    ```

1. チャットビューのエージェントピッカーから**Ask**を選択します。

1. オプションで、[プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)して、より正確な応答を取得します。

1. **送信**を選択するか、kb(workbench.action.chat.submit)を押してプロンプトを送信します。

</details>

<details>
<summary>Edit</summary>

Editは、プロジェクト内の複数のファイルにまたがってコード編集を行うために最適化されています。Editは、行いたい変更と編集したいファイルについてよく理解している場合のコーディングタスクに役立ちます。

VS Codeはコードの変更をエディターに直接適用し、そこで確認できます。エディターオーバーレイコントロールを使用して、kbstyle(Up)およびkbstyle(Down)コントロールで編集間を移動し、変更を保持するか元に戻すことができます。

Editでチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=edit) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=edit)

### Editを使い始める

1. チャット入力フィールドにリクエストを入力します。たとえば、次のように質問できます。

    ```prompt
    OAuth2を使用するように認証ロジックをリファクタリングする
    ```

    または

    ```prompt
    ユーザーサービスの単体テストを追加する
    ```

1. チャットビューのエージェントピッカーから**Edit**を選択します。

1. [プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)して、AIが正しいファイルで編集を行うようにガイドします。

1. **送信**を選択するか、kb(workbench.action.chat.submit)を押してプロンプトを送信します。

1. オーバーレイコントロールを使用して、エディターでコードの変更を確認します。

</details>

## ワークフローに合わせてチャットをカスタマイズする

コンテキストを追加することで、チャットからより関連性の高い応答を得ることができます。特定のプロジェクトガイドラインや開発プラクティスに合わせてチャットをさらに調整するために、VS Codeでチャットをいくつかの方法でカスタマイズできます。

* [**カスタム指示**](/docs/copilot/customization/custom-instructions.md): コーディング標準、優先フレームワーク、アーキテクチャガイドラインなど、すべての会話でチャットの動作をガイドする永続的な指示を追加します。
* [**プロンプトファイル**](/docs/copilot/customization/prompt-files.md): `/`コマンドで呼び出すことができる再利用可能なプロンプトテンプレートを定義して、チーム全体で一般的なワークフローを標準化します。
* [**カスタムエージェント**](/docs/copilot/customization/custom-agents.md): コードレビュー、計画、ドキュメント作成など、特定の開発役割やタスクに合わせて調整された、さまざまなペルソナ用の特別なカスタムエージェントを作成します。
* [**MCPサーバー**](/docs/copilot/customization/mcp-servers.md): Model Context Protocolを介して外部ツールやサービスを統合することで、カスタム機能でチャットを拡張します。

## 効果的なプロンプトを作成する

チャットから最良の結果を得るために、プロンプトを作成するときは次のヒントに留意してください:

* **`#`-mentionsでコンテキストを追加する**: 特定のファイル(`#file`)、コードベース(`#codebase`)、またはターミナル出力(`#terminalSelection`)を参照します。チャット入力フィールドに`#`と入力すると、利用可能なすべてのコンテキスト項目が表示されます。[プロンプトへのコンテキストの追加](/docs/copilot/chat/copilot-chat-context.md)の詳細をご覧ください。

* **`/`コマンドを使用する**: `/`を入力して`/new`や`/explain`などの一般的なコマンドにアクセスするか、独自の[カスタムプロンプト](/docs/copilot/customization/prompt-files.md)を作成します。

* **ツールを参照する**: `#`の後にツール名を入力して、チャット機能を拡張します。たとえば、`#fetch`はWebコンテンツを取得し、`#githubRepo`はGitHubリポジトリを検索します。[チャットでのツールの追加と使用](/docs/copilot/chat/chat-tools.md)の詳細をご覧ください。

## 次のステップ

基本を理解したので、さらに多くのチャット機能を探索してください:

* [複数のチャットセッションを作成する](/docs/copilot/chat/chat-sessions.md)
* [プロンプトにコンテキストを追加して、より関連性の高い応答を取得する](/docs/copilot/chat/copilot-chat-context.md)
* [MCPサーバーまたは拡張機能のツールを使用してチャットの機能を拡張する](/docs/copilot/chat/chat-tools.md)

## 追加リソース

* コードベースの理解、コードの生成、デバッグ、ノートブックの操作など、一般的なタスクをカバーする[チャットプロンプトの例](/docs/copilot/chat/prompt-examples.md)からインスピレーションを得てください。

* [GitHub Copilot](https://github.com/features/copilot)と、VS Codeでの使用方法の詳細については、[GitHub Copilotドキュメント](https://docs.github.com/copilot/getting-started-with-github-copilot?tool=vscode)を参照してください。

* YouTubeの[VS Code Copilotシリーズ](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)をご覧ください。ここでは、Copilotを[Python](https://www.youtube.com/watch?v=DSHfHT5qnGc)、[C#](https://www.youtube.com/watch?v=VsUQlSyQn1E)、[Java](https://www.youtube.com/watch?v=zhCB95cE0HY)、[PowerShell](https://www.youtube.com/watch?v=EwtRzAFiXEM)、[C++](https://www.youtube.com/watch?v=ZfT2CXY5-Dc)などで使用するための入門コンテンツやプログラミング固有の動画を見つけることができます。
