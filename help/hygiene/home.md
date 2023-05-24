---
title: 資料衛生概述
description: Adobe Experience Platform資料衛生服務允許您通過更新或清除過時或不準確的記錄來管理資料的生命週期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 2913e9e687843e566db4ebf2031e610d1891d4c9
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Adobe Experience Platform資料衛生

>[!IMPORTANT]
>
>目前，資料衛生功能僅適用於已購買的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**。 這些功能將在不久的將來發佈。 有關他們即將上市的更多資訊，請與您的Adobe服務代表聯繫。 但是，你可以馬上 [刪除資料集 [!UICONTROL 資料集] UI](../catalog/datasets/user-guide.md#delete)。

Adobe Experience Platform公司提供一套強大的工具來管理大型、複雜的資料操作，以協調消費者體驗。 隨著資料逐漸被引入系統，管理資料儲存變得越來越重要，這樣資料就可以按預期使用，當不正確的資料需要更正時更新，當組織策略認為有必要時刪除。

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

這些活動可以使用 [[!UICONTROL 資料衛生] UI工作區](#ui) 或 [資料衛生API](#api)。 當資料衛生作業執行時，系統在處理的每個步驟提供透明度更新。 請參閱 [時間表和透明度](#timelines-and-transparency) 的子菜單。

## [!UICONTROL 資料衛生] UI工作區 {#ui}

的 [!UICONTROL 資料衛生] 平台UI中的工作區允許您配置和安排資料衛生操作，從而幫助確保記錄按預期進行維護。

有關在UI中管理資料衛生任務的詳細步驟，請參見 [資料衛生UI指南](./ui/overview.md)。

## 資料衛生API {#api}

的 [!UICONTROL 資料衛生] UI構建在資料衛生API之上，如果您希望自動執行資料衛生活動，其端點可供您直接使用。 查看 [資料衛生API指南](./api/overview.md) 的子菜單。

## 時間表和透明度

記錄刪除和資料集過期請求每個都有自己的處理時間表，並在其各自工作流的關鍵點提供透明度更新。

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

以下是 [資料集過期請求](./ui/dataset-expiration.md) 已建立：

| 測試 | 計畫到期後的時間 | 說明 |
| --- | --- | --- |
| 請求已提交 | 0 小時 | 資料管理員或隱私分析員提交資料集在給定時間過期的請求。 請求在 [!UICONTROL 資料衛生UI] 在提交後，並且一直處於掛起狀態，直到計畫到期時間，在此時間後，請求將執行。 |
| 已刪除資料集 | 1 小時 | 從 [資料集清單頁](../catalog/datasets/user-guide.md) 的子菜單。 資料湖中的資料只是軟刪除，並且將一直保留到過程結束，之後將硬刪除。 |
| 已更新配置檔案計數 | 30 小時 | 根據要刪除的資料集的內容，如果某些配置檔案的所有元件屬性都與該資料集關聯，則可能會從系統中刪除這些配置檔案。 在刪除資料集30小時後，在總體配置檔案計數中出現的任何更改都反映在 [儀表板小部件](../dashboards/guides/profiles.md#profile-count-trend) 等報告。 |
| 已更新段 | 48 小時 | 更新所有受影響的配置檔案後，所有相關 [段](../segmentation/home.md) 更新以反映其新大小。 根據刪除的資料集和要分割的屬性，每個段的大小可能會因刪除而增加或減少。 |
| 更新的旅程和目的地 | 50 小時 | [旅程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html)。 [活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), [目的地](../destinations/home.md) 會根據相關分類之變動而更新。 |
| 硬刪除完成 | 14 天 | 與資料集相關的所有資料都從資料湖中硬刪除。 的 [衛生工作的狀況](./ui/browse.md#view-details) 將更新刪除資料集以反映這一點。 |

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

本文檔概述了平台的資料衛生功能。 要開始在UI中發出資料衛生請求，請參閱 [UI指南](./ui/overview.md)。 要瞭解如何以寫程式方式建立資料衛生作業，請參閱 [資料衛生API指南](./api/overview.md)
