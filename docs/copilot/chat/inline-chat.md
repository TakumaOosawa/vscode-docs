---
ContentId: e6b33fcb-8240-49dd-b6ca-5412d6fa669a
DateApproved: 12/10/2025
MetaDescription: Visual Studio Codeのインライン チャットを使用して、エディターで直接編集したり、ターミナルでコマンド候補を取得したりします。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# インライン チャット

Visual Studio Codeのインライン チャットを使用すると、エディターで直接コード生成や編集を依頼したり、統合ターミナル内でシェル コマンドのヘルプを得たりできます。インライン チャットを使うと、別のChatビューに切り替えることなく作業の流れを保てます。

## 前提条件

* 最新バージョンの[Visual Studio Code](/download)をインストールする
* [GitHub Copilot](/docs/copilot/setup.md)にアクセスできる

## エディターのインライン チャットを使用する

エディターのインライン チャットを使用すると、プロンプトはアクティブなエディター内のコードにスコープされます。インライン チャットは、ワークスペース内の他のファイルの内容をプロンプトのコンテキストとして使用する場合があります。

エディターのインライン チャットを使用するには:

1. Open a file in the editor.
1. エディターでファイルを開きます。

1. Open editor inline chat by using the `kb(inlinechat.start)` keyboard shortcut or by selecting **Open Inline Chat** from the Chat menu in the title bar.
1. `kb(inlinechat.start)`キーボード ショートカットを使用するか、タイトル バーのChatメニューから**インライン チャットを開く**を選択して、エディターのインライン チャットを開きます。

1. Type your prompt in the chat input field and press `kbstyle(Enter)`.
1. チャット入力フィールドにプロンプトを入力し、`kbstyle(Enter)`を押します。

    > [!TIP]
    > エディターでコードのブロックを選択すると、プロンプトのスコープをそのコードに限定できます。

1. VS Code shows a diff with the code suggestion inline in the editor. Accept or reject the changes.
1. VS Codeは、コード提案をエディター内にインラインで差分として表示します。変更を承認または拒否します。

    ![階乗関数で再帰を使用しないように求めるエディターのインライン チャットのスクリーンショット。](images/copilot-chat/inline-chat-no-recursion.png)

1. Optionally, ask a follow-up question to get other suggestions or refine the results.
1. 必要に応じて、フォローアップの質問をして別の提案を得たり、結果を改善したりします。

> [!TIP]
> インライン チャットのプロンプトにコンテキストを添付して、関連ファイル、コード シンボル、またはその他のコンテキストを含めます。詳しくは、[チャット プロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)をご覧ください。

## ターミナルのインライン チャットを使用する

[統合ターミナル](/docs/terminal/basics.md)でターミナルのインライン チャットを開いて、シェル コマンドのヘルプを得たり、ターミナルに関する質問をしたりできます。

ターミナルのインライン チャットを使用するには:

1. Open the terminal in VS Code by selecting the **View** > **Terminal** menu item or using the `kb(workbench.action.terminal.toggleTerminal)` keyboard shortcut.
1. **表示**>**ターミナル**メニュー項目を選択するか、`kb(workbench.action.terminal.toggleTerminal)`キーボード ショートカットを使用して、VS Codeでターミナルを開きます。

1. Start terminal inline chat by using the `kb(workbench.action.terminal.chat.start)` keyboard shortcut or running the **Terminal Inline Chat** command in the Command Palette.
1. `kb(workbench.action.terminal.chat.start)`キーボード ショートカットを使用するか、コマンド パレットで**ターミナル インライン チャット**コマンドを実行して、ターミナルのインライン チャットを開始します。

1. Type your prompt in the chat input field and press `kbstyle(Enter)`.
1. チャット入力フィールドにプロンプトを入力し、`kbstyle(Enter)`を押します。

    !["src dir内で最大のファイル上位5つを一覧表示"のような複雑な質問ができることを示すスクリーンショット](images/copilot-chat/terminal-chat-2.png)

1. Review the response and select the **Run** (`kb(workbench.action.terminal.chat.runCommand)`) to run the command in the terminal
1. 応答を確認し、**実行**(`kb(workbench.action.terminal.chat.runCommand)`)を選択してターミナルでコマンドを実行します。

    Alternatively, select **Insert** (`kb(workbench.action.terminal.chat.insertCommand)`) to insert the command into the terminal and modify it before running.
    または、**挿入**(`kb(workbench.action.terminal.chat.insertCommand)`)を選択して、コマンドをターミナルに挿入し、実行前に変更します。

## 関連リソース

* [チャット プロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)
