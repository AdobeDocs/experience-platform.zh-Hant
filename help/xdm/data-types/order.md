---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；順序；資料類型；資料類型；
solution: Experience Platform
title: 訂單資料類型
description: 本文檔概述了訂單體驗資料模型(XDM)資料類型。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# [!UICONTROL 訂單] 資料類型

[!UICONTROL 訂單] 是標準的體驗資料模型(XDM)資料類型，它描述產品清單的訂單。

<img src="../images/data-types/order.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `payments` | 陣列 [[!UICONTROL 付款項]](./payment-item.md) | 此訂單的付款清單。 |
| `currencyCode` | 字串 | 用於訂單合計的ISO 4217幣種代碼。 所有實例都必須符合規則運算式 `^[A-Z]{3}$`。 範例如下：`USD` 和 `EUR`。 |
| `priceTotal` | 雙倍 | 已應用所有折扣和稅後此訂單的總價格。 |
| `purchaseID` | 字串 | 賣方為此採購或合同分配的唯一標識符。 由於這是由賣方定義的，因此不能保證ID是唯一的。 |
| `purchaseOrderNumber` | 字串 | 購買者為此採購或合同分配的唯一標識符。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
