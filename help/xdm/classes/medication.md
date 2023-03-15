---
title: 藥物類
description: 本檔案概述Experience Data Model(XDM)中的「藥物」類別。
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL 藥物] 類

在Experience Data Model(XDM)中， [!UICONTROL 藥物] 類別會擷取定義用於治療的物質（特別是藥物或藥物）的最小屬性集。

![類結構](../images/classes/medication.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。 |
| `medicationId` | [!UICONTROL 字串] | 藥物的唯一標識符。 |
| `medicationName` | [!UICONTROL 字串] | 藥物的名字。 |

{style="table-layout:auto"}

可使用 [[!UICONTROL 保健藥物] 欄位群組](../field-groups/medication/healthcare-medication.md) 來進一步說明藥物或藥物的細節。
