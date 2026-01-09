---
ContentId: 101027aa-e73c-4d1b-a93f-b8ce10e1f946
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotを使用して、AIでJupyter Notebookを編集する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでAIを使用してJupyter Notebookを編集する

Visual Studio Codeは、[Jupyter Notebook](/docs/datascience/jupyter-notebooks.md)をネイティブでサポートしているほか、[Pythonコードファイル](/docs/python/jupyter-support-py.md)を通じてもサポートしています。VS CodeのAI機能は、ノートブックの作成や編集、データの分析や可視化に役立ちます。この記事では、VS CodeのAI機能を使用してJupyter Notebookを操作する方法について説明します。

## 新しいノートブックのひな形を作成する

新しいノートブックの作業を迅速に開始するために、VS CodeのAI機能を使用して新しいノートブックのひな形を作成できます。自然言語を使用して、追加したい機能や使用したいライブラリについての詳細を指定します。

AIを使用して新しいノートブックを作成するには、次のいずれかのオプションを選択します。

* チャット入力ボックスにスラッシュコマンド`/newNotebook`を入力し、その後に作成するノートブックの詳細を入力します。

* [エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択し、新しいノートブックの作成を依頼する自然言語プロンプトを入力します。

効果的なノートブックプロンプトについては、[プロンプトの例](/docs/copilot/chat/prompt-examples.md#working-with-jupyter-notebooks)の記事を参照してください。

次のスクリーンショットは、*Create a Jupyter notebook to read data from #housing.csv*というプロンプトに対するエージェントからの出力を示しています (このデータセットは[Kaggle](https://www.kaggle.com/search?q=housing+dataset+in%3Adatasets)から入手できます)。

![ワークスぺース内の'housing.csv'ファイルを読み込む、エージェントによって作成された新しいノートブックを示すスクリーンショット。](../images/notebooks-with-ai/agent-mode-create-new-notebook.png)

新しい`.ipynb`ファイルが作成されていることに注目してください。これには、CSVファイルを読み取り、データの最初の数行を表示するためのMarkdownとコードセルが含まれています。

ノートブックを手動でさらに編集したり、AIを使用してインライン編集を行ったり、フォローアップのチャットリクエストを送信してノートブックを変更したりできます。

## ノートブックセルでのインライン編集

すでにノートブックがあり、セル内でインライン変更を行いたい場合は、コードファイルと同じようにインラインチャットを使用できます。

セル内でインライン編集を行うには、`kb(notebook.cell.chat.start)`を押します。これによりインラインチャットビューが開き、プロンプトを入力できます。

> [!TIP]
> チャットプロンプトでカーネル変数を参照できます。変数名の前に`#`を付けて参照します。たとえば、`df`という名前の変数がある場合、チャットプロンプトで`#df`と入力して参照できます。

![ノートブックセル内のインラインチャットビューを示すスクリーンショット。](../images/notebooks-with-ai/notebook-inline-chat.png)

応答が生成されると、ノートブックセルのコードが更新されることに注目してください。変更を**承認**したり、**承認して実行**したりすることを決定できます。

AIを使用して新しいセルを生成するには、ノートブックビューの**生成**ボタンを選択するか、セルにフォーカスを合わせずに`kb(notebook.cell.chat.start)`を押して、新しいセルのインラインチャットビューを開きます。

## 複数のセルにわたる編集

複数のセルにわたる大規模な編集を行うには、チャットビューで[エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)の使用に切り替えることができます。ノートブックへの変更を要求するプロンプトを提供すると、エージェントはタスクを反復して変更を実装します。

!['Plot a graph of the price distribution'というプロンプトに対するチャットからの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-plot-prices.png)

オーバーレイコントロールを使用して、さまざまな編集候補間を移動したり、変更を保持または元に戻したりできることに注目してください。

## ノートブックの内容について質問する

チャットインターフェースを使用して、ノートブックの内容について質問できます。これは、コード、データ、または視覚化の説明を取得するのに役立ちます。セルの出力、グラフ、エラーなど、チャットリクエストに追加のコンテキストを加えることができます。

次の例は、ノートブック内の視覚化について質問する方法を示しています。

1. グラフの横にある`...`を選択し、**Add Cell Output to Chat**(セルの出力をチャットに追加)を選択して、チャートをコンテキストとしてチャットリクエストに追加します。

    ![ノートブックセル内のグラフのコンテキストメニューを示すスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-add-cell-output.png)

1. チャット入力フィールドにプロンプト*Explain this chart*を入力します。

    チャートの詳細な説明が表示されることに注目してください。

    !['Explain this chart'というプロンプトに対するチャットからの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-explain-chart.png)

## データ分析と可視化の実行

チャットのエージェントを使用して、データセットの完全なデータ分析と可視化ノートブックを作成できます。エージェントはデータセットを分析し、新しいノートブックのひな形を作成し、データ分析を実行するためのコードを実装し、セルを実行してデータを処理および可視化します。必要に応じて、エージェントは関連するツールやターミナルコマンドを呼び出してタスクを完了します。

たとえば、住宅データセットのデータ分析を実行するには、次のようにします。

1. チャットビューのエージェントピッカーから[エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択します。

1. チャット入力フィールドに次のプロンプトを入力します: *Perform data analysis of the data in #housing.csv*。

    エージェントがさまざまなタスクを反復することに注目してください。必要に応じて、ツールとコマンドの呼び出しを承認します。
1. 結果として、データクリーニング、データの可視化、統計分析を含む、データセットの完全なデータ分析を備えた新しいノートブックが作成されます。

    !['Perform data analysis of the data in housing.csv'というプロンプトに対するチャットからの応答を示すスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-data-analysis.png)

ノートブックを手動でさらに編集したり、AIを使用してインライン編集を行ったり、フォローアップのチャットリクエストを送信してノートブックを変更したりできます。

## 次のステップ

* [VS CodeでのJupyter Notebookについての詳細情報](/docs/datascience/jupyter-notebooks.md)
* [VS CodeのAI機能についての詳細情報](/docs/copilot/overview.md)
* [VS Codeでのチャットについての詳細情報](/docs/copilot/chat/copilot-chat.md)
