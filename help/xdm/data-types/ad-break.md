---
title: 廣告插播資料型別
description: 瞭解廣告插播體驗資料模型(XDM)資料型別。
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 21%

---

# [!UICONTROL 廣告插播]資料型別

[!UICONTROL 廣告插播]是標準的體驗資料模型(XDM)資料型別，可描述如何將計時廣告插入定時媒體中。

![資料型別結構](../images/data-types/ad-break.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc.title` | 字串 | 廣告插播的易記名稱。 |
| `_id` | 字串 | 廣告插播的唯一識別碼。 |
| `offset` | 整數 | 從主要內容開始的廣告插播偏移量 (秒數)。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
