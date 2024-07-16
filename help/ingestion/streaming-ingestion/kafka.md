---
keywords: Experience Platform；首頁；熱門主題；kafka；kafka聯結器；Kafka；
solution: Experience Platform
title: Kafka聯結器
description: Adobe Experience Platform的串流聯結器以Apache Kafka Connect為基礎。 此資料庫可用來將資料中心中Kafka主題的JSON事件直接串流到即時Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 適用於Adobe Experience Platform的[!DNL Kafka]聯結器

Adobe Experience Platform的資料流聯結器是以[!DNL Apache Kafka Connect]為基礎。 此資料庫可用來將資料中心中[!DNL Kafka]個主題的JSON事件即時直接串流到[!DNL Experience Platform]。

串流聯結器是接收器（單向）聯結器，將來自[!DNL Kafka]主題的資料傳遞至[!DNL Experience Platform]上的已登入端點。 若要使用此聯結器，您必須下載程式庫、將其新增至您現有的[!DNL Kafka]部署，並將[!DNL Kafka]主題設定至Adobe串流HTTP URL。 額外的程式碼是&#x200B;**不需要**。 聯結器支援下列功能：

- 已驗證的資料集合
- 批次處理訊息以減少網路呼叫並提高輸送量

如需[!DNL Kafka]聯結器的詳細資訊，包括如何設定聯結器的說明，請閱讀[快速入門手冊](https://github.com/adobe/experience-platform-streaming-connect)。 如需更詳細的工作流程，請參閱[開發人員指南](https://www.adobe.com/go/kafka-connector-developer-guide)。
