---
title: Microsoft Dynamics對應欄位
description: 下表包含Microsoft Dynamics來源欄位與其對應XDM欄位之間的對應。
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: ec42cf27c082611acb1a08500b7bbd23fc34d730
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 8%

---

# [!DNL Microsoft Dynamics]欄位對應

下表包含[!DNL Microsoft Dynamics]來源欄位與其對應的Experience Data Model (XDM)欄位之間的對應。

## 連絡人 {#contacts}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `birthdate` | `person.birthDate` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `contactid` | `b2b.personKey.sourceID` |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `department` | `extendedWorkDetails.departments` |
| `fullname` | `person.name.fullName` |
| `suffix` | `person.name.suffix` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | 次要識別碼。 |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `lastname` | `person.name.lastName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |
| `telephone1` | `workPhone.number` |

{style="table-layout:auto"}

## 銷售機會 {#leads}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `telephone1` | `workPhone.number` |
| `mobilephone` | `mobilePhone.number` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | 次要識別碼 |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `fax` | `faxPhone.number` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `lastname` | `person.name.lastName` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `leadid` | `b2b.personKey.sourceID` |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |

{style="table-layout:auto"}

## 帳戶 {#accounts}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `accountid` | `accountKey.sourceID` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `accountnumber` | `accountNumber` |
| `accountratingcode` | `accountOrganization.rating` |
| `address1_addressid` | `accountPhysicalAddress._id` |
| `address1_city` | `accountPhysicalAddress.city` |
| `address1_country` | `accountPhysicalAddress.country` |
| `address1_county` | `accountPhysicalAddress.region` |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |
| `address1_line1` | `accountPhysicalAddress.street1` |
| `address1_line2` | `accountPhysicalAddress.street2` |
| `address1_line3` | `accountPhysicalAddress.street3` |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |
| `address1_name` | `accountPhysicalAddress.label` |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `accountDescription` |
| `fax` | `accountFax.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `name` | `accountName` |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |
| `revenue` | `accountOrganization.annualRevenue.amount` |
| `sic` | `accountOrganization.SICCode` |
| `telephone1` | `accountPhone.number` |
| `tickersymbol` | `accountOrganization.tickerSymbol` |
| `websiteurl` | `accountOrganization.website` |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |

{style="table-layout:auto"}

## 機會 {#opportunities}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `name` | `opportunityName` |
| `"Dynamics"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |
| `actualclosedate` | `actualCloseDate` |
| `actualvalue` | `opportunityAmount.amount` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |
| `closeprobability` | `probabilityPercentage` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `opportunityDescription` |
| `estimatedclosedate` | `expectedCloseDate` |
| `estimatedvalue` | `expectedRevenue.amount` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `opportunityid` | `opportunityKey.sourceID` |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `salesstage` | `opportunityStage` |
| `stepname` | `nextStep` |

{style="table-layout:auto"}

## 機會聯絡人角色 {#opportunity-contact-roles}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `connectionid` | `opportunityPersonKey.sourceID` |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `connectionrole1.name` | `personRole` |
| `record1objecttypecode` | *自訂欄位群組必須定義為目標結構描述。*&#x200B;如需詳細資訊，請參閱[如何將挑選清單型別來源欄位對應到目標XDM結構描述](#picklist-type-fields)的相關步驟，請參閱附錄一節。 | 如需`record1objecttypecode`來源欄位的可能和值及標籤清單，請參閱此[[!DNL Microsoft Dynamics] 連線實體參考檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options)。 |
| `record2objecttypecode` | *自訂欄位群組必須定義為目標結構描述。*&#x200B;如需詳細資訊，請參閱[如何將挑選清單型別來源欄位對應到目標XDM結構描述](#picklist-type-fields)的相關步驟，請參閱附錄一節。 | 如需`record2objecttypecode`來源欄位的可能和值及標籤清單，請參閱此[[!DNL Microsoft Dynamics] 連線實體參考檔案](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options)。 |

{style="table-layout:auto"}

## 行銷活動 {#campaigns}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `"Dynamics"` | `campaignKey.sourceType` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey`是次要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `description` | `campaignDescription` |
| `name` | `campaignName` |
| `totalactualcost` | `actualCost.amount` |
| `budgetedcost` | `budgetedCost.amount` |
| `expectedrevenue` | `expectedRevenue.amount` |
| `actualend` | `campaignEndDate` |
| `actualstart` | `campaignStartDate` |
| `expectedresponse` | `expectedResponse` |
| `utcconversiontimezonecode` | `timeZone` |
| `utcconversiontimezonecode` | `timezoneName` |

{style="table-layout:auto"}

## 行銷清單 {#marketing-list}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `description` | `marketingListDescription` |
| `listname` | `marketingListName` |
| `listid` | `marketingListKey.sourceID` |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## 行銷清單成員 {#marketing-list-members}

| 來源欄位 | 目標XDM欄位 | 附註 |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | 主要身分。 將自動取代`"${CRM_ORG_ID}"`的值。 |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## 附錄

以下各節提供您可在為[!DNL Microsoft] Dynamics來源設定B2B對應時使用的其他資訊。

### 挑選清單型別欄位 {#picklist-type-fields}

您可以使用[計算欄位](../../../../data-prep/ui/mapping.md#calculated-fields)將挑選清單型別來源欄位從[!DNL Microsoft Dynamics]對應到目標XDM欄位。

例如，`genderCode`欄位包含兩個選項：

| 值 | 標籤 |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

您可以使用下列選項將`genderCode`來源欄位對應到`person.gender`目標欄位：

#### 使用邏輯運運算元

| 來源欄位 | 目標XDM欄位 |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

在此案例中，如果索引鍵在選項中找到，則值對應到索引鍵；如果存在`default`但找不到索引鍵，則值為`default`。 如果選項為`null`或沒有`default`且找不到金鑰，則值對應至`null`。

#### 使用計算欄位

| 來源欄位 | 目標XDM欄位 |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>上述作業的巢狀反複專案類似於： `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`。

如需詳細資訊，請參閱 [!DNL Data Prep][&#128279;](../../../../data-prep/functions.md##logical-operators)中邏輯運運算元的檔案
