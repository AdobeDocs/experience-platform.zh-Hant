---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；順序；資料類型；資料類型；
solution: Experience Platform
title: 訂單資料類型
description: 本檔案概述Order Experience Data Model(XDM)資料類型。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# [!UICONTROL 順序] 資料類型

[!UICONTROL 順序] 是標準的Experience Data Model(XDM)資料類型，可說明產品清單的下單。

<img src="../images/data-types/order.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `payments` | 陣列 [[!UICONTROL 付款項]](./payment-item.md) | 此訂單的付款清單。 |
| `currencyCode` | 字串 | 用於訂單總計的ISO 4217貨幣代碼。 所有例項都必須符合規則運算式 `^[A-Z]{3}$`. 範例如下：`USD` 和 `EUR`。 |
| `priceTotal` | 雙倍 | 在應用所有折扣和稅後，此訂單的總價。 |
| `purchaseID` | 字串 | 賣方為此採購或合同分配的唯一標識符。 因為此ID由賣方定義，因此無法保證該ID是唯一的。 |
| `purchaseOrderNumber` | 字串 | 由購買者為此購買或合同分配的唯一標識符。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
