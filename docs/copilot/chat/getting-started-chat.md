---
ContentId: ae1f36a9-7597-425f-97fc-49bd51c153a3
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub CopilotのAI搭載チャット会話を使い始めましょう。コーディング中のインライン、または別のチャットビューで利用できます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでチャットを使い始める

このチュートリアルでは、Visual Studio Codeでチャットを使用する方法を説明します。AI搭載のチャット会話を利用して、コードのリファクタリング、コード理解の向上、VS Codeの設定方法の把握に役立てます。

VS CodeでCopilotを初めて使用する場合は、[Copilotの概要](/docs/copilot/overview.md)を参照するか、[Copilotクイックスタート](/docs/copilot/getting-started.md)でセットアップして主要な機能を確認してください。

> [!TIP]
> Copilotサブスクリプションをまだお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で使用できます。インライン提案とチャット対話には月間の上限があります。

## 前提条件

VS CodeでGitHub Copilotを使用するには、次のものが必要です。

* Access to GitHub Copilot
* GitHub Copilot extensions installed in VS Code

[GitHub Copilotセットアップガイド](/docs/copilot/setup.md)の手順に従ってGitHub Copilotへのアクセス権を取得し、VS CodeにCopilot拡張機能をインストールしてください。

## 最初のチャット会話を開始する

チャットでは自然言語を使ってGitHub Copilotと対話し、コーディングに関連する質問をしたり、回答を受け取ったりできます。

このチュートリアルでは、シンプルなNode.js Webアプリケーションを作成します。

1. 新しいVS Codeウィンドウを開きます。後続の手順で新しいワークスペースを作成します。

1. タイトルバーのチャットメニューから**Open Chat**を選択するか、`kb(workbench.action.chat.open)`キーボードショートカットを使用します。

    ![VS Codeエディターのスクリーンショット。Copilot Chatビューが表示され、コマンドセンター内のチャットメニューが強調表示されている。](./images/getting-started-chat/copilot-chat-menu-command-center.png)

    チャットビューがセカンダリサイドバーで開くことに注目してください。チャットビューを横に表示しておくと、コード作業をしながら会話を続けられます。

1. チャットビューで、チャットモードのドロップダウンから**Ask**を選択します。

    _ask mode_を使用して、コーディングや技術トピックに関する質問、コードの説明、アイデア出しを行います。

    ![VS Codeチャットビューのスクリーンショット。Askモードのドロップダウンが表示されている。](./images/getting-started-chat/copilot-chat-ask-mode.png)

1. 人気のWebフレームワークについて質問してみましょう。チャット入力欄に"what are the most popular web frameworks?"と入力します。

    VS Codeは、人気のWebフレームワークの一覧を返します。特定のフレームワークについて詳しく知るため、またはフレームワークを比較するために、フォローアップ質問を試してみてください。たとえば、"what are the differences between Express and Fastify?"や"how to do server-side rendering?"と質問できます。

1. 新しいWebアプリをスキャフォールドするには、チャット入力欄に"new express app with typescript and pug"と入力します。

    VS Codeが新しいワークスペースのファイルを表すファイルツリーを返すことに注目してください。ファイルツリー内の任意のファイルを選択して内容をプレビューできます。

    ![チャットビューのスクリーンショット。新しいワークスペースのファイルツリーと"Create Workspace"ボタンが表示されている。](./images/getting-started-chat/copilot-chat-view-workspace-file-tree.png)

1. **Create Workspace**を選択してアプリを作成し、ワークスペースを作成するディスク上のフォルダーを選択します。

    ダイアログで**Open**を選択して、新しく作成したワークスペースをVS Codeで開きます。

    > [!NOTE]
    > VS Codeが新しいワークスペースを信頼するかどうかを尋ねる場合があります。**Yes, I trust the contents**を選択してワークスペースを信頼します。[ワークスペースの信頼](/docs/editing/workspaces/workspace-trust.md)の詳細も参照してください。

## インラインチャットでフローを維持する

チャットビューは会話を続けるのに便利ですが、_エディターのインラインチャット_は、エディターで作業中のコードについてCopilotに質問したい場面に最適化されています。たとえば、特定のコードのリファクタリングや、複雑なアルゴリズムの説明などです。

エディターのインラインチャットをコードのリファクタリングに使用する方法を見ていきましょう。

1. `app.ts`ファイルを開き、`kb(inlinechat.start)`キーボードショートカットを使用してエディターのインラインチャットを表示します。あるいは、タイトルバーのチャットメニューから**Open Inline Chat**を選択します。

    エディター内にチャット入力欄がインラインで表示され、チャットプロンプトを入力してエディター内のコードについてCopilotに質問できます。

    ![VS Codeエディターのスクリーンショット。インラインチャットのポップアップコントロールが強調表示されている。](./images/getting-started-chat/copilot-inline-chat-popup.png)

1. チャット入力欄に"Add support for JSON output"と入力し、`kbstyle(Enter)`を押します。

    CopilotがExpressでJSON出力をサポートするためのコード提案を提示することに注目してください。

    ![VS Codeエディターのスクリーンショット。提案されたコード変更が表示されている。](./images/getting-started-chat/copilot-inline-chat-json-support.png)

1. **Accept**または**Close**を選択して、変更を適用するか無視します。

    提案されたコード変更が気に入らない場合は、**Rerun Request**コントロールを選択するか、フォローアップ質問をして別の提案を得られます。

> [!TIP]
> エディターで右クリックすると、コードの修正や説明、テストの生成など、よく使用するAIコマンドにアクセスできます。

## 複数ファイルにまたがる編集を行う

インラインチャットでは、単一のファイルに変更を加えました。チャットビューで_edit mode_に切り替えると、Copilotを使ってワークスペース内の複数ファイルにまたがる変更も行えます。

edit modeを使用して、Webアプリの構成を保存するために`.env`ファイルを利用してみましょう。

1. チャットビューを開き、チャットモードのドロップダウンから**Edit**を選択します。

    ![VS Code Copilot Chatビューのスクリーンショット。Editモードのドロップダウンが表示されている。](./images/getting-started-chat/chat-mode-dropdown-edit.png)

1. Copilotが要求の範囲を理解しやすいように、プロンプトのコンテキストとして`package.json`と`app.ts`を追加しましょう。

    1. チャットビューで**Add Context**を選択し、検索フィールドに`package`と入力して、ファイルの一覧から`package.json`ファイルを選択します。追加できるコンテキストの種類が多数あることに注目してください。

    1. エディターで`app.ts`ファイルを開き、Copilotがアクティブなファイルをチャットコンテキストに自動で追加することに注目してください。

1. チャット入力欄に"Use a .env file for configuration"と入力し、`kbstyle(Enter)`を押します。

1. Copilotが複数ファイルにまたがって更新を行い、ワークスペースに新しい`.env`ファイルを追加することに注目してください。

    チャットビューでは、変更されたファイルが太字で表示されます。

    ![VS Codeエディターのスクリーンショット。app.tsファイル内の提案されたコード変更が表示されている。](./images/getting-started-chat/copilot-inline-chat-env-file.png)

1. チャットビューで**Keep**を選択して、提案された変更をすべて確定します。

    エディターのオーバーレイコントロールを使用すると、ファイル全体にわたる個々の変更へ簡単に移動してレビューできます。

## エージェント的なコーディングフローを開始する

より複雑な要求では、_agent mode_を使用して、Copilotが要求を完了するために必要なタスクを自律的に計画し実行できるようにします。これらのタスクにはコード編集だけでなく、ターミナルでのコマンド実行も含まれます。agent modeでは、Copilotがタスクを達成するためにさまざまなツールを呼び出すことがあります。

agent modeを使用して、Webアプリを旅行のコツを共有する内容にし、テストを追加してみましょう。

1. チャットビューを開き、チャットモードのドロップダウンから**Agent**を選択します。

    ![VS Code Copilot Chatビューのスクリーンショット。Agentモードのドロップダウンが表示されている。](./images/getting-started-chat/chat-mode-dropdown-agent.png)

1. チャット入力欄に"Make the app a travel blog. Add tests to avoid code regression."と入力し、`kbstyle(Enter)`を押します。

    プロンプトにコンテキストを追加する必要はないことに注意してください。agent modeはワークスペース内のコードを自動的に分析します。

1. Copilotは反復しながらコード変更を適用し、テストの実行などのコマンドを実行します。チャットビューで**Continue**を選択してターミナルコマンドを確認します。

    ![VS Codeエディターのスクリーンショット。チャットビューでターミナルでのテスト実行の確認を求めている。](./images/getting-started-chat/copilot-chat-agent-terminal.png)

    要求の複雑さによっては、Copilotがすべてのタスクを完了するまでに数分かかる場合があります。途中で問題が発生した場合は、それを修正するために反復します。

1. Copilotがタスクを完了したら、変更を確認し、アプリをテストします。

    また、"Run the app"や"Start the server"のようなプロンプトを与えて、Copilotにアプリを実行するよう依頼することもできます。

## おめでとうございます

おめでとうございます。VS CodeでCopilot Chatを使用して質問し、ワークスペース全体にわたるコード編集を行うことに成功しました。Copilot Chatを最大限に活用するために、さまざまなプロンプトやチャットモードを引き続き試してください。

## 追加リソース

* [VS CodeのCopilot Chatの概要を確認する](/docs/copilot/chat/copilot-chat.md)
