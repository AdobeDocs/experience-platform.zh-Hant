---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；電信；訂閱；資料類型；資料類型；
solution: Experience Platform
title: 電信訂閱資料類型
description: 本檔案概述電信訂閱體驗資料模型(XDM)資料類型。
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 9%

---

# [!UICONTROL 電信訂閱] 資料類型

[!UICONTROL 電信訂閱] 是標準的Experience Data Model(XDM)資料類型，可說明特定電信訂閱類型（例如網際網路、行動裝置、媒體或固定電話）的詳細資訊。

>[!NOTE]
>
>本檔案說明資料類型。 有關相同名稱的欄位群組，請參閱 [[!UICONTROL 電信訂閱] 欄位群組參考指南](../field-groups/profile/telecom-subscription.md).
>
>如果您描述的訂閱類型與電信行業無關，請使用通用 [[!UICONTROL 訂閱] 資料類型](./subscription.md) 。

![電信訂閱結構](../images/data-types/telecom-subscription/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `devices` | 物件陣列 | 說明與計畫相關聯的設備和/或附件的清單。 請參閱 [下文](#devices) 以取得每個陣列項目之預期結構的詳細資訊。 |
| `subscriber` | [[!UICONTROL 「人」]](./person.md) | 說明訂閱的擁有者。 |
| `ID` | 字串 | 訂閱實例的唯一標識符。 |
| `billingPeriod` | 字串 | 付款之間的持續時間。 |
| `billingStartDate` | 日期 | 開單期間開始的日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `chargeMethod` | 字串 | 帳單設定方式，以向客戶收費。 |
| `contractID` | 字串 | 管轄此訂閱之合約的唯一ID。 |
| `country` | 字串 | 訂購合同和協定條款根源所在的國家。 |
| `endDate` | 日期 | 目前訂閱期限的結束日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentDueDate` | 日期 | 訂閱付款到期的日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentMethod` | 字串 | 循環付款的付款方法。 |
| `paymentStatus` | 字串 | 帳戶的付款狀況。 |
| `planName` | 字串 | 訂閱的人類看得懂的名稱。 |
| `reason` | 字串 | 成員使用訂閱的一般意圖。 |
| `renew` | 字串 | 訂購可於結束日期後繼續的協定方式。 |
| `startDate` | 日期 | 訂閱開始的日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `status` | 字串 | 訂閱的當前狀態。 |
| `subscriptionCategory` | 字串 | 此類訂閱的主要頂級分類。 |
| `subscriptionSKU` | 字串 | 訂閱的庫存保管單元(SKU)。 |
| `subscriptionSubCategory` | 字串 | 訂閱的特定子分類。 |
| `term` | 整數 | 訂閱詞語的數值。 |
| `termUnitOfTime` | 字串 | 期限期間的時間單位。 |
| `topUp` | 字串 | 說明在帳單期間如何購回訂閱的消耗性部分的協定條款。 |
| `type` | 字串 | 與訂閱涵蓋的人數有關的權利範圍。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` 是物件的陣列，每個物件都描述與訂閱相關聯的裝置或配件。

![器件陣列結構](../images/data-types/telecom-subscription/devices.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `deviceFees` | 物件 | 獲取路由器、資料機和接收器等項的任何設備費用的對象。 預期下列屬性：<ul><li>`amount`:貨幣金額，如 `currencyCode`.</li><li>`conversionDate`:進行貨幣轉換的日期。</li><li>`currencyCode`:此 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 貨幣代碼 `amount`.</li></ul> |
| `ID` | 字串 | 裝置的唯一ID。 |
| `OS` | 字串 | 設備作業系統。 |
| `deviceInsurance` | 字串 | 指出客戶是否已選擇為此裝置購買保險。 |
| `manufacturer` | 字串 | 設備製造商。 |
| `name` | 字串 | 裝置的名稱。 |
| `paymentOptions` | 字串 | 指出裝置是分期支付還是全額零售價。 |
| `serialNumber` | 字串 | 設備序列號。 |
| `status` | 字串 | 設備狀態。 |
| `storageCapacity` | 字串 | 設備儲存容量。 |
| `type` | 字串 | 裝置類型。 |

{style="table-layout:auto"}
