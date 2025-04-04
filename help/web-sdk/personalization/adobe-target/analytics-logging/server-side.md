---
title: Experience Platform Web SDK中A4T資料的伺服器端記錄
description: 瞭解如何使用Experience Platform Web SDK為Adobe Analytics for Target (A4T)啟用伺服器端記錄。
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t；target；web；sdk；平台；記錄；
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Experience Platform Web SDK中A4T資料的伺服器端記錄

Adobe Experience Platform Web SDK可讓您在Experience Platform Edge Network上實作Adobe Analytics for Target (A4T)功能。 啟用伺服器端記錄時，所有透過Edge Network傳送的Analytics點選都會在伺服器端以Target詳細資料增加，不必經過點選拼接程式。

在資料流設定中啟用Analytics時，Analytics的伺服器端記錄會啟用：

![已啟用Analytics資料流設定](../assets/enable-analytics-datastream.png)

下圖顯示啟用伺服器端Analytics記錄時，資料如何流經系統：

![伺服器端記錄流程](../assets/analytics-server-side-logging.png)

## 後續步驟

本指南涵蓋Web SDK中A4T資料的伺服器端記錄。 請參閱[使用者端記錄](./client-side.md)的指南，以取得如何在使用者端處理A4T資料的詳細資訊。
