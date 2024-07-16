---
title: 送貨資料型別
description: 瞭解配送體驗資料模型(XDM)資料型別。
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 18%

---

# [!UICONTROL 送貨]資料型別

[!UICONTROL 出貨]是標準的體驗資料模型(XDM)資料型別，提供與一或多個產品出貨相關的詳細資訊。 其中包括後勤的詳細資訊以及訂購料號遞送的細節。


![ [!UICONTROL Shipping]資料型別的圖表。](../images/data-types/shipping.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL 送貨方法] | `shippingMethod` | 字串 | 客戶選擇的配送方式。 |
| [!UICONTROL 運費金額] | `shippingAmount` | 數字 | 客戶必須為配送支付的金額。 |
| [!UICONTROL 貨幣代碼] | `currencyCode` | 字串 | 用於為產品定價的 ISO 4217 字母貨幣代碼。 |
| [!UICONTROL 送貨目的地] | `shippingDestination` | 字串 | 使用者指定的送貨目的地（例如，住家、商店等）。 |
| [!UICONTROL 出貨日期] | `shipDate` | 字串 | 訂單中一或多個料號出貨的日期。 |
| [!UICONTROL 送貨地址] | `address` | [[!UICONTROL 位址]](./address.md) | 送貨地址。 |
| [!UICONTROL 追蹤號碼] | `trackingNumber` | 數字 | 由貨運業者提供的追蹤編號。 |
| [!UICONTROL 追蹤URL] | `trackingURL` | 字串 | 追蹤訂單專案出貨狀態的URL。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
