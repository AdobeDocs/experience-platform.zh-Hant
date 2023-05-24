---
title: 策略類
description: 本文檔概述了「體驗資料模型」(XDM)中的「策略」類。
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 7%

---

# [!UICONTROL 策略] 類

在經驗資料模型(XDM)中， [!UICONTROL 策略] 類捕獲定義保單的最小屬性集。

![](../images/classes/policy.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `assignedBeneficiary` | 陣列 [[!UICONTROL 人員]](../data-types/person.md) 資料類型 | 捕獲分配給政策的受益人（或受益人）。 |
| `benefitAmount` | [[!UICONTROL 貨幣]](../data-types/currency.md) | 根據政策條款應支付的金額。 |
| `location` | [[!UICONTROL 郵政地址]](../data-types/postal-address.md) | 發放保單的地點。 |
| `owner` | [!UICONTROL 物件] | 捕獲策略持有人的配置檔案資訊。 |
| `owner.faxPhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 所有者的傳真電話號碼。 |
| `owner.homeAddress` | [[!UICONTROL 郵政地址]](../data-types/postal-address.md) | 所有者的住宅地址。 |
| `owner.homePhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 所有者的家庭電話號碼。 |
| `owner.mobilePhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 所有者的手機號碼。 |
| `owner.personalEmail` | [[!UICONTROL 電子郵件地址]](../data-types/email-address.md) | 所有者的個人電子郵件地址。 |
| `ID` | [!UICONTROL 字串] | 保險單的標識符。 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `endDate` | [!UICONTROL 日期時間] | 保險單保險範圍結束（或結束）的日期。 |
| `hasAssignedBeneficiary` | [!UICONTROL 布林值] | 指示是否為策略分配了受益人。 |
| `name` | [!UICONTROL 字串] | 保險單的名稱。 |
| `startDate` | [!UICONTROL 日期時間] | 保險單覆蓋開始（或開始）的日期。 |
| `type` | [!UICONTROL 字串] | 保險單類型，如家庭、汽車、租賃人或船。 |

{style="table-layout:auto"}
