---
ContentId: 2f4a8e9d-3c5b-4f6e-a7d8-1c2b3e4f5a6b
DateApproved: 10/16/2025
MetaDescription: Learn how to use the Chat Debug view to inspect AI requests, responses, system prompts, and tool invocations in Visual Studio Code.
MetaSocialImage: ../images/shared/github-copilot-social.png
---
# Chat Debug view

MetaDescription: Visual Studio CodeでChat Debug viewを使用して、AIリクエスト、応答、システムプロンプト、ツールの呼び出しを確認する方法を説明します。

Chat Debug viewは、Visual Studio Codeの専用ビューで、AIリクエストと応答の詳細を確認できます。このビューは、言語モデルにどのような情報が送信され、どのように応答するのかを理解するのに役立ちます。

この記事では、Chat Debug viewを開いて使用し、AIのやり取りを確認する方法を説明します。

Chat Debug viewでは、各やり取りについて次の情報が表示されます。

* AIの動作を設定するシステムプロンプト
* 送信したユーザープロンプト
* 言語モデルに送信されるコンテキスト
* 言語モデルからの詳細な応答
* チャットリクエストの一部として呼び出されるツールからの応答

## Open the Chat Debug view

Chat Debug viewを開くには、次の手順に従います。

* Chatのオーバーフローメニューを選択し、**Show Chat Debug View**を選択します。

* コマンドパレットから、**Developer: Show Chat Debug View**コマンドを実行します。

Chat Debug viewが開き、実行した各チャットリクエストの詳細が表示されます。

![Screenshot of the Chat Debug view, showing the details of a chat request and response.](../images/chat-debug-view/chat-debug-view.png)

各セクションを展開して、すべての詳細を確認できます。これは、単一のリクエストの一部として複数のツールが呼び出される可能性がある[エージェントを使用する場合](/docs/copilot/chat/copilot-chat.md#switch-between-agents)に特に便利です。

## Related resources

* [VS CodeでAIをトラブルシューティングする](/docs/copilot/faq.md#troubleshooting-and-feedback)
* [VS CodeでAIを使用する際のセキュリティに関する考慮事項](/docs/copilot/security.md)
