---
ContentId: 33e63aa1-1d8f-4d23-9733-1475f8c9f502
DateApproved: 3/9/2026
MetaDescription: さまざまなAI言語モデルから選択する方法と、Visual Studio Codeで独自の言語モデルAPIキーを使用する方法について学習します。
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
# VS Codeの AI言語モデル

Visual Studio Codeは、異なるタスクに最適化されたさまざまなビルトイン言語モデルを提供しています。また、独自の言語モデルAPIキーを使用して、他のプロバイダーのモデルを使用することもできます。

言語モデルの動作とその主な特性に関する背景については、[言語モデルの概念](/docs/copilot/concepts/language-models.md)を参照してください。

この記事では、チャットまたはインライン提案の言語モデルを変更する方法と、独自のAPIキーを使用する方法について説明します。

## タスクに適したモデルを選択する

デフォルトでは、チャットはベースモデルを使用して、コーディング、要約、知識ベースの質問、推論など、幅広いタスクに対して高速で能力のある応答を提供します。

ただし、このモデルのみを使用するに限定されていません。[言語モデルの選択](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat#ai-models-for-copilot-chat-1)から選択でき、それぞれに固有の強みがあります。一般的なガイドラインとして、高速モデル（GPT-5 Miniなど）を迅速な編集と簡単な質問に使用し、推論モデル（Claude Opusなど）を複雑なリファクタリング、アーキテクチャの決定、または複数ステップのタスクに使用してください。詳細な比較については、GitHubCopilotのドキュメントの[タスクに適したAIモデルを選択する](https://docs.github.com/en/copilot/using-github-copilot/ai-models/choosing-the-right-ai-model-for-your-task)を参照してください。

使用している[エージェント](/docs/copilot/customization/custom-agents.md)によっては、使用可能なモデルのリストが異なる場合があります。たとえば、エージェントモードでは、モデルのリストはツール呼び出しに対して適切なサポートを備えたものに制限されています。

> [!NOTE]
> Copilot BusinessまたはEnterpriseユーザーの場合、管理者はGitHub.comの[Copilotポリシー設定](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#enabling-copilot-features-in-your-organization)で`Editor Preview Features`にオプトインすることで、組織の特定のモデルを有効にする必要があります。

## チャット会話のモデルを変更する

チャット入力フィールドの言語モデルピッカーを使用して、チャット会話とコード編集に使用するモデルを変更します。

![チャットビューのモデルピッカーを示すスクリーンショット。](../images/language-models/model-dropdown-change-model.png)

> [!TIP]
> AI Toolkitエクステンションをインストールして、GitHub Copilotの機能を強化するために言語モデルを追加します。
>
> 詳細については、[チャットモデルを変更する](https://docs.github.com/en/copilot/how-tos/use-ai-models/change-the-chat-model#adding-more-models)を参照してください。

[独自の言語モデルAPIキーを使用](#独自の言語モデルキーを使用する)することで、利用可能なモデルのリストをさらに拡張できます。

有料Copilotプランがある場合、モデルピッカーはプレミアムモデルのプレミアムリクエスト乗数を表示します。GitHubCopilotドキュメントの[プレミアムリクエスト](https://docs.github.com/en/copilot/managing-copilot/monitoring-usage-and-entitlements/about-premium-requests#premium-requests)について詳しく説明しています。

## 自動モデル選択

> [!NOTE]
> 自動モデル選択はVSCodeリリース1.104以降で利用可能です。

自動モデル選択を使用すると、VSCodeは自動的にモデルを選択して、最適なパフォーマンスを確保し、特定の言語モデルの過度な使用によるレート制限を減らします。モデルのパフォーマンス低下を検出し、その時点で最適なモデルを使用します。このフィーチャーを改善し続けて、ニーズに最も適したモデルを選択します。

自動モデル選択を使用するには、チャットのモデルピッカーから**Auto**を選択します。

現在、自動はClaude Sonnet4、GPT-5、GPT-5mini、その他のモデルから選択します。組織が[特定のモデルをオプトアウト](https://docs.github.com/en/copilot/how-tos/use-ai-models/configure-access-to-ai-models)している場合、自動はそれらのモデルを選択しません。これらのモデルが利用できない場合またはプレミアムリクエストが不足している場合、自動は0x乗数でモデルにフォールバックします。

### 乗数割引

自動モデル選択を使用する場合、VSCodeは選択したモデルに基づいて変数[モデル乗数](https://docs.github.com/en/copilot/concepts/billing/copilot-requests#model-multipliers)を使用します。有料ユーザーの場合、自動はリクエスト割引を適用します。

いつでも、チャット応答にホバーすることで、使用されているモデルとモデル乗数を確認できます。

![ホバー時に選択されたモデルを表示しているチャット応答のスクリーンショット。](../images/language-models/chat-response-selected-model.png)

## 言語モデルを管理する

言語モデルエディターを使用して、利用可能なすべてのモデルを表示し、モデルピッカーに表示されるモデルを選択し、ビルトインプロバイダーまたはエクステンション提供のモデルプロバイダーから追加してモデルを追加できます。

言語モデルエディターを開くには、チャットビューのモデルピッカーから**モデルを管理**を開くか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。言語モデルエディターはデフォルトで、エディター領域の上の[モーダルオーバーレイ](/docs/getstarted/userinterface.md#modal-editors)で開きます。

![言語モデルエディターを示すスクリーンショット。](../images/language-models/language-models-editor.png)

エディターは、利用可能なすべてのモデルをリストし、モデル機能、コンテキストサイズ、課金詳細、可視性ステータスなどの重要な情報を表示します。デフォルトでは、モデルはプロバイダーでグループ化されていますが、可視性によってグループ化することもできます。

次のオプションを使用してモデルを検索およびフィルタリングできます:

* 検索ボックスでのテキスト検索
* プロバイダー: `@provider:"OpenAI"`
* 機能: `@capability:tools`、`@capability:vision`、`@capability:agent`
* 可視性: `@visible:true/false`

### モデルピッカーをカスタマイズする

言語モデルエディターでモデルの可視性ステータスを変更することで、モデルピッカーに表示されるモデルをカスタマイズできます。任意のプロバイダーからモデルを表示または非表示にできます。

リスト内のモデルの上にカーソルを置き、目のアイコンを選択して、モデルピッカーでモデルを表示または非表示にします。

![言語モデルエディターのスクリーンショット。モデルピッカーでモデルを表示または非表示にするための目のアイコンが表示されています。](../images/language-models/language-models-hide.png)

## 独自の言語モデルキーを使用する

> [!IMPORTANT]
> 独自のモデルキーを使用することは、現在Copilot BusinessまたはCopilot Enterpriseユーザーは利用できません。これは個別の最新モデルでの試験的使用を目的としています。BusinessプランとEnterpriseプランのサポートは今年の後半を予定しています。

VSCodeのGitHubCopilotには、異なるタスク用に最適化されたさまざまなビルトイン言語モデルが付属しています。ビルトインモデルとして利用できないモデルを使用したい場合は、独自の言語モデルAPIキー（BYOK）を使用して、他のプロバイダーのモデルを使用できます。

VSCodeで独自の言語モデルAPIキーを使用する利点はいくつかあります:

* **モデルの選択**: ビルトインモデルを超える、異なるプロバイダーからの数百のモデルにアクセスできます。
* **試験的使用**: ビルトインモデルではまだ利用できない新しいモデルまたはフィーチャーを試験できます。
* **ローカルコンピュート**: GitHubCopilotでサポート済みのモデルの1つのために独自のコンピュートを使用するか、まだ利用できないモデルを実行します。
* **より細かい制御**: 独自のキーを使用することで、ビルトインモデルに課せられた標準レート制限と制限をバイパスできます。

VSCodeは、モデルを追加するためのさまざまなオプションを提供します:

* [ビルトインモデルプロバイダー](#ビルトインプロバイダーからモデルを追加する)のいずれかを使用する

* Visual Studio Marketplaceから[言語モデルプロバイダーエクステンション](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)をインストール（たとえば、[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)）

### 独自のモデルキーを使用する場合の考慮事項

* チャット体験のみに適用され、インライン提案またはVSCodeのその他のAI対応フィーチャーには影響しません。
* 機能はモデル依存で、ビルトインモデルとは異なる場合があります。たとえば、ツール呼び出し、ビジョン、または思考のサポート。
* CopilotサービスAPIは、埋め込みの送信、リポジトリインデックス作成、クエリの絞り込み、意図検出、サイドクエリなどの一部のタスクに使用されます。
* BYOKを使用する場合、モデルの出力に責任あるAIフィルタリングが適用されることの保証はありません。

### ビルトインプロバイダーからモデルを追加する

VSCodeは、チャットのモデルピッカーにモデルをさらに追加するために使用できるいくつかのビルトインモデルプロバイダーをサポートしています。

ビルトインプロバイダーから言語モデルを構成するには:

1. チャットビューの言語モデルピッカーから**モデルを管理**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. 言語モデルエディターで、ページの**モデルを追加**を選択してから、リストからモデルプロバイダーを選択します。

    ![モデルプロバイダークイックピックを示すスクリーンショット。](../images/language-models/model-provider-quick-pick.png)

1. APIキーやエンドポイントURLなどのプロバイダー固有の詳細を入力します。

1. プロバイダーに応じて、モデルの詳細を入力するか、リストからモデルを選択します。

    次のスクリーンショットは、ローカルで実行されているOllamaのモデルピッカーを示しており、Phi-4モデルが展開されています。

    ![ローカルで実行されているOllamaのモデルピッカーを示すスクリーンショット。利用可能なモデルのリストから選択できます。](../images/language-models/ollama-installed-models-quick-pick.png)

1. これでチャットのモデルピッカーからモデルを選択できます。

    [エージェント](/docs/copilot/agents/overview.md)を使用する場合、モデルが利用可能になるには、ツール呼び出しをサポートする必要があります。モデルがツール呼び出しをサポートしていない場合、モデルピッカーに表示されません。

> [!NOTE]
> カスタムOpenAI互換モデルの構成は、現在[VSCode Insiders](https://code.visualstudio.com/insiders/)ではリリース1.104以降でのみ利用可能です。`setting(github.copilot.chat.customOAIModels)`設定でOpenAI互換モデル構成を手動で追加することもできます。

## モデルプロバイダーの詳細を更新する

以前に構成したモデルプロバイダーの詳細を更新するには:

1. チャットビューの言語モデルピッカーから**モデルを管理**を選択するか、コマンドパレットから**Chat: Manage Language Models**コマンドを実行します。

1. 言語モデルエディターで、更新したいモデルプロバイダーの歯車アイコンを選択します。

   ![プロバイダー名の横に歯車アイコンが表示されているモデルプロバイダークイックピックを示すスクリーンショット。](../images/language-models/reconfigure-model-provider.png)

1. APIキーやエンドポイントURLなどのプロバイダーの詳細を更新します。

## インラインチャットのモデルを変更する

エディターのインラインチャット用にデフォルト言語モデルを構成できます。これにより、チャット会話用とは異なるモデルをインラインチャット用に使用できます。

インラインチャットのデフォルトモデルを構成するには、`setting(inlineChat.defaultModel)`設定を使用します。この設定は、モデルピッカーの利用可能なすべてのモデルをリストします。

インラインチャットセッション中にモデルを変更する場合、選択はセッションの残り期間にわたって保持されます。VSCodeを再度読み込むと、モデルは`setting(inlineChat.defaultModel)`設定で指定された値にリセットされます。

## インライン提案のモデルを変更する

エディターでインライン提案を生成するために使用される言語モデルを変更するには:

1. VSCodeタイトルバーのチャットメニューから**インライン提案を構成...**を選択します。

1. **完了モデルを変更...**を選択してから、リストからモデルの1つを選択します。

> [!NOTE]
> インライン提案に利用可能なモデルは、サポートするモデルを追加するにつれて時間経過とともに進化する可能性があります。

## よくある質問

### 独自のモデルキーを使用することがCopilot BusinessまたはCopilot Enterpriseで利用できないのはなぜですか?

独自のモデルキーを使用することは、主に個別の最新モデルでの試験的使用を目的としており、まだBusinessプランやEnterpriseプランでは利用できません。これらのプランのサポートは今年の後半を予定しています。CopilotBusinessおよびEnterpriseユーザーは、ビルトイン管理モデルを引き続き使用できます。

### VSCodeのCopilotでローカルホストモデルを使用できますか?

チャットでローカルホストモデルを使用するには、[独自のモデルキーを使用](#独自の言語モデルキーを使用する)（BYOK）を使用し、ローカルモデルへの接続をサポートするモデルプロバイダーを使用できます。ローカルモデルに接続するためのさまざまなオプションがあります:

* ローカルモデルをサポートするビルトインモデルプロバイダーを使用する
* [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?term=tag%3Alanguage-models&target=VSCode&category=All%20categories&sortBy=Relevance)からエクステンションをインストール（たとえば、[AI Toolkit for VS Code with Foundry Local](https://aka.ms/AIToolkit)）

現在、インライン提案用のローカルモデルに接続することはできません。VSCodeは[`InlineCompletionItemProvider`](/api/references/vscode-api.md#InlineCompletionItemProvider)エクステンションAPIを提供して、エクステンションがカスタム完了プロバイダーに寄与できるようにします。[インライン完了サンプル](https://github.com/microsoft/vscode-extension-samples/blob/main/inline-completions)で始めることができます。

> [!NOTE]
> 現在、ローカルホストモデルを使用する場合でも、いくつかのタスクについてCopilotサービスが必要です。そのため、GitHubアカウントはCopilotプラン（たとえば、Copilot Free）へのアクセス権を持つ必要があり、オンラインである必要があります。この要件は将来のリリースで変更される可能性があります。

### インターネット接続なしでローカルモデルを使用できますか?

現在、ローカルモデルを使用するにはCopilotサービスへのアクセスが必要で、オンラインである必要があります。この要件は将来のリリースで変更される可能性があります。

### Copilotプランなしでローカルモデルを使用できますか?

いいえ、現在ローカルモデルを使用するにはCopilotプラン（たとえば、Copilot Free）へのアクセス権を持つ必要があります。この要件は将来のリリースで変更される可能性があります。

## 関連リソース

* [GitHubCopilotで利用可能な言語モデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat?tool=vscode)
* [VSCodeのAIのセキュリティに関する考慮事項](/docs/copilot/security.md)

