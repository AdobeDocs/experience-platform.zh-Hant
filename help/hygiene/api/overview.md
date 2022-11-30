---
title: 資料衛生API指南
description: 了解如何以程式設計方式修正或刪除客戶在Adobe Experience Platform中儲存的個人資料。
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 資料衛生API指南

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**.

資料衛生API可讓您以程式設計方式修正或刪除客戶在Adobe Experience Platform中儲存的個人資料，並排程資料集的到期日。 本指南涵蓋使用API的先決條件步驟，並提供指向更多端點特定檔案的連結。

## 快速入門

您可以透過下列根路徑存取資料衛生API: `https://platform.adobe.io/data/core/hygiene/`

以下各節概述在嘗試呼叫API前，您需要了解的核心概念。

### 收集必要標題的值

若要呼叫資料衛生API，您必須先收集驗證憑證。 關注 [API驗證指南](../../landing/api-authentication.md) 為資料衛生API的每個必要標題產生值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

### 讀取範例API呼叫

本檔案提供範例API呼叫，以示範如何設定請求格式。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/api-guide.md#sample-api) (位於Experience PlatformAPI快速入門手冊中)。

## 資料集有效期

資料集過期是因時間延遲而「刪除資料集」的動作。 透過建立資料集的有效期，您可以指定日後刪除該資料集的時間。 請參閱 [資料集過期端點指南](./dataset-expiration.md) 如需API中排程資料集有效期的詳細資訊。

## 記錄刪除

>[!IMPORTANT]
>
>記錄刪除請求僅適用於已購買的組織 **Adobe醫療保健盾**.
>
>
>記錄刪除旨在用於資料清除、刪除匿名資料或將資料最小化。 是 **not** 用於與一般資料保護規範(GDPR)等隱私權法規相關的資料主體權利要求（法規遵循）。 對於所有合規性使用案例，請使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 。

資料衛生API可讓您刪除一或所有資料集中與身分相關的所有記錄。 刪除身份的所有資料衛生任務都由稱為工作單的構造表示。 請參閱 [工作單端點指南](./workorder.md) 有關在API中使用記錄刪除的詳細資訊。

## 配額

貴組織受限於每類資料衛生操作的預定每月工作配額，這可能因許可而異。 請參閱 [quota endpoint wide（配額終結點指南）](./quota.md) 有關查看資料衛生流程的當前配額狀態的詳細資訊。

## 後續步驟

本指南說明如何使用API呼叫管理資料衛生請求。 如需如何在Platform UI中執行這些動作的詳細資訊，請參閱 [資料衛生UI指南](../ui/overview.md).
