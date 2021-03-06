---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；付款項；資料類型；資料類型；
solution: Experience Platform
title: 付款項資料類型
topic-legacy: overview
description: 本文檔概述了「付款項體驗資料模型」(XDM)資料類型。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---

# [!UICONTROL 付款項] 資料類型

[!UICONTROL 付款] 項是標準的體驗資料模型(XDM)資料類型，它描述與訂單關聯的付款，該訂單定義付款類型、金額和關聯幣種。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `currencyCode` | 字串 | 用於訂單總計的ISO 4217貨幣代碼。 所有實例都必須符合規則表達式`^[A-Z]{3}$`。 範例如下：`USD` 和 `EUR`。 |
| `paymentAmount` | 雙倍 | 付款的價值。 |
| `paymentType` | 字串 | 此訂單的付款方式。 接受的列舉值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字串 | 此付款項的唯一事務處理標識符。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
