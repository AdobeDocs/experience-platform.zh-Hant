---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；裝置；資料類型；資料類型；貨幣；
solution: Experience Platform
title: 貨幣資料類型
description: 本檔案概述貨幣XDM資料類型。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL 貨幣] 資料類型

[!UICONTROL 貨幣] 是描述貨幣量的標準XDM資料類型，包括貨幣類型和轉換日期。

![](../images/data-types/currency.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `amount` | 雙倍 | 由 `currencyCode`. |
| `conversionDate` | DateTime | 貨幣轉換時間的時間戳記。 |
| `currencyCode` | 字串 | ISO 4217代碼，用於指示 `amount` 代表。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
