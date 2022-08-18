---
title: 《資料衛生API指南》
description: 瞭解如何以寫程式方式更正或刪除客戶在Adobe Experience Platform儲存的個人資料。
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 49ba5263c6dc8eccac2ffe339476cf316c68e486
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---

# 資料衛生API指南

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

資料衛生API允許您以寫程式方式更正或刪除客戶在Adobe Experience Platform儲存的個人資料，並為資料集安排過期日期。 本指南介紹使用API的先決條件步驟，並提供指向更多特定於端點的文檔的連結。

## 快速入門

您可以通過以下根路徑訪問資料衛生API: `https://platform.adobe.io/data/core/hygiene/`

以下各節概述了在嘗試調用API之前需要瞭解的核心概念。

### 收集所需標題的值

要調用資料衛生API，必須先收集身份驗證憑據。 關注 [API驗證指南](../../landing/api-authentication.md) 為資料衛生API的每個必需標頭生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* `Content-Type: application/json`

### 讀取示例API調用

本文檔提供了一個示例API調用，以演示如何格式化請求。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/api-guide.md#sample-api) 的FTP伺服器連接設定。

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## 資料集過期

資料集過期是延遲的「刪除資料集」操作。 通過建立資料集過期，您將指定將來刪除該資料集的時間。 查看 [資料集到期終結點指南](./dataset-expiration.md) 有關在API中計畫資料集過期的詳細資訊。

## 後續步驟

本指南介紹了如何使用API調用管理資料衛生請求。 有關如何在平台UI中執行這些操作的資訊，請參見 [資料衛生UI指南](../ui/overview.md)。
