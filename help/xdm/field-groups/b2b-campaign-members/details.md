---
title: XDM業務市場活動成員詳細資訊架構欄位組
description: 本文檔提供XDM Business Campaign Member Details架構欄位組的概覽。
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# [!UICONTROL XDM業務活動成員詳細資訊] 架構欄位組

[!UICONTROL XDM業務活動成員詳細資訊] 是標準架構欄位組 [[!UICONTROL XDM業務活動成員] 類](../../classes/b2b/business-campaign-members.md)，它捕獲有關業務活動的詳細資訊。

![XDM業務活動成員詳細資訊欄位組在UI中顯示時的結構](../../images/field-groups/b2b/business-campaign-member-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 獲取此市場活動成員的市場活動的組合ID。 |
| `acquiredByCampaignID` | [!UICONTROL 字串] | 獲取此市場活動成員的市場活動的字串標識符。 |
| `firstRespondedDate` | [!UICONTROL 日期時間] | ISO 8601時間戳，表示人員首次響應市場活動的時間。 |
| `hasReachedSuccess` | [!UICONTROL 布林值] | 指示此市場活動成員是否導致成功轉換。 |
| `hasResponded` | [!UICONTROL 布林值] | 指示此市場活動成員是否已對市場活動做出響應。 |
| `isDeleted` | [!UICONTROL 布林值] | 指示此市場活動成員是否已在Marketo Engage中刪除。<br><br>使用 [Marketo源連接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，在Marketo刪除的任何記錄將自動反映在即時客戶配置檔案中。 但是，與這些檔案有關的記錄可能仍會在Data Lake中保留。 通過設定 `isDeleted` 至 `true`，可以使用該欄位在查詢資料湖時過濾已從源中刪除的記錄。 |
| `isExhausted` | [!UICONTROL 布林值] | 指示此市場活動成員是否已用盡所有市場活動交互。 |
| `lastStatus` | [!UICONTROL 字串] | 市場活動成員的最後狀態。 |
| `memberStatus` | [!UICONTROL 字串] | 市場活動成員的當前狀態。 |
| `memberStatusReason` | [!UICONTROL 字串] | 市場活動成員的當前狀態背後的原因。 |
| `membershipDate` | [!UICONTROL 日期時間] | 市場活動成員的當前狀態背後的原因。 |
| `nurtureCadence` | [!UICONTROL 字串] | 向活動成員提供與活動相關的資訊的時間節點。 |
| `nurtureTrackName` | [!UICONTROL 字串] | 此活動成員所受的培養計畫的名稱。 |
| `reachedSuccessDate` | [!UICONTROL 日期時間] | ISO 8601時間戳，用於為市場活動成員成功轉換的時間。 |
| `webinarConfirmationUrl` | [!UICONTROL 字串] | 活動成員的網路研討會確認URL。 |
| `webinarRegistrationID` | [!UICONTROL 字串] | 活動成員的網路研討會註冊ID。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
