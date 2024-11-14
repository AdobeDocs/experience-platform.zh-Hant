---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 量度API端點
description: 瞭解如何使用可觀察性深入分析API在Experience Platform中擷取可觀察性量度。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: bd5018a2d867d0483f3f2f0c45e356ea69a01801
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 3%

---

# 量度端點

可觀察性量度可為Adobe Experience Platform中的各種功能提供使用統計資料、歷史趨勢和績效指標的深入分析。 [!DNL Observability Insights API]中的`/metrics`端點可讓您以程式設計方式擷取[!DNL Platform]中組織活動的量度資料。

>[!NOTE]
>
>先前版本的量度端點(V1)已被取代。 本檔案僅針對目前版本(V2)。 如需舊版實作之V1端點的詳細資訊，請參閱[API參考](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1)。

## 快速入門

本指南中使用的API端點是[[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 擷取可觀察性量度

您可以向`/metrics`端點發出POST要求，指定您要在裝載中擷取的量度，以擷取量度資料。

**API格式**

```http
POST /metrics
```

**要求**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `start` | 擷取量度資料的最早日期/時間。 |
| `end` | 擷取量度資料的最新日期/時間。 |
| `granularity` | 選擇性欄位，指出度量資料除以的時間間隔。 例如，值`DAY`會傳回`start`與`end`日期之間每天的量度，而值`MONTH`會改為依月份群組量度結果。 |
| `metrics` | 一個物件陣列，您要擷取的每個量度各一個。 |
| `name` | 「可觀察性深入分析」所識別的量度名稱。 如需接受的量度名稱完整清單，請參閱[附錄](#available-metrics)。 |
| `filters` | 此選用欄位可讓您依據特定資料集篩選量度。 欄位是一個物件陣列（每個濾鏡各一個），每個物件包含下列屬性： <ul><li>`name`：篩選量度的實體型別。 目前僅支援`dataSets`。</li><li>`value`：一或多個資料集的識別碼。 多個資料集ID可以單一字串形式提供，每個ID都以垂直長條字元(`\|`)分隔。</li><li>`groupBy`：設定為true時，表示對應的`value`代表多個資料集，這些資料集的量度結果應分別傳回。 如果設為false，這些資料集的量度結果會分組在一起。</li></ul> |
| `aggregator` | 指定應該用來將多個時間序列記錄分組為單一結果的彙總函式。 目前支援的彙總值為最小值、最大值、總和以及平均，視量度定義而定。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回要求中所指定量度和篩選器的結果資料點。

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `metricResponses` | 陣列，其物件代表要求中指定的每個度量。 每個物件都包含有關篩選器設定和傳回量度資料的資訊。 |
| `metric` | 請求中提供的其中一個量度的名稱。 |
| `filters` | 指定量度的篩選器設定。 |
| `datapoints` | 陣列，其物件代表指定量度和篩選器的結果。 陣列中的物件數目取決於請求中提供的篩選選項。 如果未提供篩選器，則陣列將僅包含代表所有資料集的單一物件。 |
| `groupBy` | 如果在量度的`filter`屬性中指定了多個資料集，且請求中的`groupBy`選項設定為true，則此物件將包含對應`dps`屬性套用的資料集識別碼。<br><br>如果此物件在回應中顯示為空白，則對應的`dps`屬性會套用至`filters`陣列中提供的所有資料集（如果未提供篩選器，則套用至[!DNL Platform]中的所有資料集）。 |
| `dps` | 針對指定的量度、篩選器及時間範圍傳回的資料。 此物件中的每個索引鍵都代表時間戳記，其中包含指定量度的對應值。 每個資料點之間的時間長度取決於要求中指定的`granularity`值。 |

{style="table-layout:auto"}

## 附錄

以下區段包含使用`/metrics`端點的其他資訊。

### 可用量度 {#available-metrics}

下表列出[!DNL Observability Insights]公開的所有度量，並依[!DNL Platform]服務劃分。 每個量度都包含說明和接受的ID查詢引數。

>[!NOTE]
>
>除非另有說明，否則所有列出的ID查詢引數均為選用引數。

#### [!DNL Data Ingestion] {#ingestion}

下表概述Adobe Experience Platform [!DNL Data Ingestion]的量度。 **bold**&#x200B;中的量度為串流擷取量度。

| 分析量度 | 說明 | ID查詢引數 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | 針對一個資料集或所有資料集擷取的所有資料累積大小。 | 資料集 ID |
| timeseries.ingestion.dataset.dailysize | 針對一個資料集或所有資料集根據每日使用量擷取的資料大小。 | 資料集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一個資料集或所有資料集失敗的批次數量。 | 資料集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 針對一個資料集或所有資料集擷取的批次數。 | 資料集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 為一個資料集或所有資料集擷取的記錄數。 | 資料集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一個資料集或所有資料集的無效「存在」訊息總數。 | 資料集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 針對一個資料輸入或所有資料輸入接收的訊息總數。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 針對一個資料匯入或所有資料匯入接收的資料總大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 對單一資料輸入或所有資料輸入的成功HTTP呼叫總數。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 對單一資料輸入或所有資料輸入失敗的HTTP呼叫總數。 | 入口ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

下表概述Adobe Experience Platform [!DNL Identity Service]的量度。

| 分析量度 | 說明 | ID查詢引數 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 針對一個資料集或所有資料集，[!DNL Identity Service]寫入其資料來源的記錄數。 | 資料集 ID |
| timeseries.identity.dataset.recordfailed.count | 一個資料集或所有資料集的[!DNL Identity Service]失敗的記錄數。 | 資料集 ID |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 略過的身分記錄數。 | 組織 ID |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 儲存在組織身分圖表中的唯一身分數量。 | 不適用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 儲存在名稱空間身分圖表中的唯一身分數目。 | 名稱空間ID （**必要**） |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 針對特定圖表強度（「未知」、「弱」或「強」）儲存在身分圖表中的獨特身分數。 | 圖表強度（**必要**） |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

下表概述[!DNL Real-Time Customer Profile]的量度。

| 分析量度 | 說明 | ID查詢引數 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | [!DNL Profile]從[!DNL Data Lake]讀取的記錄數（針對一個資料集或所有資料集）。 | 資料集 ID |
| timeseries.profiles.dataset.recordsuccess.count | [!DNL Profile]針對一個資料集或所有資料集寫入其資料來源的記錄數。 | 資料集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 為資料集或所有資料集擷取的[!DNL Profile]批次數量。 | 資料集 ID |

{style="table-layout:auto"}

### 錯誤訊息

在某些條件下，來自`/metrics`端點的回應可能會傳回錯誤訊息。 這些錯誤訊息會以下列格式傳回：

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `title` | 包含錯誤訊息及其可能原因的字串。 |
| `report` | 包含有關錯誤的內容相關資訊，包括觸發錯誤的作業中所使用的沙箱和組織。 |

{style="table-layout:auto"}

下表列出API可傳回的不同錯誤代碼：

| 錯誤代碼 | 標題 | 說明 |
| --- | --- | --- |
| `INSGHT-1000-400` | 錯誤的請求承載 | 請求承載發生問題。 請確定您完全符合以上所示的裝載格式[](#v2)。 觸發此錯誤的可能原因有：<ul><li>遺失必要欄位，例如`aggregator`</li><li>無效的量度</li><li>請求包含無效彙總</li><li>開始日期發生在結束日期之後</li></ul> |
| `INSGHT-1001-400` | 量度查詢失敗 | 嘗試查詢量度資料庫時發生錯誤，因為錯誤請求或查詢本身無法剖析。 在重試之前，請確定您的請求已正確格式化。 |
| `INSGHT-1001-500` | 量度查詢失敗 | 由於伺服器錯誤，嘗試查詢量度資料庫時發生錯誤。 請再次嘗試該請求，如果問題仍然存在，請聯絡Adobe支援。 |
| `INSGHT-1002-500` | 服務錯誤 | 由於內部錯誤，無法處理請求。 請再次嘗試該請求，如果問題仍然存在，請聯絡Adobe支援。 |
| `INSGHT-1003-401` | 沙箱驗證錯誤 | 由於沙箱驗證錯誤，無法處理請求。 在重試請求之前，請確定您在`x-sandbox-name`標頭中提供的沙箱名稱代表貴組織啟用的有效沙箱。 |

{style="table-layout:auto"}
