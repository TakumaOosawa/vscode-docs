---
ContentId: 9d8f3a2b-5c6e-4f7a-8b9c-1d2e3f4a5b6c
DateApproved: 12/10/2025
MetaDescription: コードの生成、デバッグ、テスト、Notebookの操作など、さまざまなシナリオにおけるVS Codeでのチャットの効果的なプロンプト例を紹介します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでのチャットのプロンプト例

この記事では、さまざまなシナリオやエージェントにおけるVisual Studio Codeでのチャットのプロンプト例を紹介します。これらの例を参考に、ご自身の開発タスクに合わせた効果的なプロンプトを作成してください。

VS Codeでのチャットの使用が初めての場合は、[チャットを始める](/docs/copilot/chat/copilot-chat.md)について学ぶか、[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)を確認してください。

## 一般的なコーディングと技術に関する質問

VS Codeのチャットを使用して、コーディングの概念、技術的なトピック、一般的なプログラミングの質問に対する回答をすばやく得ることができます。

```prompt
リンクリストとは何ですか？
```

```prompt
Reactで検索機能を実装する3つの方法を教えてください。
```

```prompt
async/awaitとPromiseの違いを説明してください。
```

## コードベースの理解と探索

VS Codeのチャットを使用して、プロジェクトの仕組みを理解したり、特定の機能を見つけたり、コードの関係を調べたりすることができます。

```prompt
#codebase で認証がどのように機能するか説明してください。
```

```prompt
データベース接続文字列はどこで構成されていますか？ #codebase
```

```prompt
この #codebase はどのようにビルドしますか？
```

```prompt
#calculator.test.js にはどのテストフレームワークが使用されていますか？
```

## コードの生成と編集

VS Codeのチャットを使用して、新しいコードの生成、機能の追加、または既存の機能の変更を行うことができます。

```prompt
ログインボタンを追加し、 #styles.css に基づいてスタイルを設定してください。
```

```prompt
ReactとNode.jsを使用して、食事計画Webアプリを作成してください。
```

```prompt
このコードをasync/awaitを使用するようにリファクタリングしてください。
```

## テストと品質保証

VS Codeのチャットを使用して、テストを生成したり、失敗したテストを修正したりすることができます。

```prompt
ユーザーサービスの単体テストを追加してください。
```

```prompt
失敗しているテストを修正してください #testFailure
```

## デバッグと問題の修正

VS Codeのチャットを使用して、コード内の特定の問題を特定し、修正することができます。

```prompt
#problems の問題を修正してください
```

```prompt
失敗しているテストを修正してください #testFailure
```

```prompt
この関数がundefinedを返すのはなぜですか？
```

## ソース管理の操作

VS Codeのチャットを使用して、保留中の変更を処理したり、リリースのドキュメントを生成したりすることができます。

```prompt
#changes を要約してください
```

```prompt
#changes に基づいてリリースノートを生成してください
```

```prompt
#changes の変更を要約してください
```

## 外部リソースとの連携

VS Codeのチャットを使用して、ウェブやGitHubリポジトリのコンテンツを参照することができます。

```prompt
React 18で 'useState' フックを使用するにはどうすればよいですか？ #fetch https://18.react.dev/reference/react/useState#usage
```

```prompt
#githubRepo contoso/api-templates のテンプレートを使用して、住所情報を取得するAPIエンドポイントを構築してください
```

```prompt
このワークスペースの上位の #extensions は何ですか？
```

## ターミナルとコマンドラインタスク

ターミナルのインラインチャットを使用して、シェルコマンドやターミナル操作に関するヘルプを得ることができます。

```prompt
npmパッケージをインストールするにはどうすればよいですか？
```

```prompt
srcディレクトリ内のサイズが大きいファイル上位5つをリストしてください
```

```prompt
最後のgitコミットを取り消してください
```

## Jupyter Notebookの操作

VS Codeのチャットを使用して、Jupyter Notebookを作成、編集、操作することができます。

```prompt
/newNotebook pandasとseabornを使用して、タイタニックデータセットを読み込み、視覚化してください。データセットの重要な情報を表示してください。
```

```prompt
#housing.csv からデータを読み込み、価格の分布をプロットするノートブックを作成してください
```

```prompt
視覚化と処理を行う前に、データがクリーニングされていることを確認してください
```

```prompt
データセット内のさまざまな特徴間の相関関係を表示してください
```

## 効果的なプロンプトを作成するためのヒント

* **具体的にする**: 達成したいこと、使用する技術、期待される出力形式などの詳細を含めます。
* **コンテキストを追加する**: `#-mentions`を使用して、ファイル、シンボル、または`#codebase`、`#changes`、`#problems`などのコンテキスト変数を参照します。
* **反復する**: 簡単なプロンプトから始めて、回答に基づいて改良します。結果を改善するためにフォローアップの質問をします。
* **複雑なタスクを分割する**: 一度にすべてを求めるのではなく、大きなタスクを小さく管理しやすいステップに分割します。

[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)や[プロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)方法については、詳細をご覧ください。

## 関連リソース

* GitHubドキュメントの[Copilotチャットクックブック](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat)

* [チャットプロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)
