---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 卡夫卡連接器
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# [!DNL Kafka] Adobe Experience Platform的連接器

Adobe Experience Platform的串流連接器以為基礎 [!DNL Apache Kafka Connect]。 此程式庫可用來將JSON事件從資料 [!DNL Kafka] 中心的主題直接串流 [!DNL Experience Platform] 至即時。

串流連接器是匯入器（單向）連接器，將資料從主題傳 [!DNL Kafka] 送至上的註冊端點 [!DNL Experience Platform]。 若要使用此連接器，您必須下載程式庫、將其新增至您現有的 [!DNL Kafka] 部署，並將主 [!DNL Kafka] 題設定至Adobe串流HTTP URL。 不需要其 **他程式碼** 。 連接器支援以下功能：

- 已驗證的資料收集
- 對消息進行批次處理以減少網路呼叫並提高吞吐量

有關連接器的詳 [!DNL Kafka] 細資訊，包括如何設定連接器的說明，請閱讀快速 [入門指南](https://github.com/adobe/experience-platform-streaming-connect)。 如需更詳細的工作流程，請閱讀開發 [人員指南](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)。