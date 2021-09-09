---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；交易；資料類型；資料類型；
title: 交易資料類型
description: 本檔案概述「交易體驗資料模型」(XDM)資料類型。
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

#  交易資料類型

 交易是標準的體驗資料模型(XDM)資料類型，可說明貨幣交易的詳細資訊。

![交易結構](../images/data-types/transaction.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL 貨幣]](./currency.md) | 說明交易中交換的貨幣金額。 |
| `transactionDate` | [!UICONTROL DateTime] | 發生交易的時間戳記。 |
| `transactionId` | [!UICONTROL 字串] | 交易的唯一標識符。 |
| `transactionType` | [!UICONTROL 字串] | 訪客使用的交易類型。 |

{style=&quot;table-layout:auto&quot;}
