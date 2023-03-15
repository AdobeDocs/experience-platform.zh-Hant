---
title: 醫療保健成員詳細資訊架構欄位組
description: 本文檔提供醫療保健成員詳細資訊架構欄位組的概述。
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 3%

---

# [!UICONTROL 醫療保健會員詳細資訊] 方案欄位組

[!UICONTROL 醫療保健會員詳細資訊] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 擷取已接受或將接受醫療服務或護理的人員的詳細資訊，例如聯絡資訊、初級護理醫生和計畫資訊。

![欄位群組結構](../../images/field-groups/healthcare-member-details/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL 郵遞區號]](../../data-types/postal-address.md) | 此人的帳單地址。 |
| `faxPhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 此人的傳真號碼。 |
| `homeAddress` | [[!UICONTROL 郵遞區號]](../../data-types/postal-address.md) | 此人的住址。 |
| `homePhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 此人的家電。 |
| `mailingAddress` | [[!UICONTROL 郵遞區號]](../../data-types/postal-address.md) | 此人的郵寄地址。 |
| `memberDetails` | 物件 | 一個對象，包含有關人員醫療保健相關屬性和關係的詳細資訊。 請參閱 [下文](#memberDetails) 以取得物件結構的詳細資訊。 |
| `mobilePhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 此人的手機號碼。 |
| `person` | [[!UICONTROL 「人」]](../../data-types/person.md) | 與個人醫療會籍相關的個人參與者、連絡人或擁有者。 |
| `personalEmail` | [[!UICONTROL 電子郵件地址]](../../data-types/email-address.md) | 該人的個人電子郵件地址。 |
| `shippingAddress` | [[!UICONTROL 郵遞區號]](../../data-types/postal-address.md) | 該人的裝運地址。 |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` 是一個對象，包含有關人員醫療保健相關屬性和關係的詳細資訊。 的結構 `memberDetails` 如下所述。

![memberDetails結構](../../images/field-groups/healthcare-member-details/memberDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `emergencyContact` | 物件 | 捕獲該人員的以下緊急聯繫詳細資訊： <ul><li>`fullName`:（字串）緊急聯絡人的全名。</li><li>`phone`:（字串）緊急聯絡人的電話號碼。</li><li>`relationshipToMember`:（字串）緊急聯絡人與該人的關係。</li></ul> |
| `medications` | 物件陣列 | 列出與此人相關的當前和過去藥物的詳細資訊。 每個陣列項目都是一個物件，可擷取下列詳細資料： <ul><li>`refillLocation`:([[!UICONTROL 郵遞區號]](../../data-types/postal-address.md))藥的再灌區。</li><li>`ID`:（字串）藥物識別碼。</li><li>`isCurrent`:（布林值）指示藥物是當前還是過去。</li><li>`numberOfRefills`:（整數）由此藥物提供者規定的補滿次數。</li><li>`startDate`:(DateTime)人開始服藥的日期。</li></ul> |
| `multipleBirth` | 物件 | 捕獲與多胎有關的詳細資訊： <ul><li>`isMultipleBirth`:（布林值）指出該人是否生育多胎。</li><li>`multipleBirthNumber`:（整數）如果 `isMultipleBirth` 為true。</li></ul> |
| `plans` | 物件陣列 | 列出與該人員相關聯的當前和過去醫療計畫的詳細資訊。 每個陣列項目都是一個物件，可擷取下列詳細資料： <ul><li>`coverageEndDate`:(DateTime)計畫覆蓋終止的日期。</li><li>`coverageStartDate`:(DateTime)計畫範圍開始的日期。</li><li>`isActive`:（布林值）指示計畫是否處於活動狀態。</li><li>`planId`:（字串）計畫ID。</li></ul> |
| `primaryCarePhysicians` | 物件陣列 | 列出與該人相關聯的初級保健醫師的詳細資訊。 每個陣列項目都是一個物件，可擷取下列詳細資料： <ul><li>`endDate`:(DateTime)初級護理醫生終止對該人的護理的日期。</li><li>`fullname`:（字串）醫生的全名。</li><li>`providerId`:（字串）醫師的唯一識別碼。</li><li>`startDate`:(DateTime)初級護理醫生開始照料該人的日期。</li></ul> |
| `specialists` | 物件陣列 | 列出與該人員相關聯的醫療保健專家的詳細資訊。 每個陣列項目都是一個物件，可擷取下列詳細資料： <ul><li>`fullname`:（字串）專員的全名。</li><li>`providerId`:（字串）專家的唯一識別碼。</li><li>`specialty`:（字串）提供者的專業（例如麻醉學、泌尿科、放射科、皮膚科等）。</li></ul> |
| `beneficiaryRelationship` | 字串 | 如果該人是受扶養人，則受益人與醫療保健成員的關係（例如，自己、配偶、子女等）。 |
| `billingAccountID` | 字串 | 人員帳單帳戶的唯一識別碼。 |
| `dateAgeCollected` | DateTime | 收集人員年齡的日期。 |
| `deceasedDate` | DateTime | 死者死亡的日期。 |
| `isDeceased` | 布林值 | 指出該人是否已死亡。 |
| `isDependent` | 布林值 | 指示人員是否為從屬人員。 |
| `nationality` | 字串 | 使用ISO 3166-1 Alpha-2代碼表示的個人與其國家之間的法律關係。 |
| `preferredAvailability` | 字串 | 該人的首選日期和約會時間。 |
| `primaryMemberID` | 字串 | 主訂閱者的唯一標識符（如果人員是相依用戶）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

如需如何使用此欄位群組來提供常見項目的詳細資訊，請參閱產業結構檔案 [醫療保健行業使用案例](../../schema/industries/healthcare.md).
