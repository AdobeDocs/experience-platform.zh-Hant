---
title: Adobe Analytics目標(A4T)登錄平台Web SDK
description: 瞭解如何使用Experience PlatformWeb SDK控制目標(A4T)資料的Adobe Analytics的收集。
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;web sdk
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Adobe Analytics用於目標(A4T)登錄平台Web SDK

使用Adobe Target進行個性化時，您可以選擇要用於效能度量的系統。 每個 [目標活動](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 允許您在目標報告和Adobe Analytics報告之間進行選擇。

如果使用分析報告，Adobe Target必須將以下內容與分析通信：

* 您的訪客所進入的Adobe Target活動
* 他們看過哪些經驗
* 已達到哪個轉換

Adobe Experience PlatformWeb SDK支援兩種類型的目標分析(A4T)用例分析日誌：

| 記錄方法 | 說明 |
| --- | --- |
| 伺服器端分析日誌記錄 | 通過邊緣網路發送的所有分析命中都通過伺服器端的目標詳細資訊進行增強，而不必經過命中縫合過程。 |
| 用戶端分析記錄 | 目標資料在客戶端返回，允許您使用 [資料插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html)。 |

日誌記錄方法由您的配置中是否啟用了Adobe Analytics [資料流](../../../datastreams/overview.md):

![測井方法決策流程](../assets/analytics-logging.png)

## 後續步驟

本文檔簡要介紹了Web SDK中A4T資料的不同記錄方法。 有關這些方法的詳細資訊，請參閱以下文檔：

* [平台Web SDK中A4T資料的伺服器端日誌記錄](./server-side.md)
* [平台Web SDK中A4T資料的客戶端日誌](./client-side.md)
