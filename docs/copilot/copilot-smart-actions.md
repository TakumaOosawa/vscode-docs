---
ContentId: f0f31de2-a344-4ee6-8d5b-d3ac4e11e149
DateApproved: 12/10/2025
MetaDescription: VS Codeのスマートアクションを使用して、コミットメッセージの生成、シンボル名の変更、コーディングエラーの修正などの一般的な開発タスクについてAIの支援を受けます。
MetaSocialImage: images/shared/github-copilot-social.png
---
# Visual Studio CodeのAIスマートアクション

いくつかの一般的なシナリオでは、プロンプトを書かずにAIの支援を受けるために_スマートアクション_を使用できます。これらのスマートアクションの例として、コミットメッセージの生成、ドキュメントの生成、コードの説明や修正、またはコードレビューの実行があります。これらのスマートアクションは、VS Code UI全体で利用できます。

## コミットメッセージとPR情報を生成する

コード変更に基づいて、コミットメッセージやpull request(PR)のタイトルと説明の生成を支援してもらえます。Source ControlビューまたはGitHub PR拡張機能の_sparkle_アイコンを使用して、変更を要約するタイトルと説明を生成します。

![Source Controlの入力ボックスのsparkleボタンにホバーすると「Generate Commit Message」が表示される](images/copilot-smart-actions/generate-commit-message.png)

## AIでマージ競合を解決する(実験的)

AIを使用してGitのマージ競合の解決を支援してもらえます。エディターで**Resolve Merge Conflict with AI**ボタンを選択してチャットビューを開き、マージ競合の解決を支援するエージェント的なフローを開始します。マージベースと各ブランチからの変更が、AIのコンテキストとして提供されます。

![エディターで提案されたマージ競合の解決策のスクリーンショット。](images/copilot-smart-actions/ai-merge-conflict-resolution.png)

## todoコメントを実装する

[GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)拡張機能をインストールしている場合、[Copilot coding agent](/docs/copilot/agents/cloud-agents.md#github-copilot-coding-agent)を使用して、AIでコード内の`TODO`コメントを実装できます。

1. [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)拡張機能がインストールされていることを確認します。
1. コードに`TODO`コメントを追加します。コメントの横にコードアクション(電球)が表示されます。
1. コードアクションを選択し、**Delegate to coding agent**を選択します。

    ![`TODO`コメントに対してStart Coding Agentオプションが表示されているコードアクションメニューのスクリーンショット。](images/copilot-smart-actions/start-coding-agent-todo.png)

## シンボル名を変更する

コード内のシンボル名を変更すると、シンボルとコードベースのコンテキストに基づいて、AIが生成した新しい名前の候補を取得できます。

![Pythonファイル内のシンボルに対して新しい名前を提案するインラインチャット](images/copilot-smart-actions/copilot-inline-chat-rename-suggestion.png)

## Markdown内の画像の代替テキストを生成する

AIを使用して、Markdownファイル内の画像の代替テキストを生成または更新します。代替テキストを生成するには、次の手順に従います。

1. Markdownファイルを開きます。
1. 画像リンクにカーソルを置きます。
1. コードアクション(電球)アイコンを選択し、**Generate alt text**を選択します。

    ![Markdownの画像リンクに対してGenerate alt textオプションが表示されているコードアクションメニューのスクリーンショット。](images/copilot-smart-actions/generate-alt-text.png)

1. すでに代替テキストがある場合は、コードアクションを選択し、**Refine alt text**を選択します。

## ドキュメントを生成する

AIを使用して、複数の言語向けのコードドキュメントを生成します。

1. アプリケーションのコードファイルを開きます。
1. 必要に応じて、ドキュメント化したいコードを選択します。
1. 右クリックし、**Generate Code** > **Generate Docs**を選択します。

    ![電卓クラス向けのドキュメント用コードコメントを生成するインラインチャットの/doc例](images/copilot-smart-actions/inline-chat-doc-example.png)

## テストを生成する

プロンプトを書かずにアプリケーションコードのテストを生成するには、エディターのスマートアクションを使用できます。

1. アプリケーションのコードファイルを開きます。
1. 必要に応じて、テストしたいコードを選択します。
1. 右クリックし、**Generate Code** > **Generate Tests**を選択します。

    VS Codeは、既存のテストファイルにテストコードを生成します。テストファイルが存在しない場合は、新しいテストファイルを作成します。

1. 必要に応じて、Inline Chatのプロンプトで追加のコンテキストを提供して、生成されたテストを調整します。

## コードを説明する

エディター内のコードブロックの説明を支援してもらえます。

1. アプリケーションのコードファイルを開きます。
1. 説明したいコードを選択します。
1. 右クリックし、**Explain**を選択します。

    VS Codeは、選択したコードブロックの説明を提供します。

## コーディングエラーを修正する

プロンプトを書かずにアプリケーションコードのコーディング問題を修正するには、エディターのスマートアクションを使用できます。

1. アプリケーションのコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックし、**Generate Code** > **Fix**を選択します。

    VS Codeは、コードを修正するためのコード提案を提供します。

1. 必要に応じて、チャットプロンプトで追加のコンテキストを提供して、生成されたコードを調整します。

または、コードファイルにコンパイルまたはリンティングの問題がある場合、VS Codeはエディターにコードアクションを表示して、問題の解決を支援します。

![問題を説明または修正するためのsparkleアイコンとCopilotコンテキストメニューが表示されているエディターのスクリーンショット。](images/copilot-smart-actions/copilot-code-action-fix.png)

## テストエラーを修正する

Test Explorerから直接、コードベース内で失敗しているテストの修正を支援してもらえます。

1. Test Explorerで、失敗しているテストにホバーします
1. **Fix Test Failure**ボタン(sparkleアイコン)を選択します
1. Copilotが提案した修正を確認して適用します

または、次の操作を行うこともできます。

1. チャットビューを開きます
1. `/fixTestFailure`コマンドを入力します
1. Copilotの提案に従ってテストを修正します

> [!TIP]
> [agents](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、エージェントはテスト実行時にテスト出力を監視し、失敗しているテストの修正と再実行を自動的に試行します。

## ターミナルエラーを修正する

ターミナルでコマンドの実行に失敗すると、VS Codeはガターにsparkleを表示し、何が起きたかを説明するQuick Fixを提供します。

![ターミナルコマンドの失敗後、ターミナルにFix with Copilotオプションが表示されている。](images/copilot-smart-actions/terminal-command-explanation.png)

## コードをレビューする

VS Codeは、エディター内のコードブロック、またはpull requestに含まれるすべての変更のレビューを支援できます(pull requestのレビューには[GitHub Pull Requests extension](https://marketplace.visualstudio.com/items/?itemName=GitHub.vscode-pull-request-github)が必要です)。

エディターでコードブロックをレビューするには、次の手順に従います。

1. アプリケーションのコードファイルを開きます。
1. レビューしたいコードを選択します。
1. 右クリックし、**Generate Code** > **Review**を選択します。

    VS Codeは**Comments**パネルにレビューコメントを作成し、エディター内にもインラインで表示します。

pull request内のすべての変更をレビューするには、次の手順に従います。

1. GitHub Pull Requests拡張機能でpull requestを作成します
1. **Files Changed**ビューで**Code Review**ボタンを選択します。

    VS Codeは**Comments**パネルにレビューコメントを作成し、エディター内にもインラインで表示します。

## セマンティック検索結果(プレビュー)

VS CodeのSearchビューでは、ファイル全体にわたってテキストを検索できます。セマンティック検索では、テキストが完全一致しない場合でも、検索クエリに対して意味的に関連する結果を見つけることができます。これは、特定の用語ではなく概念に関連するコードスニペットやドキュメントを探している場合や、検索に使う正確な用語が分からない場合に特に便利です。

![検索条件に完全一致しないセマンティック検索結果が表示されているSearchビュー。](images/copilot-smart-actions/semantic-search-results.png)

Searchビューでセマンティック検索を構成するには、`setting(search.searchView.semanticSearchBehavior)`設定を使用します。セマンティック検索を自動的に実行するか、明示的に要求したときのみ実行するかを選択できます。

また、SearchビューでAIが生成したキーワード提案を取得して、関連する代替の検索用語を提示できます。検索キーワード提案を有効にするには、`setting(search.searchView.keywordSuggestions)`設定を使用します。

![検索クエリに基づくキーワード提案が表示されているSearchビュー。](images/copilot-smart-actions/search-keyword-suggestions.png)

**Add Context**クイックピックから**Get results from the search view**を選択すると、チャットプロンプトで検索結果を参照できます。あるいは、チャットプロンプトで`#searchResults`と入力します。

## AIで設定を検索する

変更したい設定の正確な名前が分からない場合、検索クエリに基づいて関連する設定を見つけるためにAIを使用できます。たとえば、「increase text size」を検索して、エディターのフォントサイズを制御する設定を見つけることができます。

この機能を有効にするには、`setting(workbench.settings.showAISearchToggle)`設定を使用します。その後、設定エディターで**Search Settings with AI**ボタンを使用して、AI検索結果のオン/オフを切り替えられます。

![設定に対するAI生成の提案が表示されている設定エディターのスクリーンショット。](images/copilot-smart-actions/settings-suggestions.png)

## 関連リソース

* [Copilot Quickstartを開始する](/docs/copilot/getting-started.md)。
