---
keywords: Experience Platform；下載分數；customer ai；熱門主題；匯出；匯出；customer ai下載；customer ai分數
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 在Customer AI中下載分數
topic-legacy: Downloading scores
description: Customer AI可讓您下載Parquet檔案格式的分數。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 165e5ccae5ca78b3912fef1ba0b3fd4567e231fb
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# 在Customer AI中下載分數

本檔案可做為下載Customer AI分數的指南。

## 快速入門

Customer AI可讓您下載Parquet檔案格式的分數。 本教學課程需要您已閱讀並完成下載的Customer AI分數區段，位於 [快速入門](../getting-started.md) 指南。

此外，若要存取Customer AI的分數，您必須有一個可使用成功執行狀態的服務執行個體。 若要建立新的服務例項，請造訪 [設定Customer AI例項](./configure.md). 如果您最近建立了一個服務實例，但該實例仍在訓練和分數中，請允許24小時以完成運行。

目前，有兩種方式可下載Customer AI分數：

1. 如果您想要在個別層級下載分數，且/或未啟用「即時客戶設定檔」，請先導覽至 [尋找資料集ID](#dataset-id).
2. 如果您已啟用「設定檔」，且想要下載已使用Customer AI設定的區段，請導覽至 [下載已設定Customer AI的區段](#segment).

## 尋找資料集ID {#dataset-id}

在您的Customer AI分析服務例項中，按一下 *更多動作* 右上方導覽的下拉式清單，然後選取 **[!UICONTROL 存取分數]**.

![更多動作](../images/insights/more-actions.png)

隨即出現新的對話方塊，其中包含下載分數檔案的連結以及您目前執行個體的資料集ID。 將資料集ID複製到剪貼簿，然後繼續下一步。

![資料集 ID](../images/download-scores/access-scores.png)

## 擷取批次ID {#retrieve-your-batch-id}

若要使用上一步驟的資料集ID，您必須呼叫目錄API，才能擷取批次ID。 此API呼叫會使用其他查詢參數，以傳回最新成功批次，而非屬於您組織的批次清單。 要返回附加批，請將限制查詢參數的數量增加到希望返回的所需數量。 如需可用查詢參數類型的詳細資訊，請參閱 [使用查詢參數篩選目錄資料](../../../catalog/api/filter-data.md).

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「存取分數」對話方塊中可用的資料集ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含批次ID物件的裝載。 在此範例中，傳回物件的索引鍵值為批次ID `01E5QSWCAASFQ054FNBKYV6TIQ`. 複製您的批次ID以用於下一個API呼叫。

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## 使用您的批次ID擷取下一個API呼叫 {#retrieve-the-next-api-call-with-your-batch-id}

取得批次ID後，您就可以向 `/batches`. 請求會傳回一個連結，用作下一個API請求。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步驟中擷取的批次ID [擷取批次ID](#retrieve-your-batch-id). |

**要求**

使用您自己的批次ID，提出下列要求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含 `_links` 物件。 在 `_links` 物件是 `href` 以新API呼叫作為其值。 複製此值以繼續執行下一個步驟。

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## 擷取您的檔案 {#retrieving-your-files}

使用 `href` 您在上一個步驟中以API呼叫取得的值，請提出新的GET要求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id). 您也可以在 `data` 物件類型下的陣列 `dataSetFileId`. |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包含一個資料陣列，該陣列可能包含一個條目，或該目錄下的檔案清單。 以下範例包含檔案清單，並已壓縮以供閱讀。 在此案例中，您必須遵循每個檔案的URL才能存取檔案。

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| 參數 | 說明 |
| --------- | ----------- |
| `_links.self.href` | 用於下載目錄中檔案的GET要求URL。 |


複製 `href` 值 `data` 陣列，然後繼續下一步。

## 下載您的檔案資料

若要下載檔案資料，請向 `"href"` 您在上一步驟中複製的值 [擷取檔案](#retrieving-your-files).

>[!NOTE]
>
>如果您直接在命令列中提出此要求，系統可能會提示您在要求標題後新增輸出。 下列請求範例使用 `--output {FILENAME.FILETYPE}`.

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值來自 [上一步](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | 檔案的名稱。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>提出GET要求之前，請確定您所在的目錄或資料夾正確無誤，檔案才會儲存至。

**回應**

回應會下載您在目前目錄中請求的檔案。 在此範例中，檔案名稱為「filename.parquet」。

![終端](../images/download-scores/response.png)

## 下載使用Customer AI設定的區段 {#segment}

下載分數資料的另一種方法是將對象匯出至資料集。 分段作業成功完成後( `status` 屬性為「SUCCEEDED」)，您可以將對象匯出至資料集，以便存取資料集並據以處理。 若要進一步了解細分，請造訪 [細分概述](../../../segmentation/home.md).

>[!IMPORTANT]
>
>若要運用此匯出方法，必須為資料集啟用即時客戶設定檔。

此 [匯出區段](../../../segmentation/tutorials/evaluate-a-segment.md) 區段評估指南中的一節涵蓋匯出受眾資料集的必要步驟。 本指南概述並提供下列範例：

- **建立目標資料集：** 建立資料集以保留對象成員。
- **在資料集中產生對象設定檔：** 根據區段工作的結果，以XDM個別設定檔填入資料集。
- **監視導出進度：** 檢查導出進程的當前進度。
- **讀取受眾資料：** 擷取代表您對象成員的產生XDM個別設定檔。

## 後續步驟

本檔案概述下載Customer AI分數所需的步驟。 您現在可以繼續瀏覽其他 [Intelligent Services](../../home.md) 以及提供的指南。
