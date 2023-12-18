---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；付款專案；資料型別；資料型別；
solution: Experience Platform
title: 付款專案資料型別
description: 瞭解付款專案體驗資料模型(XDM)資料型別。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---

# [!UICONTROL 付款專案] 資料型別

[!UICONTROL 付款專案] 是標準的體驗資料模型(XDM)資料型別，可描述與訂單相關聯的付款，並定義付款型別、金額和相關聯的貨幣。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `currencyCode` | 字串 | 用於訂單總額的ISO 4217貨幣代碼。 所有執行個體都必須符合規則運算式 `^[A-Z]{3}$`. 範例如下：`USD` 和 `EUR`。 |
| `paymentAmount` | 雙倍 | 付款的值。 |
| `paymentType` | 字串 | 此訂單的付款方式。 接受的列舉值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字串 | 此付款專案的唯一交易識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
