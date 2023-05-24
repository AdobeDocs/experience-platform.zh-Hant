---
title: 平台Web SDK中A4T資料的伺服器端日誌
description: 瞭解如何使用Experience PlatformWeb SDK為目標(A4T)啟用Adobe Analytics的伺服器端日誌記錄。
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;logging
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# 平台Web SDK中A4T資料的伺服器端日誌

Adobe Experience PlatformWeb SDK允許您在平台邊緣網路上實現目標(A4T)功能的Adobe Analytics。 啟用伺服器端日誌記錄後，通過邊緣網路發送的所有分析命中都會通過伺服器端的目標詳細資訊進行增強，而不必經過命中縫合過程。

在資料流配置中啟用分析時，將啟用分析的伺服器端日誌記錄：

![已啟用分析資料流配置](../assets/enable-analytics-datastream.png)

下圖顯示了啟用伺服器端分析日誌記錄時資料如何通過系統：

![伺服器端日誌流](../assets/analytics-server-side-logging.png)

## 後續步驟

本指南涵蓋Web SDK中A4T資料的伺服器端日誌記錄。 請參閱上的指南 [客戶端日誌](./client-side.md) 的子菜單。
