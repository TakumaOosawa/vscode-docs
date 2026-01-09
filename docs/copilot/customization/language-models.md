---
ContentId: 33e63aa1-1d8f-4d23-9733-1475f8c9f502
DateApproved: 12/10/2025
MetaDescription: 異なるAI言語モデルの選択方法と、Visual Studio Codeで独自の言語モデルAPIキーを使用する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeのAI言語モデル

Visual Studio Codeは、さまざまなタスクに最適化された異なる組み込み言語モデルを提供します。また、他のプロバイダーのモデルを使用するために、独自の言語モデルAPIキーを持ち込むこともできます。この記事では、チャットやインライン候補の言語モデルを変更する方法と、独自のAPIキーを使用する方法について説明します。

## タスクに適したモデルを選択する

デフォルトでは、チャットはベースモデルを使用して、コーディング、要約、知識ベースの質問、推論など、幅広いタスクに対して高速で有能な応答を提供します。

ただし、このモデルのみの使用に限定されるわけではありません。それぞれの強みを持つ[言語モデルの選択肢](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat#ai-models-for-copilot-chat-1)から選択できます。AIモデルの詳細な比較については、GitHub Copilotドキュメントの[タスクに適したAIモデルの選択](https://docs.github.com/en/copilot/using-github-copilot/ai-models/choosing-the-right-ai-model-for-your-task)を参照してください。

使用している[エージェント](/docs/copilot/customization/custom-agents.md)によっては、利用可能なモデルのリストが異なる場合があります。たとえば、エージェントモードでは、モデルのリストはツール呼び出しのサポートが優れているモデルに限定されます。

> [!NOTE]
> Copilot BusinessまたはEnterpriseユーザーの場合、管理者がGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインして、組織に対して特定のモデルを有効にする必要があります。

## チャット会話のモデルを変更する

チャット入力フィールドの言語モデルピッカーを使用して、チャット会話やコード編集に使用されるモデルを変更します。

![チャットビューのモデルピッカーを示すスクリーンショット。](../images/language-models/model-dropdown-change-model.png)

> [!TIP]
> AI Toolkit拡張機能をインストールして、より多くの言語モデルを追加し、GitHub Copilot機能を強化します。
>
> 詳細については、[チャットモデルの変更](https://docs.github.com/en/copilot/how-tos/use-ai-models/change-the-chat-model#adding-more-models)を参照してください。

[独自の言語モデルAPIキーを使用する](#bring-your-own-language-model-key)ことで、利用可能なモデルのリストをさらに拡張できます。

有料のCopilotプランをお持ちの場合、モデルピッカーにはプレミアムモデルのプレミアムリクエスト乗数が表示されます。詳細については、GitHub Copilotドキュメントの[プレミアムリクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests#premium-requests)を参照してください。

## 自動モデル選択

> [!NOTE]
> 自動モデル選択は、VS Codeリリース1.104から利用可能です。

自動モデル選択を使用すると、VS Codeは最適なパフォーマンスを確保し、特定の言語モデルの過剰な使用によるレート制限を減らすために、モデルを自動的に選択します。モデルのパフォーマンス低下を検出し、その時点で最適なモデルを使用します。ニーズに最も適したモデルを選択するために、この機能の改善を続けています。

自動モデル選択を使用するには、チャットのモデルピッカーから**Auto**を選択します。

現在、自動機能はClaude Sonnet 4、GPT-5、GPT-5 mini、その他のモデルから選択します。組織が[特定のモデルをオプトアウト](https://docs.github.com/en/copilot/how-tos/use-ai-models/configure-access-to-ai-models)している場合、自動機能はそれらのモデルを選択しません。これらのモデルのいずれも利用できない場合、またはプレミアムリクエストを使い果たした場合、自動機能は0x乗数のモデルにフォールバックします。

### 乗数割引

自動モデル選択を使用する場合、VS Codeは選択されたモデルに基づいて、変動する[モデル乗数](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers)を使用します。有料ユーザーの場合、自動機能はリクエスト割引を適用します。

いつでも、チャット応答にカーソルを合わせることで、使用されているモデルとモデル乗数を確認できます。

![ホバー時に選択されたモデルを表示するチャット応答のスクリーンショット。](../images/language-models/chat-response-selected-model.png)

## 言語モデルの管理

言語モデルエディターを使用して、利用可能なすべてのモデルを表示し、モデルピッカーに表示されるモデルを選択し、組み込みプロバイダーまたは拡張機能提供のモデルプロバイダーから追加してモデルを増やすことができます。

言語モデルエディターを開くには、チャットビューのモデルピッカーを開き、**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

![言語モデルエディターを示すスクリーンショット。](../images/language-models/language-models-editor.png)

エディターには、利用可能なすべてのモデルが一覧表示され、モデルの機能、コンテキストサイズ、請求の詳細、可視性ステータスなどの重要な情報が表示されます。デフォルトでは、モデルはプロバイダーごとにグループ化されますが、可視性ごとにグループ化することもできます。

以下のオプションを使用して、モデルを検索およびフィルタリングできます。

* 検索ボックスによるテキスト検索
* プロバイダー: `@provider:"OpenAI"`
* 機能: `@capability:tools`, `@capability:vision`, `@capability:agent`
* 可視性: `@visible:true/false`

### モデルピッカーのカスタマイズ

言語モデルエディターでモデルの可視性ステータスを変更することで、モデルピッカーに表示されるモデルをカスタマイズできます。任意のプロバイダーのモデルを表示または非表示にできます。

リスト内のモデルにカーソルを合わせ、目のアイコンを選択して、モデルピッカーでモデルを表示または非表示にします。

![モデルピッカーでモデルを表示または非表示にするための目のアイコンが付いた言語モデルエディターを示すスクリーンショット。](../images/language-models/language-models-hide.png)

## 独自の言語モデルキーを持ち込む

> [!IMPORTANT]
> この機能は現在、Copilot BusinessまたはCopilot Enterpriseユーザーには利用できません。

VS CodeのGitHub Copilotには、さまざまなタスクに最適化されたさまざまな組み込み言語モデルが付属しています。組み込みモデルとして利用できないモデルを使用したい場合は、独自の言語モデルAPIキー(BYOK)を持ち込んで、他のプロバイダーのモデルを使用できます。

VS Codeで独自の言語モデルAPIキーを使用すると、以下のようないくつかの利点があります。

* **モデルの選択**: 組み込みモデルを超えて、さまざまなプロバイダーの何百ものモデルにアクセスできます。
* **実験**: 組み込みモデルではまだ利用できない新しいモデルや機能を実験できます。
* **ローカルコンピューティング**: GitHub Copilotですでにサポートされているモデルの1つに独自のコンピューティングを使用するか、まだ利用できないモデルを実行します。
* **より大きな制御**: 独自のキーを使用することで、組み込みモデルに課せられた標準のレート制限や制約を回避できます。

VS Codeは、より多くのモデルを追加するためのさまざまなオプションを提供します。

* [組み込みモデルプロバイダーのいずれかを使用する](#add-a-model-from-a-built-in-provider)

* Visual Studio Marketplaceから[言語モデルプロバイダー拡張機能](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)をインストールします。たとえば、[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)などです。

### 独自のモデルキーを使用する際の考慮事項

* チャット体験にのみ適用され、VS Codeのインライン候補やその他のAI機能には影響しません。
* 機能はモデルに依存し、ツール呼び出し、ビジョン、思考のサポートなど、組み込みモデルとは異なる場合があります。
* 埋め込み送信、リポジトリのインデックス作成、クエリの調整、意図の検出、サイドクエリなどの一部のタスクには、CopilotサービスAPIが引き続き使用されます。
* BYOKを使用する場合、責任あるAIフィルタリングがモデルの出力に適用される保証はありません。

### 組み込みプロバイダーからモデルを追加する

VS Codeは、チャットのモデルピッカーにさらにモデルを追加するために使用できるいくつかの組み込みモデルプロバイダーをサポートしています。

組み込みプロバイダーから言語モデルを構成するには:

1. チャットビューの言語モデルピッカーから**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. 言語モデルエディターで、**Add Models**を選択し、リストからモデルプロバイダーを選択します。

    ![モデルプロバイダーのクイックピックを示すスクリーンショット。](../images/language-models/model-provider-quick-pick.png)

1. APIキーやエンドポイントURLなど、プロバイダー固有の詳細を入力します。

1. プロバイダーに応じて、モデルの詳細を入力するか、リストからモデルを選択します。

    次のスクリーンショットは、Phi-4モデルがデプロイされた状態でローカルで実行されているOllamaのモデルピッカーを示しています。

    ![利用可能なモデルのリストからモデルを選択できる、ローカルで実行されているOllamaのモデルピッカーを示すスクリーンショット。](../images/language-models/ollama-installed-models-quick-pick.png)

1. これで、チャットのモデルピッカーからモデルを選択できます。

    [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用するときにモデルを利用できるようにするには、そのモデルがツール呼び出しをサポートしている必要があります。モデルがツール呼び出しをサポートしていない場合、モデルピッカーには表示されません。

> [!NOTE]
> カスタムOpenAI互換モデルの構成は、リリース1.104の時点で[VS Code Insiders](https://code.visualstudio.com/insiders/)でのみ利用可能です。`setting(github.copilot.chat.customOAIModels)`設定でOpenAI互換モデル構成を手動で追加することもできます。

## モデルプロバイダーの詳細を更新する

以前に構成したモデルプロバイダーの詳細を更新するには:

1. チャットビューの言語モデルピッカーから**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. 言語モデルエディターで、更新するモデルプロバイダーの歯車アイコンを選択します。

   ![プロバイダー名の横に歯車アイコンがあるモデルプロバイダーのクイックピックを示すスクリーンショット。](../images/language-models/reconfigure-model-provider.png)

1. APIキーやエンドポイントURLなどのプロバイダー詳細を更新します。

## インライン候補のモデルを変更する

エディターでのインライン候補の生成に使用される言語モデルを変更するには:

1. VS Codeタイトルバーのチャットメニューから**Configure Inline Suggestions...**を選択します。

1. **Change Completions Model...**を選択し、リストからモデルのいずれかを選択します。

> [!NOTE]
> より多くのモデルのサポートを追加するにつれて、インライン候補に使用できるモデルは時間の経過とともに進化する可能性があります。

## よくある質問

### Copilot BusinessまたはCopilot Enterpriseで独自のモデルキーを持ち込むことができないのはなぜですか?

独自のモデルキーを持ち込むことがCopilot BusinessまたはCopilot Enterpriseで利用できないのは、主に、ユーザーが最新のモデルが発表された瞬間に、Copilotの組み込みモデルとしてまだ利用できないものを実験できるようにすることを目的としているためです。

組織がこの機能を大規模に使用するための要件をよりよく理解するため、独自のモデルキーを持ち込む機能は、今年後半にCopilot BusinessおよびEnterpriseプランに追加される予定です。Copilot BusinessおよびEnterpriseユーザーは、引き続き組み込みのマネージドモデルを使用できます。

### VS CodeのCopilotでローカルにホストされたモデルを使用できますか?

[独自のモデルキーを持ち込む](#bring-your-own-language-model-key)(BYOK)を使用し、ローカルモデルへの接続をサポートするモデルプロバイダーを使用することで、チャットでローカルにホストされたモデルを使用できます。ローカルモデルに接続するには、いくつかのオプションがあります。

* ローカルモデルをサポートする組み込みモデルプロバイダーを使用する
* [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)から拡張機能をインストールします。たとえば、[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)などです。
* [カスタムOpenAI互換モデル](#_add-an-openaicompatible-model)を構成する

現在、インライン候補のためにローカルモデルに接続することはできません。VS Codeは、拡張機能がカスタム補完プロバイダーを提供できるようにする拡張機能API[`InlineCompletionItemProvider`](/api/references/vscode-api.md#InlineCompletionItemProvider)を提供しています。[インライン候補サンプル](https://github.com/microsoft/vscode-extension-samples/blob/main/inline-completions)で開始できます。

> [!NOTE]
> 現在、ローカルにホストされたモデルを使用する場合でも、一部のタスクにはCopilotサービスが必要です。したがって、GitHubアカウントがCopilotプラン(Copilot Freeなど)にアクセスできる必要があり、オンラインである必要があります。この要件は、将来のリリースで変更される可能性があります。

### インターネット接続なしでローカルモデルを使用できますか?

現在、ローカルモデルを使用するにはCopilotサービスへのアクセスが必要であるため、オンラインである必要があります。この要件は、将来のリリースで変更される可能性があります。

### Copilotプランなしでローカルモデルを使用できますか?

いいえ、現在、ローカルモデルを使用するには、Copilotプラン(Copilot Freeなど)にアクセスできる必要があります。この要件は、将来のリリースで変更される可能性があります。

## 関連リソース

* [GitHub Copilotで利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)
