---
ContentId: 8f9a3e5c-2b4d-4a7f-9c8e-1d6f3a2b5c4e
DateApproved: 3/9/2026
MetaDescription: VS Code チャットでプラン エージェントと todo リストを使用して、自律的な計画とタスク管理を行う方法を学びます。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Code でエージェントを使用した計画

プラン エージェントを使用すると、実装を開始する前に詳細な実装計画を作成して、すべての要件が満たされていることを確認できます。Todo リストを使用すると、エージェントは全体的な目標に焦点を当て、進行状況を効果的に追跡できます。

プラン エージェントがエージェント アーキテクチャにどのように適合するかについては、[エージェントの概念](/docs/copilot/concepts/agents.md#planning)を参照してください。

この記事では、VS Code でプラン エージェントと todo リストを使用する方法について説明します。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントを使用して機能を計画する">
プラン エージェントを使用して、新機能の構造化された実装計画を作成します。

* [VS Code で開く](vscode://GitHub.Copilot-Chat/chat?agent=agent%26prompt=%2Fplan%20a%20terminal%20UI%20app%20to%20track%20my%20todo%20list.)

</div>

## タスクを計画する方法

タスクを計画するには、チャット ビューで組み込みの**プラン** エージェントを使用し、タスクを説明して、生成された計画を反復処理します。

1. `kb(workbench.action.chat.open)`を押してチャット ビューを開き、エージェント ドロップダウンから**プラン**を選択します

    または、`/plan`の後にタスクの説明を入力して、プラン エージェントに切り替え、1 ステップで計画を開始できます。

1. 高度なタスク（機能、リファクタリング、バグなど）を入力して送信します。例:

    ```prompt-plan
    OAuth2 と JWT を使用したユーザー認証システムを実装する
    ```

    チャット入力ボックスから`/plan`スラッシュ コマンドを使用して直接計画を開始します:

    ```prompt
    /plan すべての API エンドポイントのユニット テストを追加する
    ```

1. タスク調査後、エージェントが質問する説明質問に答えます。

1. プラン エージェントは、高度な計画サマリー、実装と検証のステップを生成します。計画ドラフトを確認し、要件を満たすまで計画を反復処理するためにフォローアップ プロンプトを送信します。

1. 計画が確定したら、実装を開始するか、計画プロンプトをエディターで開いて詳細確認するかを選択します。

    計画を実装するには、同じセッションで続行するか、新しい[Copilot CLI セッション](/docs/copilot/agents/copilot-cli.md)を開始して、バックグラウンドで計画を実装できます。

> [!TIP]
> プラン エージェントは、実装計画をセッション メモリ ファイル(`/memories/session/plan.md`)に自動的に保存します。このファイルにアクセスするには、**Chat: Show Memory Files** コマンドを実行し、リストから`plan.md`を選択します。セッション メモリはメモリ終了時にクリアされるため、後続のセッションでは計画は利用できません。

## 計画をカスタマイズする

チームのワークフローに合わせて計画プロセスを調整できます:

* **カスタム計画エージェントを作成します。** アーキテクチャ ガイドラインの適用や特定の計画成果物を必要とするなど、計画プロセスの特定の指示で[カスタム エージェント](/docs/copilot/customization/custom-agents.md)を定義します。

* **計画と実装のモデルを選択します。** `setting(chat.planAgent.defaultModel)`設定を使用してプラン エージェントのデフォルト モデルを選択し、実装ステップには`setting(github.copilot.chat.implementAgent.model)`を使用します。

* **プラン エージェントに追加ツールを追加します（試験段階）。** `setting(github.copilot.chat.planAgent.additionalTools)`設定を使用して、調査と計画フェーズ中にプラン エージェントに追加ツールへのアクセスを許可します。たとえば、MCP サーバーを使用して内部データ ソースまたはツールに接続します。

## 関連リソース

* [VS Code エージェントのメモリ](/docs/copilot/agents/memory.md)
* [エージェントのツールを構成する](/docs/copilot/agents/agent-tools.md)
* [コンテキスト エンジニアリング ユーザー ガイド](/docs/copilot/guides/context-engineering-guide.md)

