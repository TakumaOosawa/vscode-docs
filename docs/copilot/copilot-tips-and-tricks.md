---
ContentId: 58ea6755-9bfa-42c2-a4c8-ff0510f9c031
DateApproved: 02/06/2025
MetaDescription: VS CodeのGitHub Copilotで開発体験を最適化するためのヒントとコツ。
MetaSocialImage: images/shared/github-copilot-social.png
---
# VS CodeのCopilotのヒントとコツ

この記事では、Visual Studio CodeでGitHub Copilotを使用する際の開発体験を最適化するためのヒントとコツを紹介します。

## VS CodeでCopilotを使用するためのチェックリスト

Copilotを最大限に活用するために、次のチェックリストを使用してください。

1. [適切なツールを選ぶ](#choose-the-right-copilot-tool)。_編集、質問、またはコード記述のフローを維持するのに最適化されたツールを使用します。_

1. [Copilotをパーソナライズする](#personalize-copilot-with-instructions-files)。_カスタム指示を使用して、あなたのスタイルやコーディング慣行に合ったコード提案を得ます。_

1. [効果的なプロンプトを書く](#prompt-engineering)と、[コンテキスト](#provide-the-right-context-and-tools)を提供する。_最も関連性の高い応答を得ます。_

1. [ワークスペースをインデックス化する](#workspace-indexing)。_コードベースに関する質問に対して正確な応答を受け取ります。_

1. [AIモデルを選ぶ](#choose-your-ai-model)。_高速コーディング向け、または計画/推論向けのモデルから選択します。_

1. [プロンプトを再利用する](#reusable-prompts)。_タスク固有のプロンプトを保存し、チーム内で再利用することで時間を節約します。_

## 適切なCopilotツールを選ぶ

タスクに応じて、さまざまなCopilotツールから選択できます。

| Tool | Use case |
|------|----------|
| [インライン提案](/docs/copilot/ai-powered-suggestions.md) | フローを維持しながらコーディングを効率化します。<br/>エディターで入力している間に、コードスニペット、変数名、関数のインライン提案を受け取れます。 |
| [チャット](/docs/copilot/chat/copilot-chat.md) | 設計アイデアのブレインストーミングやコード提案の取得のために継続的なチャット会話を行います。必要に応じて、ドメイン固有のチャット参加者を呼び出すこともできます。<br/>特定のコード提案をコードベースに適用することを選択できます。 |
| [エージェントを使用する](/docs/copilot/chat/copilot-chat.md#built-in-agents) | エージェント型のコーディングフローを開始して、高レベルの要件を実装します。<br/>エージェントは複数のツールを自律的に呼び出し、必要なコード変更やタスクの計画と実装を行います。 |

## 指示ファイルでCopilotをパーソナライズする

Copilotがコードを生成したり質問に回答したりするとき、使用しているライブラリや変数の命名方法など、あなたのコーディング慣行や好みに合わせようとします。ただし、常に十分なコンテキストがあるとは限らず、効果的に合わせられない場合があります。たとえば、特定のフレームワークバージョンで作業している場合は、プロンプトに追加のコンテキストを提供する必要があります。

AIの応答を強化するために、_指示ファイル_を使用して、チームのコーディング慣行、ツール、プロジェクト固有の情報などのコンテキスト詳細を提供できます。これらの指示をチャットプロンプトに添付することも、自動的に適用することもできます。

ワークスペースで指示ファイルを有効にするには:

1. コマンド パレットから**Chat: New Instructions File**コマンドを実行します。

    このコマンドにより、`.github/instructions`フォルダーに`.instructions.md`ファイルが作成されます。

1. ファイルにMarkdown形式で指示を追加します。例:

    ```markdown
    # Copilotのカスタム指示

    ## プロジェクトのコンテキスト
    このプロジェクトはReactとNode.jsで構築されたWebアプリケーションです。

    ## インデント
    スペースではなくタブを使用します。

    ## コーディングスタイル
    変数名にはcamelCaseを使用し、従来の関数式よりもアロー関数を優先します。

    ## テスト
    ユニットテストにはJestを使用し、エンドツーエンドテストにはPlaywrightを使用します。
    ```

1. 必要に応じて、`applyTo`メタデータ フィールドにglobパターンを追加し、指示を適用するファイルを指定します。

    ```markdown
    ---
    applyTo: "**/*.ts"
    ---
    TypeScriptファイルのコーディング慣行。
    ...
    ```

[VS Codeで指示ファイルを使用する](/docs/copilot/customization/custom-instructions.md)詳細をご覧ください。

## プロンプト エンジニアリング

効果的なプロンプトを使用すると、Copilotの応答品質を向上できます。よく練られたプロンプトは、Copilotが要件をより理解しやすくし、より関連性の高いコード提案を生成するのに役立ちます。

* まずは大まかに始めて、次に具体化します。

    ```text
    Calculatorクラスを生成してください。
    加算、減算、乗算、除算、階乗のメソッドを追加してください。
    外部ライブラリは使用せず、再帰も使用しないでください。
    ```

* 求める結果の例を示します。

    ```text
    文字列を受け取り、その中の母音の数を返す関数を生成してください。
    例:
    findVowels("hello")は2を返す
    findVowels("sky")は0を返す
    ```

* 複雑なタスクは、より単純なタスクに分割します。

    Copilotに献立プランナー アプリを生成するよう求める代わりに、より小さなタスクに分割します:
    * 材料のリストを受け取り、レシピのリストを返す関数を生成します。
    * レシピのリストを受け取り、買い物リストを返す関数を生成します。
    * レシピのリストを受け取り、1週間分の食事プランを返す関数を生成します。

* コードの選択、ファイル、ターミナル出力などの[適切なコンテキスト](#provide-the-right-context-and-tools)を提供します。

    例: `#codebase`変数を使用してコードベース全体を参照します:

    ```text
    Where is the database connection string used in #codebase?
    ```

* プロンプトを反復して改善します。

    フォローアップ プロンプトを提示して、応答を洗練または変更します。例:

    * "数の階乗を計算する関数を書いてください。"
    * "再帰は使わず、キャッシュを使用して最適化してください。"
    * "意味のある変数名を使ってください。"

* チャット履歴の関連性を保ちます。

    Copilotは会話の履歴をコンテキストとして使用します。関連しない過去の質問や応答は履歴から削除してください。あるいは、コンテキストを変えたい場合は新しいセッションを開始してください。

[プロンプト エンジニアリング](/docs/copilot/guides/prompt-engineering-guide.md)の詳細をご覧ください。

GitHub Copilotのドキュメントで、チャットで使用できる実用的な[プロンプト例](https://docs.github.com/en/copilot/copilot-chat-cookbook)を確認してください。

## 適切なコンテキストとツールを提供する

関連するコンテキストでプロンプトを強化すると、チャットでより正確で関連性の高い応答を得られます。適切なツールを使うことで、開発者の生産性を高められます。

* [チャット](/docs/copilot/chat/chat-tools.md)でツール ボタンを選択して、使用したいツールを構成するか、プロンプトに明示的に追加します。
* `#codebase`を使用すると、Copilotがコード検索を実行して適切なファイルを自動的に見つけます。
* `#fetch`ツールを使用してWebページからコンテンツを取得するか、`#githubRepo`を使用してGitHubリポジトリ上でコード検索を実行します。
* `#<file name>`、`#<folder name>`、`#<symbol>`を使用して、プロンプトでファイル、フォルダー、またはシンボルを参照します。
* ファイル、フォルダー、またはエディター タブをチャット プロンプトにドラッグ アンド ドロップします。
* シナリオ固有のコンテキストとして、問題、テストの失敗、またはターミナル出力をチャット プロンプトに追加します。
* 画像やスクリーンショットをプロンプトに追加して、Copilotに画像を分析させます。
* エージェントを使用する場合は、アプリをプレビューするよう促して、組み込みのシンプル ブラウザーで直接開きます。

[エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用すると、エージェントが関連するファイルとコンテキストを自律的に見つけます。

[チャット プロンプトへのコンテキスト追加](/docs/copilot/chat/copilot-chat-context.md)の詳細をご覧ください。

## 再利用可能なプロンプト

プロンプト ファイルを使用すると、特定のタスク向けのプロンプトを、そのコンテキストと指示とともにMarkdownファイルに保存できます。その後、そのプロンプトをチャットに添付して再利用できます。プロンプトをワークスペースに保存すれば、チームと共有することもできます。

再利用可能なプロンプトを作成するには:

1. コマンド パレットの**Chat: New Prompt File**コマンドでプロンプト ファイルを作成します。

    このコマンドにより、ワークスペースのルートにある`.github/prompts`フォルダーに`.prompt.md`ファイルが作成されます。

1. プロンプトと関連するコンテキストをMarkdown形式で記述します。

    たとえば、このプロンプトを使用して新しいReactフォーム コンポーネントを生成します。

    ```markdown
    目的は、新しいReactフォーム コンポーネントを生成することです。

    フォーム名とフィールドが提供されていない場合は、尋ねてください。

    フォームの要件:
    * Use form design system components: [design-system/Form.md](../docs/design-system/Form.md)
    * フォームの状態管理には`react-hook-form`を使用する:
    * フォーム データには常にTypeScript型を定義する
    * registerを使用する*非制御*コンポーネントを優先する
    * 不要な再レンダーを防ぐために`defaultValues`を使用する
    * 検証には`yup`を使用する:
    * 再利用可能な検証スキーマを別ファイルに作成する
    * 型安全性を確保するためにTypeScript型を使用する
    * UXに配慮した検証ルールをカスタマイズする
    ```

1. 必要に応じて、チャットでプロンプトを実行する方法に関するメタデータを追加します。`agent`フィールドでエージェントを指定し、`tools`フィールドで使用するエージェント モードのツールを指定します。

    ```markdown
    ---
    agent: 'agent'
    tools: ['githubRepo', 'search/codebase']
    description: '新しいReactフォーム コンポーネントを生成する'
    ---
    目的は、#githubRepo contoso/react-templates内のテンプレートに基づいて新しいReactフォーム コンポーネントを生成することです。

    フォームの要件:
    * Use form design system components: [design-system/Form.md](../docs/design-system/Form.md)
    * フォームの状態管理には`react-hook-form`を使用する:
    * フォーム データには常にTypeScript型を定義する
    ```

1. チャット入力フィールドで`/`に続けてプロンプト ファイル名を入力して、コマンドを実行します。

    たとえば、`new-react-form.prompt.md`という名前のプロンプト ファイルを実行するには`/new-react-form`と入力します。

[プロンプト ファイル](/docs/copilot/customization/prompt-files.md)を始めましょう。

## AIモデルを選ぶ

Copilotでは、複数のAIモデルから選択できます。高速なコーディング タスクに最適化されたモデルもあれば、より時間をかける計画や推論タスクに適したモデルもあります。

| Model type | Models |
|-----------|--------|
| 高速コーディング | <ul><li>GPT-4o</li><li>Claude Sonnet 3.5</li><li>Claude Sonnet 3.7</li><li>Gemini 2.0 Flash</li></ul> |
| 推論/計画 | <ul><li>Claude Sonnet 3.7 Thinking</li><li>o1</li><li>o3-mini</li></ul> |

チャット入力フィールドのモデル ピッカーを使用して、ニーズに最も合うモデルを選択してください。

GitHub Copilotのドキュメントで、[Copilot ChatのAIモデル](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat)の詳細をご覧ください。

## ワークスペースのインデックス化

Copilotはインデックスを使用して、コードベース内の関連するコード スニペットを迅速かつ正確に検索します。このインデックスはGitHubによって維持される場合もあれば、ローカル マシンに保存される場合もあります。

GitHubリポジトリでは、[GitHub code search](https://docs.github.com/en/enterprise-cloud@latest/copilot/using-github-copilot/asking-github-copilot-questions-in-github#asking-exploratory-questions-about-a-repository)に基づくワークスペースのリモート インデックスを使用できます。これにより、コードベースが非常に大きい場合でも、Copilotはコードベース全体を非常に迅速に検索できます。

[ワークスペースのインデックス化](/docs/copilot/reference/workspace-context.md)の詳細をご覧ください。

## 関連リソース

* [プロンプト エンジニアリング ガイド](/docs/copilot/guides/prompt-engineering-guide.md)
* GitHub Copilotのドキュメントの[GitHub Copilotを使用するためのベスト プラクティス](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
* [VS Codeでチャットをカスタマイズする](/docs/copilot/customization/overview.md)
