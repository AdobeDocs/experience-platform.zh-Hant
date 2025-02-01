---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；欄位；綱要；綱要；訂閱；資料型別；資料型別；
solution: Experience Platform
title: 訂閱資料型別
description: 瞭解訂閱體驗資料模型(XDM)資料型別。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 28%

---

# [!UICONTROL 訂閱]資料型別

[!UICONTROL 訂閱]是標準的Experience Data Model (XDM)資料型別，說明軟體、服務或商品的授權權益，這些軟體、服務或商品的使用是根據時間或使用狀況。

![](../images/data-types/subscription-data-type.png){width=500}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [[!UICONTROL 裝置]](./device.md) | 說明連結至訂閱之裝置的詳細資訊。 |
| `environment` | [[!UICONTROL 環境]](./environment.md) | 包含有關發生事件觀察的周圍情況的資訊，尤其會詳細說明網路或軟體版本之類的臨時性資訊。 |
| `subscriber` | [[!UICONTROL 人員]](./person.md) | 說明個人。 這也可以代表擔任各種角色的人員，例如客戶、聯絡人或擁有者。 |
| `SKU` | 字串 | 庫存單位(SKU)，產品的唯一識別碼。 |
| `billingPeriod` | 字串 | 寄送帳單之間的持續時間。 |
| `billingStartDate` | 日期 | 第一筆帳單到期日。 日期格式（沒有時間）應遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節標準。 |
| `category` | 字串 | 此類訂閱的主要頂層分類。 |
| `chargeMethod` | 字串 | 設定開立帳單的方式以向客戶收費。 |
| `contractID` | 字串 | 適用於規範此訂閱之合約的唯一ID。 |
| `country` | 字串 | 訂閱合約和協議條款根源的國家/地區。 |
| `endDate` | 日期 | 目前訂閱期結束的日期。 日期格式（沒有時間）應遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節標準。 |
| `paymentMethod` | 字串 | 定期付款的付款方式。 |
| `paymentStatus` | 字串 | 帳戶的付款狀態。 |
| `planName` | 字串 | 適用於此訂閱的可讀取名稱。 |
| `reason` | 字串 | 會員對於訂閱的使用具備的一般性意圖。 |
| `renew` | 字串 | 訂閱在結束日期之後可能持續的議定方式。 |
| `revision` | 字串 | 相同名稱和類別階層的訂閱之間的識別方式。 |
| `startDate` | 日期 | 訂閱開始日期。 日期格式（沒有時間）應遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節標準。 |
| `status` | 字串 | 目前的訂閱狀態。 |
| `subCategory` | 字串 | 訂閱的特定子分類。 |
| `term` | 整數 | 訂閱期限的數值。 |
| `termUnitOfTime` | 字串 | 適用於此期限期間的時間單位。 |
| `topUp` | 字串 | 說明在計費期間如何重新購買訂閱之可消耗專案的議定條款。 |
| `type` | 字串 | 與訂閱所涵蓋人數相關的權益範圍。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
