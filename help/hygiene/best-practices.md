---
title: 進階資料生命週期管理的最佳作法
description: 瞭解如何使用進階資料生命週期管理UI和資料衛生API，有效管理Adobe Experience Platform中的資料衛生請求。 本指南涵蓋最佳實務，例如最大化每個請求的身分、指定個別資料集，以及注意API節流以防止速度變慢。 本檔案包含設定自動資料集清理的准則、如何監視工單狀態，以及詳細的回應擷取方法。 遵循這些實務來簡化您的請求處理，並最佳化回應時間。
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# 進階資料生命週期管理的最佳作法

使用進階資料生命週期管理UI和資料衛生API來有效管理清理請求，並從Adobe Experience Platform服務中移除資料。 遵循這些最佳實務來簡化您的請求處理，並最佳化完成回應時間。

## 先決條件 {#prerequisites}

本指南需要您實際瞭解資料生命週期工作區和[資料衛生API](./api/overview.md)。 在繼續本檔案之前，請先在UI[&#128279;](./ui/dataset-expiration.md)中或透過API熟悉[進階資料生命週期管理](./home.md)和[建立記錄刪除請求](./ui/record-delete.md)或資料集有效期的指南。

## 工單建立准則 {#work-order-creation-guidelines}

您可以使用資料衛生API中的`/workorder`端點，以程式設計方式管理Experience Platform中的記錄刪除請求。 使用此端點，您可以建立刪除請求、檢查其狀態或更新現有請求。 請參閱[工單端點檔案](./api/workorder.md)，瞭解如何使用API執行這些動作。

>[!TIP]
>
>工單是結構化請求，可執行特定資料管理操作，例如資料清理或轉換，以確保有效率且系統地處理。

請遵循下列准則，將清理請求提交最佳化：

1. **將每個請求的身分最大化：**&#x200B;包含每個清理請求最多100,000個身分，以提高效率。 將多個身分批次處理為單一請求有助於降低API呼叫的頻率，並將由於過多的單一身分請求而造成的效能問題風險降至最低。 以最大身分數提交請求，因為工單是以批次方式提高效率，讓處理速度更快。
2. **指定個別資料集：**&#x200B;為達到最高效率，請指定個別資料集進行處理。
3. **API節流考量事項：**&#x200B;注意API節流以防止減慢。 頻率較高的較小請求(&lt; 100 ID)可能會導致429個回應，並需要以可接受的速率重新提交。

### 管理429錯誤 {#manage-429-errors}

如果您收到429錯誤，表示您已在指定時段內超過允許的請求數。 遵循這些最佳實務來有效管理429錯誤：

- **讀取&#39;Retry-After&#39;標頭**：傳回429錯誤時，請檢查&#39;Retry-After&#39;回應標頭。 此標頭會指定重試要求前的等待時間。
- **實作重試邏輯**：使用&#39;Retry-After&#39;值在您的應用程式中實作重試邏輯，確保指定時間之後再嘗試重試以避免後續429錯誤。
- **批次處理您的請求**：請避免連續快速地提交許多小型請求。 反之，將多個身分批次處理為單一請求，以降低呼叫頻率並將達到率限制的風險降至最低。

## 資料集期限 {#dataset-expiration}

設定短期資料的自動資料集清理。 使用資料衛生API上的`/ttl`端點，根據指定的時間或日期排程資料集的清除到期日。 請參閱資料集到期端點指南，瞭解如何[建立資料集到期日](./api/dataset-expiration.md)和[接受的查詢引數](./api/dataset-expiration.md#query-params)。

## 監視工單和資料集到期狀態 {#monitor}

您可以使用&#x200B;**I/O事件**，有效監控資料生命週期管理的進度。 I/O事件是一種機制，用於接收有關Experience Platform中各種服務之變更或更新的即時通知。

I/O事件警示可以傳送至已設定的webhook，以啟用活動監視的自動化。 若要透過webhook接收警報，您必須在Adobe Developer Console中註冊Experience Platform警報的webhook。 如需詳細指示，請參閱[訂閱Adobe I/O事件通知](../observability/alerts/subscribe.md)的指南。

使用下列資料生命週期方法和准則，有效擷取和監視工作狀態：

### I/O事件 {#io-events}

若要有效監控資料生命週期工作的進度，請依照下列步驟設定及使用I/O事件：

- 設定Webhook以接收狀態變更的推播通知。
- 使用通知來監視進度並在完成時接收更新。
- 避免實作輪詢機制以最小化API流量。

### 擷取單一工單的詳細回應 {#retrieve-detailed-work-order-response}

如需個別工單的深入資訊，請使用下列方法：

- 向`/workorder/{work_order_id}`端點發出GET要求以取得詳細的回應資料。
- 擷取產品專屬回應和成功訊息。
- 請避免將此方法用於定期輪詢活動。

遵循這些最佳實務，您就能在進階資料生命週期管理中，有效管理清理請求並最佳化回應時間。
