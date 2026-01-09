---
ContentId: 5d8a707d-a239-4cc7-92ee-ccc763e8eb9c
DateApproved: 12/10/2025
MetaDescription: "VS CodeでAIを使用する際のコンテキスト管理（ワークスペースのインデックス作成、ファイルやシンボルの#メンション、Webコンテンツの参照、カスタム指示など）について説明します。"
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# AIのコンテキスト管理

適切なコンテキストを提供することで、VS CodeのAIからより適切で正確な回答を得ることができます。この記事では、ファイル、フォルダー、シンボルを参照するための#メンションの使用方法、Webコンテンツの参照方法、AIの回答をガイドするためのカスタム指示の使用方法など、チャットでコンテキストを管理する方法について説明します。

## ワークスペースのインデックス作成

VS Codeはインデックスを使用して、関連するコードスニペットをコードベースから迅速かつ正確に検索します。このインデックスは、GitHubによって管理されるか、ローカルマシンに保存されます。

以下のワークスペースインデックスオプションが利用可能です:

* **リモートインデックス**: コードがGitHubリポジトリでホストされている場合、リモートインデックスを構築してコードベースをすばやく検索できます（大規模なコードベースでも同様）。
* **ローカルインデックス**: ローカルマシンに保存された高度なセマンティックインデックスを使用して、コードベースに対して高速かつ正確な検索結果を提供します。
* **基本インデックス**: ローカルインデックスが利用できない場合、より大きなコードベースに対してローカルで動作するように最適化された、よりシンプルなアルゴリズムを使用できます。

[ワークスペースのインデックス作成](/docs/copilot/reference/workspace-context.md)の詳細をご覧ください。

## 暗黙的なコンテキスト

VS Codeは、現在のアクティビティに基づいてチャットプロンプトにコンテキストを自動的に提供します。以下の情報は暗黙的にチャットコンテキストに含まれます:

* アクティブエディターで現在選択されているテキスト。
* アクティブエディターのファイル名またはノートブック名。
* AskまたはEditを使用している場合、アクティブなファイルは自動的にコンテキストとして含まれます。
* エージェントを使用する場合、エージェントはプロンプトに基づいてアクティブなファイルをチャットコンテキストに追加する必要があるかどうかを自律的に判断します。

![チャット入力ボックスに提案されたコンテキスト項目としてアクティブファイルが表示されているチャットビューのスクリーンショット。](./images/copilot-chat/chat-context-current-file.png)

## #-メンション

`#`に続けて言及したいコンテキスト項目を入力することで、プロンプトにコンテキストを明示的に追加できます。VS Codeは、ファイル、フォルダー、コードシンボル、ツール、ターミナル出力、ソース管理の変更など、さまざまな種類のコンテキスト項目をサポートしています。

チャット入力フィールドに`#`記号を入力して利用可能なコンテキスト項目のリストを表示するか、チャットビューで**Add Context**を選択してコンテキストピッカーを開きます。

![チャット変数ピッカーが表示されているVS Codeチャットビューのスクリーンショット。](./images/copilot-chat/copilot-chat-view-chat-variables.png)

[サポートされているコンテキスト項目](/docs/copilot/reference/copilot-vscode-features.md#chat-tools)の完全なリストを表示します。

### ファイルをコンテキストとして追加

特定のファイル、フォルダー、またはシンボルをコンテキストとして提供するには、次の方法を使用してチャットに追加します:

* チャットメッセージで、`#`に続けてファイル、フォルダー、またはシンボルの名前を入力して#-メンションします。
    シンボルを参照するには、まずエディターでそのシンボルを含むファイルを開いていることを確認してください。

* エクスプローラービュー、検索ビュー、またはエディタータブからファイルまたはフォルダーをチャットビューにドラッグアンドドロップして、コンテキストとして追加します。

* チャットビューで**Add Context**を選択し、クイックピックから**Files & Folders**または**Symbols**を選択します。

> [!NOTE]
> ファイルを添付する場合、可能であればファイルの全内容が含まれます。コンテキストウィンドウに収まらないほど大きい場合は、実装を含まない関数とその説明を含むファイルの概要が含まれます。概要も大きすぎる場合、そのファイルはプロンプトの一部にはなりません。

### コードベース検索の実行

個々のファイルを手動で追加する代わりに、VS Codeにコードベースから適切なファイルを自動的に見つけさせることができます。これは、どのファイルが質問に関連しているかわからない場合に便利です。

プロンプトに`#codebase`を追加するか、**Add Context** > **Tools** > **codebase**を選択して、ワークスペースのコード検索を有効にします。

以下のプロンプトの例は、コードベース検索の使用方法を示しています:

* `"Explain how authentication works in #codebase"`
* `"Where is the database connecting string configured? #codebase"`
* `"Add a new API route for updating the address #codebase"`

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、エージェントは質問に答えるために追加のコンテキストが必要であると判断すると、自動的にコードベース検索を使用します。質問がさまざまな方法で解釈される可能性があり、エージェントがコードベース検索を使用するようにしたい場合は、`#codebase`を追加することもできます。

### Webコンテンツの参照

最新のAPIリファレンスやコード例を取得するなど、チャットプロンプトでWebのコンテンツを参照できます。

* `#fetch <URL>`

    `fetch`ツールを使用して、特定のWebページからコンテンツを取得します。このツールを使用するには、`#fetch`に続けて参照したいページのURLを入力します。

    `fetch`ツールは、パフォーマンスを向上させるためにWebページのコンテンツを期間限定でキャッシュします。ページのコンテンツが変更された場合は、VS Codeを再起動して更新を強制できます。ページに到達できない場合、キャッシュは短時間（約5分）で期限切れになります。

    VS Codeは、プライバシーとセキュリティを保護するために、外部URLにアクセスする前に確認を求めます。[URL自動承認の構成](/docs/copilot/chat/chat-tools.md#url-approval)の詳細をご覧ください。

    `fetch`ツールを使用したプロンプトの例:

    * `"What are the highlights of VS Code 1.100 #fetch https://code.visualstudio.com/updates/v1_100"`
    * `"Update the asp.net app to .net 9 #fetch https://learn.microsoft.com/en-us/aspnet/core/migration/80-90"`

* `#githubRepo <repo name>`

    `githubRepo`ツールを使用して、GitHubリポジトリ内でコード検索を実行します。`#githubRepo`に続けてリポジトリ名を入力します。

    `githubRepo`ツールを使用したプロンプトの例:

    * `"How does routing work in next.js #githubRepo vercel/next.js"`
    * `"Perform a code review to validate it's consistent with #githubRepo microsoft/typescript"`

### ツールの参照

エージェントを使用する場合、エージェントは特定のタスクを実行するためにツールを使用するかどうかを自律的に決定します。チャットプロンプトでツールを明示的に参照したい場合は、#-メンションを使用できます。`#`に続けてツール名とオプションのパラメーターを入力します:

* `"Summarize #fetch https://code.visualstudio.com/updates"`
* `"How does routing work? #githubRepo vercel/next.js"`
* `"what are my open issues #github-mcp"` (GitHub MCPサーバーのツールを使用)

ツールセットまたはMCPサーバーを名前で参照する場合、そのセットまたはサーバーのすべてのツールが、現在のプロンプトに対してエージェントで使用可能になります。

[チャットでのツールの追加と使用](/docs/copilot/chat/chat-tools.md)の詳細をご覧ください。

## @-メンション

チャット参加者は、チャットでドメイン固有の質問をすることができる専門のアシスタントです。チャット参加者を、チャットリクエストを渡すと残りの処理を行ってくれるドメインエキスパートと想像してください。

チャット参加者は、特定のタスクに貢献し実行するためのエージェントフローの一部として呼び出される[ツール](#reference-tools)とは異なります。

チャット参加者を呼び出すには、@-メンションを使用します: `@`に続けて参加者名を入力します。VS Codeには、`@vscode`、`@terminal`、`@workspace`などの組み込みのチャット参加者がいくつかあります。これらはそれぞれのドメインに関する質問に答えるように最適化されています。

以下の例は、チャットプロンプトで@-メンションを使用する方法を示しています:

* `"@vscode how to enable word wrapping"`
* `"@terminal what are the top 5 largest files in the current directory"`

チャット入力フィールドに`@`を入力して利用可能なチャット参加者のリストを表示します。

拡張機能は独自の[チャット参加者](/api/extension-guides/ai/chat.md)を提供することもできます。

## ビジョン

チャットはビジョン機能をサポートしており、画像をコンテキストとしてチャットプロンプトに添付し、それについて質問することができます。たとえば、コードブロックのスクリーンショットを添付して説明を求めたり、UIのスケッチを添付してエージェントに実装を依頼したりできます。

> [!TIP]
> Webブラウザーから画像をチャットビューにドラッグアンドドロップしてコンテキストとして追加できます。

## ブラウザー要素の追加 (Experimental)

VS Codeには、Webアプリケーションの迅速なテストやデバッグなどを行うために、VS Code内でWebページをプレビューおよび操作できる組み込みブラウザーがあります。

Simple Browserウィンドウの要素をコンテキストとしてチャットプロンプトに追加できます。これは、HTML要素、CSSスタイル、JavaScriptコードなど、Webページの特定の部分についてヘルプが必要な場合に便利です。

Simple Browserからチャットプロンプトに要素を追加するには:

1. `setting(chat.sendElementsToChat.enabled)`設定を使用してSimple Browserからの選択を有効にします。
1. Webアプリケーションを開始します。
1. コマンドパレットから**Simple Browser: Show**コマンドを実行してSimple Browserビューを開きます。
1. **Start**ボタンを選択して、現在のページから要素の選択を開始します。
1. Webページの要素にカーソルを合わせ、クリックしてチャットプロンプトに追加します。

    <video src="images/copilot-chat/simple-browser-select-element.mp4" title="Simple Browserからチャットプロンプトへの要素の追加" autoplay loop controls muted></video>

    選択した要素が現在のチャットプロンプトにコンテキストとして追加されることに注目してください。

コンテキストに含まれる情報を構成できます:

* CSSを添付 - `setting(chat.sendElementsToChat.attachCSS)`設定で有効にします。
* 画像を添付 - `setting(chat.sendElementsToChat.attachImages)`設定で有効にします。

> [!TIP]
> この機能は[Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)拡張機能（プレリリース）でも利用できます。
