---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；裝置；資料型別；資料型別；貨幣；
solution: Experience Platform
title: 貨幣資料型別
description: 瞭解貨幣XDM資料型別。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# [!UICONTROL 貨幣]資料型別

[!UICONTROL Currency]是標準的XDM資料型別，說明貨幣金額，包括貨幣型別和轉換日期。

![](../images/data-types/currency.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `amount` | 雙精度 | 由`currencyCode`定義的貨幣金額。 |
| `conversionDate` | 日期時間 | 進行貨幣轉換的時間戳記。 |
| `currencyCode` | 字串 | 表示`amount`所代表之貨幣型別的ISO 4217代碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
