---
ContentId: 2e8a4b9c-3d1f-5e7a-9c2b-4f6d8e1a3b5c
DateApproved: 3/9/2026
MetaDescription: VS Codeで AIをカスタマイズするためのステップバイステップガイド。手順、プロンプトファイル、カスタムエージェント、スキルについて説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
Keywords:
- customization
- instructions
- prompt files
- custom agents
- skills
- copilot
- ai
- tutorial
---
# プロジェクト用のAIをカスタマイズする

このガイドでは、Visual Studio Codeでプロジェクト向けのAIカスタマイズを設定する方法を説明します。基本的なコーディング標準から始まり、より対象を絞った機能を段階的に追加します。

完了時には、プロジェクトに以下の機能が備わります:

* すべてのチャットリクエストに適用されるプロジェクト全体のコーディング標準
* フロントエンドコード用のファイル固有の手順
* 一般的なタスク用の再利用可能なプロンプトファイル
* ツールが制限されたカスタムエージェント
* 専門的な機能のためのスキル

## 前提条件

* [VS Code](https://code.visualstudio.com/download)がインストールされていること
* [GitHub Copilotプラン](https://docs.github.com/en/copilot/about-github-copilot/subscription-plans-for-github-copilot)(Free、Pro、Business、またはEnterprise)
* [GitHub Copilot拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)がインストールされていること
* VS Code内でワークスペースまたはフォルダが開かれていること

## ステップ1: プロジェクト全体のコーディング標準を設定する

プロジェクトのコーディング標準をキャプチャする手順ファイルを生成することから始めましょう。これらの手順はすべてのチャットリクエストに自動的に含まれます。

1. チャットビューを開きます(`kb(workbench.action.chat.open)`)。

1. `/init`を入力し、`kbstyle(Enter)`キーを押します。

  ```prompt
  /init
  ```

1. VS Codeがプロジェクト構造を分析し、コードベースに対応した`.github/copilot-instructions.md`ファイルを生成します。

1. 生成されたファイルを確認して、カスタマイズします。たとえば、推奨インポートスタイルについてのルールを追加します:

  ```markdown
  ## インポート
  - デフォルトインポートではなく、名前付きインポートを使用してください。
  - インポートをグループ化してください: 外部ライブラリ、内部モジュール、相対パスの順です。
  ```

1. ファイルを保存します。

**動作確認**: Copilotにコードを生成するよう指示します(たとえば、「日付フォーマット用のユーティリティ関数を作成してください」)。レスポンスがコーディング標準に従っていることを確認します。チャットレスポンスの**References**セクションを選択して、`copilot-instructions.md`が含まれていることを確認します。

> [!TIP]
> [カスタム手順を使用する](/docs/copilot/customization/custom-instructions.md#use-a-githubcopilot-instructionsmd-file)で、常に有効な手順について詳細を確認してください。

## ステップ2: ファイル固有の手順を追加する

コードベースの別々の部分が異なる規約に従う場合は、`applyTo`パターン付きの手順ファイルを使用して、特定のファイルタイプを対象にします。

1. チャットビューで、**Configure Chat**(ギアアイコン) > **Instructions & Rules**を選択し、**New instruction file**を選択します。

1. `.github/instructions/`を選択して、手順をプロジェクトに保存します。

1. `react`などのファイル名を入力します。

1. ファイルに以下の内容を追加します:

  ```markdown
  ---
  applyTo: "**/*.tsx,**/*.jsx"
  ---
  # Reactコンポーネントガイドライン

  - 関数型コンポーネントとhooksを使用してください。
  - TypeScriptインターフェースでプロップタイプを定義してください。
  - コンポーネントスタイリングにはCSSモジュールを使用してください。
  - コンポーネントは名前付きエクスポートとしてエクスポートしてください。
  ```

1. ファイルを保存します。

**動作確認**: `.tsx`ファイルを開き、Copilotに「ユーザープロファイルカードコンポーネントを作成してください」と指示します。レスポンスがReact固有の規約に従うはずです。**References**セクションを確認して、手順ファイルが適用されたことを確認します。

> [!TIP]
> 異なるファイルタイプ、フレームワーク、またはモジュール用に複数の手順ファイルを作成できます。詳細は[`.instructions.md`ファイルを使用する](/docs/copilot/customization/custom-instructions.md#use-instructionsmd-files)を参照してください。

## ステップ3: 再利用可能なプロンプトファイルを作成する

プロンプトファイルは、チャットで呼び出せるスラッシュコマンドとして一般的なタスクをエンコードします。定期的に実行するタスク用に作成します。

1. チャットビューで、**Configure Chat**(ギアアイコン) > **Prompt Files**を選択し、**New prompt file**を選択します。

1. `.github/prompts/`を選択して、プロンプトファイルをプロジェクトに保存します。

1. `create-component`などのファイル名を入力します。

1. ファイルに以下の内容を追加します:

  ```markdown
  ---
  description: テスト付きの新しいReactコンポーネントをスキャフォルド
  agent: agent
  tools: ['editFiles', 'createFile']
  ---
  ユーザーの説明に基づいて新しいReactコンポーネントを作成してください。

  各コンポーネントについて、以下を生成してください:
  1. `src/components/`内のコンポーネントファイル
  2. `src/components/__tests__/`内のテストファイル

  [Reactガイドライン](../instructions/react.instructions.md)の規約に従ってください。
  ```

1. ファイルを保存します。

**動作確認**: チャットビューで、`/create-component ソートおよびフィルタリング機能付きのデータテーブル`と入力し、`kbstyle(Enter)`キーを押します。Copilotが規約に従ってコンポーネントとテストファイルをスキャフォルドするはずです。

> [!TIP]
> チャットで`/create-prompt`と入力して、AI支援によるプロンプトファイルを生成します。進行中の会話から再利用可能なプロンプトを抽出するには、「このワークフローをプロンプトとして保存してください」と指示することもできます。詳細は[プロンプトファイルを使用する](/docs/copilot/customization/prompt-files.md)を参照してください。

## ステップ4: カスタムエージェントを構築する

カスタムエージェントを使用すると、AIは特定のツールアクセス権を持つ専門化されたペルソナを採用できます。コードのみを読くことができ、変更することはできないコードレビュアーエージェントを作成してください。

1. チャットビューで、**Configure Chat**(ギアアイコン) > **Custom Agents**を選択し、**Create new custom agent**を選択します。

1. `.github/agents/`を選択して、エージェントをプロジェクトに保存します。

1. `reviewer`などのファイル名を入力します。

1. ファイルに以下の内容を追加します:

  ```markdown
  ---
  description: コード品質、セキュリティ、ベストプラクティスをレビュー
  tools: ['search/codebase', 'search/workspace', 'githubRepo']
  ---
  あなたはコードレビュアーです。提供されたコードを分析し、以下を特定してください:

  1. **セキュリティ問題**: SQLインジェクション、XSS、ハードコードされたシークレット、安全でない依存関係
  2. **コード品質**: 複雑な関数、重複したロジック、エラーハンドリングの欠落
  3. **ベストプラクティス**: 命名規則、ドキュメント、テストカバレッジ

  具体的で実行可能なフィードバックを提供してください。関連するコード位置を参照してください。
  ファイルを変更しないでください。レビューと調査結果の報告のみしてください。
  ```

1. ファイルを保存します。

**動作確認**: チャットビューのエージェントドロップダウンから**Reviewer**エージェントを選択し、「認証モジュールをレビューしてください」と指示します。エージェントが変更を加えずにコードを分析するはずです。

> [!TIP]
> エージェントに`handoffs`を追加して、ガイド付きワークフローを作成できます。たとえば、計画エージェントから実装エージェントにハンドオフします。詳細は[カスタムエージェント](/docs/copilot/customization/custom-agents.md#handoffs)を参照してください。

## ステップ5: 専門的な機能のためのスキルを作成する

スキルは、手順、スクリプト、およびリソースのフォルダであり、Copilotは関連する専門的なタスクを実行する際にロードします。コーディング標準を定義する手順ファイルとは異なり、スキルはCopilotに特定のワークフローの実行方法を教えます。

1. ワークスペースに`.github/skills/update-readme/`ディレクトリを作成します。

1. ディレクトリに`SKILL.md`ファイルを作成し、以下の内容を追加します:

  ```markdown
  ---
  name: update-readme
  description: 最近のコード変更を反映するようにプロジェクトREADMEを更新してください。コード変更が加えられるたびに、このスキルは変更をレビューし、新機能、使用方法、APIリファレンスを含むREADMEを更新します。
  ---
  # READMEを更新する

  READMEを更新する際:
  1. 最近のコード変更をレビューして、新規または変更された機能を特定してください
  2. 関連するセクション(インストール、使用方法、APIリファレンス)を更新してください
  3. 新しいコマンド、設定オプション、環境変数のエントリを追加してください
  4. 削除または廃止された機能のドキュメントを削除してください
  5. 既存のトーン、構造、フォーマット規則を保持してください
  ```

1. ファイルを保存します。

**動作確認**: チャットで、Copilotにプロジェクトに新機能を追加するよう指示します(たとえば、「ヘルスチェックエンドポイントを追加してください」)。コードを生成するとき、READMEも新しいエンドポイントのドキュメントで自動的に更新するはずです。チャットで`/update-readme`と入力してスキルを直接呼び出すこともできます。

> [!TIP]
> チャットで`/create-skill`と入力して、AI支援によるスキルを生成します。進行中の会話からスキルを抽出するには、「我々が行ったことからスキルを作成してください」と指示することもできます。詳細は[エージェントスキル](/docs/copilot/customization/agent-skills.md)を参照してください。

## 構築内容

プロジェクトは現在、階層化されたAIカスタマイズセットアップを備えています:

```text
your-project/
  .github/
  copilot-instructions.md          # プロジェクト全体のコーディング標準(ステップ1)
  instructions/
    react.instructions.md          # React固有の規約(ステップ2)
  prompts/
    create-component.prompt.md     # 再利用可能なコンポーネントスキャフォルド(ステップ3)
  agents/
    reviewer.agent.md              # 読み取り専用コードレビュアー(ステップ4)
  skills/
    update-readme/
    SKILL.md                     # READMEアップデーターワークフロー(ステップ5)
```

## 次のステップ

* [MCPサーバー](/docs/copilot/customization/mcp-servers.md)を追加して、外部ツールとサービスでエージェントを拡張してください
* [フック](/docs/copilot/customization/hooks.md)を設定して、ファイルの編集後にフォーマッターを実行するなど、エージェントライフサイクルポイントでタスクを自動化してください
* [エージェントプラグイン](/docs/copilot/customization/agent-plugins.md)をブラウズして、コミュニティマーケットプレイスからパッケージ化されたカスタマイズをインストールしてください
* `.github/`ディレクトリをリポジトリにコミットして、チームとカスタマイズを共有してください
* [チャットカスタマイズエディター](/docs/copilot/customization/overview.md#chat-customizations-editor)ですべてのカスタマイズを一箇所で確認してください

