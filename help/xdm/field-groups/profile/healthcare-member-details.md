---
title: 醫療保健成員詳細資訊架構欄位組
description: 本文檔概述了醫療保健成員詳細資訊架構欄位組。
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 4%

---

# [!UICONTROL 醫療保健成員詳細資訊] 架構欄位組

[!UICONTROL 醫療保健成員詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 它捕獲已接受或將接受醫療服務或護理的人員的詳細資訊，如聯繫資訊、初級護理醫生和規劃資訊。

![欄位組結構](../../images/field-groups/healthcare-member-details/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL 郵政地址]](../../data-types/postal-address.md) | 人員的帳單地址。 |
| `faxPhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 此人的傳真電話號碼。 |
| `homeAddress` | [[!UICONTROL 郵政地址]](../../data-types/postal-address.md) | 該人的住宅地址。 |
| `homePhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 此人的家庭電話號碼。 |
| `mailingAddress` | [[!UICONTROL 郵政地址]](../../data-types/postal-address.md) | 此人的通訊地址。 |
| `memberDetails` | 物件 | 包含有關人員醫療保健相關屬性和關係的詳細資訊的對象。 查看 [下文](#memberDetails) 的子菜單。 |
| `mobilePhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 此人的手機號碼。 |
| `person` | [[!UICONTROL 「人」]](../../data-types/person.md) | 與個人醫療保健會員相關的個人參與者、聯繫人或所有者。 |
| `personalEmail` | [[!UICONTROL 電子郵件地址]](../../data-types/email-address.md) | 此人的個人電子郵件地址。 |
| `shippingAddress` | [[!UICONTROL 郵政地址]](../../data-types/postal-address.md) | 人員的送貨地址。 |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` 是一個對象，包含有關人員醫療保健相關屬性和關係的詳細資訊。 結構 `memberDetails` 如下所述。

![memberDetails結構](../../images/field-groups/healthcare-member-details/memberDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `emergencyContact` | 物件 | 捕獲此人的以下緊急聯繫詳細資訊： <ul><li>`fullName`:（字串）緊急聯繫人的全名。</li><li>`phone`:（字串）緊急聯繫人的電話號碼。</li><li>`relationshipToMember`:（字串）緊急聯繫人與人員的關係。</li></ul> |
| `medications` | 對象陣列 | 列出與人員關聯的當前和過去藥物的詳細資訊。 每個陣列項都是捕獲以下詳細資訊的對象： <ul><li>`refillLocation`:([[!UICONTROL 郵政地址]](../../data-types/postal-address.md))藥物的再填充位置。</li><li>`ID`:（字串）藥物ID。</li><li>`isCurrent`:（布爾值）指示藥物是當前藥物還是過去藥物。</li><li>`numberOfRefills`:（整數）此藥物提供者規定的補充數。</li><li>`startDate`:(DateTime)患者開始服用藥物的日期。</li></ul> |
| `multipleBirth` | 物件 | 捕獲與多胎有關的詳細資訊： <ul><li>`isMultipleBirth`:（布爾值）指示人員是否生育多胎。</li><li>`multipleBirthNumber`:（整數）在 `isMultipleBirth` 是真的。</li></ul> |
| `plans` | 對象陣列 | 列出與人員關聯的當前和過去醫療計畫的詳細資訊。 每個陣列項都是捕獲以下詳細資訊的對象： <ul><li>`coverageEndDate`:(DateTime)計畫覆蓋範圍結束的日期。</li><li>`coverageStartDate`:(DateTime)計畫覆蓋範圍開始的日期。</li><li>`isActive`:（布爾值）指示計畫是否處於活動狀態。</li><li>`planId`:（字串）計畫ID。</li></ul> |
| `primaryCarePhysicians` | 對象陣列 | 列出與該人關聯的初級保健醫生的詳細資訊。 每個陣列項都是捕獲以下詳細資訊的對象： <ul><li>`endDate`:(DateTime)初級護理醫生結束對該人的護理的日期。</li><li>`fullname`:（字串）醫生的全名。</li><li>`providerId`:（字串）醫生的唯一標識符。</li><li>`startDate`:(DateTime)初級護理醫生開始為人提供護理的日期。</li></ul> |
| `specialists` | 對象陣列 | 列出與該人員關聯的醫療保健專家的詳細資訊。 每個陣列項都是捕獲以下詳細資訊的對象： <ul><li>`fullname`:（字串）專家的全名。</li><li>`providerId`:（字串）專家的唯一標識符。</li><li>`specialty`:（弦）提供者的專業（如麻醉學、泌尿學、放射學、皮膚學等）。</li></ul> |
| `beneficiaryRelationship` | 字串 | 如果該人是受扶養人，則受益人與醫療保健成員的關係（例如，自己、配偶、子女等）。 |
| `billingAccountID` | 字串 | 人員開單帳戶的唯一標識符。 |
| `dateAgeCollected` | 日期時間 | 收集人員年齡的日期。 |
| `deceasedDate` | 日期時間 | 死者死亡的日期。 |
| `isDeceased` | 布林值 | 指示此人是否已死亡。 |
| `isDependent` | 布林值 | 指示此人是否是家屬。 |
| `nationality` | 字串 | 人員與其國家之間的法律關係，使用ISO 3166-1 Alpha-2代碼表示。 |
| `preferredAvailability` | 字串 | 人員的約會首選日期和時間可用性。 |
| `primaryMemberID` | 字串 | 主訂戶的唯一標識符（如果人員是從屬者）。 |

{style=&quot;table-layout:auto&quot;&quot;

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

有關如何使用此欄位組來提供通用服務的詳細資訊，請參閱行業架構文檔 [醫療保健行業使用案例](../../schema/industries/healthcare.md)。
