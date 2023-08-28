---
keywords: Experience Platform；啟動；疑難排解；護欄；指引；限制
title: 啟用資料的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 進一步瞭解資料啟用預設使用量和速率限制。
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 0835021523a7eb1642a6dbcb24334eac535aaa6d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 1%

---

# 啟用資料的護欄

此頁面提供啟動行為的預設使用量和速率限制。 檢閱下列護欄時，系統假設您已正確設定 [已連線至目的地](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 大多數客戶不會超過這些預設限制。 如果您想瞭解自訂限制，請聯絡客戶服務代表。
>* 本檔案中所概述的限制會持續改善。 請定期回來檢視更新。
>* 根據個別下游限制，某些目的地的護欄可能會比此頁面上記錄的護欄更嚴格。 也請務必檢查 [目錄](/help/destinations/catalog/overview.md) 您連線並啟用資料的目標頁面。

## 限制型別 {#limit-types}

本檔案有兩種預設限制：

* **軟性限制：** 可以超越軟性限制，但軟性限制提供系統效能的建議指引。
* **硬限制：** 硬限制可提供絕對最大值。 Experience PlatformUI或API不允許您超出此限制，否則會在您超出此限制時傳回錯誤。


## 啟用限制 {#activation-limits}

在將即時客戶設定檔資料啟用至目的地時，下列護欄會提供建議的限制。

### 一般啟動護欄 {#general-activation-guardrails}

以下護欄通常適用於透過啟動 [所有目的地型別](/help/destinations/destination-types.md#destination-types).

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 單一目的地的受眾數量上限 | 250 | 柔光 | 建議將最多250個對象對應至資料流中的單一目的地。 <br><br> 如果您需要針對一個目的地啟用超過250個對象，您可以： <ul><li> 取消對應您不想再啟用的對象，或</li><li>建立新資料流到所需的目的地，並將對象對應到這個新資料流。</li></ul> <br> 請注意，在某些目的地的情況下，您對應至目的地的對象可能限制在250個以下。 這些目的地將在頁面下方各自的區段中進一步說明。 |
| 對應到目的地的屬性數目上限 | 50 | 柔光 | 如果有多種目的地和目的地型別，您可以選取要對應以匯出的設定檔屬性和身分。 為獲得最佳效能，在資料流中應將最多50個屬性對應到目的地。 |
| 目的地數量上限 | 100 | 強烈 | 您可以建立最多100個目的地，以便連線並啟用資料， *每個沙箱*. [邊緣個人化目的地（自訂個人化）](#edge-destinations-activation) 在100個建議的目的地中，最多可以組成10個。 |
| 啟用至目的地的資料型別 | 設定檔資料，包括身分和身分對應 | 強烈 | 目前只能匯出 *設定檔記錄屬性* 至目的地。 說明事件資料的XDM屬性目前不支援匯出。 |
| 啟用至目的地的資料型別 — 陣列和對應屬性支援 | 未提供 | 強烈 | 目前為 **非** 可匯出 *陣列或對應屬性* 至目的地。 此規則的例外情況是 [身分對應](/help/xdm/field-groups/profile/identitymap.md)，這會在串流和檔案型啟用中匯出。 |

{style="table-layout:auto"}

### 串流啟用 {#streaming-activation}

以下護欄適用於透過啟動 [串流目的地](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 每秒的啟用數目（包含設定檔匯出的HTTP訊息） | 不適用 | - | 目前每秒從Experience Platform傳送至合作夥伴目的地API端點的訊息數沒有限制。 <br> 任何限制或延遲皆由Experience Platform傳送資料的端點指定。 也請務必檢查 [目錄](/help/destinations/catalog/overview.md) 您連線並啟用資料的目標頁面。 |

{style="table-layout:auto"}

### 批次（檔案式）啟用 {#batch-file-based-activation}

以下護欄適用於透過啟動 [批次（以檔案為基礎）目的地](/help/destinations/ui/activate-batch-profile-destinations.md).

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 啟用頻率 | 每3、6、8或12小時進行一次每日完整匯出或更頻繁的增量匯出。 | 強烈 | 閱讀 [匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 檔案區段，以取得批次匯出頻率遞增的詳細資訊。 |
| 在指定小時可匯出的受眾數上限 | 100 | 柔光 | 建議您將最多100個對象新增到批次目的地資料流。 |
| 要啟用的每個檔案的最大列數（記錄） | 500萬 | 強烈 | Adobe Experience Platform會自動將匯出的檔案分割為每個檔案500萬筆記錄（列）。 每一列代表一個設定檔。 分割檔案名稱會附加一個數字，指示檔案是較大匯出的一部分，例如： `filename.csv`， `filename_2.csv`， `filename_3.csv`. 如需詳細資訊，請閱讀 [排程區段](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 啟動batch destinations教學課程的。 |

{style="table-layout:auto"}

### 臨機啟動 {#ad-hoc-activation}

以下護欄適用於 [臨機啟動](/help/destinations/api/ad-hoc-activation-api.md) 方法。

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 根據臨機操作啟用工作啟用的對象 | 80 | 強烈 | 目前，每個隨選啟動工作最多可啟動80個對象。 嘗試為每個工作啟用超過80個對象會導致工作失敗。 未來版本可能會對此行為有所變更。 |
| 每個受眾同時進行的臨機啟動工作 | 1 | 強烈 | 請勿對每個對象同時執行多個臨機操作啟用工作。 |

{style="table-layout:auto"}

### 邊緣個人化目的地啟用 {#edge-destinations-activation}

以下護欄適用於透過啟動 [邊緣個人化目的地](/help/destinations/destination-types.md#streaming-profile-export).

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 最大數量 [自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md) 目的地 | 10 | 柔光 | 您可以將資料流設定為每個沙箱10個自訂個人化目的地。 |
| 每個沙箱對應至個人化目的地的最大屬性數量 | 30 | 強烈 | 每個沙箱在資料流中最多可以將30個屬性對應到個人化目的地。 |
| 對應至單一的最大受眾數量 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目的地 | 50 | 柔光 | 您可以在至單一Adobe Target目的地的啟用流程中啟用最多50個對象。 |

{style="table-layout:auto"}

### [!BADGE 測試版]{type=Informative}資料集匯出 {#dataset-exports}

目前支援的資料集匯出功能有 **[!UICONTROL 先完整再增量]** [圖樣](/help/destinations/ui/export-datasets.md#scheduling). 本節所述的護欄適用於資料集匯出工作流程設定後發生的首次完整匯出。

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 匯出的資料集大小 | 50億筆記錄 | 柔光 | 此處所述的資料集匯出限製為 *軟式護欄*. 例如，雖然使用者介面不會阻止您匯出超過50億筆記錄的資料集，但行為無法預測，且匯出可能會失敗或發生很長的匯出延遲。 |

{style="table-layout:auto"}

<!--

### Dataset Types {#dataset-types}

Datasets exported from Experience Platform can be of two types, as described below:

**Timeseries**
Timeseries datasets are also known as *XDM Experience Events* datasets in Experience Platform terminology.
The dataset schema includes a top level *timestamp* column. Data is ingested in an append-only fashion.

**Record** 
Record datasets are also known as *XDM Individual Profile* datasets in Experience Platform terminology.
The dataset schema does not include a top level *timestamp* column. Data is ingested in upsert fashion.

The guardrails below are grouped by the format of the exported file, and then further by dataset type.

**Parquet output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| Record | N/A | Five billion records per file | Only the data from the last seven days is exported. |

{style="table-layout:auto"}

**JSON output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| <p>Record</p> | <p><ul><li>Yes</li><li>No</li></ul></p> | <p><ul><li>Five billion records per compressed file</li><li>One million records per uncompressed file</li></ul></p> | <p>The record count of the dataset must be less than five billion for compressed files and one million for uncompressed files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</p> |

{style="table-layout:auto"}

-->

<!--

<table>
<thead>
  <tr>
    <th>Output format</th>
    <th>Dataset type</th>
    <th>Compression</th>
    <th>Guardrail</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Parquet</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td>Record</td>
    <td>-</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td rowspan="3">JSON</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td rowspan="2">Record</td>
    <td>Yes</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td>No</td>
    <td>One million records per file</td>
    <td>The record count of the dataset must be less than one million, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
</tbody>
</table>

-->

### Destination SDK護欄 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 是一套設定API，可讓您根據您選擇的資料和驗證格式，設定Experience Platform的目的地整合模式，以將對象和設定檔資料傳送至您的端點。 以下護欄適用於您使用Destination SDK設定的目的地。

| 護欄 | 限制 | 限制型別 | 說明 |
| --- | --- | --- | --- |
| 最大數量 [私人自訂目的地](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 柔光 | 您可以使用Destination SDK建立最多5個私人自訂串流或批次目的地。 如果您需要建立超過5個這類目的地，請聯絡自訂服務代表。 |
| Destination SDK的設定檔匯出原則 | <ul><li>`maxBatchAgeInSecs` （最小1.800，最大3.600）</li><li>`maxNumEventsInBatch` （最小1.000，最大10.000）</li></ul> | 強烈 | 使用時 [可設定的彙總](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 您目的地的選項，請留意決定HTTP訊息傳送至API型目的地頻率的最小和最大值，以及訊息應包含多少設定檔。 |

{style="table-layout:auto"}

### 目的地節流並重試原則 {#destination-throttling-and-retry-policy}

有關指定目的地的節流臨界值或限制的詳細資訊。 本節也提供有關目的地重試原則的資訊。

| 目的地型別 | 說明 |
| --- | --- |
| 企業目的地(HTTP API、Amazon Kinesis、Azure EventHubs) | 在95%的時間中，Experience Platform會嘗試為成功傳送的訊息提供少於10分鐘的輸送量延遲，每個資料流到企業目的地的每秒請求率少於10,000個。 <br> 如果對您的企業目的地的請求失敗，Experience Platform會儲存失敗的請求，並重試兩次以將請求傳送至您的端點。 |

{style="table-layout:auto"}

## 其他Experience Platform服務的護欄 {#guardrails-other-services}

檢視其他Experience Platform服務的護欄資訊：

* 護欄 [資料擷取](/help/ingestion/guardrails.md)
* 護欄 [[!DNL Identity Service] 資料](/help/identity-service/guardrails.md)
* 護欄 [[!DNL Real-Time Customer Profile] 資料](/help/profile/guardrails.md)
* 護欄 [[!DNL Query Service] 資料](/help/query-service/guardrails.md)
