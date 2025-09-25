---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；marketo engage；Marketo；對應
solution: Experience Platform
title: Marketo Engage Source的對應欄位
description: 下表包含Marketo資料集中欄位與其對應XDM欄位之間的對應。
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: 3b21d952da603b519c9919b08467cd5c6091f235
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 5%

---

# [!DNL Marketo Engage]欄位對應 {#marketo-engage-field-mappings}

下表包含九個[!DNL Marketo]資料集中的欄位與其對應的體驗資料模型(XDM)欄位之間的對應。

>[!TIP]
>
>除[!DNL Marketo]以外的所有`Activities`資料集現在都支援`isDeleted`。 您現有的資料流會自動包含`isDeleted`，但僅會針對新擷取的資料擷取標幟。 如果您想要將標幟套用至所有歷史資料，則必須停止現有資料流並使用新對應重新建立資料流。 請注意，如果您移除`isDeleted`，則您將無法再存取該功能。 自動填入對應後，請務必保留對應。

## 活動 {#activities}

[!DNL Marketo]來源現在支援其他標準活動。 若要使用標準活動，您必須使用[結構描述自動產生公用程式](../marketo/marketo-namespaces.md)來更新結構描述，因為如果您建立新的`activities`資料流而不更新結構描述，對應範本將會失敗，因為新的目標欄位將不會出現在結構描述中。 如果您選擇不更新您的結構描述，您仍然可以建立新的資料流並解除任何錯誤。 不過，任何新欄位或更新後的欄位都不會內嵌到Experience Platform中。

閱讀[XDM體驗事件類別](../../../../xdm/classes/experienceevent.md)的檔案，以瞭解XDM類別和XDM欄位群組的詳細資訊。

>[!NOTE]
>
>`iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)`來源欄位是必須使用Experience Platform UI中的&#x200B;**[!UICONTROL 新增計算欄位]**&#x200B;選項新增的計算欄位。 閱讀有關[新增計算欄位](../../../../data-prep/ui/mapping.md#calculated-fields)的教學課程，以瞭解詳細資訊。

| Marketo來源欄位 | 活動型別ID | Source資料集 | xdm目標欄位 | 附註 |
| -------------------- | ---------------- | -------------- | ---------------- | ----- |
| `_id` |  | `_id` | `_id` |  |
|  |  | `"Marketo"` | `personKey.sourceType` |  |
|  |  | `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `leadId` |  | `personID` | `personKey.sourceID` |  |
|  |  | `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `activityTypeId` |  | `eventType` | `eventType` |  |
| <ul><li>如果<code>activityTypeId</code> 是1、2、3、9、10或11 →標籤<code>productedBy</code> 做為<strong>self</strong>。</li><li>如果<code>activityTypeId</code> 是6、7、8、12、21、22、24、25、27、32、34、35、36、46、101、104、110、113、114或115→記號<code>productedBy</code> 作為<strong>系統</strong>。</li><li>對於所有其他值，→標籤<code>productedBy</code> 做為<strong>self</strong>。</li></ul> |  | `producedBy` | `producedBy` |  |
| `activityDate` |  | `timestamp` | `timestamp` |  |
| `attributes.Webpage URL` |  | `web.webPageDetails.URL` | `web.webPageDetails.URL` |  |
| `attributes.User Agent` |  | `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |  |
| `attributes.Client IP Address` |  | `environment.ipV4` | `environment.ipV4` |  |
| `attributes.Search Query` |  | `search.keywords` | `search.keywords` |  |
| `attributes.Search Engine` |  | `search.searchEngine` | `search.searchEngine` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.name` | `web.webPageDetails.name` |  |
| `attributes.Personalized URL` | 1 | `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |  |
| `attributes.Query Parameters` | 1 | `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |  |
| `attributes.Referrer URL` |  | `web.webReferrer.URL` | `web.webReferrer.URL` |  |
| `primaryAttributeValueId when activityTypeId in (24, 25)` | 24， 25 | `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |  |
| `attributes.Is Primary` | 34,35,36 | `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |  |
| 在(34、35、36)中的activityTypeId時為primaryAttributeValueId | 34， 35， 36 | `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |  |
| `attributes.Role` | 34， 35， 36 | `opportunityEvent.role` | `opportunityEvent.role` |  |
| `attributes.Created Date` |  | `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |  |
| `attributes.Form Name` |  | `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |  |
| `attributes.Lead Source` |  | `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |  |
| `attributes.List Name` |  | `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |  |
| `attributes.SFDC Type` |  | `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |  |
| `attributes.Source Type` |  | `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |  |
| activityTypeId = 21時的primaryAttributeValue | 21 | `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |  |
| `attributes.Converted Status` | 21 | `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |  |
| `attributes.Send Notification Email` | 21 | `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |  |
| 在(7， 8， 9， 10， 11， 27)中的activityTypeId時為primaryAttributeValueId | 7， 8， 9， 10， 11， 27 | `iif(${directMarketing\\.mailingID} != null && ${directMarketing\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `directMarketing.mailingKey` |  |
| 在(7， 8， 9， 10， 11， 27)中的activityTypeId時為primaryAttributeValueId | 7， 8， 9， 10， 11， 27 | `directMarketing.mailingName` | `directMarketing.mailingName` |  |
|  |  | `directMarketing.testVariantName` | `directMarketing.testVariantName` |  |
| `attributes.Test Variant` |  | `directMarketing.testVariantID` | `directMarketing.testVariantID` |  |
| `attributes.Subcategory` <ul><li><strong>activityTypeId = 8</strong><ul><li>1099 →訊息已封鎖</li><li>Source上已封鎖1003 →垃圾訊息</li><li>1004 →封郵件上的垃圾訊息</li><li>2003 →電子郵件地址無效</li><li>2001 →電子郵件地址錯誤</li><li>* →未知的跳出原因</li></ul></li><li><strong>activityTypeId = 27</strong><ul><li>3999 →訊息未接受</li><li>3001 →信箱已滿</li><li>3004 →發生逾時</li><li>4003 → DNS失敗</li><li>4002 →訊息太大</li><li>4006 →原則違規</li><li>4999 →暫時性失敗</li><li>收到9999 →錯誤回應</li><li>* →軟退信的未知原因</li></ul></li></ul> | 8， 27 | `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |  |
| `attributes.Details` |  | `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |  |
| `attributes.Email` |  | `directMarketing.email` | `directMarketing.email` |  |
| `attributes.Is Mobile Device` |  | `device.isMobileDevice` | `device.isMobileDevice` |  |
| `attributes.device` |  | `device.model` | `device.model` |  |
| `attributes.Platform` |  | `environment.operatingSystem` | `environment.operatingSystem` |  |
| `attributes.Link` |  | `directMarketing.linkURL` | `directMarketing.linkURL` |  |
| activityTypeId = 3 else attributes.Link ID時的primaryAttributeValueId | 3 | `iif(${web\\.webInteraction\\.linkID} != null && ${web\\.webInteraction\\.linkID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.webInteraction\\.linkID}, \"sourceKey\", concat(${web\\.webInteraction\\.linkID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.webInteraction.webInteractionKey` |  |
| activityTypeId = 2 else attributes.Webform ID時的primaryAttributeValueId | 2 | `iif(${web\\.fillOutForm\\.webFormID} != null && ${web\\.fillOutForm\\.webFormID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.fillOutForm\\.webFormID}, \"sourceKey\", concat(${web\\.fillOutForm\\.webFormID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.fillOutForm.webFormKey` |  |
| activityTypeId = 2時為primaryAttributeValueId，否則為null | 2 | `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |  |
| activityTypeId = 3 else attributes.Link時的primaryAttributeValueId | 3 | `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |  |
| `attributes.Change Value` | 22 | `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |  |
| `attributes.New Value` | 22 | `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |  |
| `attributes.Old Value` | 22 | `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |  |
| `attributes.Priority` | 22 | `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |  |
| `attributes.Reason` | 22 | `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |  |
| `attributes.Relative Score` | 22 | `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |  |
| `attributes.Relative Urgency` | 22 | `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |  |
| activityTypeId = 22時的primaryAttributeValueId | 22 | `iif(${leadOperation\.changeScore\.scoreAttributeID} != null && ${leadOperation\.changeScore\.scoreAttributeID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeScore\.scoreAttributeID}, "sourceKey", concat(${leadOperation\.changeScore\.scoreAttributeID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeScore.scoreAttributeKey` |  |
| activityTypeId = 22時的primaryAttributeValueId | 22 | `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |  |
| `attributes.Urgency` | 22 | `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |  |
| `attributes.Data Value Changes` |  | `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |  |
| activityTypeId = 104時的primaryAttributeValueId | 104 | `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |  |
| `attributes.Acquired By` | 104 | `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |  |
| `attributes.Success` | 104 | `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |  |
| `attributes.New Status ID` | 104 | `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |  |
| `attributes.New Status` | 104 | `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |  |
| `attributes.Old Status ID` | 104 | `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |  |
| `attributes.Old Status` | 104 | `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |  |
| `attributes.Reason` | 104 | `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |  |
| `attributes.Date` | 46 | `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |  |
| `attributes.Description` | 46 | `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |  |
| `attributes.Source` | 46 | `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |  |
| activityTypeId = 46時的primaryAttributeValue | 46 | `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |  |
| activityTypeId = 110時的primaryAttributeValueId | 110 | `iif(${leadOperation\\.callWebhook\\.webhookID} != null && ${leadOperation\\.callWebhook\\.webhookID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.callWebhook.webhookKey` |  |
| activityTypeId = 110時的primaryAttributeValueId | 110 | `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |  |
| `attributes.Error Type` | 110 | `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |  |
| activityTypeId = 115時的primaryAttributeValueId | 115 | `iif(${leadOperation\\.changeCampaignCadence\\.campaignID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeCampaignCadence.campaignKey` |  |
| `attributes.New Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |  |
| `attributes.Previous Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |  |
| activityTypeId = 114時的primaryAttributeValueId | 113 | `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |  |
| `attributes.Track ID` | 113 | `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |  |
| `attributes.Stream Name` | 113 | `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |  |
| activityTypeId = 115時的primaryAttributeValueId | 115 | `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |  |
| `attributes.New Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |  |
| `attributes.New Track Name` | 115 | `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |  |
| `attributes.Previous Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |  |
| `attributes.Previous Stream Name` | 115 | `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |  |
| activityTypeId = 101時的primaryAttributeValueId | 101 | `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |  |
| activityTypeId = 101時的primaryAttributeValueId | 101 | `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |  |
| `attributes.New Stage ID` | 101 | `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |  |
| `attributes.New Stage` | 101 | `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |  |
| `attributes.Old Stage ID` | 101 | `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |  |
| `attributes.Old Stage` | 101 | `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |  |
| `attributes.Reason` | 101 | `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |  |
| `attributes.Merge IDs` （當activityTypeId = 32） | 32 | `json_to_object(${leadOperation\.mergeLeads\.mergeIDs})` | `leadOperation.mergeLeads.sourceKeys` |  |
| `attributes.Master Updated` | 32 | `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |  |
| `attributes.Merged in Sales` | 32 | `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |  |
| `attributes.Merge Source` | 32 | `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |  |
| activityTypeId = 6時的primaryAttributeValueId | 6 | `iif(${directMarketing\.emailSent\.mailingID} != null && ${directMarketing\.emailSent\.mailingID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${directMarketing\.emailSent\.mailingID}, "sourceKey", concat(${directMarketing\.emailSent\.mailingID},"@${MUNCHKIN_ID}.Marketo")), null)` | `directMarketing.emailSent.mailingKey` |  |
| activityTypeId = 6時的primaryAttributeValueId | 6 | `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |  |
| `attributes.Test Variant` | 6 | `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |  |
| 附註 — 衍生自次要資產值 |  | `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |  |
| `attributes.Campaign Run ID` | 6 | `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |  |
|  |  | `directMarketing.automationRunID` | `directMarketing.automationRunID` |  |

{style="table-layout:auto"}

## 方案 {#programs}

閱讀[XDM商業活動概覽](../../../../xdm/classes/b2b/business-campaign.md)，瞭解有關XDM類別的更多資訊。 如需XDM欄位群組的詳細資訊，請閱讀[商業促銷活動詳細資料結構描述欄位群組](../../../../xdm/field-groups/b2b-campaign/details.md)指南。

>[!NOTE]
>
>對於自訂標籤型別，請前往結構描述並建立新的欄位群組。 然後，新增將來源欄位與目的地XDM欄位對應所需的所有其他欄位名稱。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `"Marketo"` | `campaignKey.sourceType` |  |
| `channel` | `channelName` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `cost` | `actualCost.amount` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `description` | `campaignDescription` |  |
| `endDate` | `campaignEndDate` |  |
| `id` | `campaignKey.sourceID` |  |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |  |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分。 CRM_TYPE和CRM_ORG_ID將會取代為探索API的一部分 |
| `integrationPartner` | `integrationPartnerName` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `name` | `campaignName` |  |
| `startDate` | `campaignStartDate` |  |
| `status` | `campaignStatus` |  |
| `type` | `campaignType` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |  |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |  |
| `webinarSessionDescription` | `webinarSessionDescription` |  |
| `webinarSessionName` | `webinarSessionName` |  |

{style="table-layout:auto"}

## 計畫成員資格 {#program-memberships}

閱讀[XDM商業活動會員總覽](../../../../xdm/classes/b2b/business-campaign-members.md)，瞭解有關XDM類別的更多資訊。 如需XDM欄位群組的詳細資訊，請閱讀[XDM商業促銷活動成員詳細資料結構描述欄位群組](../../../../xdm/field-groups/b2b-campaign-members/details.md)指南。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `id` | `campaignMemberKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | 關係 |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 關係 |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |  |
| `reachedSuccess` | `hasReachedSuccess` |  |
| `isExhausted` | `isExhausted` |  |
| `statusName` | `memberStatus` |  |
| `statusReason` | `memberStatusReason` |  |
| `membershipDate` | `membershipDate` |  |
| `nurtureCadence` | `nurtureCadence` |  |
| `trackName` | `nurtureTrackName` |  |
| `webinarUrl` | `webinarConfirmationUrl` |  |
| `registrationCode` | `webinarRegistrationID` |  |
| `reachedSuccessDate` | `reachedSuccessDate` |  |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分。 CRM_TYPE和CRM_ORG_ID將會取代為探索API的一部分 |
| `sfdc.lastStatus` | `lastStatus` |  |
| `sfdc.hasResponded` | `hasResponded` |  |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 公司 {#companies}

如需有關XDM類別的詳細資訊，請閱讀[XDM商業帳戶總覽](../../../../xdm/classes/b2b/business-account.md)。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` | |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` | |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| <ul><li><code>iif(mktoCdpExternalId！= null &amp;&amp; mktoCdpExternalId ！= &quot;&quot;， to_object(&quot;sourceType&quot;， &quot;${CRM_TYPE}&quot;， &quot;sourceInstanceID&quot;， &quot;${CRM_ORG_ID}&quot;， &quot;sourceID&quot;， mktoCdpExternalId， &quot;sourceKey&quot;， concat(mktoCdpExternalId，&quot;@${CRM_ORG_ID}。${CRM_TYPE}&quot;)， null)</code></li><li><code>iif(msftCdpExternalId！= null &amp;&amp; msftCdpExternalId ！= &quot;&quot;， to_object(&quot;sourceType&quot;， &quot;${CRM_TYPE}&quot;， &quot;sourceInstanceID&quot;， &quot;${CRM_ORG_ID}&quot;， &quot;sourceID&quot;， msftCdpExternalId， &quot;sourceKey&quot;， concat(msftCdpExternalId，&quot;@${CRM_ORG_ID}。${CRM_TYPE}&quot;)， null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分。 CRM_ORG_ID和CRM_TYPE將會取代為探索API的一部分 |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |
| `billingCity` | `accountBillingAddress.city` | |
| `billingCountry` | `accountBillingAddress.country` | |
| `billingPostalCode` | `accountBillingAddress.postalCode` | |
| `billingState` | `accountBillingAddress.state` | |
| `billingStreet` | `accountBillingAddress.street1` | |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` | |
| `sicCode` | `accountOrganization.SICCode` | |
| `industry` | `accountOrganization.industry` | |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` | |
| `website` | `accountOrganization.website` | |
| `mainPhone` | `accountPhone.number` | |
| `company` | `accountName` | |
| `companyNotes` | `accountDescription` | |
| `site` | `accountSite` | |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` | |
| `marketoIsDeleted` | `isDeleted` | |

{style="table-layout:auto"}

## 靜態清單 {#static-lists}

閱讀[XDM業務行銷清單總覽](../../../../xdm/classes/b2b/business-marketing-list.md)，瞭解有關XDM類別的更多資訊。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `id` | `marketingListKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `name` | `marketingListName` |  |
| `description` | `marketingListDescription` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 靜態清單成員資格 {#static-list-memberships}

閱讀[XDM業務行銷清單成員總覽](../../../../xdm/classes/b2b/business-marketing-list-members.md)，瞭解有關XDM類別的更多資訊。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |  |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | 關係 |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 關係 |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 具名帳戶 {#named-accounts}

>[!IMPORTANT]
>
>具名帳戶資料集僅適用於Marketo的帳戶型行銷(ABM)功能。 如果您未使用ABM，則不需要為已命名帳戶設定對應。

如需有關XDM類別的詳細資訊，請閱讀[XDM商業帳戶總覽](../../../../xdm/classes/b2b/business-account.md)。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |  |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分。 CRM_TYPE和CRM_ORG_ID將會取代為探索API的一部分 |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `city` | `accountBillingAddress.city` |  |
| `country` | `accountBillingAddress.country` |  |
| `state` | `accountBillingAddress.state` |  |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `sicCode` | `accountOrganization.SICCode` |  |
| `industry` | `accountOrganization.industry` |  |
| `logoUrl` | `accountOrganization.logoUrl` |  |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `name` | `accountName` |  |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |  |
| `sourceType` | `accountSourceType` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 機會 {#opportunities}

閱讀[XDM商業機會總覽](../../../../xdm/classes/b2b/business-opportunity.md)以瞭解有關XDM類別的詳細資訊。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `id` | `opportunityKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分。 CRM_TYPE和CRM_ORG_ID將會取代為探索API的一部分 |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | 關係 |
| `description` | `opportunityDescription` |  |
| `name` | `opportunityName` |  |
| `stage` | `opportunityStage` |  |
| `type` | `opportunityType` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `expectedRevenue` | `expectedRevenue.amount` |  |
| `amount` | `opportunityAmount.amount` |  |
| `closeDate` | `expectedCloseDate` |  |
| `fiscalQuarter` | `fiscalQuarter` |  |
| `fiscalYear` | `fiscalYear` |  |
| `forecastCategory` | `forecastCategory` |  |
| `forecastCategoryName` | `forecastCategoryName` |  |
| `isClosed` | `isClosed` |  |
| `isWon` | `isWon` |  |
| `quantity` | `opportunityQuantity` |  |
| `probability` | `probabilityPercentage` |  |
| `iif(mktoCdpSourceCampaignId != null && mktoCdpSourceCampaignId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpSourceCampaignId, "sourceKey", concat(mktoCdpSourceCampaignId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | 僅供具有Salesforce整合的客戶使用 |
| `lastActivityDate` | `lastActivityDate` |  |
| `leadSource` | `leadSource` |  |
| `nextStep` | `nextStep` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## 機會聯絡人角色 {#opportunity-contact-roles}

閱讀[XDM商業機會個人關係總覽](../../../../xdm/classes/b2b/business-account-person-relation.md)，以瞭解有關XDM類別的詳細資訊。

| Source資料集 | xdm目標欄位 | 附註 |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `"Marketo"` | `opportunityPersonKey.sourceType` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `id` | `opportunityPersonKey.sourceID` |  |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 關係 |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | 關係 |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分。 CRM_TYPE和CRM_ORG_ID將會取代為探索API的一部分 |
| `isPrimary` | `isPrimary` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `role` | `personRole` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |

{style="table-layout:auto"}

## 人員 {#persons}

閱讀[XDM個人設定檔總覽](../../../../xdm/classes/individual-profile.md)，瞭解有關XDM類別的詳細資訊。 如需有關XDM欄位群組的詳細資訊，請閱讀[XDM商業人士詳細資料結構描述欄位群組](../../../../xdm/field-groups/profile/business-person-details.md)指南和[XDM商業人士元件結構描述欄位群組](../../../../xdm/field-groups/profile/business-person-components.md)指南。

| 來源欄位 | 目標XDM欄位 | 附註 |
|---|---|---|
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | Munchkin_ID將會隨著探索API被取代 |
| `"Marketo"` | `b2b.personKey.sourceType` | |
| `address` | `workAddress.street1` | |
| `city` | `workAddress.city` | |
| `company` | `organizations` | |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | 主要身分。 Munchkin_ID將會隨著探索API被取代 |
| `country` | `workAddress.country` | |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `dateOfBirth` | `person.birthDate` | |
| `email` | `personComponents.workEmail.address` | |
| `email` | `workEmail.address` | |
| `fax` | `faxPhone.number` | |
| `firstName` | `person.name.firstName` | |
| `id` | `b2b.personKey.sourceID` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` | |
| <ul><li><code>iif(decode(sfdcType， &quot;Contact&quot;， sfdcContactId， &quot;Lead&quot;， sfdcLeadId， null) ！= null， to_object(&quot;sourceType&quot;， &quot;${CRM_TYPE}&quot;， &quot;sourceInstanceID&quot;， &quot;${CRM_ORG_ID}&quot;，&quot;sourceID&quot;，解碼(sfdcType， &quot;Contact&quot;， sfdcContactId， &quot;Lead&quot;， sfdcLeadId ， null)， &quot;sourceKey&quot;， concat(decode(sfdcType， &quot;Contact&quot;， sfdcContactId， null)，&quot;@${CRM_ORG_ID}。${CRM_TYPE}&quot;)， null)</code></li><li><code>iif(decode(msftType， &quot;Contact&quot;， msftContactId， &quot;Lead&quot;， msftLeadId， null) ！= null， to_object(&quot;sourceType&quot;， &quot;${CRM_TYPE}&quot;， &quot;sourceInstanceID&quot;， &quot;${CRM_ORG_ID}&quot;，&quot;sourceID&quot;，解碼(msftType， &quot;Contact&quot;， msftContactId， &quot;Lead&quot;， msftLeadId ， null)， &quot;sourceKey&quot;， concat(decode(msftType， &quot;Contact&quot;， msftContactId， &quot;LeadId， null)，&quot;@${CRM_ORG_ID}。${CRM_TYPE}&quot;)， null)</code></li></ul> | `personComponents.sourceExternalKey` | |
| <ul><li><code>iif(decode(sfdcType， &quot;Contact&quot;， sfdcContactId， &quot;Lead&quot;， sfdcLeadId， null) ！= null， to_object(&quot;sourceType&quot;， &quot;${CRM_TYPE}&quot;， &quot;sourceInstanceID&quot;， &quot;${CRM_ORG_ID}&quot;，&quot;sourceID&quot;，解碼(sfdcType， &quot;Contact&quot;， sfdcContactId， &quot;Lead&quot;， sfdcLeadId ， null)， &quot;sourceKey&quot;， concat(decode(sfdcType， &quot;Contact&quot;， sfdcContactId， null)，&quot;@${CRM_ORG_ID}。${CRM_TYPE}&quot;)， null)</code></li><li><code>iif(decode(msftType， &quot;Contact&quot;， msftContactId， &quot;Lead&quot;， msftLeadId， null) ！= null， to_object(&quot;sourceType&quot;， &quot;${CRM_TYPE}&quot;， &quot;sourceInstanceID&quot;， &quot;${CRM_ORG_ID}&quot;，&quot;sourceID&quot;，解碼(msftType， &quot;Contact&quot;， msftContactId， &quot;Lead&quot;， msftLeadId ， null)， &quot;sourceKey&quot;， concat(decode(msftType， &quot;Contact&quot;， msftContactId， &quot;LeadId， null)，&quot;@${CRM_ORG_ID}。${CRM_TYPE}&quot;)， null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey`是次要身分 |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | 這是計算欄位 |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` | |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.convertedContactKey` | 這是計算欄位 |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceConvertedContactKey` | 這是計算欄位 |
| `iif(unsubscribed == 'true', 'n', 'y' )` | `consents.marketing.email.val` | 如果取消訂閱為true （即值= 1），則將consents.marketing.email.val設為「n」。 如果取消訂閱為false （即值= 0），則將consents.marketing.email.val設定為null |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` | |
| `lastName` | `person.name.lastName` | |
| `leadPartitionId` | `b2b.personGroupID` | |
| `leadPartitionId` | `personComponents.personGroupID` | |
| `leadScore` | `b2b.personScore` | |
| `leadScore` | `personComponents.personScore` | |
| `leadSource` | `b2b.personSource` | |
| `leadSource` | `personComponents.personSource` | |
| `leadStatus` | `b2b.personStatus` | |
| `leadStatus` | `personComponents.personStatus` | |
| `marketingSuspended` | `b2b.isMarketingSuspended` | |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` | |
| `marketoIsDeleted` | `isDeleted` | |
| `middleName` | `person.name.middleName` | |
| `mktoCdpConvertedDate` | `b2b.convertedDate` | |
| `mktoCdpIsConverted` | `b2b.isConverted` | |
| `mobilePhone` | `mobilePhone.number` | |
| `personType` | `b2b.personType` | |
| `personType` | `personComponents.personType` | |
| `phone` | `workPhone.number` | |
| `postalCode` | `workAddress.postalCode` | |
| `salutation` | `person.name.courtesyTitle` | |
| `state` | `workAddress.state` | |
| `title` | `extendedWorkDetails.jobTitle` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |

{style="table-layout:auto"}

## 後續步驟

閱讀本檔案後，您已經取得[!DNL Marketo]資料集與其對應XDM欄位之間對應關係的insight。 請參閱有關[建立 [!DNL Marketo] 來源連線](../../../tutorials/ui/create/adobe-applications/marketo.md)的教學課程，以完成您的[!DNL Marketo]資料流。