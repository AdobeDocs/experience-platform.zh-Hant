---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；付款項；資料類型；資料類型；
solution: Experience Platform
title: 付款項資料類型
topic-legacy: overview
description: 此文檔概述了付款項體驗資料模型(XDM)資料類型。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 5%

---

# [!UICONTROL Payment Item] 資料類型

[!UICONTROL Payment Item] 是標準的「體驗資料模型」(XDM)資料類型，它描述與訂單相關的付款，該訂單定義付款類型、金額和相關貨幣。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `currencyCode` | 字串 | 用於訂購總計的ISO 4217貨幣代碼。 所有實例都必須符合規則運算式`^[A-Z]{3}$`。 範例如下：`USD` 和 `EUR`。 |
| `paymentAmount` | 雙倍 | 付款的值。 |
| `paymentType` | 字串 | 此訂單的付款方式。 接受的列舉值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字串 | 此付款項的唯一事務處理標識符。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
