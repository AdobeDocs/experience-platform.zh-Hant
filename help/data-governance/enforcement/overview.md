---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 策略實施概述
description: 了解如何在Adobe Experience Platform上執行資料使用原則。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 策略實施概述

一次 [資料使用量標籤](../labels/overview.md) 已應用， [資料使用原則](../policies/overview.md) ，您可以強制執行這些策略以防止構成策略違規的資料操作。

>[!NOTE]
>
>本檔案著重於資料使用原則的實作。 有關訪問控制策略的資訊，請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md).

在Adobe Experience Platform上有兩種政策執行方法：自動實作和API型實作。

## 自動執行

Experience Platform利用資料處理、資料分類和策略管理功能，自動評估和顯示策略違規。 請參閱 [自動策略執行](./auto-enforcement.md) 以取得更多資訊。

## API型實作

此 [!DNL Policy Service] API提供的端點可讓您針對資料集或資料使用標籤的任意組合測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制執行資料控管原則符合性。

請參閱 [API型實作](./api-enforcement.md) 以取得如何使用API評估原則的步驟。
