---
title: XDM Business Campaign詳細資訊結構欄位群組
description: 本檔案提供「 XDM業務促銷活動詳細資料結構」欄位群組的概觀。
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 5%

---

# [!UICONTROL XDM商業促銷活動詳細資訊] 方案欄位組

[!UICONTROL XDM商業促銷活動詳細資訊] 是的標準架構欄位組 [[!UICONTROL XDM商業宣傳] 類](../../classes/b2b/business-campaign.md)，可擷取有關商業促銷活動的詳細資訊。

![UI中顯示的XDM「業務促銷活動詳細資料」欄位群組結構](../../images/field-groups/b2b/business-campaign-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 代表商業促銷活動的實際成本。 |
| `budgetedCost` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 表示業務活動的預算成本。 |
| `expectedRevenue` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 代表業務促銷活動預計產生的收入。 |
| `parentCampaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 父促銷活動的複合ID（如果適用）。 |
| `campaignEndDate` | [!UICONTROL DateTime] | 促銷活動結束或將結束的ISO 8601時間戳記。 |
| `campaignProgressionName` | [!UICONTROL 字串] | 促銷活動進展名稱。 |
| `campaignStartDate` | [!UICONTROL DateTime] | 促銷活動開始或將開始的ISO 8601時間戳記。 |
| `campaignStatus` | [!UICONTROL 字串] | 促銷活動的目前狀態。 |
| `channelName` | [!UICONTROL 字串] | 與此促銷活動相關聯的管道名稱。 |
| `expectedResponse` | [!UICONTROL 字串] | 促銷活動的預期回應。 |
| `integrationPartnerName` | [!UICONTROL 字串] | 已與此促銷活動整合的合作夥伴的名稱。 |
| `isActive` | [!UICONTROL 布林值] | 指出此促銷活動是否有效。 |
| `isDeleted` | [!UICONTROL 布林值] | 指出此促銷活動是否已在Marketo Engage中刪除。<br><br>使用 [Marketo來源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md),Marketo中刪除的任何記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄仍可能會保留在Data Lake。 設定 `isDeleted` to `true`，您可以使用欄位來篩選已在查詢資料湖時從來源刪除的記錄。 |
| `lastActivityDate` | [!UICONTROL DateTime] | 與促銷活動相關聯的上次活動的ISO 8601時間戳記。 |
| `timeZone` | [!UICONTROL 字串] | 促銷活動運作的時區。 |
| `timeZoneDelivery` | [!UICONTROL 字串] | 促銷活動運作的傳送時區。 |
| `timeZoneName` | [!UICONTROL 字串] | 促銷活動所在時區的名稱。 |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | 此促銷活動上次網路研討會歷史記錄同步的ISO 8601時間戳記。 |
| `webinarHistorySyncStatus` | [!UICONTROL 字串] | 此促銷活動的網路研討會歷史記錄同步的狀態。 |
| `webinarSessionDescription` | [!UICONTROL 字串] | 與此促銷活動相關聯的網路研討會會期說明。 |
| `webinarSessionName` | [!UICONTROL 字串] | 與此促銷活動相關聯的網路研討會工作階段的名稱。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
