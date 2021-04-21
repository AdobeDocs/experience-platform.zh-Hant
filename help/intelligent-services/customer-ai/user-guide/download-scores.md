---
keywords: Experience Platform；下載分數；客戶ai；熱門主題；導出；導出；客戶ai下載；客戶ai分數
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 在客戶人工智慧中下載分數
topic-legacy: Downloading scores
description: 客戶AI可讓您下載Parce檔案格式的分數。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 2%

---

# 在客戶人工智慧中下載分數

本檔案可做為下載客戶AI分數的指南。

## 快速入門

客戶AI可讓您下載Parce檔案格式的分數。 本教學課程要求您已閱讀並完成[快速入門](../getting-started.md)指南中的「Customer AI」（客戶AI）分數區段下載。

此外，為了存取客戶AI的分數，您需要有成功執行狀態的服務例項。 要建立新服務實例，請訪問[配置客戶AI實例](./configure.md)。 如果您最近建立了一個服務例項，但它仍在訓練和計分中，請允許24小時以完成執行。

目前，有兩種方式可下載客戶AI分數：

1. 如果您想要下載個別層級的分數，且／或未啟用即時客戶設定檔，請先導覽至[尋找資料集ID](#dataset-id)。
2. 如果您已啟用描述檔，並想要下載您使用客戶AI設定的區段，請導覽至[下載使用客戶AI設定的區段。](#segment)

## 尋找您的資料集ID {#dataset-id}

在您的客戶AI見解服務例項中，按一下右上角導覽的「更多動作&#x200B;*」下拉式清單，然後選取「**[!UICONTROL Access scores]**」。*

![更多動作](../images/insights/more-actions.png)

此時會出現新對話方塊，其中包含下載分數檔案的連結以及目前例項的資料集ID。 將資料集ID複製至剪貼簿，然後繼續下一步驟。

![資料集 ID](../images/download-scores/access-scores.png)

## 擷取您的批次ID {#retrieve-your-batch-id}

使用上一步的資料集ID，您必須呼叫目錄API以擷取批次ID。 此API呼叫會使用其他查詢參數，以傳回最新成功的批次，而非屬於您組織的批次清單。 要返回附加批，請將限制查詢參數的數量增加到希望返回的所需金額。 有關可用查詢參數類型的詳細資訊，請訪問[使用查詢參數](../../../catalog/api/filter-data.md)過濾目錄資料的指南。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「存取分數」對話方塊中提供的資料集ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含批次ID物件的裝載。 在此示例中，返回對象的鍵值是批ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 複製您的批次ID以用於下一個API呼叫。

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

## 使用您的批次ID {#retrieve-the-next-api-call-with-your-batch-id}擷取下一個API呼叫

一旦擁有批次ID，您就可以向`/batches`提出新的GET請求。 請求會傳回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步[中擷取的批次ID會擷取您的批次ID](#retrieve-your-batch-id)。 |

**要求**

使用您自己的批次ID，請提出下列要求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含`_links`對象的裝載。 在`_links`物件中是`href`，其值是新的API呼叫。 複製此值以繼續下一步。

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

## 檢索檔案{#retrieving-your-files}

使用您在上一步驟中取得的`href`值做為API呼叫，提出新的GET請求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID會從[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 在`data`陣列中，對象類型`dataSetFileId`下也可以訪問它。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包含一個資料陣列，該陣列可能包含一個條目，或是屬於該目錄的檔案清單。 以下範例包含檔案清單，並已壓縮為可讀性。 在此案例中，您必須遵循每個檔案的URL才能存取檔案。

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
| `_links.self.href` | 用於下載目錄中檔案的GET請求URL。 |


複製`data`陣列中任何檔案對象的`href`值，然後繼續執行下一步。

## 下載您的檔案資料

若要下載檔案資料，請向您在上一步驟[中複製的`"href"`值提出GET要求，以擷取您的檔案](#retrieving-your-files)。

>[!NOTE]
>
>如果您直接在命令列中提出此請求，可能會提示您在請求標題後新增輸出。 下列請求範例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID會從[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 |
| `{FILE_NAME}` | 檔案的名稱。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>在提出GET請求之前，請確定您位在您要儲存檔案的正確目錄或資料夾中。

**回應**

回應會下載您在目前目錄中要求的檔案。 在此範例中，檔案名稱為&quot;filename.parce&quot;。

![終端](../images/download-scores/response.png)

## 下載使用客戶AI {#segment}設定的區段

另一種下載分數資料的方式是將讀者匯出至資料集。 分段工作成功完成後（`status`屬性的值為&quot;SUCCEEDED&quot;），您可以將對象匯出至資料集，供您存取並執行操作。 若要進一步瞭解區段，請造訪[區段概述](../../../segmentation/home.md)。

>[!IMPORTANT]
>
>為了運用此匯出方法，資料集需要啟用即時客戶設定檔。

區段評估指南中的[匯出區段](../../../segmentation/tutorials/evaluate-a-segment.md)區段涵蓋匯出觀眾資料集的必要步驟。 本指南概述並提供下列範例：

- **建立目標資料集：** 建立資料集以容納對象成員。
- **在資料集中產生觀眾設定檔：** 根據區段工作的結果，以XDM個別設定檔填入資料集。
- **監視導出進** 度：檢查導出進程的當前進度。
- **讀取觀眾資料：** 擷取代表觀眾成員的XDM個人設定檔。

## 後續步驟

本檔案概述下載客戶AI分數所需的步驟。 您現在可以繼續瀏覽其他提供的[智慧型服務](../../home.md)和參考線。
