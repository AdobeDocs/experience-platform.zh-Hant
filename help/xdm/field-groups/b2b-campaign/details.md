---
title: XDM業務市場活動詳細資訊架構欄位組
description: 本文檔提供了XDM業務活動詳細資訊架構欄位組的概覽。
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 4%

---

# [!UICONTROL XDM業務活動詳細資訊] 架構欄位組

[!UICONTROL XDM業務活動詳細資訊] 是標準架構欄位組 [[!UICONTROL XDM業務活動] 類](../../classes/b2b/business-campaign.md)，它捕獲有關業務活動的詳細資訊。

![XDM業務活動詳細資訊欄位組的結構，如UI中所示](../../images/field-groups/b2b/business-campaign-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 表示業務活動的實際成本。 |
| `budgetedCost` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 表示業務活動的預算成本。 |
| `expectedRevenue` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 表示業務市場活動預期產生的收入。 |
| `parentCampaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 父市場活動的組合ID（如果適用）。 |
| `campaignEndDate` | [!UICONTROL 日期時間] | 市場活動結束或將結束的ISO 8601時間戳。 |
| `campaignProgressionName` | [!UICONTROL 字串] | 市場活動進展名稱。 |
| `campaignStartDate` | [!UICONTROL 日期時間] | 市場活動開始時間或將開始時間的ISO 8601時間戳。 |
| `campaignStatus` | [!UICONTROL 字串] | 市場活動的當前狀態。 |
| `channelName` | [!UICONTROL 字串] | 與此市場活動關聯的渠道的名稱。 |
| `expectedResponse` | [!UICONTROL 字串] | 該活動的預期響應。 |
| `integrationPartnerName` | [!UICONTROL 字串] | 與此活動整合的合作夥伴的名稱。 |
| `isActive` | [!UICONTROL 布林值] | 指示此市場活動是否有效。 |
| `isDeleted` | [!UICONTROL 布林值] | 指示此市場活動是否已在Marketo Engage中刪除。<br><br>使用 [Marketo源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo刪除的任何記錄將自動反映在即時客戶配置檔案中。 但是，與這些檔案有關的記錄可能仍會在Data Lake中保留。 通過設定 `isDeleted` 至 `true`，可以使用該欄位在查詢資料湖時過濾已從源中刪除的記錄。 |
| `lastActivityDate` | [!UICONTROL 日期時間] | 與市場活動關聯的上一活動的ISO 8601時間戳。 |
| `timeZone` | [!UICONTROL 字串] | 市場活動所在的時區。 |
| `timeZoneDelivery` | [!UICONTROL 字串] | 市場活動所在的交貨時區。 |
| `timeZoneName` | [!UICONTROL 字串] | 市場活動所在時區的名稱。 |
| `webinarHistorySyncDate` | [!UICONTROL 日期時間] | 此活動上次網路研討會歷史同步的ISO 8601時間戳。 |
| `webinarHistorySyncStatus` | [!UICONTROL 字串] | 此活動的網路研討會歷史同步的狀態。 |
| `webinarSessionDescription` | [!UICONTROL 字串] | 與此活動關聯的網路研討會的說明。 |
| `webinarSessionName` | [!UICONTROL 字串] | 與此活動關聯的網路研討會的名稱。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json)。
