---
ContentId: ae1f36a9-7597-425f-97fc-49bd51c153a3
DateApproved: 01/08/2026
MetaDescription: コーディング中にインラインで、または別のチャットビューでGitHub Copilotを使用したAI搭載のチャット会話をVisual Studio Codeで開始します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでのチャットの開始

このチュートリアルでは、Visual Studio Codeでのチャットの使用方法について説明します。AI搭載のチャット会話を使用して、コードのリファクタリング、コード理解の向上、VS Codeの構成の把握を支援します。

VS CodeでのCopilotの使用が初めての場合は、[Copilotの概要](/docs/copilot/overview.md)を参照するか、[Copilotクイックスタート](/docs/copilot/getting-started.md)でセットアップを行い、主要な機能を確認してください。

> [!TIP]
> Copilotサブスクリプションをまだお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップすることでCopilotを無料で使用でき、インライン提案とチャット対話の月間制限を取得できます。

## 前提条件

VS CodeでGitHub Copilotを使用するには、以下が必要です。

* GitHub Copilotへのアクセス
* VS CodeにインストールされたGitHub Copilot拡張機能

[GitHub Copilotセットアップガイド](/docs/copilot/setup.md)の手順に従ってGitHub Copilotへのアクセスを取得し、VS CodeにCopilot拡張機能をインストールしてください。

## 最初のチャット会話を取得する

チャットを使用すると、自然言語を使用してGitHub Copilotと対話し、コーディング関連の質問をして回答を受け取ることができます。

このチュートリアルでは、シンプルなNode.js Webアプリケーションを作成します。

1. 新しいVS Codeウィンドウを開きます。次のステップで新しいワークスペースを作成します。

1. タイトルバーのチャットメニューから**Open Chat**を選択するか、キーボードショートカット `kb(workbench.action.chat.open)` を使用します。

    ![VS Codeエディターのスクリーンショット。Copilot Chatビューを表示し、コマンドセンターのチャットメニューを強調表示しています。](./images/getting-started-chat/copilot-chat-menu-command-center.png)

    Chatビューがセカンダリサイドバーで開くことに注目してください。Chatビューを側面に配置することで、コードに取り組みながら会話を続けることができます。

1. Chatビューで、チャットモードのドロップダウンから**Ask**を選択します。

    コーディングやテクノロジーのトピックについて質問したり、コードを説明したり、アイデアをブレインストーミングしたりするには、_askモード_を使用します。

    ![VS Code Chatビューのスクリーンショット。Askモードのドロップダウンを表示しています。](./images/getting-started-chat/copilot-chat-ask-mode.png)

1. 人気のあるWebフレームワークについて質問してみましょう。チャット入力フィールドに「what are the most popular web frameworks?」と入力します。

    VS Codeは人気のあるWebフレームワークのリストを返します。特定のフレームワークに関する詳細情報を取得したり、フレームワークを比較したりするために、フォローアップの質問をしてみてください。たとえば、「what are the differences between Express and Fastify?」や「how to do server-side rendering?」と質問できます。

1. 新しいWebアプリのスキャフォールディングを行うには、チャット入力フィールドに「new express app with typescript and pug」と入力します。

    VS Codeが新しいワークスペースファイルを表すファイルツリーを返す方法に注目してください。ファイルツリー内の任意のファイルを選択して、そのコンテンツをプレビューします。

    ![Chatビューのスクリーンショット。新しいワークスペースのファイルツリーと「ワークスペースの作成」ボタンを表示しています。](./images/getting-started-chat/copilot-chat-view-workspace-file-tree.png)

1. **Create Workspace**を選択してアプリを作成し、ディスク上のワークスペースを作成するフォルダーを選択します。

    ダイアログで**Open**を選択して、作成したワークスペースをVS Codeで開きます。

    > [!NOTE]
    > VS Codeから新しいワークスペースを信頼するかどうか尋ねられる場合があります。**Yes, I trust the contents**を選択してワークスペースを信頼します。詳細については、[ワークスペースの信頼](/docs/editing/workspaces/workspace-trust.md)を参照してください。

## インラインチャットでフローを維持する

Chatビューは会話を続けるのに最適ですが、_エディターインラインチャット_は、エディターで現在作業中のコードについてCopilotに質問したい状況に最適化されています。たとえば、特定のコードのリファクタリングや、複雑なアルゴリズムの説明などです。

コードのリファクタリングにエディターインラインチャットを使用する方法を見てみましょう。

1. `app.ts`ファイルを開き、キーボードショートカット `kb(inlinechat.start)` を使用してエディターインラインチャットを表示します。または、タイトルバーのチャットメニューから**Open Inline Chat**を選択します。

    エディター内にチャット入力フィールドがインラインで表示され、チャットプロンプトを入力してエディター内のコードについてCopilotに質問できます。

    ![VS Codeエディターのスクリーンショット。インラインチャットのポップアップコントロールを強調表示しています。](./images/getting-started-chat/copilot-inline-chat-popup.png)

1. チャット入力フィールドに「Add support for JSON output」と入力し、`kbstyle(Enter)` を押します。

    ExpressでJSON出力のサポートを追加するためのコード提案をCopilotがどのように提供するかに注目してください。

    ![提案されたコード変更を含むVS Codeエディターのスクリーンショット。](./images/getting-started-chat/copilot-inline-chat-json-support.png)

1. **Accept**または**Close**を選択して、変更を適用または無視します。

    提案されたコード変更に満足できない場合は、**Rerun Request**コントロールを選択するか、フォローアップの質問をして別の提案を得ることができます。

> [!TIP]
> エディター内を右クリックすると、コードの修正や説明、テストの生成など、一般的に使用されるAIコマンドにアクセスできます。

## 複数のファイルにわたって編集を行う

インラインチャットでは、単一のファイルに変更を加えました。Chatビューで_editモード_に切り替えることで、Copilotを使用してワークスペース内の複数のファイルに変更を加えることもできます。

editモードを使用して、Webアプリの構成を保存するために`.env`ファイルを使用してみましょう。

1. Chatビューを開き、チャットモードのドロップダウンから**Edit**を選択します。

    ![VS Code Copilot Chatビューのスクリーンショット。Editモードのドロップダウンを表示しています。](./images/getting-started-chat/chat-mode-dropdown-edit.png)

1. Copilotがリクエストのスコープを理解できるように、プロンプトのコンテキストとして`package.json`と`app.ts`を追加しましょう。

    1. Chatビューで**Add Context**を選択し、検索フィールドに `package` と入力して、ファイルリストから`package.json`ファイルを選択します。追加できるコンテキストには多くの種類があることに注目してください。

    1. エディターで`app.ts`ファイルを開くと、Copilotがアクティブなファイルをチャットコンテキストに自動的に追加することに注目してください。

1. チャット入力フィールドに「Use a .env file for configuration」と入力し、`kbstyle(Enter)` を押します。

1. Copilotが複数のファイルに更新を行い、新しい`.env`ファイルをワークスペースに追加する方法に注目してください。

    Chatビューには、変更されたファイルが太字で表示されます。

    ![VS Codeエディターのスクリーンショット。app.tsファイルで提案されたコード変更を表示しています。](./images/getting-started-chat/copilot-inline-chat-env-file.png)

1. Chatビューで**Keep**を選択して、提案されたすべての変更を確認します。

    エディターのオーバーレイコントロールを使用すると、ファイル全体の個々の変更を簡単にナビゲートして確認できます。

## エージェントコーディングフローを開始する

より複雑なリクエストの場合、_agentモード_を使用して、Copilotにリクエストを完了するために必要なタスクを自律的に計画および実行させることができます。これらのタスクにはコードの編集だけでなく、ターミナルでのコマンド実行も含まれる場合があります。agentモードでは、Copilotはタスクを達成するためにさまざまなツールを呼び出す場合があります。

agentモードを使用して、旅行のヒントを共有するWebアプリを作成し、テストを追加してみましょう。

1. Chatビューを開き、チャットモードのドロップダウンから**Agent**を選択します。

    ![VS Code Copilot Chatビューのスクリーンショット。Agentモードのドロップダウンを表示しています。](./images/getting-started-chat/chat-mode-dropdown-agent.png)

1. チャット入力フィールドに「Make the app a travel blog. Add tests to avoid code regression.」と入力し、`kbstyle(Enter)` を押します。

    プロンプトにコンテキストを追加する必要がないことに注意してください。agentモードは、ワークスペース内のコードを自動的に分析します。

1. Copilotは繰り返し処理を行い、コード変更の適用やテストの実行などのコマンドを実行します。Chatビューで**Continue**を選択して、ターミナルコマンドを確認します。

    ![VS Codeエディターのスクリーンショット。ターミナルでのテスト実行の確認を求めるChatビューを表示しています。](./images/getting-started-chat/copilot-chat-agent-terminal.png)

    リクエストの複雑さに応じて、Copilotがすべてのタスクを完了するのに数分かかる場合があります。途中で問題が発生した場合、Copilotは修正のために繰り返し処理を行います。

1. Copilotがタスクを完了したら、変更を確認してアプリをテストします。

    「Run the app」や「Start the server」などのプロンプトを指定して、Copilotにアプリの実行を依頼することもできます。

## おめでとうございます

おめでとうございます。VS CodeでCopilot Chatを使用して質問をし、ワークスペース全体でコード編集を行うことができました。さまざまなプロンプトとチャットモードを試して、Copilot Chatを最大限に活用してください。

## 追加リソース

* [VS CodeでのCopilot Chatの概要](/docs/copilot/chat/copilot-chat.md)
