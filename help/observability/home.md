---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Adobe Experience Platform可觀性見解
topic: overview
description: 可觀測性洞察是REST風格的API，可讓您在Adobe Experience Platform中公開關鍵的可觀測性度量。 這些量度可提供平台使用統計資料、平台服務狀況檢查、歷史趨勢以及各種平台功能效能指標的深入資訊。
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 2%

---


# Adobe Experience Platform可觀性洞察概觀

可觀測性洞察是REST風格的API，可讓您在Adobe Experience Platform中公開關鍵的可觀測性度量。 這些量度可提供使用統 [!DNL Platform] 計資料的深入資訊、服務狀況 [!DNL Platform] 檢查、歷史趨勢，以及各種功能的效能 [!DNL Platform] 指標。

本檔案示範對Encomberity Insights API的範例呼叫。 如需完整的可觀測端點清單，請參閱可觀 [測洞察API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)。

## 快速入門

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要進行操作的沙盒名稱。 如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../sandboxes/home.md)。

* x-sandbox-name: `{SANDBOX_NAME}`

## 擷取可觀測度量

您可以在「可觀性洞察API」中對端點提出GET請求， `/metrics` 以擷取可觀性度量。

**API格式**

使用端點 `/metrics` 時，必須至少提供一個量度請求參數。 其他查詢參數是篩選結果的可選參數。

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 參數 | 說明 |
| --- | --- |
| `{METRIC}` | 您要公開的量度。 在單一呼叫中合併多個量度時，您必須使用&amp;符號(`&`)來分隔個別量度。 例如：`metric={METRIC_1}&metric={METRIC_2}`。 |
| `{ID}` | 您要公開其度 [!DNL Platform] 量的特定資源的識別碼。 此ID可能是選用、必要或不適用，視使用的量度而定。 如需每個度量的可用度量清單以及支援的ID（必要和可選），請參閱可用度量的參考 [檔案](metrics.md)。 |
| `{DATE_RANGE}` | 您要公開的量度日期範圍，使用ISO 8601格式(例如 `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`)。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回對象清單，每個對象都包含提供的時間戳和請求路徑中 `dateRange` 指定的度量的相應值。 如果請 `id` 求路 [!DNL Platform] 徑中包含資源，則結果將僅適用於該特定資源。 若省略 `id` 此項目，結果將套用至IMS組織內的所有適用資源。

```json
{
    "id": "5cf8ab4ec48aba145214abeb",
    "imsOrgId": "{IMS_ORG}",
    "timeseries": {
        "granularity": "MONTH",
        "items": [
            {
                "timestamp": "2019-06-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1125,
                    "timeseries.ingestion.dataset.size": 32320
                }
            },
            {
                "timestamp": "2019-05-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1003,
                    "timeseries.ingestion.dataset.size": 31409
                }
            },
            {
                "timestamp": "2019-04-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-03-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-02-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 390,
                    "timeseries.ingestion.dataset.size": 16801
                }
            }
        ],
        "_page": null,
        "_links": null
    },
    "stats": {}
}
```

## 後續步驟

本檔案提供可觀性分析API的概觀。 如需可用 [量度的完整清單](metrics.md) ，請參閱可用量度上的檔案。