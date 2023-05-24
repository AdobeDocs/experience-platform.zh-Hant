---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；設備；資料類型；資料類型；貨幣；
solution: Experience Platform
title: 貨幣資料類型
description: 此文檔概述了貨幣XDM資料類型。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 3%

---

# [!UICONTROL 貨幣] 資料類型

[!UICONTROL 貨幣] 是一個標準XDM資料類型，它描述了幣種金額，包括幣種類型和折換日期。

![](../images/data-types/currency.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `amount` | 雙倍 | 由 `currencyCode`。 |
| `conversionDate` | 日期時間 | 進行貨幣兌換的時間戳。 |
| `currencyCode` | 字串 | ISO 4217代碼，它指示 `amount` 表示。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
