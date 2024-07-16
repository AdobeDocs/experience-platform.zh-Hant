---
title: 醫療保健成員詳細資料結構欄位群組
description: 瞭解Healthcare Member Details結構欄位群組。
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 3%

---

# [!UICONTROL 醫療保健會員詳細資料]結構描述欄位群組

[!UICONTROL 醫療保健會員詳細資訊]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組，可擷取已經或即將接受醫療服務或照護之人員的詳細資訊，例如聯絡資訊、初級保健醫生和計畫資訊。

![欄位群組結構](../../images/field-groups/healthcare-member-details/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL 郵寄地址]](../../data-types/postal-address.md) | 個人的帳單地址。 |
| `faxPhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 人員的傳真電話號碼。 |
| `homeAddress` | [[!UICONTROL 郵寄地址]](../../data-types/postal-address.md) | 人員的住家地址。 |
| `homePhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 個人的住家電話號碼。 |
| `mailingAddress` | [[!UICONTROL 郵寄地址]](../../data-types/postal-address.md) | 個人的郵寄地址。 |
| `memberDetails` | 物件 | 此物件包含有關個人醫療保健相關屬性和關係的詳細資訊。 如需物件結構的詳細資訊，請參閱](#memberDetails)下方的[子區段。 |
| `mobilePhone` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 個人的行動電話號碼。 |
| `person` | [[!UICONTROL 人員]](../../data-types/person.md) | 與個人的醫療保健會籍相關的個別執行者、聯絡人或擁有者。 |
| `personalEmail` | [[!UICONTROL 電子郵件地址]](../../data-types/email-address.md) | 個人的個人電子郵件地址。 |
| `shippingAddress` | [[!UICONTROL 郵寄地址]](../../data-types/postal-address.md) | 人員的送貨地址。 |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails`是一個物件，其中包含有關個人的醫療保健相關屬性和關係的詳細資訊。 `memberDetails`的結構描述如下。

![memberDetails結構](../../images/field-groups/healthcare-member-details/memberDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `emergencyContact` | 物件 | 擷取此人的下列緊急聯絡詳細資料： <ul><li>`fullName`： （字串）緊急聯絡人的全名。</li><li>`phone`： （字串）緊急聯絡人的電話號碼。</li><li>`relationshipToMember`： （字串）緊急聯絡人與個人的關係。</li></ul> |
| `medications` | 物件陣列 | 列出與個人相關的目前和過去藥物的詳細資訊。 每個陣列專案都是一個物件，可擷取以下詳細資訊： <ul><li>`refillLocation`： （[[!UICONTROL 郵寄地址]](../../data-types/postal-address.md)）藥物重新補充的位置。</li><li>`ID`： （字串）藥物識別碼。</li><li>`isCurrent`： （布林值）指出藥物為目前或過去。</li><li>`numberOfRefills`： （整數）此藥物提供者所訂明的重新填入次數。</li><li>`startDate`： (DateTime)人員開始服用藥物的日期。</li></ul> |
| `multipleBirth` | 物件 | 擷取與多胞胎相關的細節： <ul><li>`isMultipleBirth`： （布林值）指出此人是否生了多個孩子。</li><li>`multipleBirthNumber`： （整數）如果`isMultipleBirth`為True，則為出生的嬰兒數。</li></ul> |
| `plans` | 物件陣列 | 列出與個人相關的目前和過去醫療計畫的詳細資訊。 每個陣列專案都是一個物件，可擷取以下詳細資訊： <ul><li>`coverageEndDate`： (DateTime)計畫涵蓋範圍結束的日期。</li><li>`coverageStartDate`： (DateTime)計畫涵蓋範圍開始的日期。</li><li>`isActive`： （布林值）指出計畫是否有效。</li><li>`planId`： （字串）計畫識別碼。</li></ul> |
| `primaryCarePhysicians` | 物件陣列 | 列出與個人相關之基層照護醫師的詳細資訊。 每個陣列專案都是一個物件，可擷取以下詳細資訊： <ul><li>`endDate`： (DateTime)基層照護醫師終止照顧該人的日期。</li><li>`fullname`： （字串）醫師的全名。</li><li>`providerId`： （字串）醫師的唯一識別碼。</li><li>`startDate`： (DateTime)基層照護醫師開始照顧該人員的日期。</li></ul> |
| `specialists` | 物件陣列 | 列出與個人相關的醫療保健專家的詳細資訊。 每個陣列專案都是一個物件，可擷取以下詳細資訊： <ul><li>`fullname`： （字串）專員的全名。</li><li>`providerId`： （字串）專員的唯一識別碼。</li><li>`specialty`： （字串）提供者的專長（例如麻醉學、泌尿科、放射科、皮膚科等）。</li></ul> |
| `beneficiaryRelationship` | 字串 | 如果人員是受撫養人（例如本人、配偶、子女等），則為與醫療保健會員的受益人關係。 |
| `billingAccountID` | 字串 | 個人帳單帳戶的唯一識別碼。 |
| `dateAgeCollected` | 日期時間 | 收集個人年齡的日期。 |
| `deceasedDate` | 日期時間 | 如果人員已死亡，則為死亡日期。 |
| `isDeceased` | 布林值 | 指出人員是否已死亡。 |
| `isDependent` | 布林值 | 指出人員是否為受撫養人。 |
| `nationality` | 字串 | 個人與其國家之間的法律關係，使用ISO 3166-1Alpha2代碼表示。 |
| `preferredAvailability` | 字串 | 個人偏好的預約日期和時間。 |
| `primaryMemberID` | 字串 | 如果個人是受撫養人，為主要訂閱者的唯一識別碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

請參閱產業結構描述檔案，以進一步瞭解此欄位群組如何用於提供常見的[醫療保健產業使用案例](../../schema/industries/healthcare.md)。
