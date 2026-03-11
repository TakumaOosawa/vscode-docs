---
ContentId: 8b3c9f5e-4d2a-6f9b-3e1c-7a8d5f2e9b0c
DateApproved: 3/9/2026
MetaDescription: VS Codeのコンテキスト分離されたサブエージェントを使用して、チャットセッション内で複雑なタスクを自律的なエージェントに委任する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- subagents
- agents
- context isolation
- copilot
- ai
- context window
- parallel
---

# Visual Studio Codeのサブエージェント

複雑なタスクに取り組むときは、サブタスクをサブエージェントに委任できます。サブエージェントは、トピックの調査、コード分析、変更のレビューなどの詳細な作業を実行し、結果をメインエージェントに報告する独立したAIエージェントです。

サブエージェントの概念（コンテキスト分離、同期および並列実行）の背景については、「[エージェントの概念](/docs/copilot/concepts/agents.md#subagents)」を参照してください。

この記事では、使用シナリオ、呼び出しパターン、カスタムエージェントをサブエージェントとして実行する方法を含む、VS Codeのサブエージェントの使用方法について説明します。

### ユーザーに表示される内容

サブエージェントが実行されると、チャットに折りたたみ可能なツール呼び出しとして表示されます。デフォルトではサブエージェントは折りたたまれており、以下が表示されます:

* カスタムエージェントの名前（指定した場合）
* 現在実行中のツール（例えば、「ファイルを読み込み中...」または「コードベースを検索中...」）

サブエージェントツール呼び出しを選択して展開すると、サブエージェントが実行したすべてのツール呼び出し、サブエージェントに渡されたプロンプト、返された結果を含む詳細全体を表示できます。

この可視性により、メインの会話を中間ステップで散らかすことなく、表示される詳細量を制御できます。

## 使用シナリオ

次のシナリオは、サブエージェントがAI支援開発ワークフローを改善する場合を示しています。

<details>
<summary>実装前の調査</summary>

新機能を構築する場合、サブエージェントを使用して、メインエージェントが実装を開始する前に、ベストプラクティスを調査したり、ライブラリを評価したり、コードベース内の既存のパターンを分析したりします:

```prompt
Node.jsアプリケーション用のOAuth 2.0実装パターンを調査するサブエージェントを使用します。
passport.js対auth0対カスタム実装を比較します。メリットとデメリット付きの推奨事項を返します。
```

メインエージェントは最終的な推奨事項のみを受け取るため、実装作業のためのコンテキストはクリーンに保たれます。

</details>

<details>
<summary>並列コード分析</summary>

コードのリファクタリングまたはレビューの場合、複数のサブエージェントを並列で実行して、異なる側面を分析します:

```prompt
このコードベースでリファクタリングの機会を分析します。サブエージェントを使用して:
1. 重複するコードパターンを検出
2. 未使用のエクスポートとデッドコードを特定
3. エラーハンドリングの一貫性をレビュー
4. セキュリティの脆弱性をチェック

調査結果を優先度付けされたアクション計画にコンパイルします。
```

</details>

<details>
<summary>複数のソリューションを探索</summary>

最適なアプローチについて不確かな場合、サブエージェントを使用してメインコンテキストを汚さずに異なるオプションを探索します:

```prompt
このAPIのキャッシングを実装する必要があります。3つのサブエージェントを並列で実行して:
1. Redisベースのキャッシングソリューションを設計
2. LRUキビクションを備えたインメモリキャッシングソリューションを設計
3. 段階的キャッシングを備えたハイブリッドアプローチを設計

結果を比較し、ユースケースに最適なアプローチを推奨します。
```

</details>

<details>
<summary>特定のフォーカスを備えたコードレビュー</summary>

カスタムエージェントをサブエージェントとして使用して、異なるレビューの視点を適用します:

```prompt
サブエージェントを使用してこのPRの変更をレビューします:
- security-reviewerエージェントを実行して脆弱性をチェック
- performance-reviewerエージェントを実行してボトルネックを特定
- accessibility-reviewerエージェントを実行してa11yコンプライアンスを確認

調査結果を単一のレビュー概要に統合します。
```

</details>

## サブエージェントを呼び出す

### エージェント開始対ユーザー呼び出し

サブエージェントは通常、ユーザーがチャットで直接呼び出すのではなく、**エージェント開始**です。メインエージェントがサブエージェントを呼び出すことを許可するには、`runSubagent`ツールが有効になっていることを確認してください。

メインエージェントは、コンテキスト分離が役立つ場合を判断します。タスクごとに「サブエージェントを実行」と手動で入力する必要はありません。パターンは次のように機能します:

1. あなた（またはカスタムエージェントの指示）が複雑なタスクを説明します。
1. メインエージェントは、分離されたコンテキストから利益を得るタスクの部分を認識します。
1. エージェントはサブエージェントを開始し、関連するサブタスクのみを渡します。
1. サブエージェントは自律的に機能し、概要を返します。
1. メインエージェントは結果を組み込み続行します。

プロンプトを分離された調査または並列分析を示唆するように表現することで、サブエージェント委任が必要であることをヒントすることができます。メインエージェントがサブエージェントを開始し、タスクをそれに渡して、最終結果のみを受け取ります。

> [!TIP]
> サブエージェントの一貫した動作のため、毎回手動でプロンプトするのではなく、カスタムエージェントの指示にサブエージェントを使用する場合を定義します。

サブエージェントのパフォーマンスを最適化するには、タスクと予期される出力を明確に定義します。これにより、サブエージェントは不要なコンテキストをメインエージェントに戻さずに特定の目標に集中するのに役立ちます。

使用シナリオセクションで、サブエージェントを呼び出すプロンプトを構造化する方法の例を参照してください。

### プロンプトファイルでサブエージェントを呼び出す

プロンプトファイル内でサブエージェントを呼び出すには、`runSubagent`または`agent`ツールが`tools`フロントマター プロパティに含まれていることを確認してください:

```markdown
---
name: document-feature
tools: ['agent', 'read', 'search', 'edit']
---
Run a subagent to research the new feature implementation details and return only information relevant for user documentation.
Then update the docs/ folder with the new documentation.
```

プロンプト指示では、特定のサブタスクに対する分離された調査または並列分析を示唆することで、エージェントにサブエージェントを使用するようにヒントできます。

## カスタムエージェントをサブエージェントとして実行（実験的）

デフォルトでは、サブエージェントはメインチャットセッションからエージェントを継承し、同じモデルとツールを使用します。サブエージェント用の特定の動作を定義するには、[カスタムエージェント](/docs/copilot/customization/custom-agents.md)を使用します。カスタムエージェントは独自のモデル、ツール、指示を指定できます。サブエージェントとして使用されると、これらの設定はメインセッションから継承されたデフォルトをオーバーライドします。

### サブエージェント呼び出しを制御

2つのフロントマタープロパティを使用して、カスタムエージェントの呼び出し方法を制御できます:

* `user-invocable`: エージェントがチャットのエージェントドロップダウンに表示されるかどうかを制御します（デフォルトは`true`）。サブエージェントとしてのみアクセス可能なエージェントを作成するには、`false`に設定します。
* `disable-model-invocation`: エージェントが他のエージェントによってサブエージェントとして呼び出されるのを防ぎます（デフォルトは`false`）。エージェントをユーザーが明示的にトリガーする場合のみの場合は、`true`に設定します。

例えば、サブエージェントとしてのみ使用可能なエージェント（ドロップダウンに表示されない）を作成するには:

```markdown
---
name: internal-helper
user-invocable: false
---

This agent can only be invoked as a subagent.
```

> [!NOTE]
> `infer`プロパティは非推奨です。より詳細な制御のために`user-invocable`と`disable-model-invocation`を代わりに使用してください。

カスタムエージェントをサブエージェントとして実行するには、カスタムまたはビルト インエージェントをサブエージェントに使用するようにAIにプロンプトします。例えば:

* `Run the Research agent as a subagent to research the best auth methods for this project.`
* `Use the Plan agent in a subagent to create an implementation plan for myfeature. Then save the plan in plans/myfeature.plan.md`

### 使用できるサブエージェントを制限（実験的）

デフォルトでは、`disable-model-invocation: true`を持たないすべてのカスタムエージェントはサブエージェントとして使用可能です。2つ以上のエージェントが同様の名前または説明を持つ場合、AIは意図しないエージェントを選択する可能性があります。

メインエージェントのフロントマターで`agents`プロパティを指定し、許可するカスタムエージェントのリストを提供することで、サブエージェントとして使用できるカスタムエージェントを制限できます。

`agents`プロパティは以下を受け入れます:

* エージェント名のリスト（例えば、`['Edit', 'Search']`）特定のエージェントのみを許可
* `*`すべての利用可能なエージェントを許可（デフォルトの動作）
* 空配列`[]`サブエージェントの使用を防止

> [!NOTE]
> `agents`配列にエージェントを明示的にリストすると、`disable-model-invocation: true`がオーバーライドされます。これは、一般的なサブエージェント使用から保護されていが、それらを明示的に許可する特定のコーディネーターエージェントにアクセス可能なエージェントを作成できることを意味します。

例えば、テスト駆動開発（TDD）エージェントは、`Red`、`Green`、および`Refactor`エージェントのみをサブエージェントとして使用する必要があります。制限されない場合、TDDエージェントはテストを実装するために特化したTDDエージェントの代わりにより汎用的なコーディングエージェントを選択する可能性があります。

```markdown
---
name: TDD
tools: ['agent']
agents: ['Red', 'Green', 'Refactor']
---
Implement the following feature using test-driven development. Use subagents to guide the following steps:
1. Use the Red agent to write failing tests
2. Use the Green agent to implement code to pass the tests
3. Use the Refactor agent to improve the code quality
```

## オーケストレーションパターン

サブエージェントは、コーディネーターエージェントが仕事を特化したワーカーエージェントに委任する**オーケストレーションパターン**を有効にします。このアプローチは、各エージェントが最適なことに焦点を当てながら洗練されたワークフローを構築するのに役立ちます。

### コーディネーターとワーカーパターン

コーディネーターエージェントは全体的なタスクを管理し、サブタスクを特化したサブエージェントに委任します。各ワーカーエージェントは調整されたツールセットを持つことができます。例えば、計画およびレビューエージェントは読み取り専用アクセスのみが必要であり、実装者は編集機能が必要です。

```markdown
---
name: Feature Builder
tools: ['agent', 'edit', 'search', 'read']
agents: ['Planner', 'Plan Architect', 'Implementer', 'Reviewer']
---
You are a feature development coordinator. For each feature request:

1. Use the Planner agent to break down the feature into tasks.
2. Use the Plan Architect agent to validate the plan against codebase patterns.
3. If the architect identifies reusable patterns or libraries, send feedback to the Planner to update the plan.
4. Use the Implementer agent to write the code for each task.
5. Use the Reviewer agent to check the implementation.
6. If the reviewer identifies issues, use the Implementer agent again to apply fixes.

Iterate between planning and architecture, and between review and implementation, until each phase converges.
```

ワーカーエージェントはそれぞれ独自のツールアクセスを定義し、よりナロー なフォーカスのため高速またはコスト効率的なモデルを選択できます:

```markdown
---
name: Planner
user-invocable: false
tools: ['read', 'search']
---
Break down feature requests into implementation tasks. Incorporate feedback from the Plan Architect.
```

```markdown
---
name: Plan Architect
user-invocable: false
tools: ['read', 'search']
---
Validate plans against the codebase. Identify existing patterns, utilities, and libraries that should be reused. Flag any plan steps that duplicate existing functionality.
```

```markdown
---
name: Implementer
user-invocable: false
model: ['Claude Haiku 4.5 (copilot)', 'Gemini 3 Flash (Preview) (copilot)']
---
Write code to complete assigned tasks.
```

このパターンは、コーディネーターのコンテキストを高レベルのワークフローに集約しておき、各ワーカーエージェントはクリーンなコンテキストと特定のジョブのための適切なアクセス許可を持ちます。

### マルチパースペクティブコードレビュー

コードレビューは複数の視点から利益を得ます。単一のパーサーは多くの問題を見逃す傾向があります。異なるレンズを通して見ると明らかになる問題があります。サブエージェントを使用して各レビュー視点を並列で実行し、調査結果を統合します。

```markdown
---
name: Thorough Reviewer
tools: ['agent', 'read', 'search']
---
You review code through multiple perspectives simultaneously. Run each perspective as a parallel subagent so findings are independent and unbiased.

When asked to review code, run these subagents in parallel:
- Correctness reviewer: logic errors, edge cases, type issues.
- Code quality reviewer: readability, naming, duplication.
- Security reviewer: input validation, injection risks, data exposure.
- Architecture reviewer: codebase patterns, design consistency, structural alignment.

After all subagents complete, synthesize findings into a prioritized summary. Note which issues are critical versus nice-to-have. Acknowledge what the code does well.
```

このパターンは機能します。各サブエージェントは他の視点が見つけたことによってアンカーされることなく、コードに初めてアプローチするためです。この例では、オーケストレーターはプロンプトを通じて各サブエージェントのフォーカスエリアを形成します。これは追加のエージェントファイルを必要としない軽量なアプローチです。

> [!TIP]
> より多くの制御のため、各レビュー視点は特化したツールアクセスを持つ独自のカスタムエージェントになることができます。例えば、セキュリティレビュアーはセキュリティに焦点を当てたMCPサーバーを使用する可能性があり、コード品質レビュアーはリンティングCLIツールへのアクセスを持つ可能性があります。このアプローチにより、各視点は特定のフォーカスに最適なツールを使用できます。

## 関連リソース

* [エージェントの概要](/docs/copilot/agents/overview.md)-VS Codeの異なるタイプのエージェントについて学習
* [カスタムエージェント](/docs/copilot/customization/custom-agents.md)-独自のAIエージェントを作成
* [チャットセッション](/docs/copilot/chat/chat-sessions.md)-VS Codeでチャットセッションを管理

