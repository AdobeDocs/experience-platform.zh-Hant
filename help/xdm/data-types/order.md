---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；順序；資料型別；資料型別；
solution: Experience Platform
title: 訂單資料型別
description: 瞭解訂單體驗資料模型(XDM)資料型別。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL 訂單]資料型別

[!UICONTROL 訂單]是標準的體驗資料模型(XDM)資料型別，可描述產品清單的訂單。

![ [!UICONTROL 訂單]資料型別的圖表。](../images/data-types/order.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| 購買 ID | `purchaseID` | 字串 | 賣家為此購買或合約所指派的唯一識別碼。 不保證ID為唯一，因為此ID是由賣家定義。 |
| 採購單號碼 | `purchaseOrderNumber` | 字串 | 購買者為此購買或合約所指派的唯一識別碼。 |
| 付款清單 | `payments` | [[!UICONTROL 付款專案]](./payment-item.md)的陣列 | 此訂單的付款清單。 付款在[!UICONTROL 付款專案]規格中詳細說明。 |
| 退款清單 | `refunds` | [[!UICONTROL 退款專案]](./refund-item.md)的陣列 | 此訂單的退款清單。 退款在[!UICONTROL 退款專案]規格中詳細說明。 |
| 傳回資訊 | `returns` | [[!UICONTROL 傳回資訊]](./return.md) | RMA （退貨授權）簽發。 在[!UICONTROL 傳回資訊]規格中會詳細說明傳回。 |
| 貨幣 | `currencyCode` | 字串 | 用於訂單總額的ISO 4217貨幣代碼。 範例包括`USD`和`EUR`。 所有執行個體都必須符合模式`^[A-Z]{3}$`。 |
| 稅捐金額 | `taxAmount` | 數字 | 買方支付作為最終付款一部分的稅捐金額。 |
| 折扣金額 | `discountAmount` | 數字 | 套用至整個訂單（而非個別產品）的一般價格與特殊價格之間的差異。 |
| 總價 | `priceTotal` | 數字 | 此訂單套用所有折扣和稅額之後的總價。 |
| 訂單類型 | `orderType` | 字串 | 已下單的訂單型別。 可能的值為`checkout`和`instant_purchase`。 |
| 上次更新日期 | `lastUpdatedDate` | 字串 | 商業系統中特定訂單記錄的上次更新時間。 格式：日期時間。 |
| 建立日期 | `createdDate` | 字串 | 在商務系統中建立新訂單的時間/日期。 格式：日期時間。 |
| 取消日期 | `cancelDate` | 字串 | 購物者啟動訂單取消的日期/時間。 格式：日期時間。 |
| 已退款的總金額 | `refundTotal` | 數字 | 此退款中針對訂單提供的總金額，結合所有退款專案及任何折扣後等。 已套用。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
