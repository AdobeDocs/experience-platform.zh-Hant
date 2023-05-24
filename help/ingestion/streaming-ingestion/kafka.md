---
keywords: Experience Platform；首頁；熱門主題；kafka;kafka連接器；Kafka;
solution: Experience Platform
title: 卡夫卡連接器
description: Adobe Experience Platform的流連接器基於Apache Kafka Connect。 此庫可用於將JSON事件從資料中心的Kafka主題直接流式傳輸到即時Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform連接器

Adobe Experience Platform的流連接器基於 [!DNL Apache Kafka Connect]。 此庫可用於流JSON事件 [!DNL Kafka] 資料中心的主題直接 [!DNL Experience Platform] 即時。

流連接器是匯流（單向）連接器，用於從 [!DNL Kafka] 主題到的註冊終結點 [!DNL Experience Platform]。 要使用此連接器，必須下載庫並將其添加到現有庫 [!DNL Kafka] 部署和配置 [!DNL Kafka] 主題到Adobe流HTTP URL。 其他代碼為 **不** 。 連接器支援以下功能：

- 已驗證的資料集合
- 對消息進行批處理以減少網路呼叫並提高吞吐量

有關 [!DNL Kafka] 連接器，包括有關如何設定連接器的說明，請閱讀 [入門指南](https://github.com/adobe/experience-platform-streaming-connect)。 有關更詳細的工作流，請閱讀 [開發者指南](https://www.adobe.com/go/kafka-connector-developer-guide)。
