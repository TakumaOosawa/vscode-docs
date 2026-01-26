---
ContentId: 58ea6755-9bfa-42c2-a4c8-ff0510f9c031
DateApproved: 02/06/2025
MetaDescription: VS CodeでのGitHub Copilotを使用した開発体験を最適化するためのヒントとテクニック。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeでのCopilotのヒントとテクニック

この記事では、Visual Studio CodeでGitHub Copilotを使用するための開発体験を最適化するためのヒントとテクニックを紹介します。

## VS CodeでCopilotを使用するためのチェックリスト

Copilotを最大限に活用するには、次のチェックリストを使用してください：

1. [適切なツールを選択する](#choose-the-right-copilot-tool)。_編集、質問、またはコード記述のフローを維持するために最適化されたツールを使用してください。_

1. [Copilotをパーソナライズする](#personalize-copilot-with-instructions-files)。_カスタム指示を使用して、自分のスタイルやコーディング規約に合ったコード提案を取得してください。_

1. [効果的なプロンプトを作成する](#prompt-engineering)および[コンテキスト](#provide-the-right-context-and-tools)を提供する。_最も関連性の高い回答を取得してください。_

1. [ワークスペースにインデックスを付ける](#workspace-indexing)。_コードベースに関する質問に対して正確な回答を受け取ってください。_

1. [AIモデルを選択する](#choose-your-ai-model)。_高速コーディングまたは計画/推論のためのモデルを選択してください。_

1. [プロンプトを再利用する](#reusable-prompts)。_チーム全体でタスク固有のプロンプトを保存して再利用することで時間を節約してください。_

## 適切なCopilotツールを選択する

タスクに応じて、さまざまなCopilotツールから選択できます。

| ツール | ユースケース |
|------|----------|
| [インライン提案](/docs/copilot/ai-powered-suggestions.md) | フローを維持しながらコーディングを効率化します。<br/>エディターで記述する際に、コードスニペット、変数名、関数のインライン提案を受け取ります。 |
| [チャット](/docs/copilot/chat/copilot-chat.md) | 設計アイデアのブレーンストーミングやコード提案の取得のために進行中のチャット会話を行い、必要に応じてドメイン固有のチャット参加者を呼び出します。<br/>特定のコード提案をコードベースに適用することを選択します。 |
| [エージェントの使用](/docs/copilot/chat/copilot-chat.md#built-in-agents) | エージェント型コーディングフローを開始して、高レベルの要件を実装します。<br/>エージェントは自律的に複数のツールを呼び出して、必要なコード変更とタスクを計画および実装します。 |

## 指示ファイルでCopilotをパーソナライズする

Copilotがコードを生成したり質問に答えたりするとき、使用するライブラリや変数の命名方法など、あなたのコーディング規約や好みに合わせようとします。ただし、効果的に行うための十分なコンテキストが常にあるとは限りません。たとえば、特定のフレームワークバージョンを使用している場合、プロンプトに追加のコンテキストを提供する必要があります。

AIの応答を向上させるために、_指示ファイル_を使用して、チームのコーディング規約、ツール、またはプロジェクトの詳細に関するコンテキスト詳細を提供できます。その後、これらの指示をチャットプロンプトに添付するか、自動的に適用させることができます。

ワークスペースで指示ファイルを有効にするには：

1. コマンドパレットから**Chat: New Instructions File**コマンドを実行します。

    このコマンドは、`.github/instructions`フォルダーに`.instructions.md`ファイルを作成します。

1. マークダウン形式で指示をファイルに追加します。例：

    ```markdown
    # Custom instructions for Copilot

    ## Project context
    This project is a web application built with React and Node.js.

    ## Indentation
    We use tabs, not spaces.

    ## Coding style
    Use camelCase for variable names and prefer arrow functions over traditional function expressions.

    ## Testing
    We use Jest for unit testing and Playwright for end-to-end testing.
    ```

1. オプションで、`applyTo`メタデータフィールドにglobパターンを追加して、指示が適用されるファイルを指定します。

    ```markdown
    ---
    applyTo: "**/*.ts"
    ---
    Coding practices for TypeScript files.
    ...
    ```

[VS Codeでの指示ファイルの使用](/docs/copilot/customization/custom-instructions.md)についての詳細を取得します。

## プロンプトエンジニアリング

効果的なプロンプトを使用することで、Copilotの応答品質を向上させることができます。よく練られたプロンプトは、Copilotが要件をよりよく理解し、より関連性の高いコード提案を生成するのに役立ちます。

* 一般的なものから始めて、具体的になります。

    ```text
    Generate a Calculator class.
    Add methods for addition, subtraction, multiplication, division, and factorial.
    Don't use any external libraries and don't use recursion.
    ```

* 欲しいものの例を示します。

    ```text
    Generate a function that takes a string and returns the number of vowels in it.
    Example:
    findVowels("hello") returns 2
    findVowels("sky") returns 0
    ```

* 複雑なタスクをより単純なタスクに分割します。

    Copilotに食事プランナーアプリを生成するように頼む代わりに、より小さなタスクに分割します：
    * 食材のリストを受け取り、レシピのリストを返す関数を生成する。
    * レシピのリストを受け取り、買い物リストを返す関数を生成する。
    * レシピのリストを受け取り、1週間の食事プランを返す関数を生成する。

* コード選択、ファイル、ターミナル出力などの[適切なコンテキスト](#provide-the-right-context-and-tools)を提供します。

    例、`#codebase`変数を使用してコードベース全体を参照します：

    ```text
    Where is the database connection string used in #codebase?
    ```

* プロンプトを反復します。

    応答を改良または修正するために、フォローアッププロンプトを提供します。例：

    * "Write a function to calculate the factorial of a number."
    * "Don't use recursion and optimize by using caching."
    * "Use meaningful variable names."

* チャット履歴を関連性のあるものに保ちます。

    Copilotは会話の履歴を使用してコンテキストを提供します。関連性がない場合は、過去の質問と回答を履歴から削除します。または、コンテキストを変更したい場合は新しいセッションを開始します。

[プロンプトエンジニアリング](/docs/copilot/guides/prompt-engineering-guide.md)についての詳細を取得します。

GitHub Copilotドキュメントで[チャットで使用するプロンプトの実践的な例](https://docs.github.com/en/copilot/copilot-chat-cookbook)を見つけます。

## 適切なコンテキストとツールを提供する

プロンプトに関連するコンテキストを充実させて、チャットでより正確で関連性の高い回答を取得します。適切なツールを使用すると、開発者の生産性を高めることができます。

* [チャット](/docs/copilot/chat/chat-tools.md)で、ツールボタンを選択して使用したいツールを構成するか、プロンプトに明示的に追加します。
* `#codebase`を使用して、Copilotがコード検索を実行して適切なファイルを自動的に見つけられるようにします。
* `#fetch`ツールを使用してWebページからコンテンツを取得するか、`#githubRepo`を使用してGitHubリポジトリでコード検索を実行します。
* `#<file name>`、`#<folder name>`、または`#<symbol>`を使用して、プロンプト内のファイル、フォルダー、またはシンボルを参照します。
* ファイル、フォルダー、またはエディタータブをチャットプロンプトにドラッグアンドドロップします。
* 問題、テストの失敗、またはターミナル出力をチャットプロンプトに追加して、シナリオ固有のコンテキストを提供します。
* 画像またはスクリーンショットをプロンプトに追加して、Copilotに画像を分析させます。
* エージェントを使用する場合、アプリをプレビューするようにプロンプトを出して、組み込みのシンプルブラウザで直接開きます。

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用する場合、エージェントは関連するファイルとコンテキストを自律的に見つけます。

[チャットプロンプトへのコンテキストの追加](/docs/copilot/chat/copilot-chat-context.md)についての詳細を取得します。

## 再利用可能なプロンプト

プロンプトファイルを使用すると、特定のタスクのプロンプトをそのコンテキストと指示とともにマークダウンファイルに保存できます。その後、そのプロンプトをチャットに添付して再利用できます。プロンプトをワークスペースに保存すると、チームと共有することもできます。

再利用可能なプロンプトを作成するには：

1. コマンドパレットの**Chat: New Prompt File**コマンドを使用してプロンプトファイルを作成します。

    このコマンドは、ワークスペースのルートにある`.github/prompts`フォルダーに`.prompt.md`ファイルを作成します。

1. マークダウン形式でプロンプトと関連するコンテキストを記述します。

    たとえば、新しいReactフォームコンポーネントを生成するためにこのプロンプトを使用します。

    ```markdown
    Your goal is to generate a new React form component.

    Ask for the form name and fields if not provided.

    Requirements for the form:
    * Use form design system components: [design-system/Form.md](../docs/design-system/Form.md)
    * Use `react-hook-form` for form state management:
    * Always define TypeScript types for your form data
    * Prefer *uncontrolled* components using register
    * Use `defaultValues` to prevent unnecessary rerenders
    * Use `yup` for validation:
    * Create reusable validation schemas in separate files
    * Use TypeScript types to ensure type safety
    * Customize UX-friendly validation rules
    ```

1. オプションで、チャットでプロンプトを実行する方法に関するメタデータを追加します。`agent`フィールドを使用してエージェントを指定し、`tools`フィールドを使用して使用するエージェントモードツールを指定します。

    ```markdown
    ---
    agent: 'agent'
    tools: ['githubRepo', 'search/codebase']
    description: 'Generate a new React form component'
    ---
    Your goal is to generate a new React form component based on the templates in #githubRepo contoso/react-templates.

    Requirements for the form:
    * Use form design system components: [design-system/Form.md](../docs/design-system/Form.md)
    * Use `react-hook-form` for form state management:
    * Always define TypeScript types for your form data
    ```

1. チャット入力フィールドに`/`に続いてプロンプトファイル名を入力してコマンドを実行します。

    たとえば、`/new-react-form`と入力して、`new-react-form.prompt.md`という名前のプロンプトファイルを実行します。

[プロンプトファイル](/docs/copilot/customization/prompt-files.md)の使用を開始します。

## AIモデルを選択する

Copilotは、選択できるさまざまなAIモデルを提供しています。一部のモデルは高速なコーディングタスクに最適化されていますが、他のモデルはより遅い計画や推論のタスクに適しています。

| モデルタイプ | モデル |
|-----------|--------|
| 高速コーディング | <ul><li>GPT-4o</li><li>Claude Sonnet 3.5</li><li>Claude Sonnet 3.7</li><li>Gemini 2.0 Flash</li></ul> |
| 推論/計画 | <ul><li>Claude Sonnet 3.7 Thinking</li><li>o1</li><li>o3-mini</li></ul> |

チャット入力フィールドのモデルピッカーを使用して、ニーズに最適なモデルを選択してください。

GitHub Copilotドキュメントで[Copilot ChatのAIモデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat)について詳しく学びます。

## ワークスペースのインデックス作成

Copilotはインデックスを使用して、関連するコードスニペットについてコードベースを迅速かつ正確に検索します。このインデックスは、GitHubによって維持されるか、マシンにローカルに保存されます。

GitHubリポジトリの場合、[GitHubのコード検索](https://docs.github.com/en/enterprise-cloud@latest/copilot/using-github-copilot/asking-github-copilot-questions-in-github#asking-exploratory-questions-about-a-repository)に基づいて、ワークスペースのリモートインデックスを使用できます。これにより、Copilotはコードベースが非常に大きい場合でも、コードベース全体を非常に迅速に検索できます。

[ワークスペースのインデックス作成](/docs/copilot/reference/workspace-context.md)についての詳細を取得します。

## 関連リソース

* [プロンプトエンジニアリングガイド](/docs/copilot/guides/prompt-engineering-guide.md)
* GitHub Copilotドキュメントの[GitHub Copilotの使用に関するベストプラクティス](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
* [VS Codeでのチャットのカスタマイズ](/docs/copilot/customization/overview.md)
