---
keywords: Experience Platform；首頁；熱門主題；策略實施；自動實施；基於API的實施；資料治理
solution: Experience Platform
title: 策略實施概述
description: 瞭解如何在Adobe Experience Platform強制實施資料使用策略。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 策略實施概述

一次 [資料使用標籤](../labels/overview.md) 已應用並 [資料使用策略](../policies/overview.md) 定義後，您可以強制實施這些策略以防止構成策略違規的資料操作。

>[!NOTE]
>
>本文檔重點介紹資料使用策略的實施。 有關訪問控制策略的資訊，請參閱上的指南 [基於屬性的訪問控制](../../access-control/abac/overview.md)。

在Adobe Experience Platform，有兩種政策執行方法：自動實施和基於API的實施。

## 自動強制

Experience Platform利用資料沿襲、資料分類和策略管理功能來自動評估和顯示策略違規。 請參閱 [自動策略執行](./auto-enforcement.md) 的子菜單。

## 基於API的強制

的 [!DNL Policy Service] API提供了端點，允許您針對資料集或資料使用標籤的任意組合test營銷操作，以檢查是否發生任何策略違規。 然後，您可以根據API響應在您的體驗應用程式內設定協定，以適當強制實施資料治理策略合規性。

請參閱上的教程 [基於API的強制](./api-enforcement.md) 有關如何使用API評估策略的步驟。
