---
title: 廣告插播資料類型
description: 本檔案概述廣告插播體驗資料模型(XDM)資料類型。
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 4%

---

# [!UICONTROL 廣告插播] 資料類型

[!UICONTROL 廣告插播] 是標準的Experience Data Model(XDM)資料類型，可說明計時廣告插入計時媒體的方式。

![資料類型結構](../images/data-types/ad-break.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc.title` | 字串 | 廣告插播的易記名稱。 |
| `_id` | 字串 | 廣告插播的唯一識別碼。 |
| `offset` | 整數 | 廣告插播從主要內容開始的位移（以秒為單位）。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
