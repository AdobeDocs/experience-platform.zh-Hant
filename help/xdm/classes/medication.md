---
title: 藥物治療類
description: 本文檔概述了「體驗資料模型」(XDM)中的「藥物」類。
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL 藥物] 類

在經驗資料模型(XDM)中， [!UICONTROL 藥物] 類捕獲定義用於醫療的物質（尤其是藥物或藥物）的最小屬性集。

![類結構](../images/classes/medication.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `medicationId` | [!UICONTROL 字串] | 藥物的唯一標識符。 |
| `medicationName` | [!UICONTROL 字串] | 藥物的名稱。 |

{style=&quot;table-layout:auto&quot;}

類可與 [[!UICONTROL 一種保健藥物] 欄位組](../field-groups/medication/healthcare-medication.md) 詳細描述藥物或藥物。
