---
title: 計畫類
description: 本檔案概述Experience Data Model(XDM)中的Plan類別。
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL 計畫] 類

在Experience Data Model(XDM)中， [!UICONTROL 計畫] 類別會擷取定義計畫的最小屬性集，例如健康計畫或保險計畫。

![類結構](../images/classes/plan.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。 |
| `planId` | [!UICONTROL 字串] | 計畫的唯一標識符。 |
| `planName` | [!UICONTROL 字串] | 計畫的名稱。 |

{style="table-layout:auto"}

可使用 [[!UICONTROL 醫療保健計畫詳細資訊] 欄位群組](../field-groups/plan/healthcare-plan-details.md) 詳細描述醫療保險計畫。
