---
ContentId: 33e63aa1-1d8f-4d23-9733-1475f8c9f502
DateApproved: 01/08/2026
MetaDescription: Visual Studio Codeで異なるAI言語モデルを選択する方法、および独自の言語モデルAPIキーを使用する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeにおけるAI言語モデル

Visual Studio Codeは、異なるタスクに最適化されたさまざまな組み込み言語モデルを提供しています。また、独自の言語モデルAPIキーを持ち込んで、他のプロバイダーのモデルを使用することもできます。この記事では、チャットまたはインライン提案の言語モデルを変更する方法と、独自のAPIキーを使用する方法について説明します。

## タスクに適したモデルを選択する

デフォルトでは、チャットはベースモデルを使用して、コーディング、要約、知識ベースの質問、推論など、幅広いタスクに対して高速で有能な応答を提供します。

ただし、このモデルの使用のみに制限されるわけではありません。[言語モデルの選択](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat#ai-models-for-copilot-chat-1)から選択でき、それぞれに独自の長所があります。AIモデルの詳細な比較については、GitHub Copilotドキュメントの「[タスクに適したAIモデルの選択](https://docs.github.com/en/copilot/using-github-copilot/ai-models/choosing-the-right-ai-model-for-your-task)」を参照してください。

使用している[エージェント](/docs/copilot/customization/custom-agents.md)によっては、利用可能なモデルのリストが異なる場合があります。たとえば、エージェントモードでは、モデルのリストはツール呼び出しのサポートが良好なモデルに限定されます。

> [!NOTE]
> Copilot BusinessまたはEnterpriseユーザーの場合、管理者がGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインして、組織に対して特定のモデルを有効にする必要があります。

## チャット会話のモデルを変更する

チャット入力フィールドの言語モデルピッカーを使用して、チャット会話とコード編集に使用されるモデルを変更します。

![チャットビューのモデルピッカーを示すスクリーンショット。](../images/language-models/model-dropdown-change-model.png)

> [!TIP]
> AI Toolkit拡張機能をインストールして言語モデルを追加し、GitHub Copilotの機能を強化してください。
>
> 詳細については、「[チャットモデルの変更](https://docs.github.com/en/copilot/how-tos/use-ai-models/change-the-chat-model#adding-more-models)」を参照してください。

[独自の言語モデルAPIキーを使用する](#bring-your-own-language-model-key)ことで、利用可能なモデルのリストをさらに拡張できます。

有料のCopilotプランをお持ちの場合、モデルピッカーにはプレミアムモデルのプレミアムリクエスト乗数が表示されます。詳細については、GitHub Copilotドキュメントの[プレミアムリクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests#premium-requests)を参照してください。

## 自動モデル選択

> [!NOTE]
> 自動モデル選択は、VS Codeリリース1.104以降で利用可能です。

自動モデル選択を使用すると、VS Codeは自動的にモデルを選択し、最適なパフォーマンスを確保し、特定の言語モデルの過度の使用によるレート制限を削減します。劣化したモデルのパフォーマンスを検出し、その時点で最適なモデルを使用します。ニーズに最も適したモデルを選択するために、この機能の改善を続けています。

自動モデル選択を使用するには、チャットのモデルピッカーから**Auto**を選択します。

現在、自動選択はClaude Sonnet 4、GPT-5、GPT-5 mini、およびその他のモデルから選択します。組織が[特定のモデルをオプトアウト](https://docs.github.com/en/copilot/how-tos/use-ai-models/configure-access-to-ai-models)している場合、自動選択はそれらのモデルを選択しません。これらのモデルのいずれも利用できない場合、またはプレミアムリクエストを使い果たした場合、自動選択は0x乗数のモデルにフォールバックします。

### 乗数割引

自動モデル選択を使用する場合、VS Codeは選択されたモデルに基づいて、可変の[モデル乗数](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers)を使用します。有料ユーザーの場合、自動選択はリクエスト割引を適用します。

いつでも、チャットの応答にカーソルを合わせることで、どのモデルとモデル乗数が使用されているかを確認できます。

![
ホバー時に選択されたモデルを示すチャット応答のスクリーンショット。](../images/language-models/chat-response-selected-model.png)

## 言語モデルの管理

言語モデルエディターを使用して、利用可能なすべてのモデルを表示し、モデルピッカーに表示されるモデルを選択し、組み込みプロバイダーまたは拡張機能提供のモデルプロバイダーからモデルを追加できます。

Language Modelsエディターを開くには、チャットビューのモデルピッカーを開き、**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

![Language Modelsエディターを示すスクリーンショット。](../images/language-models/language-models-editor.png)

エディターには利用可能なすべてのモデルが一覧表示され、モデルの機能、コンテキストサイズ、請求の詳細、可視性ステータスなどの重要な情報が表示されます。デフォルトでは、モデルはプロバイダーごとにグループ化されますが、可視性ごとにグループ化することもできます。

以下のオプションを使用してモデルを検索およびフィルタリングできます：

* 検索ボックスを使用したテキスト検索
* プロバイダー：`@provider:"OpenAI"`
* 機能：`@capability:tools`、`@capability:vision`、`@capability:agent`
* 可視性：`@visible:true/false`

### モデルピッカーのカスタマイズ

Language Modelsエディターでモデルの可視性ステータスを変更することにより、モデルピッカーに表示されるモデルをカスタマイズできます。任意のプロバイダーのモデルを表示または非表示にできます。

リスト内のモデルにカーソルを合わせ、目のアイコンを選択して、モデルピッカーでモデルを表示または非表示にします。

![モデルピッカーでモデルを表示または非表示にするための目のアイコンがあるLanguage Modelsエディターを示すスクリーンショット。](../images/language-models/language-models-hide.png)

## 独自の言語モデルキーを持ち込む

> [!IMPORTANT]
> この機能は現在、Copilot BusinessまたはCopilot Enterpriseユーザーには利用できません。

VS CodeのGitHub Copilotには、さまざまなタスクに最適化されたさまざまな組み込み言語モデルが付属しています。組み込みモデルとして利用できないモデルを使用したい場合は、独自の言語モデルAPIキー（BYOK）を持ち込んで、他のプロバイダーのモデルを使用できます。

VS Codeで独自の言語モデルAPIキーを使用することには、いくつかの利点があります：

* **モデルの選択**：組み込みモデルを超えて、さまざまなプロバイダーの何百ものモデルにアクセスできます。
* **実験**：組み込みモデルではまだ利用できない新しいモデルや機能を試すことができます。
* **ローカルコンピューティング**：GitHub Copilotですでにサポートされているモデルの1つに独自のコンピューティングを使用するか、まだ利用できないモデルを実行します。
* **より優れた制御**：独自のキーを使用することで、組み込みモデルに課せられた標準のレート制限や制限を回避できます。

VS Codeは、モデルを追加するためのさまざまなオプションを提供します：

* [組み込みモデルプロバイダー](#add-a-model-from-a-built-in-provider)の1つを使用する

* Visual Studio Marketplaceから[言語モデルプロバイダー拡張機能](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)をインストールする（例：[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)）

### 独自のモデルキーを使用する際の考慮事項

* チャット体験にのみ適用され、インライン提案やVS Codeのその他のAI搭載機能には影響しません。
* 機能はモデルに依存し、組み込みモデルとは異なる場合があります（例：ツール呼び出し、ビジョン、思考のサポートなど）。
* CopilotサービスAPIは、埋め込みの送信、リポジトリのインデックス作成、クエリの詳細化、意図の検出、サイドクエリなどの一部のタスクに引き続き使用されます。
* BYOKを使用する場合、責任あるAIフィルタリングがモデルの出力に適用されるという保証はありません。

### 組み込みプロバイダーからモデルを追加する

VS Codeは、チャットのモデルピッカーにモデルを追加するために使用できるいくつかの組み込みモデルプロバイダーをサポートしています。

組み込みプロバイダーから言語モデルを構成するには：

1. チャットビューの言語モデルピッカーから**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. Language Modelsエディターで**Add Models**を選択し、リストからモデルプロバイダーを選択します。

    ![モデルプロバイダーのクイックピックを示すスクリーンショット。](../images/language-models/model-provider-quick-pick.png)

1. APIキーやエンドポイントURLなど、プロバイダー固有の詳細を入力します。

1. プロバイダーに応じて、モデルの詳細を入力するか、リストからモデルを選択します。

    次のスクリーンショットは、ローカルで実行されているOllamaのモデルピッカーを示しており、Phi-4モデルがデプロイされています。

    ![ローカルで実行されているOllamaのモデルピッカーを示し、利用可能なモデルのリストからモデルを選択できるスクリーンショット。](../images/language-models/ollama-installed-models-quick-pick.png)

1. これで、チャットのモデルピッカーからモデルを選択できます。

    [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)の使用時にモデルを利用可能にするには、ツール呼び出しをサポートしている必要があります。モデルがツール呼び出しをサポートしていない場合、モデルピッカーには表示されません。

> [!NOTE]
> カスタムOpenAI互換モデルの構成は、リリース1.104の時点で、現在[VS Code Insiders](https://code.visualstudio.com/insiders/)でのみ利用可能です。また、`setting(github.copilot.chat.customOAIModels)`設定でOpenAI互換モデルの構成を手動で追加することもできます。

## モデルプロバイダーの詳細を更新する

以前に構成したモデルプロバイダーの詳細を更新するには：

1. チャットビューの言語モデルピッカーから**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. Language Modelsエディターで、更新するモデルプロバイダーの歯車アイコンを選択します。

   ![プロバイダー名の横に歯車アイコンがあるモデルプロバイダーのクイックピックを示すスクリーンショット。](../images/language-models/reconfigure-model-provider.png)

1. APIキーやエンドポイントURLなど、プロバイダーの詳細を更新します。

## インライン提案のモデルを変更する

エディターでインライン提案の生成に使用される言語モデルを変更するには：

1. VS Codeタイトルバーのチャットメニューから**Configure Inline Suggestions...**を選択します。

1. **Change Completions Model...**を選択し、リストからモデルの1つを選択します。

> [!NOTE]
> インライン提案に使用できるモデルは、より多くのモデルのサポートを追加するにつれて、時間の経過とともに進化する可能性があります。

## よくある質問

### なぜCopilot BusinessまたはCopilot Enterpriseで独自のモデルキーを持ち込むことができないのですか？

独自のモデルキーを持ち込むことがCopilot BusinessまたはCopilot Enterpriseで利用できないのは、主にユーザーがCopilotの組み込みモデルとしてまだ利用できない最新のモデルが発表された瞬間に実験できるようにすることを目的としているためです。

組織がこの機能を大規模に使用するための要件をよりよく理解するにつれて、独自のモデルキーを持ち込む機能は今年後半にCopilot BusinessおよびEnterpriseプランに導入される予定です。Copilot BusinessおよびEnterpriseユーザーは、引き続き組み込みの管理されたモデルを使用できます。

### VS CodeのCopilotでローカルにホストされたモデルを使用できますか？

[独自のモデルキーを持ち込む](#bring-your-own-language-model-key)（BYOK）を使用し、ローカルモデルへの接続をサポートするモデルプロバイダーを使用することで、チャットでローカルにホストされたモデルを使用できます。ローカルモデルに接続するには、さまざまなオプションがあります：

* ローカルモデルをサポートする組み込みモデルプロバイダーを使用する
* [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)から拡張機能をインストールする（例：[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)）
* [カスタムOpenAI互換モデル](#_add-an-openaicompatible-model)を構成する

現在、インライン提案のためにローカルモデルに接続することはできません。VS Codeは、拡張機能がカスタム補完プロバイダーを提供できるようにする拡張機能API [`InlineCompletionItemProvider`](/api/references/vscode-api.md#InlineCompletionItemProvider)を提供しています。[インライン補完成のサンプル](https://github.com/microsoft/vscode-extension-samples/blob/main/inline-completions)を使用して開始できます。

> [!NOTE]
> 現在、ローカルにホストされたモデルを使用する場合でも、一部のタスクにはCopilotサービスが必要です。したがって、GitHubアカウントはCopilotプラン（Copilot Freeなど）にアクセスでき、オンラインである必要があります。この要件は、将来のリリースで変更される可能性があります。

### インターネット接続なしでローカルモデルを使用できますか？

現在、ローカルモデルを使用するにはCopilotサービスへのアクセスが必要であるため、オンラインである必要があります。この要件は、将来のリリースで変更される可能性があります。

### Copilotプランなしでローカルモデルを使用できますか？

いいえ、現在、ローカルモデルを使用するにはCopilotプラン（Copilot Freeなど）にアクセスできる必要があります。この要件は、将来のリリースで変更される可能性があります。

## 関連リソース

* [GitHub Copilotで利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)
