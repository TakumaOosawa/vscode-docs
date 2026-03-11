---
ContentId: 3a7e9c4f-5d1b-4e8f-a2c6-8b0d3f5e7a9c
DateApproved: 3/9/2026
MetaDescription: VS Code のエージェントがメモリツールと Copilot Memory を使用してコンテキストを保持し、設定を学習し、会話全体で時間をかけて改善する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---

# VS Code エージェントのメモリ

Visual Studio Code のエージェントはメモリを使用して会話全体でコンテキストを保持します。各セッションで最初から始めるのではなく、エージェントは設定を思い出し、以前のタスクから学んだ教訓を適用し、時間をかけてコードベースに関する知識を構築します。

メモリがエージェントアーキテクチャにどのように適合するかについては、[エージェントの概念](/docs/copilot/concepts/agents.md#memory)を参照してください。

この記事では、VS Code でメモリツールの使用方法、メモリファイルの管理方法、および Copilot Memory が開発ワークフロー全体でメモリをどのように拡張するかについて説明します。

## メモリツール

> [!NOTE]
> メモリツールは現在プレビュー段階です。`setting(github.copilot.chat.tools.memory.enabled)`設定で有効または無効にできます。

メモリツールは、エージェントが作業時にメモを保存および呼び出すことができる組み込みエージェントツールです。エージェントに何かを記憶するよう明示的に依頼することもできます。すべてのデータはマシンにローカルに保存されます。メモリツールはデフォルトで有効になっています。

### メモリ スコープ

各スコープは、情報がどのくらい永続化するべきか、どこに適用するかによって異なる目的を果たします。

| スコープ | パス | セッション全体で永続化 | ワークスペース全体で永続化 | 用途 |
|---|---|---|---|---|
| **ユーザー** | `/memories/` | はい | はい | 設定、パターン、頻繁に使用されるコマンド |
| **リポジトリ** | `/memories/repo/` | はい | いいえ(ワークスペーススコープ) | コードベース規約、プロジェクト構造、ビルドコマンド |
| **セッション** | `/memories/session/` | いいえ(チャット終了時にクリア) | いいえ | タスク固有のコンテキスト、進行中の計画 |

#### ユーザーメモリ

ユーザーメモリは、すべてのワークスペースと会話全体で永続化します。最初の200行は自動的にすべてのセッション開始時にエージェントのコンテキストに読み込まれます。ユーザーメモリは、作業しているプロジェクトに関係なく適用される一般的な設定や分析情報に使用します。

例えば、コーディング設定を記憶するようエージェントに依頼します:

```prompt
Remember that I prefer tabs over spaces and always use single quotes in JavaScript
```

後の会話で、別のワークスペース内であっても、エージェントはこの設定を思い出し、生成されたコードに適用します。

#### リポジトリメモリ

リポジトリメモリは現在のワークスペースにスコープされ、そのワークスペース内の会話全体で永続化します。アーキテクチャの判断、命名規約、またはビルドコマンドなど、特定のコードベースに関する事実に使用します。

例えば:

```prompt
Remember that this project uses the repository pattern for data access and all API endpoints require authentication
```

#### セッションメモリ

セッションメモリは現在の会話にスコープされ、会話終了時にクリアされます。一時的な作業メモまたはエージェントがマルチステップタスクを実行している間に追跡するタスク固有のコンテキストに使用します。

Plan エージェントはセッションメモリを使用して、`plan.md`ファイルに実装計画を保持します。このプランはセッション中に利用可能で、**Chat: Show Memory Files**コマンドで表示できますが、後続セッションでは利用できません。[エージェントでの計画](/docs/copilot/agents/planning.md)について詳しく説明します。

### メモリの保存と取得

メモリを保存するには、自然言語でエージェントに何かを記憶するよう依頼します。エージェントは適切なスコープを判断し、対応するメモリファイルを作成または更新します。

```prompt
Remember that our team uses conventional commits for all commit messages
```

メモリを取得するには、新しい会話でそれについて尋ねます。エージェントはメモリファイルを確認し、関連情報を思い出します。

```prompt
What are our commit message conventions?
```

エージェントのチャット応答のメモリファイル参照はクリック可能なため、メモリファイルのコンテンツをメモリファイル全体で直接表示できます。

### メモリ ファイルの管理

VS Code では、メモリファイルを表示および管理するためのコマンドを提供します:

* **Chat: Show Memory Files**: スコープ全体のすべてのメモリファイルのリストを開きます。ファイルを選択して内容を表示します。
* **Chat: Clear All Memory Files**: すべてのスコープのすべてのメモリファイルを削除します。

> [!NOTE]
> 個別のメモリファイルを削除することはまだサポートされていません。**Chat: Clear All Memory Files**を使用してすべてのメモリを削除するか、エージェントに特定のメモリファイルを更新するよう依頼して、古い情報を削除してください。

## Copilot Memory

> [!NOTE]
> Copilot Memory はプレビュー段階にあり、上記で説明されているローカルメモリツールから分離されています。

[Copilot Memory](https://docs.github.com/copilot/how-tos/use-copilot-agents/copilot-memory)は、Copilot が作業時にリポジトリ固有の分析情報を学習および保持できるようにする GitHub ホストのメモリシステムです。ローカルメモリツールとは異なり、Copilot Memory は Copilot コーディングエージェント、Copilot コードレビュー、Copilot CLI を含む複数の GitHub Copilot サーフェス全体で共有されます。

### Copilot Memory の仕組み

Copilot エージェントがリポジトリで作業すると、「メモリ」と呼ばれる厳密にスコープされた分析情報を自動的にキャプチャします。これらのメモリは:

* **リポジトリスコープ**: メモリは特定のリポジトリに関連付けられ、書き込みアクセス権を持つコントリビューターによってのみ作成できます。
* **クロスエージェント**: 1 つの Copilot エージェントが学習することは他のエージェントで利用できます。例えば、Copilot コードレビューによって発見されたパターンは、後で Copilot コーディングエージェントをガイドできます。
* **使用前に検証**: エージェントは現在のコードベースに対してメモリを検証してから適用し、古い情報または正確でない情報が結果に影響するのを防ぎます。
* **自動的に期限切れ**: メモリは28日後に削除され、古い情報を避けます。

### Copilot Memory の有効化

Copilot Memory はデフォルトでオフになっており、GitHub の設定で有効にする必要があります:

* **個別ユーザー**(Copilot Pro または Pro+): GitHub の[個人 Copilot 設定](https://github.com/settings/copilot)で Copilot Memory を有効にします。
* **組織とエンタープライズ**: 組織またはエンタープライズ設定のポリシー設定から有効にします。

さらに、VS Code で`setting(github.copilot.chat.copilotMemory.enabled)`設定を使用して Copilot Memory 統合を有効にする必要があります。

リポジトリ所有者は、**Repository Settings** > **Copilot** > **Memory**に保存されたメモリを確認および削除できます。

詳細なセットアップ手順については、GitHub ドキュメントの[Copilot Memory の有効化とキュレーション](https://docs.github.com/copilot/how-tos/use-copilot-agents/copilot-memory)を参照してください。

### メモリツール対 Copilot Memory

| | メモリツール | Copilot Memory |
|---|---|---|
| **ストレージ** | ローカル(マシン上) | GitHub ホスト型(リモート) |
| **スコープ** | ユーザー、リポジトリ、セッション | リポジトリのみ |
| **Copilot サーフェス全体で共有** | いいえ(VS Code のみ) | はい(コーディングエージェント、コードレビュー、CLI) |
| **作成者** | チャット中のあなたまたはエージェント | Copilot エージェント自動 |
| **デフォルトで有効** | はい | いいえ(オプトイン) |
| **有効期限** | 手動管理 | 自動(28日) |

2つのシステムは補完的です。VS Code での個人的な設定とセッション固有のコンテキストにはローカルメモリツールを使用します。開発ワークフロー全体のすべての Copilot エージェントに利益をもたらすリポジトリ知識には Copilot Memory を使用します。

## 関連リソース

* [エージェントでの計画](/docs/copilot/agents/planning.md)
* [エージェント ツール](/docs/copilot/agents/agent-tools.md)
* [Copilot Memory の有効化とキュレーション](https://docs.github.com/copilot/how-tos/use-copilot-agents/copilot-memory)(GitHub ドキュメント)
* [GitHub Copilot 向けエージェント型メモリシステムの構築](https://github.blog/ai-and-ml/github-copilot/building-an-agentic-memory-system-for-github-copilot/)(GitHub ブログ)

