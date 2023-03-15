---
title: 策略類
description: 本檔案概述Experience Data Model(XDM)中的原則類別。
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 7%

---

# [!UICONTROL 原則] 類

在Experience Data Model(XDM)中， [!UICONTROL 原則] 類別會擷取定義保險單的最小屬性集。

![](../images/classes/policy.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `assignedBeneficiary` | 陣列 [[!UICONTROL 人員]](../data-types/person.md) 資料類型 | 捕獲分配給策略的受益者（或受益者）。 |
| `benefitAmount` | [[!UICONTROL 貨幣]](../data-types/currency.md) | 根據政策條款應支付的金額。 |
| `location` | [[!UICONTROL 郵遞區號]](../data-types/postal-address.md) | 發放保單的位置。 |
| `owner` | [!UICONTROL 物件] | 捕獲策略持有者的配置檔案資訊。 |
| `owner.faxPhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 房主的傳真號碼。 |
| `owner.homeAddress` | [[!UICONTROL 郵遞區號]](../data-types/postal-address.md) | 房主的住址。 |
| `owner.homePhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 房主的家電。 |
| `owner.mobilePhone` | [[!UICONTROL 電話號碼]](../data-types/phone-number.md) | 主人的手機號碼。 |
| `owner.personalEmail` | [[!UICONTROL 電子郵件地址]](../data-types/email-address.md) | 擁有者的個人電子郵件地址。 |
| `ID` | [!UICONTROL 字串] | 保險單的標識符。 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。 |
| `endDate` | [!UICONTROL DateTime] | 保險單範圍結束（或結束）的日期。 |
| `hasAssignedBeneficiary` | [!UICONTROL 布林值] | 指示策略是否分配了受益人。 |
| `name` | [!UICONTROL 字串] | 保險單的名稱。 |
| `startDate` | [!UICONTROL DateTime] | 保險單保險開始（或開始）的日期。 |
| `type` | [!UICONTROL 字串] | 保險單的類型，例如家庭、汽車、租賃或船。 |

{style="table-layout:auto"}
