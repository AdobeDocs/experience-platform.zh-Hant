---
title: 付款人類
description: 本文檔概述了「體驗資料模型」(XDM)中的付款人類。
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 付款人] 類

在經驗資料模型(XDM)中， [!UICONTROL 付款人] class捕獲定義付款人業務實體的最小屬性集，該實體收集與保險公司（如健康保險）相關的資料。

![類結構](../images/classes/payer.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `payerId` | [!UICONTROL 字串] | 付款人的唯一標識符。 |
| `payerName` | [!UICONTROL 字串] | 付款人的姓名。 |

{style="table-layout:auto"}
