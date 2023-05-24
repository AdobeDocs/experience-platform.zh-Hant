---
title: 計畫類
description: 本文檔概述了「體驗資料模型」(XDM)中的「計畫」類。
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL 計畫] 類

在經驗資料模型(XDM)中， [!UICONTROL 計畫] 類捕獲定義計畫的最小屬性集，如健康計畫或保險計畫。

![類結構](../images/classes/plan.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `planId` | [!UICONTROL 字串] | 計畫的唯一標識符。 |
| `planName` | [!UICONTROL 字串] | 計畫的名稱。 |

{style="table-layout:auto"}

類可與 [[!UICONTROL 醫療保健計畫詳細資訊] 欄位組](../field-groups/plan/healthcare-plan-details.md) 詳細介紹醫療保險計畫。
