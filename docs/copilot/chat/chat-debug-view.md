---
ContentId: 2f4a8e9d-3c5b-4f6e-a7d8-1c2b3e4f5a6b
DateApproved: 10/16/2025
MetaDescription: Visual Studio CodeでChat Debugビューを使用して、AIリクエスト、レスポンス、システムプロンプト、ツールの呼び出しを検査する方法について説明します。
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# Chat Debugビュー

Chat Debugビューは、AIリクエストとレスポンスの詳細を確認できるVisual Studio Codeの専用ビューです。このビューは、どのような情報が言語モデルに送信され、どのように応答するかを理解するのに役立ちます。

この記事では、Chat Debugビューを開いてAIとのやり取りを検査する方法について説明します。

Chat Debugビューには、やり取りごとに次の情報が表示されます。

* AIの動作を設定するシステムプロンプト
* 送信したユーザープロンプト
* 言語モデルに送信されるコンテキスト
* 言語モデルからの詳細な応答
* チャットリクエストの一部として呼び出されるツールからの応答

## Chat Debugビューを開く

Chat Debugビューを開くには、次の手順を実行します。

* チャットのオーバーフローメニューを選択し、**Show Chat Debug View**を選択します。

* コマンドパレットから**Developer: Show Chat Debug View**コマンドを実行します。

Chat Debugビューが開き、作成した各チャットリクエストの詳細が表示されます。

![チャットリクエストとレスポンスの詳細を示すChat Debugビューのスクリーンショット。](../images/chat-debug-view/chat-debug-view.png)

各セクションを展開して詳細を確認できます。これは、1回のリクエストの一部として複数のツールが呼び出される可能性がある[エージェントの使用](/docs/copilot/chat/copilot-chat.md#switch-between-agents)時に特に役立ちます。

## 関連リソース

* [VS CodeでのAIのトラブルシューティング](/docs/copilot/faq.md#troubleshooting-and-feedback)
* [VS CodeでのAI使用に関するセキュリティの考慮事項](/docs/copilot/security.md)
