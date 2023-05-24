---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；支付項；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 付款項資料類型
description: 此文檔提供付款項體驗資料模型(XDM)資料類型的概覽。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---

# [!UICONTROL 付款項] 資料類型

[!UICONTROL 付款項] 是標準體驗資料模型(XDM)資料類型，它描述與訂單關聯的付款，訂單定義付款類型、金額和關聯幣種。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `currencyCode` | 字串 | 用於訂單合計的ISO 4217幣種代碼。 所有實例都必須符合規則運算式 `^[A-Z]{3}$`。 範例如下：`USD` 和 `EUR`。 |
| `paymentAmount` | 雙倍 | 付款的值。 |
| `paymentType` | 字串 | 此訂單的付款方式。 接受的枚舉值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字串 | 此付款項的唯一交易記錄標識符。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
