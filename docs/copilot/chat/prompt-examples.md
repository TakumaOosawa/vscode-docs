---
ContentId: 9d8f3a2b-5c6e-4f7a-8b9c-1d2e3f4a5b6c
DateApproved: 3/9/2026
MetaDescription: VS Codeのチャットで、コード生成、デバッグ、テスト、ノートブック操作など、さまざまなシナリオで使用できる効果的なプロンプト例を見つけてください。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# プロンプト例

この記事では、Visual Studio Codeのチャットにおける、さまざまなシナリオとエージェント向けの例示プロンプトを提供しています。これらの例を参考に、自分の開発タスクに適した効果的なプロンプトを作成してください。

VS Codeのチャットを初めて使う場合は、[チャット入門](/docs/copilot/chat/copilot-chat.md)について詳しく確認するか、[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)を参照してください。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェント入門">
VS Codeでローカル、バックグラウンド、クラウドエージェントを体験できるハンズオンチュートリアルをご利用ください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## 一般的なコーディングと技術に関する質問

**Ask**エージェントを使用して、コーディングの概念、技術トピック、一般的なプログラミング質問に関する迅速な回答を得られます。

```prompt-ask
リンクリストとは何ですか？
```

```prompt-ask
Reactで検索機能を実装する3つの方法を紹介してください。
```

```prompt-ask
async/awaitとPromiseの違いを説明してください。
```

## コードベースの理解と探索

`#codebase`を使用した**Ask**エージェントを使用して、プロジェクトの動作を理解したり、特定の機能を見つけたり、コード間の関係を探索したりできます。

```prompt-ask
#codebaseでの認証の仕組みを説明してください
```

```prompt-ask
データベース接続文字列はどこで設定されていますか？#codebase
```

```prompt-ask
この#codebaseはどのようにビルドしますか？
```

```prompt-ask
#calculator.test.jsではどのテストフレームワークが使用されていますか？
```

## コード生成と編集

複数ファイルの作成には**Agent**を使用し、対象を絞った所定の場所での編集には**インラインチャット**(`kb(inlinechat.start)`)を使用してください。

```prompt
#styles.cssに基づいて、ログインボタンを追加してスタイルを設定してください
```

```prompt
ReactとNode.jsを使用した食事計画Webアプリを作成してください
```

```prompt
このコードをasync/awaitを使用するようにリファクタリングしてください
```

## テストと品質保証

**Agent**を使用してテストを生成したり、失敗したテストを修正したりできます。

```prompt
ユーザーサービスのユニットテストを追加してください。
```

```prompt
失敗しているテストを修正してください #testFailure
```

## デバッグと問題の修正

複数のファイルにまたがる問題の修正には**Agent**を使用するか、根本原因を理解するには**Ask**を使用してください。

```prompt
#problemsの問題を修正してください
```

```prompt
この関数がundefinedを返しているのはなぜですか？
```

## ソース管理の操作

チャットを使用してペンディング中の変更を操作し、リリースドキュメンテーションを生成できます。

```prompt
#changesを要約してください
```

```prompt
#changesに基づいてリリース ノートを生成してください
```

## 外部リソースの操作

`#fetch`と`#githubRepo`を使用して、ウェブやGitHubリポジトリのコンテンツを参照できます。

```prompt
React18で'useState'フック使用方法は？#fetch https://18.react.dev/reference/react/useState#usage
```

```prompt
#githubRepoのcontoso/api-templatesのテンプレートを使用して、アドレス情報を取得するAPIエンドポイントを構築してください
```

```prompt
このワークスペースの上位#extensionsは何ですか？
```

## ターミナルとコマンドラインのタスク

[ターミナルインラインチャット](/docs/copilot/chat/inline-chat.md#use-terminal-inline-chat)を使用して、シェルコマンドとターミナル操作に関するサポートを受けられます。

```prompt
npmパッケージをインストールするにはどうすればよいですか？
```

```prompt
srcディレクトリ内の最大5つの大きなファイルをリストアップしてください
```

```prompt
直前のgitコミットを取り消してください
```

## Jupyterノートブックの操作

**Agent**を使用して、Jupyterノートブックを作成、編集、操作を行えます。

```prompt
/newNotebook pandasとseabornを使用してtitanicデータセットを読み込んで可視化します。データセットから主要な情報を表示してください。
```

```prompt
#housing.csvからデータを読み込み、価格の分布をプロットするノートブックを作成してください
```

```prompt
可視化と処理を行う前に、データが整理されていることを確認してください
```

```prompt
データセット内の異なる機能間の相関関係を表示してください
```

## 複数ターンの会話例

チャットは同じセッション内では、フォローアップ プロンプトをサポートします。複数ターンの会話を使用して、結果を反復処理し、AIの出力を洗練させることができます。

**最初のプロンプト:**

```prompt
Express.jsでユーザーとプロダクト用のエンドポイントを持つREST APIを作成してください
```

**フォローアップ プロンプト:**

```prompt
両方のエンドポイントに入力検証とエラー処理を追加してください
```

```prompt
次に検証ロジックのユニットテストを追加してください
```

以前の応答に基づいて、AIは前のステップのコンテキストを維持し、より首尾一貫したコードを生成します。

## 効果的なプロンプトを作成するためのヒント

* **具体的に**: 達成したいこと、使用する技術、期待される出力形式の詳細を含めてください。
* **コンテキストを追加**: #-mentions を使用してファイル、シンボル、または`#codebase`、`#changes`、`#problems`などのコンテキスト変数を参照してください。
* **反復処理**: シンプルなプロンプトから始めて、応答に基づいてそれを洗練させてください。フォローアップの質問をして結果を改善してください。
* **複雑なタスクを細分化**: すべてを一度に依頼するのではなく、大規模なタスクをより小さく管理しやすいステップに分割してください。

詳しくは、[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)と[プロンプトにコンテキストを追加する](/docs/copilot/chat/copilot-chat-context.md)をご覧ください。

## 関連リソース

* [チャット概要](/docs/copilot/chat/copilot-chat.md)
* [チャット プロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)
* [インラインチャット](/docs/copilot/chat/inline-chat.md)
* [Copilot Chat Cookbook](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat) (GitHub ドキュメント内)

