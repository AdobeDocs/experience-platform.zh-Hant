---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；訂閱；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 訂閱資料類型
description: 本文檔提供訂閱體驗資料模型(XDM)資料類型的概述。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 9%

---

# [!UICONTROL 訂閱] 資料類型

[!UICONTROL 訂閱] 是標準體驗資料模型(XDM)資料類型，它描述軟體、服務或商品的許可權利，這些權利根據時間或使用情況而使用。

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [[!UICONTROL 裝置]](./device.md) | 描述有關連結到訂閱的設備的詳細資訊。 |
| `environment` | [[!UICONTROL 環境]](./environment.md) | 包含有關事件觀察所發生的周圍情況的資訊，特別是詳細描述臨時資訊，如網路或軟體版本。 |
| `subscriber` | [[!UICONTROL 「人」]](./person.md) | 描述個人。 這也可以代表擔任各種角色的人員，如客戶、聯繫人或所有者。 |
| `SKU` | 字串 | 庫存單位(SKU)，產品的唯一標識符。 |
| `billingPeriod` | 字串 | 付款之間的持續時間。 |
| `billingStartDate` | 日期 | 第一個票據到期的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `category` | 字串 | 此類訂閱的主頂級分類。 |
| `chargeMethod` | 字串 | 計費設定方式以向客戶收費。 |
| `contractID` | 字串 | 管轄此訂閱的合同的唯一ID。 |
| `country` | 字串 | 訂閱合同和協定條款根據的國家/地區。 |
| `endDate` | 日期 | 當前訂閱期限結束的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentMethod` | 字串 | 經常性付款的付款方法。 |
| `paymentStatus` | 字串 | 帳戶的付款狀況。 |
| `planName` | 字串 | 訂閱的可讀名稱。 |
| `reason` | 字串 | 成員用於訂閱的一般意圖。 |
| `renew` | 字串 | 認購可在結束日期後繼續的協定方式。 |
| `revision` | 字串 | 同名和類別層次結構的訂閱之間的標識。 |
| `startDate` | 日期 | 訂閱開始的日期。 日期格式（無時間）應跟在 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `status` | 字串 | 訂閱的當前狀態。 |
| `subCategory` | 字串 | 訂閱的特定子分類。 |
| `term` | 整數 | 預訂項的數值。 |
| `termUnitOfTime` | 字串 | 期間的時間單位。 |
| `topUp` | 字串 | 描述在開單期間如何購回訂閱的消耗性部分的協定條款。 |
| `type` | 字串 | 與訂閱涵蓋的人數有關的權利範圍。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
