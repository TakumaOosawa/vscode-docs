---
ContentId: 9d8f3a2b-5c6e-4f7a-8b9c-1d2e3f4a5b6c
DateApproved: 3/9/2026
MetaDescription: VS Code のチャットで異なるシナリオ (コード生成、デバッグ、テスト、ノートブック操作など) にわたる効果的なプロンプト例を発見してください。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# プロンプト例

この記事では、Visual Studio Code のチャットの異なるシナリオとエージェント全体にわたるプロンプト例を提供します。これらの例を参考にして、独自の開発タスク用の効果的なプロンプトを作成してください。

VS Code のチャットを初めて使用する場合は、[チャットの概要](/docs/copilot/chat/copilot-chat.md)の詳細を確認するか、[プロンプトエンジニアリングのベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)を確認してください。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントの概要">
VS Code でローカル、バックグラウンド、クラウドエージェントを体験するための実習ガイドに従ってください。

* [チュートリアルを開始](/docs/copilot/agents/agents-tutorial.md)

</div>

## 一般的なコーディングと技術の質問

**Ask**エージェントを使用して、コーディング概念、技術トピック、および一般的なプログラミングの質問に関する簡単な回答を取得します。

```prompt-ask
リンクリストとは何ですか?
```

```prompt-ask
React で検索機能を実装する3つの方法を提供してください。
```

```prompt-ask
async/await と promise の違いを説明してください。
```

## コードベースの理解と探索

`#codebase`を使用して**Ask**エージェントを使用して、プロジェクトの動作方法を理解したり、特定の機能を見つけたり、コード関係を探索したりします。

```prompt-ask
#codebase で認証がどのように機能するかを説明してください
```

```prompt-ask
データベース接続文字列はどこで構成されていますか? #codebase
```

```prompt-ask
この #codebase をビルドするにはどうすればよいですか?
```

```prompt-ask
#calculator.test.js にはどのテストフレームワークが使用されていますか?
```

## コード生成と編集

複数ファイルの作成には**Agent**を、ターゲット化した場所での編集には**インラインチャット**(`kb(inlinechat.start)`)を使用します。

```prompt
#styles.css に基づいてログインボタンを追加してスタイルを設定します
```

```prompt
React と Node.js を使用して食事計画 web アプリを作成します
```

```prompt
このコードをasync/await を使用するようにリファクタリングします
```

## テストと品質保証

**Agent**を使用してテストを生成するか、失敗しているテストを修正します。

```prompt
ユーザーサービスの単位テストを追加します。
```

```prompt
失敗しているテスト #testFailure を修正します
```

## デバッグと問題の修正

ファイル全体での問題を修正するには**Agent**を使用するか、根本原因を最初に理解するには**Ask**を使用します。

```prompt
#problems の問題を修正します
```

```prompt
この関数が undefined を返す理由は何ですか?
```

## ソース管理の操作

チャットを使用して保留中の変更を操作し、リリースドキュメントを生成します。

```prompt
#changes を要約します
```

```prompt
#changes に基づいてリリースノートを生成します
```

## 外部リソースの操作

`#fetch`と`#githubRepo`を使用して、Web または GitHub リポジトリからコンテンツを参照します。

```prompt
React 18 で 'useState' フックを使用する方法は? #fetch https://18.react.dev/reference/react/useState#usage
```

```prompt
アドレス情報をフェッチするAPI エンドポイントを構築し、#githubRepo contoso/api-templates のテンプレートを使用します
```

```prompt
このワークスペースの上位 #extensions は何ですか?
```

## ターミナルとコマンドラインのタスク

[ターミナルインラインチャット](/docs/copilot/chat/inline-chat.md#use-terminal-inline-chat)を使用して、シェルコマンドとターミナル操作に関するヘルプを取得します。

```prompt
npm パッケージをインストールするにはどうすればよいですか?
```

```prompt
src ディレクトリで最大の5つのファイルをリストします
```

```prompt
最後の git コミットを元に戻します
```

## Jupyter ノートブックの操作

**Agent**を使用して、Jupyter ノートブックを作成、編集、および操作します。

```prompt
/newNotebook pandas と seaborn を使用してタイタニック データセットを読み込んで視覚化します。データセットから重要な情報を表示します。
```

```prompt
#housing.csv からデータを読み込み、価格の分布をプロットするノートブックを作成します
```

```prompt
視覚化と処理の前にデータがクリーンであることを確認します
```

```prompt
データセット内のさまざまな機能間の相関を表示します
```

## 複数ターン会話の例

チャットは同じセッション内での後続のプロンプトをサポートします。複数ターンの会話を使用して、結果を反復処理し、AI の出力を改善します。

**最初のプロンプト:**

```prompt
ユーザーとプロダクト用にエンドポイントを持つ Express.js を使用して REST API を作成します
```

**後続のプロンプト:**

```prompt
入力検証とエラーハンドリングの両方のエンドポイントに追加します
```

```prompt
検証ロジックの単位テストを追加します
```

前の応答に基づいて構築することで、AI は前のステップからコンテキストを維持し、より一貫性のあるコードを生成します。

## 効果的なプロンプトを作成するためのヒント

* **具体的にしてください**: 実現したいこと、使用するテクノロジー、および期待される出力形式に関する詳細を含めてください。
* **コンテキストを追加してください**: #-mentions を使用して、ファイル、シンボル、または`#codebase`、`#changes`、`#problems`などのコンテキスト変数を参照します。
* **反復してください**: 簡単なプロンプトで開始し、応答に基づいて精緻化します。フォローアップの質問をして結果を改善します。
* **複雑なタスクを分割してください**: すべてを一度に求める代わりに、大きなタスクを小さくて管理可能なステップに分割します。

[プロンプト作成のベストプラクティス](/docs/copilot/guides/prompt-engineering-guide.md)と[プロンプトへのコンテキストの追加](/docs/copilot/chat/copilot-chat-context.md)の詳細を確認してください。

## 関連リソース

* [チャットの概要](/docs/copilot/chat/copilot-chat.md)
* [チャットプロンプトにコンテキストを追加](/docs/copilot/chat/copilot-chat-context.md)
* [インラインチャット](/docs/copilot/chat/inline-chat.md)
* [GitHub Copilot Chat クックブック](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat)in the GitHub documentation

