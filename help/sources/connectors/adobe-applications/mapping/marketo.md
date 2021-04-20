---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；行銷活動；Marketo；映射
solution: Experience Platform
title: Marketo Engage源的映射欄位
topic: 概述
description: 下表包含Marketo資料集中各欄位與其對應的XDM欄位之間的映射。
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 3%

---


# （測試版）[!DNL Marketo Engage]欄位對應

>[!IMPORTANT]
>
>[!DNL Marketo Engage]來源目前處於測試階段。 其功能和說明檔案可能會有所變更。

下表包含9個[!DNL Marketo]資料集中欄位與其對應的「體驗資料模型」(XDM)欄位之間的映射。

## 活動 {#activities}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `personID` | `personID` | 主要身分 |
| `eventType` | `eventType` |
| `timeStamp` | `timestamp` |
| `web.webPageDetails._marketo.URL` | `web.webPageDetails._marketo.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `listOperations.listID` | `listOperations.listID` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `opportunityEvent.dataValueChanges.attributeName` | `opportunityEvent.dataValueChanges.attributeName` |
| `opportunityEvent.dataValueChanges.newValue` | `opportunityEvent.dataValueChanges.newValue` |
| `opportunityEvent.dataValueChanges.oldValue` | `opportunityEvent.dataValueChanges.oldValue` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |

{style=&quot;table-layout:auto&quot;}

## 計劃 {#programs}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `campaignID` | 主要身分 |
| `sfdcId` | `extSourceSystemAudit.externalID` | 次要識別 |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `parentProgramId` | `parentCampaignID` |
| `integrationPartner` | `integrationPartnerName` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |

{style=&quot;table-layout:auto&quot;}

## 方案成員資格{#program-memberships}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `campaignMemberID` | 主要身分 |
| `programId` | `campaignID` | 關係 |
| `leadId` | `personID` | 關係 |
| `acquiredByCampaignID` | `acquiredByCampaignID` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## 公司 {#companies}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | 主要身分 |
| `mktoCdpExternalId` | `extSourceSystemAudit.externalID` | 次要識別 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |

{style=&quot;table-layout:auto&quot;}

## 靜態清單{#static-lists}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `marketingListID` | 主要身分 |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## 靜態清單成員資格{#static-list-memnberships}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `marketingListMemberID` | `staticListMemberID` | 主要身分 |
| `marketingListID` | `staticListID` | 關係 |
| `personID` | `personID` | 關係 |
| `createdAt` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## 命名帳戶{#named-accounts}

>[!IMPORTANT]
>
>指名的帳戶資料集只有在Marketo的帳戶型行銷(ABM)功能中才必要。 如果您未使用ABM，則無需為命名帳戶設定映射。

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | 主要身分 |
| `crmGuid` | `extSourceSystemAudit.externalID` | 次要識別 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `parentAccountId` | `accountParentID` |
| `sourceType` | `accountSourceType` |

{style=&quot;table-layout:auto&quot;}

## 機會{#opportunities}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `opportunityID` | 主要身分 |
| `externalOpportunityId` | `extSourceSystemAudit.externalID` | 次要識別 |
| `mktoCdpAccountOrgId` | `accountID` | 關係 |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `Campaign-ID` | `campaignID` | 僅在您使用Salesforce整合時才建議使用。 |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## 業務機會聯繫人角色{#opportunity-contact-roles}

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `opportunityPersonID` | 主要身分 |
| `mktoCdpSfdcId` | `extSourceSystemAudit.externalID` | 次要識別 |
| `mktoCdpOpptyId` | `opportunityID` | 關係 |
| `leadId` | `personID` | 關係 |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## 人{#persons}

在平台UI的[!DNL Profiles]控制面板中，如果您用來瀏覽的合併原則中ID接合值設為`None`，則連結的身分視窗將只會顯示主要身分屬性。

因應措施是，您可以將ID拼接欄位從`None`更新為`Private graph`，以便查看所有連結到[!DNL Profile]的身分。 或者，您可以建立新的合併原則，或使用包含ID接合值設為`Private graph`的不同合併原則。 如果選擇建立新合併策略或使用不同的合併策略，則必須確保策略包含用於[!DNL Marketo]人員映射集的相同方案類型。 有關詳細資訊，請參閱[合併策略UI指南](../../../../profile/ui/merge-policies.md)。

| 來源資料集 | XDM目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `id` | `personID` | 主要身分 |
| `emailSuspended` | `b2b.personOptInOut._channels.email` |
| `emailSuspendedAt` | `b2b.personOptInOut.optOutDetails.email.optOutDate` |
| `emailSuspendedCause` | `b2b.personOptInOut.optOutDetails.email.optOutReason` |
| `contactCompany` | `b2b.accountID` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpCnvContactPersonId` | `b2b.convertedContactID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| `sfdcId` | `extSourceSystemAudit.externalID` | 次要身份 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `organizations` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `mktoCdpCnvContactPersonId` | `personComponents.sourceConvertedContactID` |
| `contactCompany` | `personComponents.sourceAccountID` |
| `sfdcContactId` | `personComponents.sourceExternalID` | 僅在您使用Salesforce整合時才建議使用。 |
| `id` | `personComponents.sourcePersonID` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

閱讀本文檔，您就[!DNL Marketo]資料集及其對應的XDM欄位之間的映射關係獲得了深入見解。 請參見有關建立 [!DNL Marketo] 源連接](../../../tutorials/ui/create/adobe-applications/marketo.md)以完成[!DNL Marketo]資料流的教程。[
