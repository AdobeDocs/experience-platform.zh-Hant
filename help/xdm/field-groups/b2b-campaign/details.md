---
title: XDM商業活動詳細資料結構欄位群組
description: 瞭解XDM商業活動詳細資訊結構欄位群組。
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL XDM商業促銷活動詳細資料]結構描述欄位群組

[!UICONTROL XDM商業促銷活動詳細資料]是[[!UICONTROL XDM商業促銷活動]類別](../../classes/b2b/business-campaign.md)的標準結構描述欄位群組，可擷取商業促銷活動的詳細資訊。

![ XDM商業活動詳細資訊欄位群組在UI中的結構](../../images/field-groups/b2b/business-campaign-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 代表商業促銷活動的實際成本。 |
| `budgetedCost` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 代表商業行銷活動的預算成本。 |
| `expectedRevenue` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 代表預期業務行銷活動產生的收入。 |
| `parentCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 上層行銷活動的複合ID （如適用）。 |
| `campaignEndDate` | [!UICONTROL 日期時間] | 促銷活動結束或即將結束時間的ISO 8601時間戳記。 |
| `campaignProgressionName` | [!UICONTROL 字串] | 促銷活動進度名稱。 |
| `campaignStartDate` | [!UICONTROL 日期時間] | 促銷活動開始或即將開始的ISO 8601時間戳記。 |
| `campaignStatus` | [!UICONTROL 字串] | 行銷活動的目前狀態。 |
| `channelName` | [!UICONTROL 字串] | 與此行銷活動相關聯的管道名稱。 |
| `expectedResponse` | [!UICONTROL 字串] | 行銷活動的預期回應。 |
| `integrationPartnerName` | [!UICONTROL 字串] | 已與此行銷活動整合的合作夥伴名稱。 |
| `isActive` | [!UICONTROL 布林值] | 指出此行銷活動是否有效。 |
| `isDeleted` | [!UICONTROL 布林值] | 指出此行銷活動是否已在Marketo Engage中刪除。<br><br>使用[Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)時，在Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過將`isDeleted`設定為`true`，您可以在查詢資料湖時使用該欄位來篩選出已從您的來源中刪除的記錄。 |
| `lastActivityDate` | [!UICONTROL 日期時間] | 與行銷活動相關之上次活動的ISO 8601時間戳記。 |
| `timeZone` | [!UICONTROL 字串] | 行銷活動運作的時區。 |
| `timeZoneDelivery` | [!UICONTROL 字串] | 行銷活動運作的傳遞時區。 |
| `timeZoneName` | [!UICONTROL 字串] | 行銷活動運作的時區名稱。 |
| `webinarHistorySyncDate` | [!UICONTROL 日期時間] | 此行銷活動上次網路研討會記錄同步的ISO 8601時間戳記。 |
| `webinarHistorySyncStatus` | [!UICONTROL 字串] | 此行銷活動的網路研討會記錄同步的狀態。 |
| `webinarSessionDescription` | [!UICONTROL 字串] | 與此行銷活動相關之網路研討會工作階段的說明。 |
| `webinarSessionName` | [!UICONTROL 字串] | 與此行銷活動相關聯的網路研討會工作階段名稱。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json)。
