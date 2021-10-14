---
keywords: Experience Platform；下載分數；customer ai；熱門主題；匯出；匯出；customer ai下載；customer ai分數
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 在Customer AI中下載分數
topic-legacy: Downloading scores
description: Customer AI可讓您下載Parquet檔案格式的分數。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# 在Customer AI中下載分數

本檔案可做為下載Customer AI分數的指南。

## 快速入門

Customer AI可讓您下載Parquet檔案格式的分數。 本教學課程需要您閱讀並完成[getting started](../getting-started.md)指南中的下載Customer AI分數區段。

此外，若要存取Customer AI的分數，您必須有一個服務執行個體，其成功的執行狀態可用。 若要建立新服務例項，請造訪[設定Customer AI例項](./configure.md)。 如果您最近建立了一個服務實例，但該實例仍在訓練和分數中，請允許24小時以完成運行。

目前，有兩種方式可下載Customer AI分數：

1. 如果您想要在個別層級下載分數，且/或未啟用「即時客戶設定檔」，請導覽至[尋找資料集ID](#dataset-id)開始。
2. 如果您已啟用「設定檔」，且想要下載已使用Customer AI設定的區段，請導覽至[下載已使用Customer AI](#segment)設定的區段。

## 尋找資料集ID {#dataset-id}

在您的Customer AI深入分析服務例項中，按一下右上方導覽中的&#x200B;*更多動作*&#x200B;下拉式清單，然後選取&#x200B;**[!UICONTROL 存取分數]**。

![更多動作](../images/insights/more-actions.png)

隨即出現新的對話方塊，其中包含下載分數檔案的連結以及您目前執行個體的資料集ID。 將資料集ID複製到剪貼簿，然後繼續下一步。

![資料集 ID](../images/download-scores/access-scores.png)

## 擷取批次ID {#retrieve-your-batch-id}

若要使用上一步驟的資料集ID，您必須呼叫目錄API，才能擷取批次ID。 此API呼叫會使用其他查詢參數，以傳回最新成功批次，而非屬於您組織的批次清單。 要返回附加批，請將限制查詢參數的數量增加到希望返回的所需數量。 有關可用查詢參數類型的詳細資訊，請訪問有關使用查詢參數](../../../catalog/api/filter-data.md)篩選目錄資料的指南。[

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含批次ID物件的裝載。 在此示例中，返回對象的鍵值為批ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 複製您的批次ID以用於下一個API呼叫。

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

取得批次ID後，您就可以向`/batches`提出新的GET請求。 請求會傳回一個連結，用作下一個API請求。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在前一個步驟[中檢索的批ID](#retrieve-your-batch-id)檢索批ID。 |

**要求**

使用您自己的批次ID，提出下列要求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含`_links`物件的裝載。 在`_links`物件內是`href`，其值是新的API呼叫。 複製此值以繼續執行下一個步驟。

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

使用您在上一步取得的`href`值作為API呼叫，提出新GET要求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在`href`值中，從上一步[返回dataSetFile ID](#retrieve-the-next-api-call-with-your-batch-id)。 也可在`data`陣列中的對象類型`dataSetFileId`下訪問。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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


複製`data`陣列中任何檔案對象的`href`值，然後繼續下一步。

## 下載您的檔案資料

若要下載檔案資料，請對您在前一個步驟[中複製的`"href"`值提出GET請求，以擷取您的檔案](#retrieving-your-files)。

>[!NOTE]
>
>如果您直接在命令列中提出此要求，系統可能會提示您在要求標題後新增輸出。 下列要求範例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在`href`值中，從前一個步驟[返回dataSetFile ID](#retrieve-the-next-api-call-with-your-batch-id)。 |
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
>提出GET要求之前，請確定您所在的目錄或資料夾正確無誤，檔案才會儲存至。

**回應**

回應會下載您在目前目錄中請求的檔案。 在此範例中，檔案名稱為「filename.parquet」。

![終端](../images/download-scores/response.png)

## 下載使用Customer AI設定的區段 {#segment}

下載分數資料的另一種方法是將對象匯出至資料集。 分段工作成功完成後（`status`屬性的值為「SUCCEEDED」），您可以將對象匯出至資料集，以便存取資料集並加以處理。 若要深入了解分段，請造訪[分段概觀](../../../segmentation/home.md)。

>[!IMPORTANT]
>
>若要運用此匯出方法，必須為資料集啟用即時客戶設定檔。

區段評估指南中的[匯出區段](../../../segmentation/tutorials/evaluate-a-segment.md)區段涵蓋匯出對象資料集的必要步驟。 本指南概述並提供下列範例：

- **建立目標資料集：** 建立資料集以保留對象成員。
- **在資料集中產生對象設定檔：** 根據區段工作的結果，以XDM個別設定檔填入資料集。
- **監控匯出進度：** 檢查匯出程式的目前進度。
- **讀取對象資料：** 擷取代表對象成員的產生XDM個別設定檔。

## 後續步驟

本檔案概述下載Customer AI分數所需的步驟。 您現在可以繼續瀏覽其他提供的[智慧服務](../../home.md)和指南。
