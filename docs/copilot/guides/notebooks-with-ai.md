---
ContentId: 101027aa-e73c-4d1b-a93f-b8ce10e1f946
DateApproved: 01/08/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用して、AIでJupyter Notebookを編集する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでAIを使用してJupyter Notebookを編集する

Visual Studio Codeは、[Jupyter Notebook](/docs/datascience/jupyter-notebooks.md)との連携をネイティブでサポートしており、[Pythonコードファイル](/docs/python/jupyter-support-py.md)を通じても利用できます。VS CodeのAI機能は、ノートブックの作成や編集、データの分析や可視化を支援します。この記事では、VS CodeのAI機能を使用してJupyter Notebookを操作する方法について説明します。

## 新しいノートブックをスキャフォールドする

新しいノートブックの作成を迅速に行うために、VS CodeのAI機能を使用して新しいノートブックをスキャフォールドできます。自然言語を使用して、追加したい機能や使用したいライブラリについての詳細を提供します。

AIを使用して新しいノートブックを作成するには、次のいずれかのオプションを選択します：

* チャット入力ボックスに`/newNotebook`スラッシュコマンドを入力し、その後に作成するノートブックの詳細を入力します。

* [エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択し、新しいノートブックの作成を依頼する自然言語プロンプトを入力します。

効果的なノートブックのプロンプトについては、[プロンプトの例](/docs/copilot/chat/prompt-examples.md#working-with-jupyter-notebooks)の記事を参照してください。

次のスクリーンショットは、プロンプト*Create a Jupyter notebook to read data from #housing.csv*（#housing.csvからデータを読み込むJupyter Notebookを作成して）（このデータセットは[Kaggle](https://www.kaggle.com/search?q=housing+dataset+in%3Adatasets)から入手できます）に対するエージェントの出力方法を示しています：

![エージェントによって作成された、ワークスペース内の 'housing.csv' ファイルを読み取る新しいノートブックを示すスクリーンショット。](../images/notebooks-with-ai/agent-mode-create-new-notebook.png)

新しい`.ipynb`ファイルが作成され、CSVファイルを読み取り、データの最初の数行を表示するためのMarkdownとコードセルが含まれていることに注目してください。

これで、ノートブックを手動でさらに編集したり、AIを使用してインライン編集を行ったり、フォローアップのチャットリクエストを送信してノートブックを変更したりできます。

## ノートブックセルでインライン編集を行う

すでにノートブックがあり、セル内でインライン変更を行いたい場合は、コードファイルと同じようにインラインチャットを使用できます。

セル内でインライン編集を行うには、`kb(notebook.cell.chat.start)`を押します。これによりインラインチャットビューが開き、プロンプトを入力できます。

> [!TIP]
> チャットプロンプトでカーネル変数を参照できます。`#`に続けて変数名を入力して参照します。たとえば、`df`という名前の変数がある場合、チャットプロンプトで`#df`と入力して参照できます。

![ノートブックセルのインラインチャットビューを示すスクリーンショット。](../images/notebooks-with-ai/notebook-inline-chat.png)

応答が生成されると、ノートブックセル内のコードが更新されることに注目してください。変更を**承認**し、セルの変更を**承認して実行**するかを決定できます。

AIを使用して新しいセルを生成するには、ノートブックビューの**生成**ボタンを選択するか、セルにフォーカスせずに`kb(notebook.cell.chat.start)`を押して新しいセルのインラインチャットビューを開きます。

## 複数のセルにわたって編集を行う

複数のセルにまたがる大規模な編集を行うには、チャットビューで[エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)の使用に切り替えることができます。ノートブックへの変更を要求するプロンプトを提供すると、エージェントはタスクを反復して変更を実装します。

![プロンプト 'Plot a graph of the price distribution' に対するチャットからの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-plot-prices.png)

オーバーレイコントロールを使用して、さまざまな編集の提案間を移動したり、変更を保持または元に戻したりできることに注目してください。

## ノートブックの内容について質問する

チャットインターフェースを使用して、ノートブックの内容について質問できます。これは、コード、データ、または視覚化の説明を取得するのに役立ちます。セルの出力、グラフ、エラーなどの追加のコンテキストをチャットリクエストに追加できます。

次の例は、ノートブック内の視覚化について質問する方法を示しています。

1. グラフの横にある`...`を選択し、**セルの出力をチャットに追加**を選択して、チャートをコンテキストとしてチャットリクエストに追加します。

    ![ノートブックセル内のグラフのコンテキストメニューを示すスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-add-cell-output.png)

1. チャット入力フィールドにプロンプト*Explain this chart*（このチャートを説明して）を入力します。

    チャートの詳細な説明が表示されることに注目してください。

    ![プロンプト 'Explain this chart' に対するチャットからの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-explain-chart.png)

## データ分析と視覚化を実行する

チャットのエージェントを使用して、データセットの完全なデータ分析と視覚化ノートブックを作成できます。エージェントはデータセットを分析し、新しいノートブックをスキャフォールドし、データ分析を実行するためのコードを実装し、セルを実行してデータを処理および視覚化します。必要に応じて、エージェントは関連するツールやターミナルコマンドを呼び出してタスクを完了します。

たとえば、住宅データセットのデータ分析を実行するには：

1. チャットビューのエージェントピッカーから[エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択します。

1. チャット入力フィールドに次のプロンプトを入力します：*Perform data analysis of the data in #housing.csv*（#housing.csvのデータのデータ分析を実行して）。

    エージェントがさまざまなタスクを反復することに注目してください。必要に応じて、ツールとコマンドの呼び出しを承認します。
1. 結果として、データクリーニング、データ視覚化、統計分析を含む、データセットの完全なデータ分析を備えた新しいノートブックが作成されます。

    ![プロンプト 'Perform data analysis of the data in housing.csv' に対するチャットからの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-data-analysis.png)

これで、ノートブックを手動でさらに編集したり、AIを使用してインライン編集を行ったり、フォローアップのチャットリクエストを送信してノートブックを変更したりできます。

## 次のステップ

* [VS CodeでのJupyter Notebookについての詳細情報](/docs/datascience/jupyter-notebooks.md)
* [VS CodeのAI機能についての詳細情報](/docs/copilot/overview.md)
* [VS Codeでのチャットについての詳細情報](/docs/copilot/chat/copilot-chat.md)
