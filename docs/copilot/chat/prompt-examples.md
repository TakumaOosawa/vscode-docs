---
ContentId: 9d8f3a2b-5c6e-4f7a-8b9c-1d2e3f4a5b6c
DateApproved: 01/08/2026
MetaDescription: コード生成、デバッグ、テスト、ノートブックでの作業など、さまざまなシナリオにわたるVS Codeでのチャットの効果的なプロンプト例を紹介します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでのチャットのプロンプト例

この記事では、Visual Studio Codeでのチャットのさまざまなシナリオやエージェントにわたるプロンプトの例を紹介します。これらの例をヒントにして、独自の開発タスクに合わせて効果的なプロンプトを作成してください。

VS Codeでのチャットを初めて使用する場合は、[チャットを始める](/docs/copilot/chat/copilot-chat.md)について詳しく学ぶか、[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)を確認してください。

## 一般的なコーディングとテクノロジに関する質問

VS Codeでチャットを使用して、コーディングの概念、テクノロジのトピック、および一般的なプログラミングの質問について、すばやく回答を得ることができます。

```prompt
リンクリストとは何ですか?
```

```prompt
Reactで検索機能を実装する3つの方法を教えてください。
```

```prompt
async/awaitとPromiseの違いを説明してください。
```

## コードベースの理解と探索

VS Codeでチャットを使用して、プロジェクトの仕組みを理解したり、特定の機能を見つけたり、コードの関係を調査したりできます。

```prompt
#codebase で認証がどのように機能するか説明してください
```

```prompt
データベース接続文字列はどこで設定されていますか? #codebase
```

```prompt
この #codebase をビルドする方法を教えてください
```

```prompt
#calculator.test.js にはどのテストフレームワークが使用されていますか?
```

## コードの生成と編集

VS Codeでチャットを使用して、新しいコードを生成したり、機能を追加したり、既存の機能を変更したりできます。

```prompt
ログインボタンを追加し、#styles.css に基づいてスタイルを設定してください
```

```prompt
ReactとNode.jsを使用して食事計画Webアプリを作成してください
```

```prompt
このコードをasync/awaitを使用するようにリファクタリングしてください
```

## テストと品質保証

VS Codeでチャットを使用して、テストを生成したり、失敗したテストを修正したりできます。

```prompt
ユーザーサービスの単体テストを追加してください。
```

```prompt
失敗しているテスト #testFailure を修正してください
```

## デバッグと問題の修正

VS Codeでチャットを使用して、コード内の問題を特定して修正できます。

```prompt
#problems の問題を修正してください
```

```prompt
失敗しているテスト #testFailure を修正してください
```

```prompt
この関数がundefinedを返すのはなぜですか?
```

## ソース管理の操作

VS Codeでチャットを使用して、保留中の変更を処理したり、リリースドキュメントを生成したりできます。

```prompt
#changes を要約してください
```

```prompt
#changes に基づいてリリースノートを生成してください
```

```prompt
#changes の変更内容を要約してください
```

## 外部リソースの使用

VS Codeでチャットを使用して、WebまたはGitHubリポジトリのコンテンツを参照できます。

```prompt
React 18で'useState'フックを使用するにはどうすればよいですか? #fetch https://18.react.dev/reference/react/useState#usage
```

```prompt
住所情報を取得するAPIエンドポイントを構築してください。#githubRepo contoso/api-templatesのテンプレートを使用してください
```

```prompt
このワークスペースの上位の #extensions は何ですか?
```

## ターミナルとコマンドラインタスク

ターミナルのインラインチャットを使用して、シェルコマンドやターミナル操作に関するヘルプを得ることができます。

```prompt
npmパッケージをインストールするにはどうすればよいですか?
```

```prompt
srcディレクトリ内で最も大きい上位5つのファイルを一覧表示してください
```

```prompt
最後のgitコミットを取り消してください
```

## Jupyterノートブックでの作業

VS Codeでチャットを使用して、Jupyterノートブックを作成、編集、操作できます。

```prompt
/newNotebook pandasとseabornを使用してタイタニックデータセットを読み込み、可視化してください。データセットからの重要な情報を表示してください。
```

```prompt
#housing.csv からデータを読み込み、価格の分布をプロットするノートブックを作成してください
```

```prompt
可視化および処理を行う前に、データがクリーンアップされていることを確認してください
```

```prompt
データセット内のさまざまな機能間の相関関係を表示してください
```

## 効果的なプロンプトを作成するためのヒント

* **具体的にする**: 達成したいこと、使用するテクノロジ、期待される出力形式などの詳細を含めます。
* **コンテキストを追加する**: #-メンションを使用して、ファイル、シンボル、または `#codebase`、`#changes`、`#problems` などのコンテキスト変数を参照します。
* **反復する**: シンプルなプロンプトから始めて、応答に基づいて調整します。結果を改善するためにフォローアップの質問をします。
* **複雑なタスクを分割する**: すべてを一度に尋ねるのではなく、大きなタスクを小さく管理しやすいステップに分割します。

[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)と[プロンプトへのコンテキストの追加](/docs/copilot/chat/copilot-chat-context.md)について詳しく学びましょう。

## 関連リソース

* GitHubドキュメントの[Copilot Chatクックブック](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat)

* [チャットプロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)
