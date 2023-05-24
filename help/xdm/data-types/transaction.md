---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；事務；資料類型；資料類型；
title: 事務資料類型
description: 本文檔概述了事務體驗資料模型(XDM)資料類型。
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 5%

---

# [!UICONTROL 交易記錄] 資料類型

[!UICONTROL 交易記錄] 是一個標準的體驗資料模型(XDM)資料類型，它描述貨幣交易的詳細資訊。

![事務結構](../images/data-types/transaction.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL 貨幣]](./currency.md) | 描述作為事務處理一部分而交換的幣種金額。 |
| `transactionDate` | [!UICONTROL 日期時間] | 事務發生時間的時間戳。 |
| `transactionId` | [!UICONTROL 字串] | 事務的唯一標識符。 |
| `transactionType` | [!UICONTROL 字串] | 訪問者使用的事務類型。 |

{style="table-layout:auto"}
