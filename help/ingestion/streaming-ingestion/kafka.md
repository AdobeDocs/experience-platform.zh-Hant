---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 卡夫卡連接器
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Adobe Experience Platform的Kafka連接器

Adobe Experience Platform的串流連接器以Apache Kafka Connect為基礎。 此程式庫可用來將JSON事件從資料中心的Kafka主題即時串流至Experience Platform。

串流連接器是匯入（單向）連接器，可將資料從Kafka主題傳送至Experience Platform上的已註冊端點。 若要使用此連接器，您必須下載程式庫、將其新增至您現有的Kafka部署，以及將Kafka主題設定至Adobe串流HTTP URL。 不需要其 **他程式碼** 。 連接器支援以下功能：

- 已驗證的資料收集
- 對消息進行批次處理以減少網路呼叫並提高吞吐量

有關Kafka連接器的更多資訊，包括如何設定連接器的說明，請閱讀快速入 [門指南](https://github.com/adobe/experience-platform-streaming-connect)。 如需更詳細的工作流程，請閱讀開發 [人員指南](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)。