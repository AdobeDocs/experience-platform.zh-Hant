---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；交易；資料類型；資料類型；
title: 交易資料類型
description: 本檔案概述「交易體驗資料模型」(XDM)資料類型。
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 5%

---

# [!UICONTROL 交易] 資料類型

[!UICONTROL 交易] 是標準的Experience Data Model(XDM)資料類型，可說明貨幣交易的詳細資訊。

![交易結構](../images/data-types/transaction.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL 貨幣]](./currency.md) | 說明交易中交換的貨幣金額。 |
| `transactionDate` | [!UICONTROL DateTime] | 發生交易的時間戳記。 |
| `transactionId` | [!UICONTROL 字串] | 交易的唯一標識符。 |
| `transactionType` | [!UICONTROL 字串] | 訪客使用的交易類型。 |

{style="table-layout:auto"}
