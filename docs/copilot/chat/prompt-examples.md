---
ContentId: 9d8f3a2b-5c6e-4f7a-8b9c-1d2e3f4a5b6c
DateApproved: 12/10/2025
MetaDescription: コード生成、デバッグ、テスト、ノートブックでの作業など、さまざまなシナリオにわたるVS Codeのチャット向けの効果的なプロンプト例を紹介します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeのチャット向けプロンプト例

この記事では、さまざまなシナリオとエージェントにわたるVisual Studio Codeのチャット向けプロンプト例を紹介します。これらの例を参考にして、自分の開発タスクに対して効果的なプロンプトを作成してください。

VS Codeでチャットを使うのが初めての場合は、[チャットの概要](/docs/copilot/chat/copilot-chat.md)を参照するか、[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)を確認してください。

## 一般的なコーディングと技術に関する質問

VS Codeのチャットを使用して、コーディングの概念、技術トピック、一般的なプログラミングの質問について素早く回答を得ましょう。

```prompt
連結リストとは何ですか？
```

```prompt
Reactで検索機能を実装する方法を3つ挙げてください。
```

```prompt
async/awaitとPromiseの違いを説明してください。
```

## コードベースの理解と探索

VS Codeのチャットを使用して、プロジェクトの仕組みを理解したり、特定の機能の場所を探したり、コード間の関係を調べたりできます。

```prompt
#codebaseで認証がどのように動作するか説明してください
```

```prompt
データベースの接続文字列はどこで設定されていますか？ #codebase
```

```prompt
この#codebaseはどのようにビルドしますか？
```

```prompt
#calculator.test.jsで使用されているテストフレームワークは何ですか？
```

## コード生成と編集

VS Codeのチャットを使用して、新しいコードの生成、機能の追加、既存機能の変更を行えます。

```prompt
#styles.cssに基づいてログインボタンを追加してスタイルを適用してください
```

```prompt
ReactとNode.jsを使用して献立作成用のWebアプリを作成してください
```

```prompt
このコードをasync/awaitを使うようにリファクタリングしてください
```

## テストと品質保証

VS Codeのチャットを使用して、テストの生成や失敗しているテストの修正を行えます。

```prompt
ユーザーサービスの単体テストを追加してください。
```

```prompt
#testFailureの失敗しているテストを修正してください
```

## デバッグと問題の修正

VS Codeのチャットを使用して、コード内の問題を特定して修正できます。

```prompt
#problemsにある問題を修正してください
```

```prompt
#testFailureの失敗しているテストを修正してください
```

```prompt
この関数がundefinedを返しているのはなぜですか？
```

## ソース管理での作業

VS Codeのチャットを使用して、保留中の変更を扱ったり、リリースドキュメントを生成したりできます。

```prompt
#changesを要約してください
```

```prompt
#changesに基づいてリリースノートを生成してください
```

```prompt
#changes内の変更を要約してください
```

## 外部リソースでの作業

VS Codeのチャットを使用して、WebやGitHubリポジトリのコンテンツを参照できます。

```prompt
React 18で'useState'フックはどのように使いますか？ #fetch https://18.react.dev/reference/react/useState#usage
```

```prompt
住所情報を取得するAPIエンドポイントを作成してください。#githubRepo contoso/api-templatesのテンプレートを使用してください
```

```prompt
このワークスペースでおすすめの#extensionsは何ですか？
```

## ターミナルとコマンドラインのタスク

ターミナルのインラインチャットを使用して、シェルコマンドやターミナル操作の支援を受けることができます。

```prompt
npmパッケージはどのようにインストールしますか？
```

```prompt
srcディレクトリ内でサイズが大きいファイル上位5つを一覧表示してください
```

```prompt
最後のgit commitを取り消してください
```

## Jupyterノートブックでの作業

VS Codeのチャットを使用して、Jupyterノートブックの作成、編集、作業を行えます。

```prompt
/newNotebook pandasとseabornを使用してtitanicデータセットを読み込み、可視化してください。データセットの主要な情報を表示してください。
```

```prompt
#housing.csvからデータを読み込み、価格の分布をプロットするノートブックを作成してください
```

```prompt
可視化と処理の前にデータがクリーンになっていることを確認してください
```

```prompt
データセット内の異なる特徴量間の相関を表示してください
```

## 効果的なプロンプトを作成するためのヒント

* **具体的にする**: 達成したいこと、使用する技術、期待する出力形式の詳細を含めてください。
* **コンテキストを追加する**: #-mentionsを使用して、ファイル、シンボル、または`#codebase`、`#changes`、`#problems`などのコンテキスト変数を参照してください。
* **反復する**: シンプルなプロンプトから始め、応答に基づいて改善してください。結果を良くするために追加の質問をしてください。
* **複雑なタスクを分割する**: 一度にすべてを求めるのではなく、大きなタスクを小さく管理しやすい手順に分割してください。

[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)と[プロンプトへのコンテキストの追加](/docs/copilot/chat/copilot-chat-context.md)の詳細をご覧ください。

## 関連リソース

* GitHubドキュメントの[Copilot Chat Cookbook](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat)

* [チャットプロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)
