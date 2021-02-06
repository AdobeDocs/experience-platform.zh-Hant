---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；付款項；資料類型；資料類型；
solution: Experience Platform
title: 付款項資料類型
topic: overview
description: 此文檔概述了付款項體驗資料模型(XDM)資料類型。
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---


# [!UICONTROL 付款項] 資料類型

[!UICONTROL 付款] 項是標準的「體驗資料模型」(XDM)資料類型，它描述與訂單關聯的付款，該訂單定義付款類型、金額和關聯幣種。

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