---
ContentId: 557a7e74-f77e-488d-90ea-fd2cfecfffda
DateApproved: 01/08/2026
MetaDescription: VS Code で GitHub Copilot チャットを始めましょう。チャットにアクセスし、自然言語を使用してコードを作成し、コードベースを理解し、問題を解決する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Code でチャットを始める

Visual Studio Code のチャットでは、自然言語を使用して AI によるコーディング支援を受けることができます。コードに関する質問、複雑なロジックの理解、新機能の生成、バグの修正などを、すべて対話型インターフェイスを通じて行うことができます。

この記事では、VS Code でさまざまなチャットエクスペリエンスにアクセスする方法、最初のプロンプトを送信する方法、より良い結果を得るための効果的なプロンプトを作成する方法、およびワークフローに合わせてチャットをカスタマイズする方法について説明します。

## VS Code でチャットにアクセスする

VS Code には、AI チャット会話を開始する 3 つの方法があり、それぞれが異なるワークフローやタスクに最適化されています。各チャットエクスペリエンスにアクセスするには、VS Code タイトルバーのチャットメニューまたは対応するキーボードショートカットを使用します。

![VS Code コマンドセンターの Copilot Chat メニューのスクリーンショット](images/copilot-chat/copilot-chat-menu-command-center.png)

<details>
<summary>チャットビュー</summary>

`kb(workbench.action.chat.open)` を押して、専用のサイドパネルでチャットビューを開きます。チャット用により広いワークスペースが必要な場合は、チャットメニューから **[新しいチャットエディター]** を選択してエディタータブとして開くか、**[新しいチャットウィンドウ]** を選択して別ウィンドウとして開くことができます。

**チャットビューの用途:**

* 継続的なマルチターンチャット会話
* 異なる[エージェント](#switch-between-agents)を切り替えて質問したり、ファイル間でコード編集を行ったり、自律的なコーディングワークフローを開始したりする
* 複数のファイルにまたがる機能の作業
* 複雑な変更の計画と実装

![チャットビューのスクリーンショット](images/copilot-chat/chat-view.png)

</details>

<details>
<summary>インラインチャット</summary>

`kb(inlineChat.start)` を押して、エディターまたはターミナルで直接チャット会話を開始します。

**インラインチャットの用途:**

* 作業中の場所で直接インラインで提案を取得する
* 現在のコンテキストでコードを理解する
* ターミナルコマンドと出力に関するヘルプを取得する

![インラインチャットのスクリーンショット](images/copilot-chat/inline-chat.png)

</details>

<details>
<summary>クイックチャット</summary>

`kb(workbench.action.quickchat.toggle)` を押して、軽量のチャットオーバーレイを開きます。

**クイックチャットの用途:**

* 長い会話を必要としない簡単な質問
* 現在のビューを変更せずに回答を得る
* 作業に集中したまま情報を検索する

![クイックチャットのスクリーンショット](images/copilot-chat/quick-chat.png)

</details>

> [!TIP]
> `code chat` コマンドを使用して、コマンドラインから直接チャットを開始できます。詳細については、[VS Code コマンドラインドキュメント](/docs/configure/command-line.md#start-chat-from-the-command-line)を参照してください。

## 最初のチャットプロンプトを送信する

VS Code でのチャットの仕組みを確認するために、基本的な電卓アプリを作成することから始めましょう。

1. `kb(workbench.action.chat.open)` を押すか、VS Code タイトルバーから **[チャット]** を選択して、チャットビューを開きます。

1. エージェントピッカーから **Agent** を選択します。

    エージェントを使用すると、チャットは何を行う必要があるかを自律的に判断し、ワークスペースに必要な変更を加えます。

    > [!IMPORTANT]
    > エージェントオプションが表示されない場合は、VS Code 設定 (`setting(chat.agent.enabled)`) でエージェントが有効になっていることを確認してください。組織がエージェントを無効にしている可能性もあります。この機能を有効にするには、管理者に問い合わせてください。

1. チャット入力フィールドに次のプロンプトを入力し、`kb(workbench.action.chat.submit)` を押して送信します。

    ```prompt
    HTML、CSS、JavaScript で基本的な電卓アプリを作成してください
    ```

    エージェントは変更をワークスペースに直接適用します。また、依存関係をインストールしたりビルドスクリプトを実行したりするために、ターミナルコマンドを実行する場合もあります。

1. エディターで、[提案された変更を確認](/docs/copilot/chat/review-code-edits.md)し、保持するか破棄するかを選択します。

1. アプリを強化するためにフォローアップの質問をします。たとえば、次のように質問します。

    ```prompt
    ダークモードの切り替えを追加してください
    ```

    または

    ```prompt
    モダンなデザインでスタイルを設定してください
    ```

    会話を続けると、VS Code はチャットプロンプトと応答の履歴をコンテキストとして使用します。このコンテキストにより、チャットとマルチターン会話を行い、結果を調整および改善できます。

> [!TIP]
> VS Code でチャットと対話するには、音声入力を使用します。[チャットでの音声入力の使用](/docs/configure/accessibility/voice.md)について詳しくはこちらをご覧ください。

## さまざまな言語モデルを調べる

VS Code には、さまざまなタスクに最適化された、いくつかの言語モデルが用意されています。高速なコーディングタスク向けに設計されたモデルもあれば、複雑な推論や計画に優れたモデルもあります。

言語モデルを変更するには、チャット入力フィールドのモデルピッカーを使用して、ニーズに最適なモデルを選択します。

![チャットビューの言語モデルピッカーのスクリーンショット。利用可能なモデルのドロップダウンリストが表示されています。](images/copilot-chat/chat-model-picker.png)

他のモデルプロバイダーのモデルを追加して、チャットで使用することもできます。[他のプロバイダーのモデルを使用する方法](/docs/copilot/customization/language-models.md)について詳しくはこちらをご覧ください。

> [!NOTE]
> 利用可能なモデルのリストは、Copilot サブスクリプションによって異なる場合があり、時間の経過とともに変更される可能性があります。[利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)の詳細については、GitHub Copilot ドキュメントを参照してください。

## エージェントを切り替える

エージェントを使用すると、チャットは特定のタスクに最適化された別の役割やペルソナを引き受けることができます。チャットセッション中はいつでもエージェントを切り替えることができます。

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)。

1. エージェントピッカーから目的のエージェントを選択します。

    ![チャットビューのスクリーンショット。エージェントピッカーが展開され、さまざまなエージェントオプションが表示されています。](../images/customization/chat-mode-dropdown.png)

### 組み込みエージェント

VS Code には、**Agent**、**Plan**、**Ask**、**Edit** の 4 つの組み込みエージェントが用意されています。より専門的なワークフローのために、独自の[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を作成することもできます。

<details>
<summary>Agent</summary>

Agent は、ターミナルコマンドやツールの実行を必要とする可能性のある、高レベルの要件に基づく複雑なコーディングタスクに最適化されています。AI は自律的に動作し、関連するコンテキストと編集するファイルを決定し、必要な作業を計画し、発生する問題を解決するために反復します。

VS Code はコードの変更をエディターに直接適用し、エディターオーバーレイコントロールを使用して、提案された編集間を移動して確認することができます。Agent は、さまざまなタスクを実行するために複数の[ツール](/docs/copilot/chat/chat-tools.md)を呼び出す場合があります。

MCP サーバーを追加するか、ツールを提供する拡張機能をインストールすることで、[追加のツールを使用してチャットをカスタマイズ](/docs/copilot/chat/chat-tools.md)できます。

Agent でチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=agent) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=agent)

> [!IMPORTANT]
> エージェントオプションが表示されない場合は、VS Code 設定 (`setting(chat.agent.enabled)`) でエージェントが有効になっていることを確認してください。組織がエージェントを無効にしている可能性もあります。この機能を有効にするには、管理者に問い合わせてください。

### エージェントを始める

> [!TIP]
> バックグラウンドエージェントやクラウドエージェントなど、さまざまなタイプのエージェントの操作方法を示すハンズオンチュートリアルについては、[エージェントチュートリアル](/docs/copilot/agents/agents-tutorial.md)を参照してください。

ローカルエージェントセッションを開始するには:

1. チャットビューのエージェントピッカーから **Agent** を選択します。

1. チャット入力フィールドに高レベルのプロンプトを入力します。たとえば、次のように質問します。

    ```prompt
    OAuth2 と JWT を使用したユーザー認証システムを実装してください。
    ```

    または

    ```prompt
    このプロジェクトの CI/CD パイプラインをセットアップしてください。
    ```

1. ツールピッカーを使用して[ツールを有効にし](/docs/copilot/chat/chat-tools.md)、エージェントにより多くの機能を与えます。

1. **[送信]** を選択するか、`kb(workbench.action.chat.submit)` を押してプロンプトを送信します。

1. エージェントがリクエストを処理する際に、コードの変更とツールの呼び出しを確認して確定します。

    > [!TIP]
    > VS Code は、ワークスペース構成設定や環境設定などの機密ファイルへの意図しない編集を防ぐのに役立ちます。[機密ファイルの編集](/docs/copilot/chat/review-code-edits.md#edit-sensitive-files)について詳しくはこちらをご覧ください。

</details>

<details>
<summary>Plan</summary>

Plan エージェントは、コーディングタスクの構造化された実装計画を作成するのに最適化されています。複雑な機能や変更を、実装前に小さく管理しやすいステップに分割したい場合は、Plan エージェントを使用します。

Plan エージェントは、必要なステップの概要を示す詳細な計画を生成し、タスクを包括的に理解するために確認の質問をします。その後、計画を実装エージェントに引き渡すか、ガイドとして使用できます。

Plan でチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=plan) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=plan)

### Plan エージェントを始める

1. チャット入力フィールドに高レベルのプロンプトを入力します。たとえば、次のように質問します。

    ```prompt
    アプリケーションを多言語ローカライズに対応するように更新してください。
    ```

    または

    ```prompt
    アプリケーションに検索機能を追加してください。
    ```

1. チャットビューのエージェントピッカーから **Plan** を選択します。

1. **[送信]** を選択するか、`kb(workbench.action.chat.submit)` を押してプロンプトを送信します。

1. 確認の質問に答えたり、必要に応じて計画を修正したりします。

1. **[実装を開始]** を選択して、計画を実装エージェントに引き渡します。

</details>

<details>
<summary>Ask</summary>

Ask は、コードベース、コーディング、一般的なテクノロジーの概念に関する質問に答えるために最適化されています。何かがどのように機能するかを理解したい場合、アイデアを探求したい場合、またはコーディングタスクのサポートが必要な場合は、Ask を使用します。複数のファイルにまたがる大きな変更や、より複雑なコーディングタスクの場合は、エージェントの使用を検討してください。

応答には、コードベースに個別に適用するコードブロックが含まれる場合があります。これは、単一のファイル内の小さな編集に適しています。コードブロックをコードベースに適用するには、コードブロックの上にマウスを置き、**[エディターに適用]** ボタンを選択します。

Ask でチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=ask) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=ask)

### Ask を始める

1. チャット入力フィールドにプロンプトを入力します。たとえば、次のように質問します。

    ```prompt
    React で検索機能を実装する 3 つの方法を教えてください。
    ```

    または

    ```prompt
    このプロジェクトで DB 接続はどこに設定されていますか？ #codebase
    ```

1. チャットビューのエージェントピッカーから **Ask** を選択します。

1. オプションで、[プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)して、より正確な応答を得ることができます。

1. **[送信]** を選択するか、`kb(workbench.action.chat.submit)` を押してプロンプトを送信します。

</details>

<details>
<summary>Edit</summary>

Edit は、プロジェクト内の複数のファイルにわたってコード編集を行うために最適化されています。Edit は、行いたい変更と編集したいファイルをよく理解している場合のコーディングタスクに役立ちます。

VS Code はコードの変更をエディターに直接適用し、そこで確認することができます。エディターオーバーレイコントロールを使用して、`kbstyle(Up)` および `kbstyle(Down)` コントロールで編集間を移動し、変更を保持するか元に戻すかを選択します。

Edit でチャットを開く: [Stable](vscode://GitHub.Copilot-Chat/chat?mode=edit) | [Insiders](vscode-insiders://GitHub.Copilot-Chat/chat?mode=edit)

### Edit を始める

1. チャット入力フィールドにリクエストを入力します。たとえば、次のように質問します。

    ```prompt
    OAuth2 を使用するように認証ロジックをリファクタリングしてください。
    ```

    または

    ```prompt
    ユーザーサービスの単体テストを追加してください。
    ```

1. チャットビューのエージェントピッカーから **Edit** を選択します。

1. AI が適切なファイルで編集を行うようにガイドするために、[プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)します。

1. **[送信]** を選択するか、`kb(workbench.action.chat.submit)` を押してプロンプトを送信します。

1. オーバーレイコントロールを使用して、エディターでコードの変更を確認します。

</details>

## ワークフローに合わせてチャットをカスタマイズする

コンテキストを追加することで、チャットからより関連性の高い応答を得ることができます。プロジェクトのガイドラインや開発手法に合わせてチャットをさらに調整するために、VS Code でチャットをいくつかの方法でカスタマイズできます。

* [**カスタム指示**](/docs/copilot/customization/custom-instructions.md): コーディング規約、推奨フレームワーク、アーキテクチャガイドラインなど、すべての会話でチャットの動作をガイドする永続的な指示を追加します。
* [**プロンプトファイル**](/docs/copilot/customization/prompt-files.md): `/` コマンドで呼び出すことができる再利用可能なプロンプトテンプレートを定義して、チーム全体で共通のワークフローを標準化します。
* [**カスタムエージェント**](/docs/copilot/customization/custom-agents.md): コードレビュー、計画、ドキュメント作成など、特定の開発ロールやタスクに合わせたさまざまなペルソナ用の専門的なカスタムエージェントを作成します。
* [**MCP サーバー**](/docs/copilot/customization/mcp-servers.md): Model Context Protocol を介して外部ツールやサービスを統合することで、カスタム機能でチャットを拡張します。

## 効果的なプロンプトを作成する

チャットから最良の結果を得るために、プロンプトを作成する際は次のヒントを念頭に置いてください。

* **# メンションでコンテキストを追加する**: 特定のファイル (`#file`)、コードベース (`#codebase`)、またはターミナル出力 (`#terminalSelection`) を参照します。チャット入力フィールドに `#` を入力すると、利用可能なすべてのコンテキストアイテムが表示されます。詳細については、[プロンプトへのコンテキストの追加](/docs/copilot/chat/copilot-chat-context.md)を参照してください。

* **「/」コマンドを使用する**: `/` を入力して、`/new` や `/explain` などの一般的なコマンドにアクセスするか、独自の[カスタムプロンプト](/docs/copilot/customization/prompt-files.md)を作成します。

* **ツールを参照する**: `#` に続けてツール名を入力し、チャット機能を拡張します。たとえば、`#fetch` は Web コンテンツを取得し、`#githubRepo` は GitHub リポジトリを検索します。[チャットでのツールの追加と使用](/docs/copilot/chat/chat-tools.md)について詳しくはこちらをご覧ください。

## 次のステップ

基本を理解したので、さらに多くのチャット機能を試してみましょう。

* [複数のチャットセッションを作成する](/docs/copilot/chat/chat-sessions.md)
* [プロンプトにコンテキストを追加して、より関連性の高い応答を得る](/docs/copilot/chat/copilot-chat-context.md)
* [MCP サーバーまたは拡張機能のツールを使用してチャットの機能を拡張する](/docs/copilot/chat/chat-tools.md)

## 追加リソース

* コードベースの理解、コードの生成、デバッグ、ノートブックの操作など、一般的なタスクをカバーする[チャットプロンプトの例](/docs/copilot/chat/prompt-examples.md)からインスピレーションを得てください。

* [GitHub Copilot](https://github.com/features/copilot) の詳細と VS Code での使用方法については、[GitHub Copilot ドキュメント](https://docs.github.com/copilot/getting-started-with-github-copilot?tool=vscode)を参照してください。

* YouTube の [VS Code Copilot シリーズ](https://www.youtube.com/playlist?list=PLj6YeMhvp2S5_hvBl2SE-7YCHYlLQ0bPt)をご覧ください。ここでは、Copilot を [Python](https://www.youtube.com/watch?v=DSHfHT5qnGc)、[C#](https://www.youtube.com/watch?v=VsUQlSyQn1E)、[Java](https://www.youtube.com/watch?v=zhCB95cE0HY)、[PowerShell](https://www.youtube.com/watch?v=EwtRzAFiXEM)、[C++](https://www.youtube.com/watch?v=ZfT2CXY5-Dc) などで使用するための入門コンテンツやプログラミング固有のビデオを見つけることができます。
