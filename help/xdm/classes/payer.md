---
title: 付款人分類
description: 本檔案概述Experience Data Model(XDM)中的付款人類別。
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 付款人] 類

在Experience Data Model(XDM)中， [!UICONTROL 付款人] 類別捕獲定義付款人業務實體的最小屬性集，該實體收集與保險公司有關的資料（如健康保險）。

![類結構](../images/classes/payer.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。 |
| `payerId` | [!UICONTROL 字串] | 付款人的唯一標識符。 |
| `payerName` | [!UICONTROL 字串] | 付款人的名稱。 |

{style="table-layout:auto"}
