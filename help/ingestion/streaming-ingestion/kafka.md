---
keywords: Experience Platform；首頁；熱門主題；kafka;kafka連接器；Kafka;
solution: Experience Platform
title: Kafka Connector
description: Adobe Experience Platform的串流連接器以Apache Kafka Connect為基礎。 此程式庫可用來將JSON事件從資料中心的Kafka主題直接串流至即時Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform連接器

Adobe Experience Platform的資料流連接器以 [!DNL Apache Kafka Connect]. 此程式庫可用來串流JSON事件，從 [!DNL Kafka] 資料中心的主題直接 [!DNL Experience Platform] 即時。

流連接器是匯流器（單向）連接器，用於從 [!DNL Kafka] 主題到的註冊端點 [!DNL Experience Platform]. 若要使用此連接器，您必須下載程式庫，並將其新增至現有的 [!DNL Kafka] 部署，並配置 [!DNL Kafka] 主題至Adobe串流HTTP URL。 其他程式碼為 **not** 必填。 連接器支援下列功能：

- 已驗證的資料集合
- 對報文進行批次處理，以減少網路呼叫並提高吞吐量

如需 [!DNL Kafka] 連接器，包括如何設定連接器的說明，請閱讀 [快速入門手冊](https://github.com/adobe/experience-platform-streaming-connect). 如需更詳細的工作流程，請參閱 [開發人員指南](https://www.adobe.com/go/kafka-connector-developer-guide).
