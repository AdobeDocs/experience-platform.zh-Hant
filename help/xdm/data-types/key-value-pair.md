---
title: 鍵值對資料類型
description: 本文檔概述了關鍵值對體驗資料模型(XDM)資料類型。
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 5%

---

# [!UICONTROL 鍵值對] 資料類型

[!UICONTROL 鍵值對] 是標準的體驗資料模型(XDM)資料類型，用於捕獲一般鍵值對的詳細資訊。 此資料類型用於 [[!UICONTROL Adobe AnalyticsExperienceEvent完全擴展] 欄位組](../field-groups/event/analytics-full-extension.md) 描述清單變數的陣列項。

![鍵值對結構](../images/data-types/key-value-pair.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `key` | 字串 | 泛型變數或值的鍵（名稱）。 |
| `value` | 字串 | 變數的值。 |

{style=&quot;table-layout:auto&quot;}

有關資料類型的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json)。
