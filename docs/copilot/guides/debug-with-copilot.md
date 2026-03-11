---
ContentId: 2f21c45a-8931-4da2-a921-af23a3b92949
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用してデバッグ構成をセットアップし、デバッグ中の問題を修正する方法を説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilotでデバッグ

GitHub CopilotはVisual Studio Codeのデバッグワークフローを改善するのに役立ちます。Copilotはプロジェクトのデバッグ構成をセットアップし、デバッグ中に発見された問題を修正するための提案を提供できます。この記事では、VS CodeでCopilotを使用してアプリケーションをデバッグする方法の概要を説明します。

Copilotは以下のデバッグタスクをサポートできます:

* **デバッグ設定の構成**: プロジェクトのlaunch構成を生成およびカスタマイズします。
* **デバッグセッションの開始**: ターミナルから`copilot-debug`を使用してデバッグセッションを開始します。
* **問題の修正**: デバッグ中に発見された問題を修正するための提案を受け取ります。

> [!TIP]
> Copilot購読をまだお持ちでない場合は、[Copilot無料プラン](https://github.com/github-copilot/signup)にサインアップしてCopilotを無料で使用でき、インライン提案とチャット操作の月間制限が付きます。

## Copilotでデバッグ構成をセットアップ

VS CodeはDebug構成を保存するために`launch.json`ファイルを使用します。Copilotはこのファイルを作成およびカスタマイズしてプロジェクトのデバッグをセットアップするのに役立ちます。

1. チャットビュー（`kb(workbench.action.chat.open)`）を開きます。
1. `/startDebugging`コマンドを入力します。
1. Copilotのガイダンスに従ってプロジェクトのデバッグをセットアップします。

または、以下のような自然言語プロンプトを使用できます:

* 「Djangoアプリのデバッグ構成を作成してください」
* 「React Nativeアプリのデバッグをセットアップしてください」
* 「Flaskアプリケーションのデバッグを構成してください」

## Copilotでデバッグを開始

`copilot-debug`ターミナルコマンドは、デバッグセッションの構成と開始プロセスを簡略化します。アプリケーション起動に使用するコマンドの先頭に`copilot-debug`を付けると、Copilotが自動的にデバッグセッションを構成して開始します。

1. 統合ターミナル（`kb(workbench.action.terminal.toggleTerminal)`）を開きます。

1. `copilot-debug`の後にアプリケーションの起動コマンドを入力します。例:

    ```bash
    copilot-debug node app.js
    ```

    または

    ```bash
    copilot-debug python manage.py
    ```

1. Copilotはアプリケーションのデバッグセッションを起動します。VS Codeの組み込みデバッグ機能を使用できるようになります。

[VS Codeのデバッグ](/docs/debugtest/debugging.md)の詳細をご覧ください。

## Copilotでコーディングの問題を修正

Copilot Chatを使用してコーディングの問題を修正またはコードを改善できます。

### チャットプロンプトを使用

1. アプリケーションコードファイルを開きます。

1. 以下のビューのいずれかを開きます:
    * チャットビュー（`kb(workbench.action.chat.open)`）
    * インラインチャット（`kb(inlineChat.start)`）

1. 以下のようなプロンプトを入力します:
    * 「/fix」
    * 「このセレクション(#selection)を修正してください」
    * 「この関数の入力を検証してください」
    * 「このコードをリファクタリングしてください」
    * 「このコードのパフォーマンスを改善してください」

[Copilot Chat](/docs/copilot/chat/copilot-chat.md)をVS Codeで使用することについての詳細をご覧ください。

### エディタの概略アクション

プロンプトを入力せずにアプリケーションコードのコーディング問題を修正するには、エディタの概略アクションを使用できます。

1. アプリケーションコードファイルを開きます。
1. 修正するコードを選択します。
1. 右クリックして**コード生成** > **修正**を選択します。

    VS Codeはコードを修正するためのコード提案を提供します。

1. 必要に応じて、チャットプロンプトで追加のコンテキストを提供して生成されたコードを改善します。

## 次のステップ

* [VS Codeの一般的なデバッグ機能](/docs/debugtest/debugging.md)を確認します。
* [VS CopilotGitHub](/docs/copilot/overview.md)の詳細をご覧ください。

