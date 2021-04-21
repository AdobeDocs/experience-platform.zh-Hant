---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas;subscription;datatype；資料類型；
solution: Experience Platform
title: 訂閱資料類型
topic-legacy: overview
description: 本檔案提供訂閱體驗資料模型(XDM)資料類型的概觀。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 9%

---

# [!UICONTROL Subscription] 資料類型

[!UICONTROL Subscription] 是標準的Experience Data Model(XDM)資料類型，可說明軟體、服務或商品的授權權利（根據時間或使用情形而使用）。

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | 說明連結至訂閱之裝置的詳細資訊。 |
| `environment` | [[!UICONTROL Environment]](./environment.md) | 包含事件觀察發生的周圍情況的相關資訊，特別詳細說明網路或軟體版本等暫存性資訊。 |
| `subscriber` | [[!UICONTROL Person]](./person.md) | 說明個人。 這也可以代表擔任不同角色的人員，例如客戶、連絡人或擁有者。 |
| `SKU` | 字串 | 庫存保留單位(SKU)，產品的唯一識別碼。 |
| `billingPeriod` | 字串 | 付款之間的期間。 |
| `billingStartDate` | Date | 第一張票據到期的日期。 日期格式（無時間）應遵循[RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6)標準。 |
| `category` | 字串 | 此類訂閱的主要頂層分類。 |
| `chargeMethod` | 字串 | 對客戶收費的計費方式。 |
| `contractID` | 字串 | 控制此訂閱之合約的唯一ID。 |
| `country` | 字串 | 訂閱合約和合約條款根據的國家。 |
| `endDate` | 日期 | 目前訂閱期限的結束日期。 日期格式（無時間）應遵循[RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6)標準。 |
| `paymentMethod` | 字串 | 循環付款的付款方法。 |
| `paymentStatus` | 字串 | 帳戶的付款狀況。 |
| `planName` | 字串 | 訂閱的可人讀名稱。 |
| `reason` | 字串 | 會員使用訂閱的一般意圖。 |
| `renew` | 字串 | 訂閱可在結束日期後繼續的協定方式。 |
| `revision` | 字串 | 同名和類別階層的訂閱之間的識別碼。 |
| `startDate` | 日期 | 訂閱開始的日期。 日期格式（無時間）應遵循[RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6)標準。 |
| `status` | 字串 | 訂閱的目前狀態。 |
| `subCategory` | 字串 | 訂閱的特定子分類。 |
| `term` | 整數 | 訂閱期限的數值。 |
| `termUnitOfTime` | 字串 | 期限期間的單位。 |
| `topUp` | 字串 | 說明在帳單期間如何購回訂閱消費性部分的協定條款。 |
| `type` | 字串 | 與訂閱涵蓋的人數相關的權益範圍。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
