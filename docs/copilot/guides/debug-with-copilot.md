---
ContentId: 2f21c45a-8931-4da2-a921-af23a3b92949
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotを使用してデバッグ構成を設定し、デバッグ中の問題を修正する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilotでデバッグ

GitHub Copilotは、Visual Studio Codeでのデバッグワークフローの改善に役立ちます。Copilotは、プロジェクトのデバッグ構成の設定を支援し、デバッグ中に見つかった問題の修正案を提示できます。この記事では、VS CodeでアプリケーションをデバッグするためにCopilotを使用する方法の概要を説明します。

Copilotは、次のデバッグタスクを支援できます。

* **デバッグ設定を構成する**: プロジェクトの起動構成を生成してカスタマイズします。
* **デバッグセッションを開始する**: ターミナルから`copilot-debug`を使用してデバッグセッションを開始します。
* **問題を修正する**: デバッグ中に見つかった問題の修正案を受け取ります。

> [!TIP]
> まだCopilotのサブスクリプションをお持ちでない場合は、[Copilot Free plan](https://github.com/github-copilot/signup)に登録してCopilotを無料で利用できます。インライン提案とチャットのやり取りには月ごとの上限があります。

## Copilotでデバッグ構成をセットアップする

VS Codeは、[デバッグ構成](/docs/debugtest/debugging-configuration.md)を`launch.json`ファイルに保存します。Copilotは、このファイルの作成とカスタマイズを支援し、プロジェクトのデバッグをセットアップできます。

1. Open the Chat view (`kb(workbench.action.chat.open)`).
1. `/startDebugging`コマンドを入力します。
1. Copilotのガイダンスに従って、プロジェクトのデバッグをセットアップします。

または、次のような自然言語のプロンプトを使用できます。

* "Djangoアプリのデバッグ構成を作成して"
* "React Nativeアプリのデバッグをセットアップして"
* "Flaskアプリケーションのデバッグを構成して"

## Copilotでデバッグを開始する

`copilot-debug`ターミナルコマンドを使用すると、デバッグセッションの構成と開始の手順を簡素化できます。アプリケーションを起動するために使用するコマンドの前に`copilot-debug`を付けると、Copilotが自動的にデバッグセッションを構成して開始します。

1. 統合ターミナルを開きます(`kb(workbench.action.terminal.toggleTerminal)`)。

1. `copilot-debug`に続けて、アプリケーションの起動コマンドを入力します。次に例を示します。

    ```bash
    copilot-debug node app.js
    ```

    or

    ```bash
    copilot-debug python manage.py
    ```

1. Copilotがアプリケーションのデバッグセッションを起動します。これで、VS Codeに組み込まれたデバッグ機能を使用できます。

[VS Codeでのデバッグ](/docs/debugtest/debugging.md)の詳細をご覧ください。

## Copilotでコーディングの問題を修正する

Copilot Chatを使用して、コーディングの問題を修正したり、コードを改善したりできます。

### チャットプロンプトを使用する

1. アプリケーションのコードファイルを開きます。

1. 次のいずれかのビューを開きます。
    * Chatビュー(`kb(workbench.action.chat.open)`)
    * Inline Chat (`kb(inlineChat.start)`)

1. 次のようなプロンプトを入力します。
    * "/fix"
    * "Fix this #selection"
    * "Validate input for this function"
    * "Refactor this code"
    * "Improve the performance of this code"

VS Codeでの[Copilot Chat](/docs/copilot/chat/copilot-chat.md)の使用方法の詳細をご覧ください。

### エディターのスマートアクションを使用する

プロンプトを書かずにアプリケーションコードのコーディングの問題を修正するには、エディターのスマートアクションを使用できます。

1. アプリケーションのコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**Generate Code** > **Fix**を選択します。

    VS Codeがコードを修正するための提案を提示します。

1. 必要に応じて、チャットプロンプトで追加のコンテキストを提供して、生成されたコードを調整します。

## 次の手順

* [VS Codeの一般的なデバッグ機能](/docs/debugtest/debugging.md)を確認します。
* [VS CodeのCopilot](/docs/copilot/overview.md)の詳細をご覧ください。
