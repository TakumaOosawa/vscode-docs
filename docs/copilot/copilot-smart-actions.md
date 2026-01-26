---
ContentId: f0f31de2-a344-4ee6-8d5b-d3ac4e11e149
DateApproved: 01/08/2026
MetaDescription: Use smart actions in VS Code to get help from AI for common development tasks, such as generating commit messages, renaming symbols, or fixing coding errors.
MetaSocialImage: images/shared/github-copilot-social.png
---
# Visual Studio Code の AI スマートアクション

いくつかの一般的なシナリオでは、*スマートアクション*を使用して、プロンプトを記述することなく AI のサポートを受けることができます。これらのスマートアクションの例として、コミットメッセージの生成、ドキュメントの生成、コードの説明または修正、コードレビューの実行などがあります。これらのスマートアクションは、VS Code UI 全体で利用できます。

## コミットメッセージと PR 情報の生成

コードの変更に基づいて、コミットメッセージやプルリクエスト (PR) のタイトルと説明の生成を支援します。ソース管理ビューまたは GitHub PR 拡張機能の*きらめき*アイコンを使用して、変更を要約したタイトルと説明を生成します。

![Hover over Source Control input box sparkle buttons shows Generate Commit Message](images/copilot-smart-actions/generate-commit-message.png)

## AI を使用したマージ競合の解決 (実験的)

AI を使用して、Git のマージ競合の解決を支援します。エディターで **Resolve Merge Conflict with AI** ボタンを選択すると、チャットビューが開き、マージ競合の解決を支援するエージェントフローが開始されます。マージベースと各ブランチからの変更が、AI のコンテキストとして提供されます。

![Screenshot of the proposed merge conflict resolution in the editor.](images/copilot-smart-actions/ai-merge-conflict-resolution.png)

## TODO コメントの実装

[GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) 拡張機能がインストールされている場合、[Copilot coding agent](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent) を使用して、AI でコード内の `TODO` コメントを実装できます。

1. [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) 拡張機能がインストールされていることを確認します。
1. コードに `TODO` コメントを追加します。コメントの横にコードアクション (電球) が表示されます。
1. コードアクションを選択し、**Delegate to coding agent** を選択します。

    ![Screenshot that shows a Code Action menu with Start Coding Agent option for a TODO comment.](images/copilot-smart-actions/start-coding-agent-todo.png)

## シンボルの名前変更

コード内のシンボルの名前を変更するときに、シンボルのコンテキストとコードベースに基づいて、新しい名前の AI 生成の提案を取得します。

![Inline chat suggesting a new name for a symbol in a Python file](images/copilot-smart-actions/copilot-inline-chat-rename-suggestion.png)

## Markdown の画像の代替テキストの生成

AI を使用して、Markdown ファイル内の画像の代替テキストを生成または更新します。代替テキストを生成するには:

1. Markdown ファイルを開きます。
1. 画像リンクにカーソルを置きます。
1. コードアクション (電球) アイコンを選択し、**Generate alt text** を選択します。

    ![Screenshot that shows a Code Action menu with Generate alt text option for a Markdown image link.](images/copilot-smart-actions/generate-alt-text.png)

1. すでに代替テキストがある場合は、コードアクションを選択し、**Refine alt text** を選択します。

## ドキュメントの生成

AI を使用して、複数の言語のコードドキュメントを生成します。

1. アプリケーションコードファイルを開きます。
1. オプションで、ドキュメント化するコードを選択します。
1. 右クリックして、**生成** > **Docs の生成**を選択します。

    ![Inline chat /doc example to generate documentation code comments for a calculator class](images/copilot-smart-actions/inline-chat-doc-example.png)

## テストの生成

プロンプトを書かずにアプリケーションコードのテストを生成するには、エディターのスマートアクションを使用できます。

1. アプリケーションコードファイルを開きます。
1. オプションで、テストするコードを選択します。
1. 右クリックして、**生成** > **テストの生成**を選択します。

    VS Code は、既存のテストファイルにテストコードを生成するか、存在しない場合は新しいテストファイルを作成します。

1. オプションで、インラインチャットのプロンプトで追加のコンテキストを提供して、生成されたテストを調整します。

## コードの説明

エディターでコードブロックの説明を取得します。

1. アプリケーションコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**説明**を選択します。

    VS Code は、選択されたコードブロックの説明を提供します。

## コーディングエラーの修正

プロンプトを書かずにアプリケーションコードのコーディングの問題を修正するには、エディターのスマートアクションを使用できます。

1. アプリケーションコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**生成** > **修正**を選択します。

    VS Code は、コードを修正するためのコード提案を提供します。

1. オプションで、チャットプロンプトで追加のコンテキストを提供して、生成されたコードを調整します。

または、コードファイルにコンパイルまたはリンティングの問題がある場合、VS Code は問題を解決するのに役立つコードアクションをエディターに表示します。

![Screenshot of the editor showing the sparkle icon and Copilot context menu to explain or fix the issue.](images/copilot-smart-actions/copilot-code-action-fix.png)

## テストエラーの修正

テストエクスプローラーから直接、コードベース内の失敗したテストの修正に関するヘルプを取得します。

1. テストエクスプローラーで、失敗したテストにカーソルを合わせます
1. **Fix Test Failure** ボタン (きらめきアイコン) を選択します
1. Copilot の提案された修正を確認して適用します

または、次のことができます:

1. チャットビューを開きます
1. `/fixTestFailure` コマンドを入力します
1. Copilot の提案に従ってテストを修正します

> [!TIP]
> [agents](/docs/copilot/chat/copilot-chat.md#built-in-agents) を使用する場合、エージェントはテストの実行時にテスト出力を監視し、失敗したテストの修正と再実行を自動的に試行します。

## ターミナルエラーの修正

ターミナルでコマンドの実行に失敗すると、VS Code はガターにきらめきを表示し、何が起こったかを説明するクイックフィックスを提供します。

![Fix with Copilot option in the terminal after a failed terminal command.](images/copilot-smart-actions/terminal-command-explanation.png)

## コードのレビュー

VS Code は、エディター内のコードブロック、またはプルリクエストに含まれるすべての変更 ([GitHub Pull Requests extension](https://marketplace.visualstudio.com/items/?itemName=GitHub.vscode-pull-request-github) が必要) のいずれかについて、コードのレビューを支援できます。

エディターでコードブロックをレビューするには:

1. アプリケーションコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**生成** > **レビュー**を選択します。

    VS Code は、**Comments** パネルにレビューコメントを作成し、エディターのインラインにも表示します。

プルリクエストのすべての変更をレビューするには:

1. GitHub Pull Requests 拡張機能を使用してプルリクエストを作成します
1. **Files Changed** ビューの **Code Review** ボタンを選択します。

    VS Code は、**Comments** パネルにレビューコメントを作成し、エディターのインラインにも表示します。

## セマンティック検索結果 (プレビュー)

VS Code の検索ビューでは、ファイル全体でテキストを検索できます。セマンティック検索により、テキストが完全に一致しなくても、検索クエリに意味的に関連する結果を見つけることができます。これは、特定の用語ではなく概念に関連するコードスニペットやドキュメントを探している場合や、検索する正確な用語がわからない場合に特に役立ちます。

![Search view showing semantic search results that are not an exact match for the search criteria.](images/copilot-smart-actions/semantic-search-results.png)

検索ビューで `setting(search.searchView.semanticSearchBehavior)` 設定を使用してセマンティック検索を構成します。セマンティック検索を自動的に実行するか、明示的に要求した場合にのみ実行するかを選択できます。

また、検索ビューで AI 生成のキーワード提案を取得して、関連する代替検索用語を提供することもできます。`setting(search.searchView.keywordSuggestions)` 設定で検索キーワードの提案を有効にします。

![Search view showing keyword suggestions based on the search query.](images/copilot-smart-actions/search-keyword-suggestions.png)

**Add Context** クイックピックから **Get results from the search view** を選択することで、チャットプロンプトで検索結果を参照できます。または、チャットプロンプトに `#searchResults` と入力します。

## AI を使用した設定の検索

変更したい設定の正確な名前がわからない場合は、AI を使用して検索クエリに基づいて関連する設定を見つけることができます。たとえば、「increase text size」を検索して、エディターのフォントサイズを制御する設定を見つけることができます。

`setting(workbench.settings.showAISearchToggle)` 設定でこの機能を有効にします。設定エディターでは、**Search Settings with AI** ボタンを使用して AI 検索結果のオンとオフを切り替えることができます。

![Screenshot that shows the Settings editor showing AI-generated suggestions for settings.](images/copilot-smart-actions/settings-suggestions.png)

## 関連リソース

* [Copilot Quickstart をはじめる](/docs/copilot/getting-started.md)。
