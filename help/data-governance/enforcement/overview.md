---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 原則執行概觀
description: 瞭解如何在Adobe Experience Platform上執行資料使用原則。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 原則執行概觀

套用[資料使用標籤](../labels/overview.md)並定義[資料使用原則](../policies/overview.md)後，您可以強制這些原則以防止構成原則違規的資料作業。

>[!NOTE]
>
>本檔案著重於資料使用原則的實作。 如需有關存取控制原則的資訊，請參閱[以屬性為基礎的存取控制](../../access-control/abac/overview.md)指南。

在Adobe Experience Platform上執行原則的方法有兩種：自動執行和API型執行。

## 自動強制執行

Experience Platform利用資料譜系、資料分類和原則管理功能，來自動評估和顯示原則違規。 如需詳細資訊，請參閱[自動原則執行](./auto-enforcement.md)的概觀。

## API型強制執行

[!DNL Policy Service] API提供的端點可讓您針對資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何原則違規。 接著，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當地強制資料控管原則相容。

如需如何使用API評估原則的步驟，請參閱有關[API型強制](./api-enforcement.md)的教學課程。
