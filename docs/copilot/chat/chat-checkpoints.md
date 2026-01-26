---
ContentId: 8f4d3e2a-9b7c-4e1d-a6f5-3c2b1d8e9f0a
DateApproved: 01/08/2026
MetaDescription: Learn how to edit previous chat requests, restore your workspace to earlier states using checkpoints, and undo changes made by chat in Visual Studio Code.
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# チェックポイントとリクエストの編集で変更を元に戻す

Visual Studio Codeのチャットセッションでは、ワークスペース内の1つ以上のファイルが変更される可能性があり、手動で元に戻すのは面倒な場合があります。たとえば、前のチャットリクエストを修正したり、別のアプローチを試したり、予期しない変更から回復したりしたい場合があります。

この記事では、以前のチャットリクエストを編集する方法と、チェックポイントを使用してチャットによるファイル変更をロールバックする方法について説明します。

## 以前のチャットリクエストの編集

> [!NOTE]
> チャットリクエストを編集する機能は、VS Code バージョン1.102から利用可能です。

会話履歴の各チャットリクエストは編集可能です。以前のチャットリクエストを編集すると、編集後のリクエストが新しいリクエストとして言語モデルに送信され、元のリクエストおよびそれ以降のリクエストによって行われたファイル変更は元に戻されます。

以前のチャットリクエストを編集するには、修正するリクエストをチャットビューで選択し、再送信します。`setting(chat.editRequests)`設定で編集体験を構成または無効にすることができます。

<video src="../images/chat-checkpoints/chat-edit-request.mp4" title="Video showing the editing of a previous chat request in the Chat view." autoplay loop controls muted></video>

## チェックポイントを使用してファイル変更を元に戻す

> [!NOTE]
> チェックポイントは、VS Code リリース 1.103から利用可能です。

チャットチェックポイントは、ワークスペースの状態を過去の時点に復元する方法を提供し、チャットのやり取りによって複数のファイルに変更が生じた場合に役立ちます。

チェックポイントが有効な場合、VS Codeはチャットのやり取り中の重要なポイントでファイルの変更のスナップショットを自動的に作成し、チャットリクエストによる変更が期待したものでなかった場合や、別のアプローチを試したい場合に、既知の良好な状態に戻ることができます。

チェックポイントを有効にするには、`setting(chat.checkpoints.enabled)`設定を構成します。

### チェックポイントの復元

チェックポイントを復元すると、VS Codeはワークスペースをそのチェックポイントの時点の状態に戻します。つまり、そのチェックポイント以降にファイルに加えられた変更は*すべて*元に戻されます。

ワークスペースを以前のチェックポイントに復元するには:

1. チャットビューで、チャットセッション内の以前のチャットリクエストに移動します。

1. チャットリクエストにカーソルを合わせ、**チェックポイントの復元 (Restore Checkpoint)** を選択します。

    ![Screenshot of the Chat view, showing the Restore Checkpoint action in the Chat view.](../images/chat-checkpoints/chat-restore-checkpoint.png)

1. チェックポイントを復元し、その時点以降に行われたファイル変更を元に戻すことを確認します。

    チャットリクエストが会話履歴から削除され、ワークスペースファイルがチェックポイントの時点の状態に復元されることに注意してください。

### 復元後のやり直し

以前のチェックポイントに復元した後、元に戻した変更をやり直すことができます。これは、誤ってチェックポイントに復元してしまった場合に役立つことがあります。

チェックポイントの復元後に変更をやり直すには、チャットビューで **やり直し (Redo)** を選択します。

![Screenshot of the Chat view, showing the Redo button to redo the changes after restoring a checkpoint to a previous state.](../images/chat-checkpoints/chat-redo-checkpoint.png)

### チェックポイントでのファイル変更の表示

各チャットリクエストの影響を理解し、どのチェックポイントに復元するかを判断しやすくするために、`setting(chat.checkpoints.showFileChanges)`設定を有効にします。これにより、各チャットリクエストの終了時に変更されたファイルのリストと、各ファイルで追加および削除された行数が表示されます。

![Screenshot of the Chat view, showing the file changes at the end of a chat request.](../images/chat-checkpoints/chat-checkpoint-changed-files.png)

## よくある質問

### チェックポイントはGitバージョン管理に代わるものですか?

いいえ。チェックポイントはチャットセッション内の迅速な反復のために設計されており、一時的なものです。Gitを補完するものであり、Gitに代わるものではありません。永続的なバージョン管理とコラボレーションにはGitを使用してください。チェックポイントは、アクティブなチャットセッション中の実験に最適です。

## 関連リソース

* [VS Codeでのチャットの開始](/docs/copilot/chat/copilot-chat.md)
