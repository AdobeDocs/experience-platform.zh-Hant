---
title: XDM業務人員詳細資訊架構欄位組
description: 本文檔提供XDM業務人員詳細資訊架構欄位組的概覽。
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---

# [!UICONTROL XDM業務人員詳細資訊] 架構欄位組

[!UICONTROL XDM業務人員詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 在企業對企業(B2B)企業中捕獲有關個人的資訊。

![](../../images/field-groups/business-person-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `b2b` | 物件 | 捕獲有關人員的B2B特定詳細資訊的對象。 |
| `b2b.accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 與人員相關的業務帳戶的組合標識符。 |
| `b2b.convertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果已轉換潛在顧客，則關聯聯繫人的組合標識符。 |
| `b2b.personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人員或配置檔案片段的複合標識符。 |
| `b2b.accountID` | 字串 | 此人關聯的業務帳戶的唯一ID。 |
| `b2b.blockedCause` | 字串 | 如果阻止了該人員，則此屬性將提供原因。 |
| `b2b.convertedContactID` | 字串 | 成功轉換潛在顧客時的聯繫人ID。 |
| `b2b.convertedDate` | 日期時間 | 成功轉換銷售線索時的轉換日期。 |
| `b2b.isBlocked` | 布林值 | 指示是否阻止該人。 |
| `b2b.isConverted` | 布林值 | 指示是否轉換銷售線索。 |
| `b2b.isMarketingSuspended` | 布林值 | 指示是否暫停人員的市場營銷。 |
| `b2b.marketingSuspendedCause` | 字串 | 如果為人員暫停市場營銷，則此屬性將提供原因。 |
| `b2b.personGroupID` | 字串 | 人員的組標識符。 |
| `b2b.personScore` | 雙倍 | 由CRM系統為人員生成的分數。 |
| `b2b.personSource` | 字串 | 從中收到此人資訊的來源。 |
| `b2b.personStatus` | 字串 | 人員的當前市場營銷或銷售狀態。 |
| `b2b.personType` | 字串 | B2B人的類型。 |
| `extSourceSystemAudit` | [外部源系統審核屬性](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部源系統，則此對象將捕獲該系統的審計屬性。 |
| `extendedWorkDetails` | 物件 | 捕獲有關人員的其他與工作相關的詳細資訊。 |
| `extendedWorkDetails.assistantDetails` | 物件 | 捕獲與人員助理相關的以下屬性： <ul><li>`name`:([人員姓名](../../data-types/person-name.md))助理的全名。</li><li>`phone`:([電話號碼](../../data-types/phone-number.md))助理的電話號碼。</li></ul> |
| `extendedWorkDetails.departments` | 字串陣列 | 人員工作的部門名稱清單。 |
| `extendedWorkDetails.jobTitle` | 字串 | 人員的職務。 |
| `extendedWorkDetails.photoUrl` | 字串 | 人員照片的URL。 |
| `extendedWorkDetails.reportsToID` | 字串 | 人員報告經理的標識符。 |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 此人的傳真電話號碼。 |
| `homeAddress` | [郵政地址](../../data-types/postal-address.md) | 該人的住宅地址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 此人的家庭電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 此人的手機號碼。 |
| `otherAddress` | [郵政地址](../../data-types/postal-address.md) | 人員的備用地址。 |
| `otherPhone` | [電話號碼](../../data-types/phone-number.md) | 人員的備用電話號碼。 |
| `person` | [「人」](../../data-types/person.md) | 個人演員、聯繫人或所有者。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 此人的個人電子郵件地址。 |
| `workAddress` | [郵政地址](../../data-types/postal-address.md) | 人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 人員的工作電話號碼。 |
| `identityMap` | 地圖 | 包含人員的一組命名空間標識的映射欄位。 當接收身份資料時，系統會自動更新此欄位。 為了正確利用此欄位 [即時客戶配置檔案](../../../profile/home.md)，不要嘗試手動更新資料操作中欄位的內容。<br /><br />請參閱中有關標識映射的章節 [架構組合基礎](../../schema/composition.md#identityMap) 的子菜單。 |
| `isDeleted` | 布林值 | 指示此人是否已在Marketo Engage中刪除。<br><br>使用 [Marketo源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo刪除的任何記錄將自動反映在即時客戶配置檔案中。 但是，與這些檔案有關的記錄可能仍會在Data Lake中保留。 通過設定 `isDeleted` 至 `true`，可以使用該欄位在查詢資料湖時過濾已從源中刪除的記錄。 |
| `organizations` | 字串陣列 | 人員工作所在的組織名稱清單。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
