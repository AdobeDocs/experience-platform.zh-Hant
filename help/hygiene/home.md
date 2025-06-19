---
title: 進階資料生命週期管理概觀
description: 進階資料生命週期管理可讓您更新或清除過時或不準確的記錄，進而管理資料的生命週期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 9ffd2db5555a4c157171d488deb9641aadbb08b4
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# Adobe Experience Platform中的進階資料生命週期管理

Adobe Experience Platform提供一套強大的工具，可管理大型複雜資料作業，以便協調消費者體驗。 隨著時間推移，資料會內嵌到系統中，因此管理您的資料存放區變得越來越重要，以便資料能如預期使用、在不正確的資料需要更正時更新，並在組織原則認為必要時刪除。

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

可以使用[[!UICONTROL 資料生命週期] UI工作區](#ui)或[資料衛生API](#api)來執行這些活動。 當資料生命週期工作執行時，系統會在流程的每個步驟提供透明度更新。 請參閱[時間表與透明度](#timelines-and-transparency)一節，以取得有關如何在系統中表示每種工作型別的詳細資訊。

>[!NOTE]
>
>進階資料生命週期管理支援透過[資料集到期端點](./api/dataset-expiration.md)進行資料集刪除，以及透過[工單端點](./api/workorder.md)使用主要身分的ID刪除（資料列層級資料）。 您也可以透過Experience Platform UI管理[資料集有效期](./ui/dataset-expiration.md)和[記錄刪除](./ui/record-delete.md)。 如需詳細資訊，請參閱連結的檔案。 請注意，資料生命週期不支援批次刪除。

## [!UICONTROL 資料生命週期] UI工作區 {#ui}

Experience Platform UI中的[!UICONTROL 資料生命週期]工作區可讓您設定及排程資料生命週期作業，協助確保您的記錄可如預期般維護。

如需在UI中管理資料生命週期任務的詳細步驟，請參閱[資料生命週期UI指南](./ui/overview.md)。

## 資料衛生API {#api}

[!UICONTROL 資料生命週期] UI建置在資料衛生API之上，如果您想要自動化您的資料生命週期活動，可以直接使用它的端點。 如需詳細資訊，請參閱[資料衛生API指南](./api/overview.md)。

## 時間軸和透明度 {#timelines-and-transparency}

[記錄刪除](./ui/record-delete.md)和資料集到期要求，每個都有各自的處理時間表，並在各自工作流程的關鍵點提供透明度更新。

>[!TIP]
>
>若要針對配額限制監視您目前的使用量，請參閱[配額參考指南](./api/quota.md)。\
>如需權益規則、每月上限、SLA時間表和例外狀況處理原則，請參閱[記錄刪除(UI)](./ui/record-delete.md#quotas)和[工單(API)](./api/workorder.md#quotas)檔案。

建立[資料集到期要求](./ui/dataset-expiration.md)時，會發生下列情況：

| 階段 | 排程到期之後的時間 | 說明 |
| --- | --- | --- |
| 已提交請求 | 0 小時 | 資料管理員或隱私權分析人員提交資料集在指定時間到期的請求。 提交要求後，要求會顯示在[!UICONTROL 資料生命週期UI]中，且會一直處於擱置狀態，直到排定的到期時間為止，之後要求才會執行。 |
| 資料集已標籤為刪除 | 0-2小時 | 執行請求後，資料集會標籤為刪除。 如果使用Amazon Web Services (AWS)資料儲存，此程式最多需要兩個小時。 在此期間，批次和串流細分、預覽或預估、匯出和存取等作業會忽略此資料集。 |
| 資料集已捨棄 | 3 小時 | **在資料集標示為要刪除的一小時後**，資料集就會從系統中完全移除。 此時，會從UI中的[資料集詳細目錄頁面](../catalog/datasets/user-guide.md)捨棄資料集。 不過，資料湖中的資料只會在此階段軟刪除，直到硬刪除程式完成為止。 |
| 設定檔計數已更新 | 30 小時 | 根據要刪除的資料集內容，如果某些設定檔的所有元件屬性都繫結到該資料集，則可能會從系統中將其移除。 資料集被刪除30小時後，整體設定檔計數中的任何變更都會反映在[儀表板widget](../dashboards/guides/profiles.md#profile-count-trend)和其他報表中。 |
| 已更新對象 | 48 小時 | 更新所有受影響的設定檔後，所有相關的[對象](../segmentation/home.md)都會更新，以反映其新大小。 根據移除的資料集和您進行區段的屬性，每個對象的大小可能會因刪除而增加或減少。 |
| 歷程和目的地已更新 | 50 小時 | [歷程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=zh-Hant)、[行銷活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=zh-Hant)和[目的地](../destinations/home.md)已根據相關區段的變更進行更新。 |
| 硬刪除完成 | 15 天 | 與資料集相關的所有資料都會從資料湖中硬刪除。 刪除資料集的資料生命週期工作[&#128279;](./ui/browse.md#view-details)的狀態已更新，以反映此情況。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Amazon Web Services (AWS)中的資料集刪除作業在完全套用變更前，可能會延遲約三個小時。 這包含最多2小時讓資料集標示為要刪除，接著是1小時，資料才會從系統完全刪除。 相反地，使用Azure Data Lake的Experience Platform執行個體的刪除請求會導致整個業務功能立即變更。
>
>對於AWS使用者而言，此延遲可能會影響批次細分、串流細分、預覽、預估、匯出和資料存取。 此延遲只會影響使用AWS的客戶，因為Azure Data Lake使用者會體驗立即更新。 若為AWS使用者，刪除請求可能需要長達三小時的時間，才能完全傳播至所有受影響的系統。 相應地調整您的期望。


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=zh-Hant), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=zh-Hant), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 後續步驟

本檔案概述Experience Platform的資料生命週期功能。 若要開始在UI中提出資料衛生請求，請參閱[UI指南](./ui/overview.md)。 若要瞭解如何以程式設計方式建立資料生命週期工作，請參閱[資料衛生API指南](./api/overview.md)
