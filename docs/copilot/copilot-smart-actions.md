---
ContentId: f0f31de2-a344-4ee6-8d5b-d3ac4e11e149
DateApproved: 12/10/2025
MetaDescription: Use smart actions in VS Code to get help from AI for common development tasks, such as generating commit messages, renaming symbols, or fixing coding errors.
MetaSocialImage: images/shared/github-copilot-social.png
---
# Visual Studio Code の AI スマートアクション

いくつかの一般的なシナリオでは、_スマートアクション_を使用して、プロンプトを記述することなく、AI からヘルプを得ることができます。これらのスマートアクションの例としては、コミット メッセージの生成、ドキュメントの生成、コードの説明または修正、コード レビューの実行などがあります。これらのスマートアクションは、VS Code UI の至る所で利用できます。

## コミット メッセージと PR 情報の生成

コードの変更に基づいて、コミット メッセージとプル リクエスト (PR) のタイトルと説明の生成に関するヘルプを取得します。ソース管理ビューまたは GitHub PR 拡張機能の _輝く星 (sparkle)_ アイコンを使用して、変更を要約するタイトルと説明を生成します。

![ソース管理の入力ボックスの輝く星ボタンにカーソルを合わせると、「コミット メッセージを生成」が表示される](images/copilot-smart-actions/generate-commit-message.png)

## AI を使用したマージ競合の解決 (試験段階)

AI を使用して、Git マージ競合の解決を支援します。エディターで **Resolve Merge Conflict with AI** ボタンを選択すると、チャット ビューが開き、マージ競合の解決を支援するエージェント フローが開始されます。マージ ベースと各ブランチからの変更が AI のコンテキストとして提供されます。

![エディターでの提案されたマージ競合解決のスクリーンショット。](images/copilot-smart-actions/ai-merge-conflict-resolution.png)

## TODO コメントの実装

[GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) 拡張機能がインストールされている場合、AI を使用して [Copilot コーディング エージェント](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent) でコード内の `TODO` コメントを実装できます。

1. [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) 拡張機能がインストールされていることを確認します。
1. コードに `TODO` コメントを追加します。コメントの横にコード アクション (電球) が表示されます。
1. コード アクションを選択し、**コーディング エージェントに委任する** を選択します。

    ![TODO コメントの [コーディング エージェントの開始] オプションがあるコード アクション メニューを示すスクリーンショット。](images/copilot-smart-actions/start-coding-agent-todo.png)

## シンボルの名前変更

コード内のシンボルの名前を変更する場合、シンボルのコンテキストとコードベースに基づいて、新しい名前の AI 生成候補を取得します。

![Python ファイル内のシンボルの新しい名前を提案するインライン チャット](images/copilot-smart-actions/copilot-inline-chat-rename-suggestion.png)

## Markdown 内の画像の代替テキストの生成

AI を使用して、Markdown ファイル内の画像の代替テキストを生成または更新します。代替テキストを生成するには:

1. Markdown ファイルを開きます。
1. カーソルを画像リンクに置きます。
1. コード アクション (電球) アイコンを選択し、**代替テキストの生成 (Generate alt text)** を選択します。

    ![Markdown 画像リンクの [代替テキストの生成 (Generate alt text)] オプションがあるコード アクション メニューを示すスクリーンショット。](images/copilot-smart-actions/generate-alt-text.png)

1. すでに代替テキストがある場合は、コード アクションを選択し、**代替テキストの調整 (Refine alt text)** を選択します。

## ドキュメントの生成

AI を使用して、複数の言語のコード ドキュメントを生成します。

1. アプリケーション コード ファイルを開きます。
1. 必要に応じて、ドキュメント化するコードを選択します。
1. 右クリックして、**Generate Code** > **Generate Docs** を選択します。

    ![電卓クラスのドキュメント コード コメントを生成するためのインライン チャット /doc の例](images/copilot-smart-actions/inline-chat-doc-example.png)

## テストの生成

プロンプトを作成せずにアプリケーション コードのテストを生成するには、エディターのスマートアクションを使用できます。

1. アプリケーション コード ファイルを開きます。
1. 必要に応じて、テストするコードを選択します。
1. 右クリックして、**Generate Code** > **Generate Tests** を選択します。

    VS Code は、既存のテスト ファイルにテスト コードを生成するか、存在しない場合は新しいテスト ファイルを作成します。

1. 必要に応じて、インライン チャット プロンプトで追加のコンテキストを提供して、生成されたテストを調整します。

## コードの説明

エディターでコード ブロックの説明に関するヘルプを取得します。

1. アプリケーション コード ファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**Explain** を選択します。

    VS Code は、選択されたコード ブロックの説明を提供します。

## コーディング エラーの修正

プロンプトを作成せずにアプリケーション コードのコーディング上の問題を修正するには、エディターのスマートアクションを使用できます。

1. アプリケーション コード ファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**Generate Code** > **Fix** を選択します。

    VS Code は、コードを修正するためのコード候補を提供します。

1. 必要に応じて、チャット プロンプトで追加のコンテキストを提供して、生成されたコードを調整します。

あるいは、コード ファイルにコンパイルまたはリンティングの問題がある場合、VS Code はエディターにコード アクションを表示して問題を解決するのに役立ちます。

![問題を説明または修正するための輝く星アイコンと Copilot コンテキスト メニューを表示するエディターのスクリーンショット。](images/copilot-smart-actions/copilot-code-action-fix.png)

## テスト エラーの修正

テスト エクスプローラーから直接、コードベース内の失敗したテストの修正に関するヘルプを取得します。

1. テスト エクスプローラーで、失敗したテストにカーソルを合わせます
1. **Fix Test Failure** ボタン (輝く星アイコン) を選択します
1. Copilot の推奨する修正を確認して適用します

あるいは、次のこともできます:

1. チャット ビューを開きます
1. `/fixTestFailure` コマンドを入力します
1. Copilot の提案に従ってテストを修正します

> [!TIP]
> [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、エージェントはテスト実行時のテスト出力を監視し、失敗したテストを自動的に修正して再実行しようとします。

## ターミナル エラーの修正

ターミナルでコマンドの実行に失敗した場合、VS Code はガターに輝く星を表示し、何が起こったかを説明するクイック フィックスを提供します。

![失敗したターミナル コマンドの後のターミナルでの [Fix with Copilot] オプション。](images/copilot-smart-actions/terminal-command-explanation.png)

## コードのレビュー

VS Code は、エディター内のコード ブロック、またはプル リクエストに含まれるすべての変更 ([GitHub Pull Requests 拡張機能](https://marketplace.visualstudio.com/items/?itemName=GitHub.vscode-pull-request-github) が必要) のコード レビューを支援します。

エディターでコード ブロックをレビューするには:

1. アプリケーション コード ファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**Generate Code** > **Review** を選択します。

    VS Code は、**コメント** パネルにレビュー コメントを作成し、エディター内でもインラインで表示します。

プル リクエスト内のすべての変更をレビューするには:

1. GitHub Pull Requests 拡張機能を使用してプル リクエストを作成します
1. **変更されたファイル (Files Changed)** ビューで **Code Review** ボタンを選択します。

    VS Code は、**コメント** パネルにレビュー コメントを作成し、エディター内でもインラインで表示します。

## セマンティック検索結果 (プレビュー)

VS Code の検索ビューでは、ファイル全体でテキストを検索できます。セマンティック検索を使用すると、テキストが完全に一致しなくても、検索クエリと意味的に関連のある結果を見つけることができます。これは、特定の用語ではなく概念に関連するコード スニペットやドキュメントを探している場合や、検索する正確な用語がわからない場合に特に便利です。

![検索条件に完全に一致しないセマンティック検索結果を表示する検索ビュー。](images/copilot-smart-actions/semantic-search-results.png)

検索ビューでのセマンティック検索は、`setting(search.searchView.semanticSearchBehavior)` 設定で構成します。セマンティック検索を自動的に実行するか、明示的に要求した場合にのみ実行するかを選択できます。

また、検索ビューで AI 生成のキーワード候補を取得して、関連する代替検索用語を提供することもできます。`setting(search.searchView.keywordSuggestions)` 設定で検索キーワード候補を有効にします。

![検索クエリに基づいたキーワード候補を表示する検索ビュー。](images/copilot-smart-actions/search-keyword-suggestions.png)

**コンテキストの追加** クイック ピックから **Get results from the search view** を選択することで、チャット プロンプトで検索結果を参照できます。あるいは、チャット プロンプトに `#searchResults` と入力します。

## AI を使用した設定の検索

変更したい設定の正確な名前がわからない場合は、AI を使用して検索クエリに基づいて関連する設定を見つけることができます。たとえば、「テキスト サイズを大きくする」と検索して、エディターのフォント サイズを制御する設定を見つけることができます。

この機能は、`setting(workbench.settings.showAISearchToggle)` 設定で有効にします。設定エディターでは、**Search Settings with AI** ボタンを使用して AI 検索結果のオンとオフを切り替えることができます。

![設定の AI 生成の候補を表示している設定エディターを示すスクリーンショット。](images/copilot-smart-actions/settings-suggestions.png)

## 関連リソース

* [Copilot クイックスタートを始める](/docs/copilot/getting-started.md)。
