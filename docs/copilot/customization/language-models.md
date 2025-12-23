---
ContentId: 33e63aa1-1d8f-4d23-9733-1475f8c9f502
DateApproved: 12/10/2025
MetaDescription: Visual Studio Codeで、複数のAI言語モデルの選び方と、独自の言語モデルAPIキーを使用する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS CodeのAI言語モデル

Visual Studio Codeには、さまざまなタスク向けに最適化された複数の組み込み言語モデルがあります。また、独自の言語モデルAPIキーを持ち込んで、他のプロバイダーのモデルを使用することもできます。この記事では、チャットまたはインライン候補で使用する言語モデルを変更する方法と、独自のAPIキーを使用する方法について説明します。

## タスクに適したモデルを選択する

既定では、チャットはベースモデルを使用して、コーディング、要約、知識に基づく質問、推論など、幅広いタスクに対して高速で有能な応答を提供します。

ただし、このモデルだけに限定されるわけではありません。それぞれ固有の強みを持つ[言語モデルの選択肢](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat#ai-models-for-copilot-chat-1)から選べます。AIモデルの詳細な比較については、GitHub Copilotドキュメントの[タスクに適したAIモデルの選び方](https://docs.github.com/en/copilot/using-github-copilot/ai-models/choosing-the-right-ai-model-for-your-task)を参照してください。

使用している[エージェント](/docs/copilot/customization/custom-agents.md)によって、利用できるモデルの一覧は異なる場合があります。たとえば、エージェントモードでは、ツール呼び出しのサポートが十分なモデルに限定されます。

> [!NOTE]
> Copilot BusinessまたはEnterpriseユーザーの場合、管理者がGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`をオプトインして、組織で特定のモデルを有効にする必要があります。

## チャット会話で使用するモデルを変更する

チャット入力欄の言語モデルピッカーを使用して、チャット会話とコード編集に使用されるモデルを変更します。

![チャットビューのモデルピッカーを示すスクリーンショット。](../images/language-models/model-dropdown-change-model.png)

> [!TIP]
> AI Toolkit拡張機能をインストールして、より多くの言語モデルを追加し、GitHub Copilotの機能を強化します。
>
> 詳細については、[チャットモデルを変更する](https://docs.github.com/en/copilot/how-tos/use-ai-models/change-the-chat-model#adding-more-models)を参照してください。

[独自の言語モデルAPIキーを使用する](#bring-your-own-language-model-key)ことで、利用可能なモデルの一覧をさらに拡張できます。

有料のCopilotプランをご利用の場合、モデルピッカーにはプレミアムモデルのプレミアムリクエストの乗数が表示されます。[プレミアムリクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests#premium-requests)の詳細は、GitHub Copilotドキュメントを参照してください。

## モデルの自動選択

> [!NOTE]
> モデルの自動選択は、VS Codeリリース1.104以降で利用できます。

モデルの自動選択では、VS Codeがモデルを自動的に選択し、最適なパフォーマンスを確保するとともに、特定の言語モデルを過度に使用することによるレート制限を抑えます。モデルの性能低下を検出し、その時点で最適なモデルを使用します。この機能は引き続き改善し、ニーズに最も適したモデルを選べるようにしていきます。

モデルの自動選択を使用するには、チャットのモデルピッカーで**Auto**を選択します。

現在、autoはClaude Sonnet 4、GPT-5、GPT-5 miniなどのモデルから選択します。組織が[特定のモデルをオプトアウト](https://docs.github.com/en/copilot/how-tos/use-ai-models/configure-access-to-ai-models)している場合、autoはそれらのモデルを選択しません。これらのモデルがいずれも利用できない場合、またはプレミアムリクエストを使い切った場合、autoは0x乗数のモデルにフォールバックします。

### 乗数の割引

モデルの自動選択を使用する場合、VS Codeは選択されたモデルに基づいて、可変の[モデル乗数](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers)を使用します。有料ユーザーの場合、autoはリクエスト割引を適用します。

いつでも、チャット応答にカーソルを合わせることで、使用されているモデルとモデル乗数を確認できます。

![チャット応答のスクリーンショット。ホバー時に選択されたモデルが表示されている。](../images/language-models/chat-response-selected-model.png)

## 言語モデルを管理する

言語モデルエディターを使用して、利用可能なすべてのモデルを表示し、モデルピッカーに表示するモデルを選択し、組み込みプロバイダーまたは拡張機能が提供するモデルプロバイダーからモデルを追加できます。

言語モデルエディターを開くには、チャットビューでモデルピッカーを開いて**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

![言語モデルエディターを示すスクリーンショット。](../images/language-models/language-models-editor.png)

エディターには利用可能なすべてのモデルが一覧表示され、モデルの機能、コンテキストサイズ、課金の詳細、表示/非表示の状態などの重要な情報が示されます。既定ではモデルはプロバイダーごとにグループ化されますが、表示/非表示でグループ化することもできます。

次のオプションを使用して、モデルを検索およびフィルターできます。

* 検索ボックスによるテキスト検索
* プロバイダー: `@provider:"OpenAI"`
* 機能: `@capability:tools`、`@capability:vision`、`@capability:agent`
* 表示/非表示: `@visible:true/false`

### モデルピッカーをカスタマイズする

言語モデルエディターでモデルの表示/非表示の状態を変更することで、モデルピッカーに表示するモデルをカスタマイズできます。任意のプロバイダーのモデルを表示または非表示にできます。

一覧内のモデルにカーソルを合わせ、目のアイコンを選択して、モデルピッカーでモデルを表示または非表示にします。

![モデルピッカーでモデルを表示/非表示にするための目のアイコンがある言語モデルエディターを示すスクリーンショット。](../images/language-models/language-models-hide.png)

## 独自の言語モデルキーを持ち込む

> [!IMPORTANT]
> この機能は現在、Copilot BusinessまたはCopilot Enterpriseユーザーは利用できません。

VS CodeのGitHub Copilotには、さまざまなタスク向けに最適化された複数の組み込み言語モデルが含まれています。組み込みモデルとして利用できないモデルを使用したい場合は、独自の言語モデルAPIキー(BYOK)を持ち込んで、他のプロバイダーのモデルを使用できます。

VS Codeで独自の言語モデルAPIキーを使用することには、次のような利点があります。

* **モデルの選択肢**: 組み込みモデルに加えて、さまざまなプロバイダーの数百のモデルにアクセスできます。
* **実験**: 組み込みモデルではまだ利用できない新しいモデルや機能を試せます。
* **ローカルの計算資源**: GitHub Copilotがすでにサポートしているモデルのいずれかに自分の計算資源を使用したり、まだ利用できないモデルを実行したりできます。
* **より高い制御性**: 独自のキーを使用することで、組み込みモデルに課される標準のレート制限や制約を回避できます。

VS Codeでは、追加のモデルを加えるために複数の方法が用意されています。

* [組み込みモデルプロバイダー](#add-a-model-from-a-built-in-provider)のいずれかを使用する

* Visual Studio Marketplaceから[言語モデルプロバイダー拡張機能](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)をインストールする(例: [Foundry Localを使用するVS Code向けAI Toolkit](https://aka.ms/AIToolkit))

### 独自のモデルキーを持ち込む場合の考慮事項

* チャット体験にのみ適用され、インライン候補やVS Codeの他のAI機能には影響しません。
* 機能はモデルに依存し、組み込みモデルとは異なる場合があります(例: ツール呼び出し、ビジョン、思考のサポート)。
* 埋め込みの送信、リポジトリのインデックス作成、クエリの精緻化、意図検出、サイドクエリなど、一部のタスクでは引き続きCopilotサービスAPIが使用されます。
* BYOKを使用する場合、モデルの出力に責任あるAIフィルタリングが適用される保証はありません。

### 組み込みプロバイダーからモデルを追加する

VS Codeは複数の組み込みモデルプロバイダーをサポートしており、チャットのモデルピッカーにさらにモデルを追加するために使用できます。

組み込みプロバイダーの言語モデルを構成するには、次の手順に従います。

1. チャットビューの言語モデルピッカーから**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. 言語モデルエディターで**Add Models**を選択し、一覧からモデルプロバイダーを選択します。

    ![モデルプロバイダーのクイックピックを示すスクリーンショット。](../images/language-models/model-provider-quick-pick.png)

1. APIキーやエンドポイントURLなど、プロバイダー固有の詳細を入力します。

1. プロバイダーによっては、モデルの詳細を入力するか、一覧からモデルを選択します。

    次のスクリーンショットは、Phi-4モデルがデプロイされた、ローカルで実行中のOllamaのモデルピッカーを示しています。

    ![ローカルで実行中のOllamaのモデルピッカーを示すスクリーンショット。利用可能なモデルの一覧からモデルを選択できる。](../images/language-models/ollama-installed-models-quick-pick.png)

1. これで、チャットのモデルピッカーからモデルを選択できるようになります。

    [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する際にモデルを利用可能にするには、ツール呼び出しをサポートしている必要があります。ツール呼び出しをサポートしていないモデルは、モデルピッカーに表示されません。

> [!NOTE]
> カスタムのOpenAI互換モデルの構成は、リリース1.104時点では[VS Code Insiders](https://code.visualstudio.com/insiders/)でのみ利用できます。また、`setting(github.copilot.chat.customOAIModels)`設定で、OpenAI互換モデルの構成を手動で追加することもできます。

## モデルプロバイダーの詳細を更新する

以前に構成したモデルプロバイダーの詳細を更新するには、次の手順に従います。

1. チャットビューの言語モデルピッカーから**Manage Models**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. 言語モデルエディターで、更新するモデルプロバイダーの歯車アイコンを選択します。

    ![プロバイダー名の横に歯車アイコンがあるモデルプロバイダーのクイックピックを示すスクリーンショット。](../images/language-models/reconfigure-model-provider.png)

1. APIキーやエンドポイントURLなど、プロバイダーの詳細を更新します。

## インライン候補で使用するモデルを変更する

エディターでインライン候補を生成する際に使用される言語モデルを変更するには、次の手順に従います。

1. VS CodeのタイトルバーにあるChatメニューから**Configure Inline Suggestions...**を選択します。

1. **Change Completions Model...**を選択し、一覧からいずれかのモデルを選択します。

> [!NOTE]
> インライン候補で利用できるモデルは、より多くのモデルのサポートを追加するにつれて、時間とともに変化する可能性があります。

## よくある質問

### Copilot BusinessまたはCopilot Enterpriseで独自のモデルキーを持ち込めないのはなぜですか?

独自のモデルキーの持ち込みはCopilot BusinessまたはCopilot Enterpriseでは利用できません。これは主に、ユーザーが発表直後の最新モデルを(まだCopilotの組み込みモデルとして利用できない段階から)試せるようにすることを目的としているためです。

組織がこの機能を大規模に利用する際の要件をより深く理解でき次第、独自のモデルキーの持ち込みは今年後半にCopilot BusinessおよびEnterpriseプランにも提供される予定です。Copilot BusinessおよびEnterpriseユーザーは、引き続き組み込みのマネージドモデルを使用できます。

### VS CodeのCopilotでローカルホストのモデルを使用できますか?

[独自のモデルキーを持ち込む](#bring-your-own-language-model-key)(BYOK)を使用し、ローカルモデルへの接続をサポートするモデルプロバイダーを利用することで、チャットでローカルホストのモデルを使用できます。ローカルモデルに接続するための選択肢はいくつかあります。

* ローカルモデルをサポートする組み込みモデルプロバイダーを使用する
* [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)から拡張機能をインストールする(例: [Foundry Localを使用するVS Code向けAI Toolkit](https://aka.ms/AIToolkit))
* [カスタムのOpenAI互換モデル](#_add-an-openaicompatible-model)を構成する

現在、インライン候補ではローカルモデルに接続できません。VS Codeには、拡張機能がカスタム補完プロバイダーを提供できる拡張機能API[`InlineCompletionItemProvider`](/api/references/vscode-api.md#InlineCompletionItemProvider)があります。[インライン補完のサンプル](https://github.com/microsoft/vscode-extension-samples/blob/main/inline-completions)から始められます。

> [!NOTE]
> 現在、ローカルホストのモデルを使用する場合でも、一部のタスクではCopilotサービスが必要です。そのため、GitHubアカウントがCopilotプラン(例: Copilot Free)にアクセスできる必要があり、オンラインである必要があります。この要件は将来のリリースで変更される可能性があります。

### インターネット接続なしでローカルモデルを使用できますか?

現在、ローカルモデルを使用するにはCopilotサービスへのアクセスが必要であり、そのためオンラインである必要があります。この要件は将来のリリースで変更される可能性があります。

### Copilotプランなしでローカルモデルを使用できますか?

いいえ。現在、ローカルモデルを使用するにはCopilotプラン(例: Copilot Free)にアクセスできる必要があります。この要件は将来のリリースで変更される可能性があります。

## 関連リソース

* [GitHub Copilotで利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)
