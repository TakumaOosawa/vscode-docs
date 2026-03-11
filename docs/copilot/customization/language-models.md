---
ContentId: 33e63aa1-1d8f-4d23-9733-1475f8c9f502
DateApproved: 3/9/2026
MetaDescription: VS Code で異なるAI言語モデルを選択する方法と、独自の言語モデルAPIキーを使用する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- language models
- BYOK
- bring your own key
- copilot
- ai
- local models
- customize
---
# VS Code のAI言語モデル

Visual Studio Code は、異なるタスク向けに最適化された複数の組み込み言語モデルを提供しています。また、独自の言語モデルAPIキーを持ち込んで、他のプロバイダーのモデルを使用することもできます。

言語モデルの仕組みと主な特性に関する背景については、「[言語モデルの概念](/docs/copilot/concepts/language-models.md)」を参照してください。

この記事では、チャットまたはインラインサジェスション用の言語モデルを変更する方法と、独自のAPIキーを使用する方法について説明します。

## タスクに適したモデルを選択する

デフォルトでは、チャットは基盤モデルを使用して、コーディング、要約、知識ベースの質問、推論など、幅広いタスク向けの高速で有能な応答を提供します。

ただし、このモデルのみの使用に限定されません。それぞれ独自の強みを持つ[言語モデルの選択](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat#ai-models-for-copilot-chat-1)から選択できます。一般的なガイドラインとして、高速モデル（GPT-5 Mini など）を使用して迅速な編集と簡単な質問に対応し、推論モデル（Claude Opus など）を使用して複雑なリファクタリング、アーキテクチャ決定、または複数ステップのタスクに対応します。詳細な比較については、GitHub Copilot ドキュメントの「[タスクに適したAI モデルの選択](https://docs.github.com/en/copilot/using-github-copilot/ai-models/choosing-the-right-ai-model-for-your-task)」を参照してください。

使用している[エージェント](/docs/copilot/customization/custom-agents.md)に応じて、利用可能なモデルのリストが異なる場合があります。たとえば、エージェントモードでは、モデルのリストはツール呼び出しに適切にサポートされているモデルに限定されます。

> [!NOTE]
> Copilot Business または Enterprise ユーザーの場合、管理者は GitHub.com の[Copilot ポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で「Editor Preview Features」をオプトインして、組織向けに特定のモデルを有効にする必要があります。

## チャット会話用のモデルを変更する

チャット入力フィールドの言語モデルピッカーを使用して、チャット会話とコード編集に使用するモデルを変更します。

![Chat ビューでモデルピッカーを表示しているスクリーンショット。](../images/language-models/model-dropdown-change-model.png)

> [!TIP]
> AI Toolkit 拡張機能をインストールして、GitHub Copilot の機能を強化するために、より多くの言語モデルを追加します。
>
> 詳細については、「[チャットモデルを変更](https://docs.github.com/en/copilot/how-tos/use-ai-models/change-the-chat-model#adding-more-models)」を参照してください。

[独自の言語モデルAPIキーを使用して](#独自の言語モデルキーを持ち込む)、利用可能なモデルのリストをさらに拡張できます。

有料の Copilot プランを使用している場合、モデルピッカーはプレミアムモデルのプレミアムリクエスト乗数を表示します。GitHub Copilot ドキュメントの「[プレミアムリクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests#premium-requests)」について詳しく了解します。

## 自動モデル選択

> [!NOTE]
> 自動モデル選択は VS Code リリース 1.104 以降で利用可能です。

自動モデル選択を使用すると、VS Code は最適なパフォーマンスを確保し、特定の言語モデルの過度な使用によるレート制限を削減するモデルを自動的に選択します。モデルのパフォーマンスの低下を検出し、その時点で最適なモデルを使用します。このフィーチャーを継続的に改善して、ニーズに最も適したモデルを選択します。

自動モデル選択を使用するには、チャットのモデルピッカーから「Auto」を選択します。

現在、自動は Claude Sonnet 4、GPT-5、GPT-5 mini、およびその他のモデルの間で選択されます。組織が[特定のモデルをオプトアウト](https://docs.github.com/en/copilot/how-tos/use-ai-models/configure-access-to-ai-models)している場合、自動はそれらのモデルを選択しません。これらのモデルが利用できない場合、またはプレミアムリクエストが使い果たされた場合、自動は 0x 乗数のモデルにフォールバックします。

### 乗数割引

自動モデル選択を使用する場合、VS Code は選択されたモデルに基づいて、変数[モデル乗数](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers)を使用します。有料ユーザーの場合、自動はリクエスト割引を適用します。

チャット応答をホバーすることで、いつでも使用されているモデルとモデル乗数を確認できます。

![チャット応答のスクリーンショット。ホバーで選択されたモデルを表示しています。](../images/language-models/chat-response-selected-model.png)

## 言語モデルを管理する

言語モデルエディターを使用して、すべての利用可能なモデルを表示し、モデルピッカーに表示されるモデルを選択し、組み込みプロバイダーから追加するか、拡張機能提供のモデルプロバイダーから追加することで、より多くのモデルを追加できます。

言語モデルエディターを開くには、チャットビューでモデルピッカーを開いて「Manage Models」を選択するか、コマンドパレットから「Chat: Manage Language Models」コマンドを実行します。言語モデルエディターは、デフォルトでエディター領域の最上位の[モーダルオーバーレイ](/docs/getstarted/userinterface.md#modal-editors)で開きます。

![言語モデルエディターを表示しているスクリーンショット。](../images/language-models/language-models-editor.png)

エディターには利用可能なすべてのモデルが列挙され、モデル機能、コンテキストサイズ、請求詳細、表示ステータスなどの重要な情報が表示されます。デフォルトでは、モデルはプロバイダーでグループ化されていますが、可視性でグループ化することもできます。

次のオプションを使用してモデルを検索およびフィルタリングできます。

* 検索ボックスを使用したテキスト検索
* プロバイダー: `@provider:"OpenAI"`
* 機能: `@capability:tools`、`@capability:vision`、`@capability:agent`
* 可視性: `@visible:true/false`

### モデルピッカーをカスタマイズする

言語モデルエディターでモデルの表示ステータスを変更することで、モデルピッカーに表示されるモデルをカスタマイズできます。任意のプロバイダーからモデルを表示または非表示にできます。

リスト内のモデルをホバーして、アイコンをクリックして、モデルピッカーでモデルを表示または非表示にします。

![モデルピッカーでモデルを表示または非表示にするアイコンを示す言語モデルエディターのスクリーンショット。](../images/language-models/language-models-hide.png)

## 独自の言語モデルキーを持ち込む

> [!IMPORTANT]
> 独自のモデルキーの持ち込みは、現在 Copilot Business または Copilot Enterprise ユーザーは利用できません。これは、個別の最新のモデル実験用です。Business および Enterprise プランで必要な機能は、今年後半に予定されています。

VS Code の GitHub Copilot には、異なるタスク向けに最適化された、さまざまな組み込み言語モデルが備わっています。組み込みモデルとして利用できないモデルを使用する場合は、独自の言語モデルAPIキー（BYOK）を持ち込んで、他のプロバイダーのモデルを使用できます。

VS Code で独自の言語モデルAPIキーを使用すると、いくつかの利点があります。

* **モデルの選択**: 組み込みモデルを超えて、異なるプロバイダーから何百ものモデルにアクセスします。
* **実験**: 組み込みモデルではまだ利用できない新しいモデルまたは新しい機能を実験します。
* **ローカルコンピューティング**: GitHub Copilot でサポート済みのいずれかのモデル用に独自のコンピューティングを使用するか、まだ利用できないモデルを実行します。
* **より大きな制御**: 独自のキーを使用することで、組み込みモデルに課せられた標準的なレート制限と制限を回避できます。

VS Code は、より多くのモデルを追加するための異なるオプションを提供します。

* [組み込みモデルプロバイダー](#組み込みプロバイダーからモデルを追加)の 1 つを使用します

* Visual Studio Marketplace から[言語モデルプロバイダー拡張機能](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)をインストールします（例：[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)）

### 独自のモデルキーを持ち込む場合の考慮事項

* チャットエクスペリエンスにのみ適用され、インラインサジェスションまたは VS Code の他のAI搭載機能には影響しません。
* 機能はモデル依存であり、組み込みモデルと異なる場合があります。たとえば、ツール呼び出し、ビジョン、思考のサポート。
* Copilot service API は、エンベディングの送信、リポジトリインデックス、クエリ精密化、意図検出、サイドクエリなどの一部のタスクにまだ使用されています。
* BYOK を使用する場合、モデルの出力に責任あるAI を使用しでフィルタ処理が適用されるという保証はありません。

### 組み込みプロバイダーからモデルを追加

VS Code は、チャットのモデルピッカーにより多くのモデルを追加するために使用できるいくつかの組み込みモデルプロバイダーをサポートしています。

組み込みプロバイダーから言語モデルを設定するには、次のようにします。

1. チャットビューの言語モデルピッカーから「Manage Models」を選択するか、コマンドパレットから「Chat: Manage Language Models」コマンドを実行します。

1. 言語モデルエディターで「Add Models」を選択してから、リストからモデルプロバイダーを選択します。

    ![モデルプロバイダーのクイックピック表示するスクリーンショット。](../images/language-models/model-provider-quick-pick.png)

1. API キーやエンドポイント URL などのプロバイダー固有の詳細を入力します。

1. プロバイダーに応じて、モデルの詳細を入力するか、リストからモデルを選択します。

    次のスクリーンショットは、Phi-4 モデルをデプロイした状態でローカルで実行されている Ollama のモデルピッカーを示しています。

    ![Ollama がローカルで実行されているモデルピッカーを表示しているスクリーンショット。利用可能なモデルのリストから模型を選択できます。](../images/language-models/ollama-installed-models-quick-pick.png)

1. これで、チャットのモデルピッカーからモデルを選択できます。

    モデルを[エージェント](/docs/copilot/agents/overview.md)を使用するときに利用可能にするには、ツール呼び出しをサポートする必要があります。モデルがツール呼び出しをサポートしていない場合、モデルピッカーに表示されません。

> [!NOTE]
> カスタム OpenAI 互換モデルの設定は、現在 [VS Code Insiders](https://code.visualstudio.com/insiders/) のリリース 1.104 以降でのみ利用可能です。`setting(github.copilot.chat.customOAIModels)` 設定に OpenAI 互換モデル設定を手動で追加することもできます。

## モデルプロバイダーの詳細を更新する

以前に設定したモデルプロバイダーの詳細を更新するには、次のようにします。

1. チャットビューの言語モデルピッカーから「Manage Models」を選択するか、コマンドパレットから「Chat: Manage Language Models」コマンドを実行します。

1. 言語モデルエディターで、更新するモデルプロバイダーの歯車アイコンを選択します。

   ![プロバイダー名の横に歯車アイコン付きのモデルプロバイダーのクイックピックを表示しているスクリーンショット。](../images/language-models/reconfigure-model-provider.png)

1. API キーやエンドポイント URL などのプロバイダーの詳細を更新します。

## インラインチャット用のモデルを変更する

エディターのインラインチャット用にデフォルトの言語モデルを設定できます。これにより、チャット会話とは異なるモデルをインラインチャットに使用できます。

インラインチャット用のデフォルトモデルを設定するには、`setting(inlineChat.defaultModel)` 設定を使用します。設定は、モデルピッカーから利用可能なすべてのモデルをリストしています。

インラインチャットセッション中にモデルを変更する場合、選択はセッションの残りの期間、保持されます。VS Code を再度読み込むうえで、モデルは `setting(inlineChat.defaultModel)` 設定で指定された値にリセットされます。

## インラインサジェスション用のモデルを変更する

エディターでインラインサジェスション生成に使用される言語モデルを変更するには、次のようにします。

1. VS Code のタイトルバーにあるチャットメニューから「Configure Inline Suggestions...」を選択します。

1. 「Change Completions Model...」を選択してから、リストからいずれかのモデルを選択します。

> [!NOTE]
> インラインサジェスションで利用可能なモデルは、より多くのモデルにサポートを追加する際に時系列で進化する場合があります。

## よくある質問

### Copilot Business または Copilot Enterprise で独自のモデルキーの持ち込みが利用できないのはなぜですか？

独自のモデルキーの持ち込みは、主に個別の最新のモデル実験用です。Business または Enterprise プランではまだ利用できません。これらのプランで必要なサポートは、今年後半に予定されています。Copilot Business および Enterprise ユーザーは、組み込みの、マネージド モデルを使用できます。

### VS Code の Copilot でローカルホストモデルを使用できますか？

[独自のモデルキーの持ち込み](#独自の言語モデルキーを持ち込む)（BYOK）とローカルモデルへの接続をサポートするモデルプロバイダーを使用して、チャットでローカルホストされたモデルを使用できます。ローカルモデルに接続するためのさまざまなオプションがあります。

* ローカルモデルをサポートする組み込みモデルプロバイダーを使用する
* [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)から拡張機能をインストールします（例：[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)）

現在、インラインサジェスション用のローカルモデルに接続することはできません。VS Code は、拡張機能がカスタム完了プロバイダーを提供できるようにする`InlineCompletionItemProvider`][/api/references/vscode-api.md#InlineCompletionItemProvider]拡張API を提供しています。[インライン完了サンプル](https://github.com/microsoft/vscode-extension-samples/blob/main/inline-completions)で始めることができます。

> [!NOTE]
> 現在、ローカルホストされたモデルを使用する場合でも、Copilot サービスの一部のタスク向けが必要です。したがって、GitHub アカウントが Copilot プラン（例：Copilot Free）にアクセスしていて、オンラインである必要があります。この要件は将来のリリースで変更される場合があります。

### インターネット接続なしでローカルモデルを使用できますか？

現在、ローカルモデルを使用する場合、Copilot サービスへのアクセスが必要であり、オンラインである必要があります。この要件は将来のリリースで変更される場合があります。

### Copilot プランなしでローカルモデルを使用できますか？

いいえ。現在、ローカルモデルを使用するには、Copilot プラン（例：Copilot Free）にアクセスしていることが必要です。この要件は将来のリリースで変更される場合があります。

## 関連リソース

* [GitHub Copilot で利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)
* [VS Code のAIセキュリティの考慮事項](/docs/copilot/security.md)

