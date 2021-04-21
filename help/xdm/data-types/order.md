---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；順序；資料類型；資料類型；
solution: Experience Platform
title: 訂單資料類型
topic-legacy: overview
description: 本檔案提供訂單體驗資料模型(XDM)資料類型的概觀。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---

# [!UICONTROL Order] 資料類型

[!UICONTROL Order] 是標準的「體驗資料模型」(XDM)資料類型，可說明產品清單的下單。

<img src="../images/data-types/order.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `payments` | [[!UICONTROL Payment Items]](./payment-item.md)陣列 | 此訂單的付款清單。 |
| `currencyCode` | 字串 | 用於訂購總計的ISO 4217貨幣代碼。 所有實例都必須符合規則運算式`^[A-Z]{3}$`。 範例如下：`USD` 和 `EUR`。 |
| `priceTotal` | 雙倍 | 在套用所有折扣和稅後，此訂單的總價格。 |
| `purchaseID` | 字串 | 賣方為此購買或合約指派的唯一識別碼。 由於此為賣方所定義，因此無法保證ID是唯一的。 |
| `purchaseOrderNumber` | 字串 | 購買者為此購買或合約指派的唯一識別碼。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
