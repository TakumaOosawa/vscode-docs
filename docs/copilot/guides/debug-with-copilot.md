---
ContentId: 2f21c45a-8931-4da2-a921-af23a3b92949
DateApproved: 3/9/2026
MetaDescription: Visual Studio CodeでGitHub Copilotを使用してデバッグ構成を設定し、デバッグ中の問題を修正する方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# GitHub Copilotでデバッグする

GitHub Copilotは、Visual Studio Codeのデバッグワークフローを改善するのに役立ちます。Copilotはプロジェクトのデバッグ構成の設定を支援し、デバッグ中に発見された問題を修正するための提案を提供します。この記事では、VS Codeでアプリケーションをデバッグするために Copilotを使用する方法の概要を説明します。

Copilotは次のデバッグタスクに役立ちます：

* **デバッグ設定を構成する**：プロジェクトのローンチ構成を生成およびカスタマイズします。
* **デバッグセッションを開始する**：`copilot-debug`を使用してターミナルからデバッグセッションを開始します。
* **問題を修正する**：デバッグ中に発見された問題を修正するための提案を受け取ります。

> [!TIP]
> まだCopilotサブスクリプションを持っていない場合は、[Copilot無料プラン](https://github.com/github-copilot/signup)にサインアップして、Copilotを無料で使用し、インラインサジェスチョンとチャット操作の月間制限を取得できます。

## Copilotでデバッグ構成を設定する

VS Codeは`launch.json`ファイルを使用して[デバッグ構成](/docs/debugtest/debugging-configuration.md)を保存します。Copilotはこのファイルを作成およびカスタマイズして、プロジェクトのデバッグを設定するのに役立ちます。

1. Chat ビュー（`kb(workbench.action.chat.open)`）を開きます。
1. `/startDebugging`コマンドを入力します。
1. Copilotのガイダンスに従ってプロジェクトのデバッグを設定します。

別の方法として、次のような自然言語プロンプトを使用できます：

* 「Djangoアプリのデバッグ構成を作成する」
* 「React Nativeアプリのデバッグを設定する」
* 「Flaskアプリケーションのデバッグを構成する」

## Copilotでデバッグを開始する

`copilot-debug`ターミナルコマンドは、デバッグセッションを構成および開始するプロセスを簡素化します。アプリケーションの起動に使用するコマンドの前に`copilot-debug`を付けて、Copilotが自動的にデバッグセッションを構成および開始するようにします。

1. 統合ターミナル（`kb(workbench.action.terminal.toggleTerminal)`）を開きます。

1. `copilot-debug`の後にアプリケーションの起動コマンドを入力します。例：

    ```bash
    copilot-debug node app.js
    ```

    または

    ```bash
    copilot-debug python manage.py
    ```

1. Copilotがアプリケーションのデバッグセッションを起動します。これで、VS Codeの組み込みデバッグ機能を使用できます。

[VS Codeでのデバッグ](/docs/debugtest/debugging.md)の詳細をご覧ください。

## Copilotでコーディングの問題を修正する

Copilot Chatを使用して、コーディングの問題を修正またはコードを改善できます。

### チャットプロンプトを使用する

1. アプリケーションコードファイルを開きます。

1. 次のいずれかのビューを開きます：
    * Chat ビュー（`kb(workbench.action.chat.open)`）
    * インラインChat（`kb(inlineChat.start)`）

1. 次のようなプロンプトを入力します：
    * 「/fix」
    * 「この#selectionを修正する」
    * 「この関数の入力を検証する」
    * 「このコードをリファクタリングする」
    * 「このコードのパフォーマンスを改善する」

VS Codeで[Copilot Chat](/docs/copilot/chat/copilot-chat.md)を使用する方法の詳細をご覧ください。

### エディタのスマートアクションを使用する

プロンプトを書かずにアプリケーションコードのコーディングの問題を修正するには、エディタのスマートアクションを使用できます。

1. アプリケーションコードファイルを開きます。
1. 修正したいコードを選択します。
1. 右クリックして、**コード生成**>**修正**を選択します。

    VS Codeがコードを修正するためのコード提案を提供します。

1. 必要に応じて、チャットプロンプトに追加のコンテキストを入力して、生成されたコードを洗練させます。

## 次のステップ

* [VS Codeの一般的なデバッグ機能](/docs/debugtest/debugging.md)を探索します。
* [VS Codeの Copilot](/docs/copilot/overview.md)の詳細をご覧ください。

