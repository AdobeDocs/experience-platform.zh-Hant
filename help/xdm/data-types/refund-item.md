---
title: 退款專案資料型別
description: 瞭解退款專案體驗資料模型(XDM)資料型別。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL 退款專案] 資料型別

[!UICONTROL 退款專案] 是標準的體驗資料模型(XDM)資料型別，可描述擷取與訂單相關退款的相關資訊。

![「退款專案」資料型態的圖表。](../images/data-types/refund-item.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL 交易 ID] | `transactionID` | 字串 | 此退款專案的唯一交易識別碼。 |
| [!UICONTROL 退款金額] | `refundAmount` | 數字 | 退款的值。 |
| [!UICONTROL 退款原因] | `refundReason` | 字串 | 發出退款的原因。 |
| [!UICONTROL 退款付款型別] | `refundPaymentType` | 字串 | 此訂單的付款方式。 允許自訂值。 |
| [!UICONTROL 貨幣代碼] | `currencyCode` | 字串 | 用於此退款專案的ISO 4217貨幣代碼。 例如：&#39;USD&#39;、&#39;EUR&#39;。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
