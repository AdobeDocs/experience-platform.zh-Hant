---
title: 策略類
description: This document provides an overview of the Policy class in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 7%

---

# [!UICONTROL 策略] 類

In Experience Data Model (XDM), the [!UICONTROL Policy] class captures the minimum set of properties that define an insurance policy.

![](../images/classes/policy.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `assignedBeneficiary` | Array of [[!UICONTROL Person]](../data-types/person.md) data types | 捕獲分配給政策的受益人（或受益人）。 |
| `benefitAmount` | [[!UICONTROL 貨幣]](../data-types/currency.md) | 根據政策條款應支付的金額。 |
| `location` | [[!UICONTROL 郵政地址]](../data-types/postal-address.md) | 發放保單的地點。 |
| `owner` | [!UICONTROL 物件] | 捕獲策略持有人的配置檔案資訊。 |
| `owner.faxPhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 所有者的傳真電話號碼。 |
| `owner.homeAddress` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | The owner&#39;s home address. |
| `owner.homePhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | The owner&#39;s home phone number. |
| `owner.mobilePhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 所有者的手機號碼。 |
| `owner.personalEmail` | [[!UICONTROL 電子郵件地址]](../data-types/email-address.md) | 所有者的個人電子郵件地址。 |
| `ID` | [!UICONTROL 字串] | 保險單的標識符。 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `endDate` | [!UICONTROL 日期時間] | 保險單保險範圍結束（或結束）的日期。 |
| `hasAssignedBeneficiary` | [!UICONTROL 布爾型] | 指示是否為策略分配了受益人。 |
| `name` | [!UICONTROL 字串] | 保險單的名稱。 |
| `startDate` | [!UICONTROL 日期時間] | The date when the insurance policy coverage starts (or started). |
| `type` | [!UICONTROL 字串] | 保險單類型，如家庭、汽車、租賃人或船。 |

{style=&quot;table-layout:auto&quot;}
