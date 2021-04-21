---
keywords: Experience Platform; home；熱門話題； kafka; kafka連接器；
solution: Experience Platform
title: Kafka Connector
topic-legacy: overview
description: Adobe Experience Platform的串流連接器是以Apache Kafka Connect為基礎。 此程式庫可用來將JSON事件從您資料中心的Kafka主題即時串流至Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform連接器

Adobe Experience Platform的流連接器基於[!DNL Apache Kafka Connect]。 此程式庫可用來將資料中心的[!DNL Kafka]主題的JSON事件即時串流至[!DNL Experience Platform]。

串流連接器是匯入器（單向）連接器，將資料從[!DNL Kafka]主題傳送至[!DNL Experience Platform]上的註冊端點。 若要使用此連接器，您必須下載程式庫，將其新增至您現有的[!DNL Kafka]部署，並將[!DNL Kafka]主題設定至Adobe串流HTTP URL。 其他代碼為&#x200B;**not**。 連接器支援以下功能：

- 已驗證的資料收集
- 對消息進行批次處理以減少網路呼叫並提高吞吐量

有關[!DNL Kafka]連接器的詳細資訊，包括如何設定連接器的說明，請閱讀[入門指南](https://github.com/adobe/experience-platform-streaming-connect)。 有關更詳細的工作流程，請閱讀[開發人員指南](https://www.adobe.com/go/kafka-connector-developer-guide)。
