---
title: Adobe Analytics for Target(A4T)在Platform Web SDK中登入
description: 了解如何使用Adobe Analytics Web SDK控制Target(A4T)資料的收集Experience Platform。
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t；記錄；analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Adobe Analytics for Target(A4T)在Platform Web SDK中登入

將Adobe Target用於個人化時，您可以選擇要用於效能測量的系統。 每個 [Target活動](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 可讓您在Target報表和Adobe Analytics報表之間進行選取。

如果您使用Analytics報表，Adobe Target必須向Analytics傳達下列資訊：

* 您的訪客已進入哪些Adobe Target活動
* 他們看過什麼經驗
* 已達到哪個轉換

Adobe Experience Platform Web SDK支援兩種Analytics記錄for Target(A4T)使用案例：

| 記錄方法 | 說明 |
| --- | --- |
| 伺服器端Analytics記錄 | 所有透過邊緣網路傳送的Analytics點擊都會在伺服器端透過Target詳細資訊而增強，而無須執行點擊拼接程式。 |
| 用戶端分析記錄 | 在用戶端傳回Target資料，可讓您使用 [資料插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

記錄方法取決於您所設定的 [資料流](../../../datastreams/overview.md):

![測井方法決策流程](../assets/analytics-logging.png)

## 後續步驟

本檔案簡要介紹Web SDK中A4T資料的不同記錄方法。 如需這些方法的詳細資訊，請參閱下列檔案：

* [Platform Web SDK中A4T資料的伺服器端記錄](./server-side.md)
* [平台Web SDK中A4T資料的用戶端記錄](./client-side.md)
