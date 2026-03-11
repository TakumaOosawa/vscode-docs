---
ContentId: 101027aa-e73c-4d1b-a93f-b8ce10e1f946
DateApproved: 3/9/2026
MetaDescription: GitHub Copilotを使用してVisual Studio CodeでJupyterノートブックを編集する方法を学習します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeでAIを使用してJupyterノートブックを編集する

Visual Studio Codeはネイティブに[Jupyterノートブック](/docs/datascience/jupyter-notebooks.md)、および[Pythonコードファイル](/docs/python/jupyter-support-py.md)を通じた作業をサポートしています。VS Codeの AI機能は、ノートブックの作成と編集、およびデータの分析と可視化に役立ちます。この記事では、Jupyterノートブックを使用するためにVS CodeのAI機能を使用する方法について学習します。

## 新しいノートブックをスキャフォールドする

新しいノートブックの概要の取得を加速するために、VS CodeのAI機能を使用して新しいノートブックをスキャフォールドできます。自然言語を使用して、追加する機能と使用するライブラリの詳細を指定します。

AIで新しいノートブックを作成するには、次のいずれかのオプションを選択します。

* チャット入力ボックスに`/newNotebook`スラッシュコマンドを入力し、続けて作成するノートブックの詳細を入力します。

* [エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択し、新しいノートブックを作成するよう要求する自然言語プロンプトを入力します。

効果的なノートブックプロンプトについては、[プロンプト例](/docs/copilot/chat/prompt-examples.md#working-with-jupyter-notebooks)記事を参照してください。

次のスクリーンショットは、プロンプト*Create a Jupyter notebook to read data from #housing.csv*（このデータセットは[Kaggle](https://www.kaggle.com/search?q=housing+dataset+in%3Adatasets)から入手できます）に対するエージェントからの出力を示しています。

![エージェントが作成した新しいノートブックのスクリーンショット。ワークスペースの'housing.csv'ファイルを読み取ります。](../images/notebooks-with-ai/agent-mode-create-new-notebook.png)

新しい`.ipynb`ファイルが作成されていることに注意してください。これには、CSVファイルを読み取りデータの最初の数行を表示するためのマークダウンセルとコードセルが含まれています。

これでノートブックをさらに手動で編集することも、AIを使用してインライン編集を行うか、ノートブックを変更するためのフォローアップチャットリクエストを送信することもできます。

## ノートブックセル内でインライン編集を作成する

既にノートブックがあり、セル内で何らかのインライン変更を加えたい場合は、コードファイル内の場合と同じように、インラインチャットを使用できます。

セル内でインライン編集を作成するには、`kb(notebook.cell.chat.start)`を押します。これによりインラインチャットビューが開き、プロンプトを入力できます。

> [!TIP]
> チャットプロンプトでカーネル変数を参照できます。変数名の前に`#`を入力して参照します。たとえば、`df`という名前の変数がある場合、チャットプロンプトで`#df`を入力して参照できます。

![ノートブックセルのインラインチャットビューのスクリーンショット。](../images/notebooks-with-ai/notebook-inline-chat.png)

応答が生成されると、ノートブックセルのコードが更新されることに注意してください。変更を**受け入れる**ことができ、セルの変更を**受け入れて実行**することもできます。

AIで新しいセルを生成するには、ノートブックビューの**生成**ボタンを選択するか、セルにフォーカスせず`kb(notebook.cell.chat.start)`を押してインラインチャットビューを開き、新しいセルを作成します。

## 複数のセル間で編集を作成する

より大きな編集を行うには、複数のセル間で[エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を使用してチャットビューに切り替えることができます。プロンプトを提供してノートブックへの変更をリクエストすると、エージェントがタスクを反復処理して変更を実装します。

![プロンプト'Plot a graph of the price distribution'に対するチャットからの応答のスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-plot-prices.png)

オーバーレイコントロールを使用して異なる編集提案を移動し、変更を保持またはやり直すことができることに注意してください。

## ノートブックコンテンツについての質問を行う

チャットインターフェイスを使用してノートブックのコンテンツについての質問をすることができます。これはコード、データ、または可視化の説明を得るのに便利です。セル出力、グラフ、またはエラーなどの追加コンテキストをチャットリクエストに追加できます。

次の例は、ノートブックの可視化について質問する方法を示しています。

1. グラフの横の`...`を選択し、**Add Cell Output to Chat**を選択して、チャートをチャットリクエストのコンテキストとして追加します。

    ![ノートブックセルのグラフのコンテキストメニューのスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-add-cell-output.png)

1. チャット入力フィールドにプロンプト*Explain this chart*を入力します。

    グラフの詳細な説明が表示されることに注意してください。

    ![プロンプト'Explain this chart'に対するチャットからの応答のスクリーンショット。](../images/notebooks-with-ai/notebook-ask-mode-explain-chart.png)

## データ分析と可視化を実行する

チャットのエージェントを使用してデータセットの完全なデータ分析と可視化ノートブックを実行できます。エージェントがデータセットを分析し、新しいノートブックをスキャフォールドし、データ分析を実行するためのコードを実装し、セルを実行してデータを処理および可視化します。必要に応じて、エージェントは関連するツールとターミナルコマンドを呼び出してタスクを完了します。

たとえば、ハウジングデータセットのデータ分析を実行するには、以下のようにします。

1. チャットビューのエージェントピッカーから[エージェント](vscode://GitHub.Copilot-Chat/chat?mode=agent)を選択します。

1. チャット入力フィールドに次のプロンプトを入力します。*Perform data analysis of the data in #housing.csv*

    エージェントが異なるタスクを反復処理することに注意してください。必要に応じて、ツールとコマンドの呼び出しを承認します。
1. 結果は、データクリーニング、データ可視化、および統計分析を含む、データセットの完全なデータ分析を含む新しいノートブックです。

    ![プロンプト'Perform data analysis of the data in housing.csv'に対するチャットからの応答のスクリーンショット。](../images/notebooks-with-ai/notebook-agent-mode-data-analysis.png)

これでノートブックをさらに手動で編集することも、AIを使用してインライン編集を行うか、ノートブックを変更するためのフォローアップチャットリクエストを送信することもできます。

## 次の手順

* [VS CodeのJupyterノートブックの詳細を学習します](/docs/datascience/jupyter-notebooks.md)
* [VS CodeのAI機能の詳細を学習します](/docs/copilot/overview.md)
* [VS Codeのチャットについての詳細を学習します](/docs/copilot/chat/copilot-chat.md)

