---
title: 曝光數資料類型
description: 本檔案概述曝光數XDM資料類型。
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

#  Impressions資料類型

 曝光是描述行銷曝光的標準XDM資料類型，此量度用於量化廣告、數位貼文或網頁等內容的數位檢視或參與次數。

![](../images/data-types/impressions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ID` | 字串 | 曝光的唯一ID。 |
| `displays` | 整數 | 向客戶顯示曝光項目的次數。 |
| `selected` | 整數 | 已選取或點按曝光項目的次數。 |
| `type` | 字串 | 曝光類型。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
