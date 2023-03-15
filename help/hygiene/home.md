---
title: 資料衛生概述
description: Adobe Experience Platform資料衛生功能可讓您更新或清除過時或不準確的記錄，以管理資料的生命週期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Adobe Experience Platform資料衛生

>[!IMPORTANT]
>
>目前，只有已購買的組織才能使用資料衛生 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**.

Adobe Experience Platform提供一組完善的工具，可管理大型、複雜的資料操作，以便協調消費者體驗。 隨著資料隨著時間傳入系統中，管理資料儲存變得越來越重要，這樣資料就能如預期般使用、在需要更正錯誤資料時更新，並在組織原則認為有必要時刪除。

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

這些活動可使用 [[!UICONTROL 資料衛生] UI工作區](#ui) 或 [資料衛生API](#api). 當執行資料衛生作業時，系統在處理的每個步驟提供透明度更新。 請參閱 [時間表和透明度](#timelines-and-transparency) 有關在系統中如何表示每個作業類型的詳細資訊。

## [!UICONTROL 資料衛生] UI工作區 {#ui}

此 [!UICONTROL 資料衛生] platform UI中的workspace可讓您設定及排程資料衛生作業，協助確保記錄可如預期般維護。

如需在UI中管理資料衛生工作的詳細步驟，請參閱 [資料衛生UI指南](./ui/overview.md).

## 資料衛生API {#api}

此 [!UICONTROL 資料衛生] UI是以資料衛生API為基礎而建置的，如果您偏好讓資料衛生活動自動化，其端點可供您直接使用。 請參閱 [資料衛生API指南](./api/overview.md) 以取得更多資訊。

## 時間表和透明度

記錄刪除和資料集過期請求各自有各自的處理時間軸，並在各自工作流程的關鍵點提供透明度更新。

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

若 [資料集過期請求](./ui/dataset-expiration.md) 已建立：

| 測試 | 排程的過期後時間 | 說明 |
| --- | --- | --- |
| 請求已提交 | 0 小時 | 資料管理員或隱私權分析員會提交資料集要求，讓資料集在指定時間過期。 請求會顯示在 [!UICONTROL 資料衛生UI] 提交後，且會維持擱置狀態，直到排程的到期時間結束為止，之後請求就會執行。 |
| 資料集已丟棄 | 1 小時 | 資料集會從 [資料集詳細目錄頁面](../catalog/datasets/user-guide.md) 在UI中。 資料湖內的資料只會遭到軟性刪除，且會一直保留，直到程式結束為止，之後資料就會遭到硬性刪除。 |
| 已更新設定檔計數 | 30 小時 | 如果某些設定檔的所有元件屬性皆系結至該資料集，系統可能會根據要刪除的資料集內容將其移除。 刪除資料集30小時後，所有導致的設定檔總數變更都會反映在 [控制面板小工具](../dashboards/guides/profiles.md#profile-count-trend) 和其他報告。 |
| 已更新區段 | 48 小時 | 更新所有受影響的設定檔後，所有相關 [區段](../segmentation/home.md) 會更新以反映其新大小。 根據已移除的資料集和您要分段的屬性，每個區段的大小可能會因刪除而增加或減少。 |
| 已更新歷程和目的地 | 50 小時 | [歷程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [行銷活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)，和 [目的地](../destinations/home.md) 會根據相關區段的變更而更新。 |
| 硬刪除完成 | 14 天 | 與資料集相關的所有資料都會從資料湖中硬性刪除。 此 [衛生工作狀況](./ui/browse.md#view-details) 會更新刪除資料集的資訊，以反映此情況。 |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 後續步驟

本檔案概述Platform的資料衛生功能。 若要開始在UI中提出資料衛生請求，請參閱 [UI指南](./ui/overview.md). 若要了解如何以程式設計方式建立資料衛生工作，請參閱 [資料衛生API指南](./api/overview.md)
