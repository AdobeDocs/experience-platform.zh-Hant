---
title: Platform Web SDK中A4T資料的伺服器端記錄
description: 了解如何使用Adobe Analytics Web SDK為Target(A4T)啟用伺服器端記錄。
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target；網頁；sdk；平台；記錄；
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Platform Web SDK中A4T資料的伺服器端記錄

Adobe Experience Platform Web SDK可讓您在平台邊緣網路上實作Adobe Analytics for Target(A4T)功能。 啟用伺服器端記錄時，所有透過邊緣網路傳送的Analytics點擊都會在伺服器端增強Target詳細資訊，而不需經過點擊拼接程式。

在資料流設定中啟用Analytics時，會啟用Analytics的伺服器端記錄：

![啟用Analytics資料流設定](../assets/enable-analytics-datastream.png)

下圖顯示啟用伺服器端Analytics記錄時，資料如何透過系統流動：

![伺服器端記錄流程](../assets/analytics-server-side-logging.png)

## 後續步驟

本指南說明Web SDK中A4T資料的伺服器端記錄。 請參閱 [用戶端記錄](./client-side.md) ，以取得在用戶端上處理A4T資料的詳細資訊。
