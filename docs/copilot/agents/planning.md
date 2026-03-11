---
ContentId: 8f9a3e5c-2b4d-4a7f-9c8e-1d6f3a2b5c4e
DateApproved: 3/9/2026
MetaDescription: VS Code チャットでplan agent と todo リストを使用した自動計画とタスク管理について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# VS Code でエージェントを使用した計画

plan agent を使用すると、実装を開始する前に詳細な実装計画を作成し、すべての要件が満たされていることを確認できます。todo リストを使用することで、エージェントは全体的な目標に焦点を当てたまま進行状況を効果的に追跡できます。

plan agent がエージェント アーキテクチャにどのように適合するかの背景については、[エージェント コンセプト](/docs/copilot/concepts/agents.md#planning)を参照してください。

この記事では、VS Code で plan agent と todo リストを使用する方法について説明します。

<div class="docs-action" data-show-in-doc="false" data-show-in-sidebar="true" title="エージェントで機能を計画する">
Plan agent を使用して、新機能の構造化された実装計画を作成します。

* [VS Code で開く](vscode://GitHub.Copilot-Chat/chat?agent=agent%26prompt=%2Fplan%20a%20terminal%20UI%20app%20to%20track%20my%20todo%20list.)

</div>

## タスクを計画する方法

タスクを計画するには、Chat ビューで組み込みの**Plan**エージェントを使用し、タスクを説明して、生成された計画を反復します。

1. `kb(workbench.action.chat.open)`を押して Chat ビューを開き、エージェント ドロップダウンから**Plan**を選択します

    または、`/plan`に続けてタスク説明を入力して、Plan agent に切り替え、1ステップで計画を開始します。

1. 高レベルのタスク（機能、リファクタリング、バグなど）を入力して送信します。例：

    ```prompt-plan
    OAuth2 と JWT を使用したユーザー認証システムを実装する
    ```

    チャット入力ボックスから`/plan`スラッシュコマンドを使用して直接計画を開始します：

    ```prompt
    /plan 全 API エンドポイントのユニットテストを追加する
    ```

1. タスクを調査した後、エージェントが質問する明確化の質問に答えます。

1. Plan agent は高レベルの計画概要、実装ステップ、検証ステップを生成します。計画ドラフトを確認し、要件を満たすまで計画を反復するためのフォローアップ プロンプトを送信します。

1. 計画が最終化されたら、実装を開始するか、エディターで計画プロンプトを開いてさらにレビューすることを選択します。

    計画を実装するには、同じセッションで続行するか、新しい[Copilot CLI セッション](/docs/copilot/agents/copilot-cli.md)を開始して、バックグラウンドで計画を実装します。

> [!TIP]
> Plan agent は実装計画をセッション メモリ ファイル（`/memories/session/plan.md`）に自動的に保存します。このファイルにアクセスするには、**Chat: Show Memory Files**コマンドを実行し、リストから`plan.md`を選択します。セッション メモリは会話の終了時にクリアされるため、計画は後続のセッションでは利用できません。

## 計画をカスタマイズする

チームのワークフローに合わせて計画プロセスを調整できます：

* **カスタム計画エージェントを作成する。** アーキテクチャ ガイドラインの実装や特定の計画成果物の要求など、計画プロセスの特定の指示を含む[カスタム エージェント](/docs/copilot/customization/custom-agents.md)を定義します。

* **計画と実装のモデルを選択する。** `setting(chat.planAgent.defaultModel)`設定を使用して plan agent のデフォルト モデルを選択し、`setting(github.copilot.chat.implementAgent.model)`を実装ステップに使用します。

* **plan agent に追加ツールを追加する（実験的）。** `setting(github.copilot.chat.planAgent.additionalTools)`設定を使用して、plan agent に研究および計画フェーズ中の追加ツールへのアクセスを権限付けます。たとえば、MCP サーバーを使用して内部データ ソースまたはツールに接続します。

## 関連リソース

* [VS Code エージェントのメモリ](/docs/copilot/agents/memory.md)
* [エージェント用ツールの構成](/docs/copilot/agents/agent-tools.md)
* [コンテキスト エンジニアリング ユーザー ガイド](/docs/copilot/guides/context-engineering-guide.md)

