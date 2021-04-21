---
keywords: Experience Platform;home；熱門主題；策略實施；自動實施；基於API的實施；資料治理
solution: Experience Platform
title: 策略實施概述
topic-legacy: guide
description: 一旦資料使用標籤套用至Adobe Experience Platform資料集，且已針對這些標籤定義資料使用策略以執行行銷動作，資料治理功能可讓您強制執行這些原則並防止構成違反原則的資料作業。 Data Governance功能在平台上提供兩種策略實施方法：基於API的實施和自動實施。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 策略實施概述

一旦資料使用標籤套用至資料集，且已針對這些標籤定義資料使用策略以執行行銷動作，Adobe Experience Platform資料治理功能可讓您強制執行這些原則並防止構成違反原則的資料作業。

[!DNL Platform]上的[!DNL Data Governance]功能提供兩種策略實施方法：以API為基礎的強制與自動強制。

## 以API為基礎的強制

[!DNL Policy Service] API提供端點，可讓您針對資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制符合資料使用原則。

有關如何使用API評估策略的步驟，請參閱[API型強制實施](./api-enforcement.md)的教學課程。

## 自動強制

Experience Platform利用資料世系、資料分類和原則管理功能，自動評估並呈現違反原則的情況。 如需詳細資訊，請參閱[自動原則實施](./auto-enforcement.md)的概述。
