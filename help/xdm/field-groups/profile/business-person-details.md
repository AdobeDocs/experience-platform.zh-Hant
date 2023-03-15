---
title: XDM業務人員詳細資訊結構欄位組
description: 本檔案提供「 XDM業務人員詳細資訊」結構欄位群組的概觀。
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---

# [!UICONTROL XDM業務人員詳細資訊] 方案欄位組

[!UICONTROL XDM業務人員詳細資訊] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 擷取企業對企業(B2B)企業情境中個人的相關資訊。

![](../../images/field-groups/business-person-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `b2b` | 物件 | 擷取有關人員的B2B特定詳細資料的物件。 |
| `b2b.accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 與人員相關的業務帳戶的複合標識符。 |
| `b2b.convertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果轉換了銷售線索，關聯聯繫人的複合標識符。 |
| `b2b.personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人員或設定檔片段的複合識別碼。 |
| `b2b.accountID` | 字串 | 此人員關聯的商業帳戶的唯一ID。 |
| `b2b.blockedCause` | 字串 | 如果該人員遭到封鎖，此屬性會提供原因。 |
| `b2b.convertedContactID` | 字串 | 如果銷售機會成功轉換，則聯繫人ID。 |
| `b2b.convertedDate` | DateTime | 成功轉換銷售機會時的轉換日期。 |
| `b2b.isBlocked` | 布林值 | 指示是否阻止該人員。 |
| `b2b.isConverted` | 布林值 | 指示是否轉換銷售線索。 |
| `b2b.isMarketingSuspended` | 布林值 | 指出是否暫停該人員的行銷。 |
| `b2b.marketingSuspendedCause` | 字串 | 如果人員的行銷已暫停，此屬性會提供原因。 |
| `b2b.personGroupID` | 字串 | 人員的群組識別碼。 |
| `b2b.personScore` | 雙倍 | 由CRM系統為人員產生的分數。 |
| `b2b.personSource` | 字串 | 收到該人資訊的來源。 |
| `b2b.personStatus` | 字串 | 人員的當前行銷或銷售狀態。 |
| `b2b.personType` | 字串 | B2B人員的類型。 |
| `extSourceSystemAudit` | [外部源系統審核屬性](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部源系統，則此對象捕獲該系統的審計屬性。 |
| `extendedWorkDetails` | 物件 | 擷取該人員的其他與工作相關的詳細資訊。 |
| `extendedWorkDetails.assistantDetails` | 物件 | 擷取與人員助理相關的下列屬性： <ul><li>`name`:([人員名稱](../../data-types/person-name.md))助理的全名。</li><li>`phone`:([電話號碼](../../data-types/phone-number.md))助理的電話號碼。</li></ul> |
| `extendedWorkDetails.departments` | 字串陣列 | 人員工作所在的部門名稱清單。 |
| `extendedWorkDetails.jobTitle` | 字串 | 人的職稱。 |
| `extendedWorkDetails.photoUrl` | 字串 | 人員像片的URL。 |
| `extendedWorkDetails.reportsToID` | 字串 | 人員報表管理員的識別碼。 |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 此人的傳真號碼。 |
| `homeAddress` | [郵遞區號](../../data-types/postal-address.md) | 此人的住址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 此人的家電。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 此人的手機號碼。 |
| `otherAddress` | [郵遞區號](../../data-types/postal-address.md) | 人員的替代地址。 |
| `otherPhone` | [電話號碼](../../data-types/phone-number.md) | 人員的備用電話號碼。 |
| `person` | [「人」](../../data-types/person.md) | 個別演員、聯絡人或擁有者。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 該人的個人電子郵件地址。 |
| `workAddress` | [郵遞區號](../../data-types/postal-address.md) | 該人的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 此人的工作電話號碼。 |
| `identityMap` | 地圖 | 一個地圖欄位，包含人員的一組命名空間身分識別。 系統會在擷取身分資料時自動更新此欄位。 為了正確利用此欄位 [即時客戶個人檔案](../../../profile/home.md)，請勿嘗試手動更新資料操作中欄位的內容。<br /><br />請參閱 [綱要構成基本知識](../../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `isDeleted` | 布林值 | 指示此人員是否已在Marketo Engage中刪除。<br><br>使用 [Marketo來源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md),Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄仍可能會保留在Data Lake。 設定 `isDeleted` to `true`，您可以使用欄位來篩選已在查詢資料湖時從來源刪除的記錄。 |
| `organizations` | 字串陣列 | 人員工作所在的組織名稱清單。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
