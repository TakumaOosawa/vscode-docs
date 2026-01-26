---
ContentId: 2f21c45a-8931-4da2-a921-af23a3b92949
DateApproved: 01/08/2026
MetaDescription: GitHub Copilotを使用してVisual Studio Codeでデバッグ構成をセットアップし、デバッグ中に問題を修正する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilotでデバッグする

GitHub Copilotは、Visual Studio Codeにおけるデバッグワークフローの改善に役立ちます。Copilotは、プロジェクトのデバッグ構成のセットアップを支援し、デバッグ中に発見された問題を修正するための提案を提供します。この記事では、VS CodeでアプリケーションをデバッグするためにCopilotを使用する方法の概要を説明します。

Copilotは、以下のデバッグタスクを支援します:

* **デバッグ設定の構成**: プロジェクトの起動構成を生成およびカスタマイズします。
* **デバッグセッションの開始**: `copilot-debug`を使用して、ターミナルからデバッグセッションを開始します。
* **問題の修正**: デバッグ中に発見された問題を修正するための提案を受け取ります。

> [!TIP]
> まだCopilotサブスクリプションをお持ちでない場合は、[Copilot Freeプラン](https://github.com/github-copilot/signup)にサインアップすることで、Copilotを無料で使用でき、インライン提案やチャット対話の月間制限を利用できます。

## Copilotでデバッグ構成をセットアップする

VS Codeは`launch.json`ファイルを使用して[デバッグ構成](/docs/debugtest/debugging-configuration.md)を保存します。Copilotは、このファイルの作成とカスタマイズを支援し、プロジェクトのデバッグをセットアップするのに役立ちます。

1. チャットビューを開きます (`kb(workbench.action.chat.open)`)。
1. `/startDebugging`コマンドを入力します。
1. プロジェクトのデバッグをセットアップするためのCopilotのガイダンスに従います。

あるいは、次のような自然言語プロンプトを使用することもできます:

* "Djangoアプリのデバッグ構成を作成する"
* "React Nativeアプリのデバッグをセットアップする"
* "Flaskアプリケーションのデバッグを構成する"

## Copilotでデバッグを開始する

`copilot-debug`ターミナルコマンドは、デバッグセッションの構成と開始のプロセスを簡素化します。アプリケーションを開始するために使用するコマンドの前に`copilot-debug`を付けると、Copilotが自動的にデバッグセッションを構成して開始します。

1. 統合ターミナルを開きます (`kb(workbench.action.terminal.toggleTerminal)`)。

1. `copilot-debug`に続いて、アプリケーションの開始コマンドを入力します。例えば:

    ```bash
    copilot-debug node app.js
    ```

    または

    ```bash
    copilot-debug python manage.py
    ```

1. Copilotは、アプリケーションのデバッグセッションを起動します。これで、VS Codeの組み込みデバッグ機能を使用できます。

[VS Codeでのデバッグ](/docs/debugtest/debugging.md)について詳しくはこちらをご覧ください。

## Copilotでコーディングの問題を修正する

Copilot Chatを使用して、コーディングの問題を修正したり、コードを改善したりできます。

### チャットプロンプトを使用する

1. アプリケーションコードファイルを開きます。

1. 以下のビューのいずれかを開きます:
    * チャットビュー (`kb(workbench.action.chat.open)`)
    * インラインチャット (`kb(inlineChat.start)`)

1. 次のようなプロンプトを入力します:
    * "/fix"
    * "この #selection を修正"
    * "この関数の入力を検証"
    * "このコードをリファクタリング"
    * "このコードのパフォーマンスを改善"

VS Codeでの[Copilot Chatの使用](/docs/copilot/chat/copilot-chat.md)について詳しくはこちらをご覧ください。

### エディターのスマートアクションを使用する

プロンプトを書かずにアプリケーションコードのコーディング問題を修正するには、エディターのスマートアクションを使用できます。

1. アプリケーションコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**コードの生成** > **修正**を選択します。

    VS Codeは、コードを修正するためのコード提案を提供します。

1. 必要に応じて、チャットプロンプトに追加のコンテキストを提供して、生成されたコードを調整します。

## 次のステップ

* [VS Codeの一般的なデバッグ機能](/docs/debugtest/debugging.md)を確認する。
* [VS CodeでのCopilot](/docs/copilot/overview.md)について詳しく学ぶ。
