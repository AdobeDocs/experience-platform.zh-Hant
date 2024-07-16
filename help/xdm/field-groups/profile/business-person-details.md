---
title: XDM商業人士詳細資料結構欄位群組
description: 瞭解XDM商業人士詳細資料結構欄位群組。
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 5%

---

# [!UICONTROL XDM商業人士詳細資料]結構描述欄位群組

[!UICONTROL XDM商業人士詳細資料]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組，可擷取企業對企業內容(B2B)中個別個人的相關資訊。

![](../../images/field-groups/business-person-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `b2b` | 物件 | 擷取個人相關B2B特定詳細資料的物件。 |
| `b2b.accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 與個人相關之商業帳戶的複合識別碼。 |
| `b2b.convertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 如果潛在客戶已轉換，則為關聯聯絡人的複合識別碼。 |
| `b2b.personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 人員或設定檔片段的複合識別碼。 |
| `b2b.accountID` | 字串 | 此人員相關聯之商業帳戶的唯一ID。 |
| `b2b.blockedCause` | 字串 | 如果人員遭到封鎖，此屬性會提供原因。 |
| `b2b.convertedContactID` | 字串 | 聯絡人ID （若已成功轉換潛在客戶）。 |
| `b2b.convertedDate` | 日期時間 | 轉換日期（若已成功轉換潛在客戶）。 |
| `b2b.isBlocked` | 布林值 | 指出此人是否遭到封鎖。 |
| `b2b.isConverted` | 布林值 | 表示是否轉換潛在客戶。 |
| `b2b.isMarketingSuspended` | 布林值 | 表示該人員的行銷活動是否暫停。 |
| `b2b.marketingSuspendedCause` | 字串 | 如果針對該人員暫停行銷，此屬性會提供原因。 |
| `b2b.personGroupID` | 字串 | 適用於個人的群組識別碼。 |
| `b2b.personScore` | 雙精度 | CRM系統產生的個人分數。 |
| `b2b.personSource` | 字串 | 接收人員資訊的來源。 |
| `b2b.personStatus` | 字串 | 個人的目前行銷或銷售狀態。 |
| `b2b.personType` | 字串 | B2B個人的型別。 |
| `extSourceSystemAudit` | [外部Source系統稽核屬性](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `extendedWorkDetails` | 物件 | 擷取有關個人的其他工作相關細節。 |
| `extendedWorkDetails.assistantDetails` | 物件 | 擷取與個人助理相關的下列屬性： <ul><li>`name`： （[個人姓名](../../data-types/person-name.md)）助理的全名。</li><li>`phone`： （[電話號碼](../../data-types/phone-number.md)）助理的電話號碼。</li></ul> |
| `extendedWorkDetails.departments` | 字串陣列 | 個人工作的部門名稱清單。 |
| `extendedWorkDetails.jobTitle` | 字串 | 個人的職稱。 |
| `extendedWorkDetails.photoUrl` | 字串 | 個人像片的URL。 |
| `extendedWorkDetails.reportsToID` | 字串 | 個人報表管理員的識別碼。 |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 人員的傳真電話號碼。 |
| `homeAddress` | [郵寄地址](../../data-types/postal-address.md) | 人員的住家地址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 個人的住家電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 個人的行動電話號碼。 |
| `otherAddress` | [郵寄地址](../../data-types/postal-address.md) | 人員的替代地址。 |
| `otherPhone` | [電話號碼](../../data-types/phone-number.md) | 個人的替代電話號碼。 |
| `person` | [人員](../../data-types/person.md) | 個別執行者、聯絡人或擁有者。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 個人的個人電子郵件地址。 |
| `workAddress` | [郵寄地址](../../data-types/postal-address.md) | 人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 個人的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 個人的工作電話號碼。 |
| `identityMap` | 地圖 | 包含人員的一組名稱空間身分的對映欄位。 系統會在擷取身分資料時自動更新此欄位。 為了正確使用此欄位進行[即時客戶設定檔](../../../profile/home.md)，請勿嘗試在您的資料作業中手動更新欄位內容。<br /><br />如需有關其使用案例的詳細資訊，請參閱[結構描述組合基本概念](../../schema/composition.md#identityMap)中身分對應一節。 |
| `isDeleted` | 布林值 | 指出此人是否已在Marketo Engage中刪除。<br><br>使用[Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)時，在Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過將`isDeleted`設定為`true`，您可以在查詢資料湖時使用該欄位來篩選出已從您的來源中刪除的記錄。 |
| `organizations` | 字串陣列 | 個人工作的組織名稱清單。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
