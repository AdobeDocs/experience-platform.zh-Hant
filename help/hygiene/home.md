---
title: 進階資料生命週期管理概觀
description: 進階資料生命週期管理可讓您更新或清除過時或不準確的記錄，進而管理資料的生命週期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: adba9d3cd979f655f477d2d80ed3e55e96fbe486
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 2%

---

# Adobe Experience Platform中的進階資料生命週期管理

Adobe Experience Platform提供一套強大的工具，可管理大型複雜資料作業，以便協調消費者體驗。 隨著時間推移，資料會內嵌到系統中，因此管理您的資料存放區變得越來越重要，以便資料能如預期使用、在不正確的資料需要更正時更新，並在組織原則認為必要時刪除。

可以使用[[!UICONTROL Data Lifecycle] UI工作區](#ui)或[資料衛生API](#api)來執行這些活動。 當資料生命週期工作執行時，系統會在流程的每個步驟提供透明度更新。 請參閱[時間表與透明度](#timelines-and-transparency)一節，以取得有關如何在系統中表示每種工作型別的詳細資訊。

>[!NOTE]
>
>進階資料生命週期管理支援透過[資料集到期端點](./api/dataset-expiration.md)進行資料集刪除，以及透過[工單端點](./api/workorder.md)使用主要身分的ID刪除（資料列層級資料）。 您也可以透過Experience Platform UI管理[資料集有效期](./ui/dataset-expiration.md)和[記錄刪除](./ui/record-delete.md)。 如需詳細資訊，請參閱連結的檔案。 請注意，資料生命週期不支援批次刪除。

## [!UICONTROL Data Lifecycle] UI工作區 {#ui}

Experience Platform UI中的[!UICONTROL Data Lifecycle]工作區可讓您設定及排程資料生命週期作業，協助確保您的記錄可如預期般維護。

如需在UI中管理資料生命週期任務的詳細步驟，請參閱[資料生命週期UI指南](./ui/overview.md)。

## 資料衛生API {#api}

[!UICONTROL Data Lifecycle] UI建置在資料衛生API之上，如果您想要自動化您的資料生命週期活動，可以直接使用其端點。 如需詳細資訊，請參閱[資料衛生API指南](./api/overview.md)。

## 時間軸和透明度 {#timelines-and-transparency}

[記錄刪除](./ui/record-delete.md)和資料集到期要求，每個都有各自的處理時間表，並在各自工作流程的關鍵點提供透明度更新。

>[!TIP]
>
>如需其他參考資訊：
>- 若要針對配額限制監視您目前的使用量，請參閱[配額參考指南](./api/quota.md)。
>- 如需權利規則、每月上限、SLA時間表和例外狀況處理原則，請參閱[記錄刪除配額指南(UI)](./ui/record-delete.md#quotas)和[工作單配額指南(API)](./api/workorder.md#quotas)。

建立[資料集到期要求](./ui/dataset-expiration.md)時，會發生下列情況：

| 階段 | 排程到期之後的時間 | 說明 |
| --- | --- | --- |
| 已提交請求 | 0 小時 | 資料管理員或隱私權分析人員提交資料集在指定時間到期的請求。 提交要求後，[!UICONTROL Data Lifecycle UI]中會顯示該要求，而且會一直保持擱置狀態，直到排定的到期時間為止，之後要求才會執行。 |
| 從資料湖捨棄資料集 | 1 小時 | 從UI中的[資料集詳細目錄頁面](../catalog/datasets/user-guide.md)捨棄資料集。 Data Lake中的資料只會軟刪除，並將一直保留至程式結束，之後會硬刪除。 |
| 資料集已從設定檔服務中刪除 | 3 小時 | 從這時開始，批次和串流分段、預覽或估計、匯出和實體存取等作業將不再從此資料集中讀取資料。 設定檔服務中的資料只會軟刪除，並將一直保留到流程結束為止，之後將硬刪除。 |
| 設定檔計數和對象已更新 | 48 小時 | 更新所有受影響的設定檔後，所有相關的[對象](../segmentation/home.md)都會更新，以反映其新大小。 根據已移除的資料集以及您正在分割的屬性，每個對象的大小可能會因刪除而增加或減少。 此時，整體設定檔計數的任何結果變更都會反映在[儀表板Widget](../dashboards/guides/profiles.md#profile-count-trend)和其他報表中。 |
| 歷程和目的地已更新 | 50 小時 | [歷程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html)、[行銷活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)和[目的地](../destinations/home.md)已根據相關區段的變更進行更新。 |
| 硬刪除完成 | 15 天 | 與資料集相關的所有資料都會從資料湖和設定檔服務中硬刪除。 刪除資料集的資料生命週期工作[&#128279;](./ui/browse.md#view-details)的狀態已更新，以反映此情況。 |

{style="table-layout:auto"}

### 記錄刪除時間表 {#record-delete-transparency}

提交[記錄刪除請求](./ui/record-delete.md)後會發生下列情況。

>[!NOTE]
>
>計時是近似值，而且會根據系統負載、批次排程和權益層級而有所不同。 端對端的SLA （Privacy and Security Shield或Healthcare Shield為30天標準、15天）是營運承諾。

| 階段 | 大約 計時 | 說明 |
| --- | --- | --- |
| 請求已提交並批次 | 第1-15天 | 工單已建立並排入佇列。 處理開始前，請求可能會排入佇列及批次最多達14天。 批次處理是不立即刪除的主要原因。 |
| 下游系統處理刪除請求 | 第16-25天 | 下游服務接收並執行記錄刪除請求。 |
| 緩衝 — 完整性檢查與重新提交 | 第25-30天 | 緩衝區視窗可用於完整性檢查，並在SLA視窗關閉前重新提交任何失敗的工作。 一旦所有系統確認刪除，工作單狀態會更新為`completed`。 |

{style="table-layout:auto"}

如需以權益為基礎的佇列持續時間和SLA值上限，請參閱[處理識別碼提交的時間表](./ui/record-delete.md#sla-processing-timelines)。

## 後續步驟 {#next-steps}

本檔案概述Experience Platform的資料生命週期功能。 若要開始在UI中提出資料衛生請求，請參閱[資料生命週期UI指南](./ui/overview.md)。 若要以程式設計方式建立資料生命週期工作，請參閱[資料衛生API指南](./api/overview.md)。
