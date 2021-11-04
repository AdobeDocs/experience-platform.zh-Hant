---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 策略實施概述
topic-legacy: guide
description: 將資料使用量標籤套用至Adobe Experience Platform資料集，並針對這些標籤定義了行銷動作的資料使用量原則後，資料控管功能可讓您強制執行這些原則，並防止發生違反原則的資料作業。 平台上的資料控管功能提供兩種策略實施方法、以API為基礎的實施和自動實施。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 策略實施概述

將資料使用量標籤套用至資料集，並針對這些標籤定義資料使用量原則以執行行銷動作後，Adobe Experience Platform資料控管功能可讓您強制執行這些原則，並防止發生違反原則的資料操作。

資料控管功能提供兩種策略實施方法， [!DNL Platform]:以API為基礎的強制與自動強制。

## API型實作

此 [!DNL Policy Service] API提供的端點可讓您針對資料集或資料使用標籤的任意組合測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制執行資料使用原則符合性。

請參閱 [API型實作](./api-enforcement.md) 以取得如何使用API評估原則的步驟。

## 自動執行

Experience Platform利用資料處理、資料分類和策略管理功能，自動評估和顯示策略違規。 請參閱 [自動策略執行](./auto-enforcement.md) 以取得更多資訊。
