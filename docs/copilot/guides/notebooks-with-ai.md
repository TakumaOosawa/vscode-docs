---
ContentId: 101027aa-e73c-4d1b-a93f-b8ce10e1f946
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotを使用して、AIでJupyterノートブックを編集する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでAIを使ってJupyterノートブックを編集する

Visual Studio Codeは、[Jupyterノートブック](/docs/datascience/jupyter-notebooks.md)をネイティブにサポートしており、[Pythonコードファイル](/docs/python/jupyter-support-py.md)を通じても利用できます。VS CodeのAI機能は、ノートブックの作成と編集に加えて、データの分析と視覚化にも役立ちます。この記事では、VS CodeのAI機能を使用してJupyterノートブックを操作する方法について説明します。

## 新しいノートブックをスキャフォールドする

新しいノートブックをすばやく始めるために、VS CodeのAI機能を使用して新しいノートブックをスキャフォールドできます。自然言語で、追加したい機能や使用したいライブラリの詳細を伝えます。

AIで新しいノートブックを作成するには、次のいずれかのオプションを選択します。

* チャットの入力ボックスに`/newNotebook`スラッシュコマンドを入力し、作成するノートブックの詳細を続けて入力します。

* [Agent](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択し、新しいノートブックを作成するように自然言語のプロンプトを入力します。

効果的なノートブック用プロンプトについては、[プロンプトの例](/docs/copilot/chat/prompt-examples.md#working-with-jupyter-notebooks)の記事を参照してください。

次のスクリーンショットは、Agentに対して*#housing.csvからデータを読み取るJupyterノートブックを作成してください*というプロンプトを入力したときの出力を示しています(このデータセットは[Kaggle](https://www.kaggle.com/search?q=housing+dataset+in%3Adatasets)から入手できます)。

![ワークスペース内の'housing.csv'ファイルを読み取る新しいノートブックがAgentによって作成されたことを示すスクリーンショット。](../images/notebooks-with-ai/agent-mode-create-new-notebook.png)

新しい`.ipynb`ファイルが作成され、CSVファイルを読み取り、データの最初の数行を表示するためのMarkdownセルとコードセルが含まれていることがわかります。

これで、ノートブックを手動でさらに編集することも、AIを使用してインライン編集を行ったり、フォローアップのチャットリクエストを送ってノートブックを変更したりすることもできます。

## ノートブックのセルでインライン編集を行う

すでにノートブックがあり、セル内でインラインの変更を加えたい場合は、コードファイルの場合と同様にインラインチャットを使用できます。

セルでインライン編集を行うには、`kb(notebook.cell.chat.start)`を押します。これによりインラインチャットビューが開き、プロンプトを入力できます。

> [!TIP]
> チャットプロンプト内でカーネル変数を参照できます。`#`に続けて変数名を入力して参照します。たとえば、`df`という名前の変数がある場合は、チャットプロンプトに`#df`と入力して参照できます。

![ノートブックのセル内にあるインラインチャットビューを示すスクリーンショット。](../images/notebooks-with-ai/notebook-inline-chat.png)

応答が生成されると、ノートブックのセル内のコードが更新されていることがわかります。変更を**承諾**し、セルの変更を**承諾して実行**するかどうかを選べます。

AIで新しいセルを生成するには、ノートブックビューで**Generate**ボタンを選択するか、セルにフォーカスしない状態で`kb(notebook.cell.chat.start)`を押して、新しいセル用のインラインチャットビューを開きます。

## 複数のセルにまたがる編集を行う

複数のセルにまたがる大きな編集を行うには、チャットビューで[agents](vscode://GitHub.Copilot-Chat/chat?mode=agent)を使用するように切り替えます。ノートブックへの変更を依頼するプロンプトを入力すると、Agentがタスクを反復して変更を実装します。

![チャットで'価格分布のグラフをプロットする'というプロンプトに対する応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-plot-prices.png)

オーバーレイコントロールを使用して、さまざまな編集提案の間を移動したり、変更を保持または元に戻したりできることがわかります。

## ノートブックの内容について質問する

チャットインターフェイスを使用して、ノートブックの内容について質問できます。これは、コード、データ、または視覚化についての説明を得るのに役立ちます。セルの出力、グラフ、またはエラーなどの追加のコンテキストをチャットリクエストに加えることができます。

次の例では、ノートブック内の視覚化について質問する方法を示します。

1. グラフの横にある`...`を選択し、**Add Cell Output to Chat**を選択して、チャットリクエストのコンテキストとしてチャートを追加します。

    ![ノートブックのセル内のグラフのコンテキストメニューを示すスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-add-cell-output.png)

1. チャット入力フィールドに*このチャートを説明してください*というプロンプトを入力します。

    チャートの詳細な説明が得られることがわかります。

    !['このチャートを説明してください'というプロンプトに対するチャットの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-explain-chart.png)

## データ分析と視覚化を実行する

チャットでagentsを使用すると、データセットの完全なデータ分析および視覚化ノートブックを作成できます。Agentはデータセットを分析し、その後、新しいノートブックをスキャフォールドし、データ分析を実行するためのコードを実装し、セルを実行してデータを処理および視覚化します。必要に応じて、Agentは関連するツールやターミナルコマンドを呼び出してタスクを完了します。

たとえば、housingデータセットのデータ分析を実行するには、次のようにします。

1. チャットビューのエージェントピッカーから[Agent](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択します。

1. チャット入力フィールドに次のプロンプトを入力します。*#housing.csv内のデータのデータ分析を実行してください*。

    Agentがさまざまなタスクを反復して進めることがわかります。必要に応じて、ツールとコマンドの呼び出しを承認します。
1. The result is a new notebook with a complete data analysis of the dataset, including data cleaning, data visualization, and statistical analysis.

    ![チャットで'housing.csv内のデータのデータ分析を実行する'というプロンプトに対する応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-data-analysis.png)

これで、ノートブックを手動でさらに編集することも、AIを使用してインライン編集を行ったり、フォローアップのチャットリクエストを送ってノートブックを変更したりすることもできます。

## 次のステップ

* [VS CodeでのJupyterノートブックについて詳しく学ぶ](/docs/datascience/jupyter-notebooks.md)
* [VS CodeのAI機能について詳しく学ぶ](/docs/copilot/overview.md)
* [VS Codeのチャットについて詳しく学ぶ](/docs/copilot/chat/copilot-chat.md)
