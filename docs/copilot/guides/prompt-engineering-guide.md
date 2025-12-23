---
ContentId: 5dfd207f-fcee-42c3-b7fe-622b42b3397c
DateApproved: 12/10/2025
MetaDescription: VS Codeのチャットにおけるプロンプト作成とコンテキスト提供のベストプラクティスで、開発体験を最適化します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Codeでのプロンプトエンジニアリング

この記事では、Visual Studio CodeでAIからより良く、より関連性の高い応答を得るためにプロンプトを書くコツを紹介します。_Prompt engineering_または_prompt crafting_は、AIについて議論するときによく耳にする表現で、どのように、そしてどの情報をパッケージ化してAI APIエンドポイントへ送るかを指します。

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/hh1nOX14TyY" title="GitHub Copilotでのプロンプトエンジニアリングの基本原則" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

VS CodeやAIが初めての場合は、まず[VS CodeのAI概要](/docs/copilot/overview.md)の記事を確認するか、[はじめに](/docs/copilot/getting-started.md)チュートリアルにそのまま進むとよいでしょう。

## インライン候補を最大限に活用する

インライン候補は、コード、コメント、テストなどを完成させるための提案を自動で提示し、より効率的にコーディングできるようにします。AIが可能な限り最適な候補を出せるようにするために、できること（「プロンプトする」こと）があります。

### コンテキストを提供する

AIは、あなたが何をしていて何の助けが必要かを理解するための十分なコンテキストがあるときに最も良く機能します。特定のプログラミング作業で助けを求めるときに同僚へコンテキストを渡すのと同じように、AIにも同様に渡すことができます。

#### ファイルを開く

インライン候補では、VS Codeがエディター内の現在のファイルと開いているファイルを見てコンテキストを分析し、適切な候補を作成します。インライン候補を使うときにVS Codeで関連ファイルを開いておくと、このコンテキストを整えるのに役立ち、AIがプロジェクトの全体像をより把握できるようになります。

#### トップレベルコメント

同僚に簡潔で高レベルな概要を伝えるのと同様に、作業中のファイルにトップレベルコメントを書いておくと、AIが作成している要素の全体的なコンテキストを理解するのに役立ちます。

#### 適切なインクルードと参照

作業に必要なインクルードやモジュール参照は手動で設定するのが最善です。AIも提案はできますが、どの依存関係を含めるべきかはあなたが最もよく知っているはずです。これは、候補を作る際に使用してほしいフレームワークやライブラリ、およびそのバージョンをAIに伝える助けにもなります。

次のTypeScriptの例では、`add`メソッドの出力をログに記録したいとします。インクルードがない場合、AIは`console.log`の使用を提案します。

![AI inline suggestion proposes Console.log when no imports in the file.](../images/prompt-engineering-guide/copilot-suggestion-console-log.png)
一方、`Log4js`への参照を追加すると、AIはそのフレームワークを使って出力をログに記録することを提案します。

![AI inline suggestion proposes logging using the imported logging framework.](../images/prompt-engineering-guide/copilot-suggestion-framework-log.png)

#### 意味のある関数名

`fetchData()`というメソッド名は、同僚（あるいは数か月後のあなた）にとってあまり意味がないのと同じで、AIにとっても`fetchData()`は役に立ちません。意味のある関数名を使うことで、AIが意図どおりの処理を行う本体を提供しやすくなります。

#### 具体的でスコープが適切な関数コメント

関数名は、過度に長くしない限り説明できる範囲に限界があります。関数コメントは、AIが知っておく必要があるかもしれない詳細を補うのに役立ちます。
<!-- Example of a meaningful function/method comment -->

#### サンプルコードでAIを事前に慣らす

AIの前提を合わせるための1つのコツは、探しているものに近いサンプルコードを、開いているエディターにコピー＆ペーストすることです。小さな例を示すことで、AIがあなたの使いたい言語や達成したいタスクに合った候補を生成しやすくなります。AIが実際に使うコードを提示し始めたら、そのサンプルコードはファイルから削除できます。これは、AIが古いコード候補を既定で出してしまう場合に、新しいライブラリバージョンへ素早く誘導するのに特に有効です。

### 一貫性を保ち、品質基準を高く保つ

AIは既存のパターンに従う候補を生成するためにあなたのコードを手がかりにするので、「garbage in, garbage out」という格言が当てはまります。
常に品質基準を高く保つには規律が必要なことがあります。特に、まず動くものを作るためにスピーディーにラフにコーディングしているときは、「hacking」モードの間は補完を無効にしたくなるかもしれません。インライン候補を一時的にスヌーズするには、ステータスバーのCopilotメニューを選択し、**Snooze**ボタンを選択してスヌーズ時間を5分増やします。インライン候補を再開するには、Copilotメニューで**Cancel Snooze**ボタンを選択します。

![Screenshot of the Copilot menu in the Status Bar with Snooze and Cancel Snooze buttons.](../images/inline-suggestions/snooze-code-completions.png)

## チャットを最大限に活用する

チャットを使用しているとき、体験を最適化するためにできることがいくつかあります。

### 関連するコンテキストを追加する

言及したいコンテキスト項目の前に`#`を付けて入力すると、プロンプトに明示的にコンテキストを追加できます。VS Codeは、ファイル、フォルダー、コードシンボル、ツール、ターミナル出力、ソース管理の変更など、さまざまな種類のコンテキスト項目をサポートしています。

チャットの入力欄で`#`記号を入力すると利用可能なコンテキスト項目の一覧が表示されます。または、Chatビューで**Add Context**を選択してコンテキストピッカーを開きます。

たとえば、`#<file name>`や`#<folder name>`を使うと、チャットプロンプトでワークスペース内の特定のファイルやフォルダーを参照できます。これにより、作業中のファイルに関するコンテキストを提供できるため、Copilot Chatからの回答があなたのコードにより関連したものになります。「#package.jsonの改善点を提案できますか？」や「#devcontainer.jsonに拡張機能を追加するにはどうすればよいですか？」のように質問できます。

個々のファイルを手動で追加する代わりに、`#codebase`を使ってVS Codeにコードベースから適切なファイルを自動的に見つけさせることができます。どのファイルが質問に関連するかわからない場合に便利です。

![Screenshot of Chat view, showing the Attach context button and context Quick Pick.](../images/prompt-engineering-guide/copilot-chat-view-attach-context.png)

[チャットでコンテキストを使用する](/docs/copilot/chat/copilot-chat-context.md)の詳細を参照してください。

### 具体的にし、シンプルに保つ

チャットに何かを依頼するときは、依頼内容を具体的にし、大きなタスクを個別の小さなタスクに分解してください。たとえば、TypeScriptとPugを使い、MongoDBデータベースからデータを取得するproductsページを持つExpressアプリを作成してほしい、といった依頼を一度にしないでください。代わりに、まずTypeScriptとPugでExpressアプリを作成するよう依頼します。次にproductsページを追加するよう依頼し、最後にデータベースから顧客データを取得するよう依頼します。

チャットに特定のタスクを依頼するときは、使用したい入力、出力、API、またはフレームワークを具体的に示してください。プロンプトが具体的であるほど、結果は良くなります。たとえば、「データベースから製品データを読み取る」ではなく、「カテゴリ別にすべての製品を読み取り、JSON形式でデータを返し、Mongooseライブラリを使用する」とします。

### 解決策を反復する

チャットに助けを求めるとき、最初の応答に縛られる必要はありません。反復して、解決策を改善するようチャットに促すことができます。チャットは、生成されたコードのコンテキストと現在の会話の両方を持っています。
次は、Inline Chatを使ってフィボナッチ数を計算する関数を作成する例です。

![フィボナッチ数を計算する関数に対するAIの最初の応答](../images/prompt-engineering-guide/fibonacci-first.png)

再帰を使わない解決策のほうがよいかもしれません。

![AIに再帰を使わないよう依頼し、新しい結果を得る](../images/prompt-engineering-guide/fibonacci-second.png)

コーディング規約に従うように、または変数名を改善するようにAIへ依頼することもできます。

![AIにより良い変数名を使うよう依頼し、新しい結果を得る](../images/prompt-engineering-guide/fibonacci-third.png)

すでに結果を受け入れていたとしても、後からいつでもAIにコードの改善を依頼できます。

## Copilotのプロンプトに関するその他のリソース

GitHub Copilotを生産的に活用する方法をさらに学びたい場合は、次の動画やブログ記事をご覧ください。

* [GitHub Copilotの効果的なプロンプト](https://www.youtube.com/watch?v=ImWfIDTxn7E)
* [GitHub Copilotを最大限に活用するための実践的なテクニック](https://www.youtube.com/watch?v=CwAzIpc4AnA)
* [VS CodeでGitHub Copilotにプロンプトを与えるためのベストプラクティス](https://www.linkedin.com/pulse/best-practices-prompting-github-copilot-vs-code-pamela-fox)
* [GitHub Copilotの使い方: プロンプト、ヒント、ユースケース](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/)
