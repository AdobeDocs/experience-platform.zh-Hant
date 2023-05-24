---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；模式；電信；訂閱；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 電信訂閱資料類型
description: 本文檔概述了電信訂閱體驗資料模型(XDM)資料類型。
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 9%

---

# [!UICONTROL 電信訂閱] 資料類型

[!UICONTROL 電信訂閱] 是標準的體驗資料模型(XDM)資料類型，它描述特定電信訂閱類型的詳細資訊，如Internet、移動、媒體或固話。

>[!NOTE]
>
>本文檔介紹資料類型。 有關同名的欄位組，請參閱 [[!UICONTROL 電信訂閱] 欄位組參考指南](../field-groups/profile/telecom-subscription.md)。
>
>如果您描述的訂閱類型與電信行業無關，請使用通用 [[!UICONTROL 訂閱] 資料類型](./subscription.md) 的雙曲餘切值。

![電信訂閱結構](../images/data-types/telecom-subscription/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `devices` | 對象陣列 | 描述與計畫關聯的設備和/或附件的清單。 查看 [下面](#devices) 的子菜單。 |
| `subscriber` | [[!UICONTROL 「人」]](./person.md) | 描述訂閱的所有者。 |
| `ID` | 字串 | 訂閱實例的唯一標識符。 |
| `billingPeriod` | 字串 | 付款之間的持續時間。 |
| `billingStartDate` | 日期 | 開單期間開始的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `chargeMethod` | 字串 | 計費設定方式以向客戶收費。 |
| `contractID` | 字串 | 管轄此訂閱的合同的唯一ID。 |
| `country` | 字串 | 訂閱合同和協定條款根據的國家/地區。 |
| `endDate` | 日期 | 當前訂閱期限結束的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentDueDate` | 日期 | 訂閱付款到期的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentMethod` | 字串 | 經常性付款的付款方法。 |
| `paymentStatus` | 字串 | 帳戶的付款狀況。 |
| `planName` | 字串 | 訂閱的可讀名稱。 |
| `reason` | 字串 | 成員用於訂閱的一般意圖。 |
| `renew` | 字串 | 認購可在結束日期後繼續的協定方式。 |
| `startDate` | 日期 | 訂閱開始的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `status` | 字串 | 訂閱的當前狀態。 |
| `subscriptionCategory` | 字串 | 此類訂閱的主頂級分類。 |
| `subscriptionSKU` | 字串 | 訂閱的庫存單位(SKU)。 |
| `subscriptionSubCategory` | 字串 | 訂閱的特定子分類。 |
| `term` | 整數 | 預訂項的數值。 |
| `termUnitOfTime` | 字串 | 期間的時間單位。 |
| `topUp` | 字串 | 描述在開單期間如何購回訂閱的消耗性部分的協定條款。 |
| `type` | 字串 | 與訂閱涵蓋的人數有關的權利範圍。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` 是對象陣列，每個對象都描述與訂閱關聯的設備或附件。

![器件陣列結構](../images/data-types/telecom-subscription/devices.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `deviceFees` | 物件 | 用於捕獲路由器、調制解調器和接收器等項的任何設備費用的對象。 需要以下屬性：<ul><li>`amount`:貨幣金額(由 `currencyCode`。</li><li>`conversionDate`:進行貨幣兌換的日期。</li><li>`currencyCode`:的 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 幣種代碼 `amount`。</li></ul> |
| `ID` | 字串 | 設備的唯一ID。 |
| `OS` | 字串 | 設備作業系統。 |
| `deviceInsurance` | 字串 | 指示客戶是否已選擇為此設備投保。 |
| `manufacturer` | 字串 | 設備製造商。 |
| `name` | 字串 | 設備的名稱。 |
| `paymentOptions` | 字串 | 指示設備是分期支付還是全額零售價。 |
| `serialNumber` | 字串 | 設備序列號。 |
| `status` | 字串 | 設備狀態。 |
| `storageCapacity` | 字串 | 設備儲存容量。 |
| `type` | 字串 | 設備類型。 |

{style="table-layout:auto"}
