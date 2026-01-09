---
ContentId: 2f21c45a-8931-4da2-a921-af23a3b92949
DateApproved: 12/10/2025
MetaDescription: Visual Studio CodeでGitHub Copilotを使用してデバッグ構成を設定し、デバッグ中の問題を修正する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilot でデバッグする

GitHub Copilotは、Visual Studio Codeでのデバッグワークフローの改善に役立ちます。Copilotは、プロジェクトのデバッグ構成のセットアップを支援し、デバッグ中に発見された問題を修正するための提案を提供します。この記事では、VS CodeでのアプリケーションのデバッグにCopilotを使用する方法の概要を説明します。

Copilotは、以下のデバッグタスクに役立ちます:

* **デバッグ設定の構成**: プロジェクトの起動構成を生成およびカスタマイズします。
* **デバッグセッションの開始**: ターミナルから `copilot-debug` を使用してデバッグセッションを開始します。
* **問題の修正**: デバッグ中に発見された問題を修正するための提案を受け取ります。

> [!TIP]
> Copilotサブスクリプションをまだお持ちでない場合は、[Copilot Free プラン](https://github.com/github-copilot/signup)にサインアップすることでCopilotを無料で使用でき、毎月のインライン提案とチャット対話の制限内で利用できます。

## Copilot でデバッグ構成を設定する

VS Codeは、`launch.json` ファイルを使用して[デバッグ構成](/docs/debugtest/debugging-configuration.md)を保存します。Copilotは、このファイルの作成とカスタマイズを支援し、プロジェクトのデバッグを設定するのに役立ちます。

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)。
1. `/startDebugging` コマンドを入力します。
1. Copilotのガイダンスに従って、プロジェクトのデバッグを設定します。

あるいは、次のような自然言語プロンプトを使用することもできます:

* "Django アプリのデバッグ構成を作成する"
* "React Native アプリのデバッグを設定する"
* "Flask アプリケーションのデバッグを構成する"

## Copilot でデバッグを開始する

`copilot-debug` ターミナルコマンドは、デバッグセッションの構成と開始のプロセスを簡素化します。アプリケーションの起動に使用するコマンドの前に `copilot-debug` を付けると、Copilotが自動的にデバッグセッションを構成して開始します。

1. 統合ターミナルを開きます (`kb(workbench.action.terminal.toggleTerminal)`)。

1. `copilot-debug` に続けてアプリケーションの起動コマンドを入力します。例えば:

    ```bash
    copilot-debug node app.js
    ```

    または

    ```bash
    copilot-debug python manage.py
    ```

1. Copilotはアプリケーションのデバッグセッションを起動します。これで、VS Codeの組み込みデバッグ機能を使用できます。

[VS Code でのデバッグ](/docs/debugtest/debugging.md)の詳細については、こちらをご覧ください。

## Copilot でコーディングの問題を修正する

Copilot Chatを使用して、コーディングの問題を修正したり、コードを改善したりできます。

### チャットプロンプトの使用

1. アプリケーションコードファイルを開きます。

1. 以下のいずれかのビューを開きます:
    * チャットビュー (`kb(workbench.action.chat.open)`)
    * インラインチャット (`kb(inlineChat.start)`)

1. 次のようなプロンプトを入力します:
    * "/fix"
    * "この #selection を修正する"
    * "この関数の入力を検証する"
    * "このコードをリファクタリングする"
    * "このコードのパフォーマンスを改善する"

VS Codeでの[Copilot Chat](/docs/copilot/chat/copilot-chat.md)の使用についての詳細はこちら。

### エディターのスマートアクションの使用

プロンプトを作成せずにアプリケーションコードのコーディングの問題を修正するには、エディターのスマートアクションを使用できます。

1. アプリケーションコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**Generate Code** > **Fix** を選択します。

    VS Codeは、コードを修正するためのコード提案を提供します。

1. 必要に応じて、チャットプロンプトに追加のコンテキストを提供して、生成されたコードを調整します。

## 次のステップ

* [VS Code の一般的なデバッグ機能](/docs/debugtest/debugging.md)を確認する。
* [VS Code の Copilot](/docs/copilot/overview.md) について詳細を学ぶ。
