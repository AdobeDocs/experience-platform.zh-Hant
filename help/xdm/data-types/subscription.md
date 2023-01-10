---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；訂閱；資料類型；資料類型；
solution: Experience Platform
title: 訂閱資料類型
description: 本檔案概述訂閱體驗資料模型(XDM)資料類型。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---

# [!UICONTROL 訂閱] 資料類型

[!UICONTROL 訂閱] 是標準的Experience Data Model(XDM)資料類型，可說明根據時間或使用情形而使用之軟體、服務或商品的授權使用情形。

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [[!UICONTROL 裝置]](./device.md) | 說明連結至訂閱之裝置的詳細資訊。 |
| `environment` | [[!UICONTROL 環境]](./environment.md) | 包含有關事件觀察發生的周圍情況的資訊，具體詳述諸如網路或軟體版本之類的臨時資訊。 |
| `subscriber` | [[!UICONTROL 「人」]](./person.md) | 說明個人。 這也可以代表擔任各種角色的人員，例如客戶、連絡人或擁有者。 |
| `SKU` | 字串 | 保存單位(SKU)，是產品的唯一識別碼。 |
| `billingPeriod` | 字串 | 付款之間的持續時間。 |
| `billingStartDate` | 日期 | 第一張賬單到期的日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `category` | 字串 | 此類訂閱的主要頂級分類。 |
| `chargeMethod` | 字串 | 帳單設定方式，以向客戶收費。 |
| `contractID` | 字串 | 管轄此訂閱之合約的唯一ID。 |
| `country` | 字串 | 訂購合同和協定條款根源所在的國家。 |
| `endDate` | 日期 | 目前訂閱期限的結束日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentMethod` | 字串 | 循環付款的付款方法。 |
| `paymentStatus` | 字串 | 帳戶的付款狀況。 |
| `planName` | 字串 | 訂閱的人類看得懂的名稱。 |
| `reason` | 字串 | 成員使用訂閱的一般意圖。 |
| `renew` | 字串 | 訂購可於結束日期後繼續的協定方式。 |
| `revision` | 字串 | 同名訂閱與類別階層之間的識別。 |
| `startDate` | 日期 | 訂閱開始的日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `status` | 字串 | 訂閱的當前狀態。 |
| `subCategory` | 字串 | 訂閱的特定子分類。 |
| `term` | 整數 | 訂閱詞語的數值。 |
| `termUnitOfTime` | 字串 | 期限期間的時間單位。 |
| `topUp` | 字串 | 說明在帳單期間如何購回訂閱的消耗性部分的協定條款。 |
| `type` | 字串 | 與訂閱涵蓋的人數有關的權利範圍。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
