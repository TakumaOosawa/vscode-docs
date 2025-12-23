---
ContentId: 9f84b21e-5b76-4c3a-a5dd-2021ab343f1f
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotを使用してテストを作成、デバッグ、修正する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilotでテストする

テストの作成と保守はソフトウェア開発において重要ですが、しばしば時間がかかります。GitHub Copilotは、Visual Studio Codeでテストをより効率的に作成、デバッグ、修正できるように支援し、このプロセスを効率化します。この記事では、Copilotのテスト機能を活用してテストのワークフローを改善し、プロジェクトのテストカバレッジを向上させる方法を紹介します。

Copilotは次のテストタスクに役立ちます。

* **テストフレームワークをセットアップする**:プロジェクトと言語に適したテストフレームワークとVS Code拡張機能の構成について支援を受けます。
* **テストコードを生成する**:アプリケーションコードをカバーする単体テスト、統合テスト、エンドツーエンドテストを作成します。
* **エッジケースを扱う**:エッジケースとエラー条件をカバーする包括的なテストスイートを生成します。
* **失敗したテストを修正する**:テストの失敗を修正するための提案を受け取ります。
* **一貫性を保つ**:プロジェクトのコーディングプラクティスに沿ったテストを生成するようにCopilotをパーソナライズします。

> [!TIP]
> まだCopilotのサブスクリプションがない場合は、[Copilot Free plan](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で使用でき、インライン候補とチャットのやり取りに月ごとの上限があります。

## テストフレームワークをセットアップする

テストのワークフローを加速するために、CopilotはプロジェクトのテストフレームワークとVS Code拡張機能のセットアップを支援できます。Copilotはプロジェクトの種類に基づいて適切なテストフレームワークを提案します。

1. Chat view(`kb(workbench.action.chat.open)`)を開きます。
1. チャットの入力フィールドに`/setupTests`コマンドを入力します。
1. Copilotのガイダンスに従ってプロジェクトを構成します。

## Copilotでテストを書く

Copilotは、コードベースをカバーするテストコードを生成することで、アプリケーションコードのテスト作成を支援できます。これには、単体テスト、エンドツーエンドテスト、エッジケースのテストが含まれます。

### チャットプロンプトを使用する

1. アプリケーションコードのファイルを開きます。

1. 次のいずれかのビューを開きます。
    * Chat view(`kb(workbench.action.chat.open)`)
    * Inline Chat(`kb(inlineChat.start)`)

1. 次のようなプロンプトを入力します。
    * "このコードのテストを生成して"
    * "エッジケースを含む単体テストを書いて"
    * "このモジュールの統合テストを作成して"

GitHubのドキュメントで、[GitHub Copilotを使用してテストを書く](https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/writing-tests-with-github-copilot)に関する詳細なガイダンスを確認してください。

### エディターのスマートアクションを使用する

プロンプトを書かずにアプリケーションコードのテストを生成するには、エディターのスマートアクションを使用できます。

1. アプリケーションコードのファイルを開きます。
1. 必要に応じて、テストしたいコードを選択します。
1. 右クリックして、**Generate Code** > **Generate Tests**を選択します。

    Copilotは既存のテストファイルにテストコードを生成するか、存在しない場合は新しいテストファイルを作成します。

1. 必要に応じて、Inline Chatプロンプトで追加のコンテキストを提供して、生成されたテストを改善します。

## 失敗したテストを修正する

CopilotはVS CodeのTest Explorerと統合されており、失敗したテストの修正を支援できます。

1. Test Explorerで、失敗しているテストにカーソルを合わせます
1. **Fix Test Failure**ボタン(きらめきアイコン)を選択します
1. Copilotが提案した修正を確認して適用します

または、次の手順でも実行できます。

1. Chat viewを開きます
1. `/fixTestFailure`コマンドを入力します
1. Copilotの提案に従ってテストを修正します

> [!TIP]
> [エージェント](/docs/copilot/chat/copilot-chat.md#built-in-agents)を使用すると、エージェントはテスト実行時のテスト出力を監視し、失敗したテストの修正と再実行を自動的に試みます。

## テスト生成をパーソナライズする

組織に特定のテスト要件がある場合は、それらの基準を満たすようにCopilotのテスト生成方法をカスタマイズできます。カスタム指示を提供することで、Copilotがテストを生成する方法をパーソナライズできます。例:

* 優先するテストフレームワークを指定する
* テストの命名規則を定義する
* コード構造の好みを設定する
* 特定のテストパターンや方法論を指定する

[テスト生成のためにCopilotをパーソナライズする](/docs/copilot/customization/overview.md)の詳細を確認してください。

## テスト生成を改善するためのヒント

Copilotでテストを生成するときに最良の結果を得るには、次のヒントに従ってください。

* 好みのテストフレームワークについて、プロンプトでコンテキストを提供する
* 必要なテストの種類(単体、統合、エンドツーエンド)を指定する
* 具体的なテストケースやエッジケースを依頼する
* プロジェクトのコーディング標準に従うテストを依頼する

## 次のステップ

* [VS CodeのCopilot](/docs/copilot/overview.md)の詳細を確認します。
* [VS Codeの一般的なテスト機能](/docs/debugtest/testing.md)を確認します。
* [単体テストの生成](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat/testing-code/generate-unit-tests)のプロンプト例を確認します。
