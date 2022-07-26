---
title: 廣告中斷資料類型
description: 本文檔概述了Ad Break體驗資料模型(XDM)資料類型。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 6%

---

# [!UICONTROL 廣告分段] 資料類型

[!UICONTROL 廣告分段] 是標準的體驗資料模型(XDM)資料類型，它描述如何將定時廣告插入到定時媒體中。

![資料類型結構](../images/data-types/ad-break.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc.title` | 字串 | 廣告分段的友好名稱。 |
| `_id` | 字串 | 廣告分段的唯一標識符。 |
| `offset` | 整數 | 廣告從主內容開始的偏移（以秒為單位）。 |

{style=&quot;table-layout:auto&quot;}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
