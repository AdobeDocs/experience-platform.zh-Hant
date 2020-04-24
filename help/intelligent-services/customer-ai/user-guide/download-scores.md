---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: 在客戶人工智慧中下載分數
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 1cf1e9c814601bdd4c7198463593be78452004dc

---


# 在客戶人工智慧中下載分數

本檔案可做為下載客戶AI分數的指南。

## 快速入門

客戶AI可讓您以鑲木地板檔案格式下載分數。 本教學課程要求您已閱讀並完成快速入門手冊中的「客戶AI [分數](../getting-started.md) 」區段。

此外，為了存取客戶AI的分數，您需要有成功執行狀態的服務例項。 若要建立新的服務例項，請造 [訪設定客戶AI例項](./configure.md)。 如果您最近建立了一個服務例項，但它仍在訓練和計分中，請允許24小時以完成執行。

目前，有兩種方式可下載客戶AI分數：

1. 如果您想要在個別層級下載分數且／或未啟用即時客戶設定檔，請先導覽至尋找資料集ID [開始](#dataset-id)。
2. 如果您已啟用描述檔且想要下載您使用客戶AI設定的區段，請導覽至下 [載使用客戶AI設定的區段](#segment)。

## Find your dataset ID {#dataset-id}

在您的客戶AI見解服務例項中，按一下右上方導覽中的 *「更多動作* 」下拉式清單，然後選取 **[!UICONTROL Access scores]**。

![更多動作](../images/insights/more-actions.png)

此時會出現新對話方塊，其中包含下載分數檔案的連結以及目前例項的資料集ID。 將資料集ID複製至剪貼簿，然後繼續下一步驟。

![資料集ID](../images/download-scores/access-scores.png)

## 擷取您的批次ID {#retrieve-your-batch-id}

使用上一步的資料集ID，您必須呼叫目錄API以擷取批次ID。 此API呼叫會使用其他查詢參數，以傳回單一批次，而非屬於貴組織的批次清單。 有關可用查詢參數類型的詳細資訊，請造訪使用查詢參數篩 [選目錄資料的指南](../../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「存取分數」對話方塊中提供的資料集ID。 |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含分數批次ID物件的裝載。 In this example, the object is `5e602f67c2f39715a87f46b1`.

分數批次ID物件中是數 `relatedObjects` 組。 此陣列包含兩個對象。 第一個物件的 `type` 值為&quot;batch&quot;，也包含ID。 在以下範例回應中，批次ID為 `035e2520-5e69-11ea-b624-51evfeba55d1`。 複製您的批次ID以用於下一個API呼叫。

```json
{   
    "5e602f67c2f39715a87f46b1": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540e14cd3d0432",
                "type": "dataSet"
            },
            {
                "id": "035e2520-5e69-11ea-b624-51evfeba55d1",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsRead": 46721830,
            "recordsWritten": 46721830,
            "avgNumExecutorsPerTask": 33,
            "startTime": 1583362385336,
            "inputSizeInKb": 10242034,
            "endTime": 1583363197517
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    }
}
```

## 使用您的批次ID擷取下一個API呼叫 {#retrieve-the-next-api-call-with-your-batch-id}

在您取得批次ID後，就可以提出新的GET要求 `/batches`。 請求會傳回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步驟中擷取的批次ID會擷 [取您的批次ID](#retrieve-your-batch-id)。 |

**請求**

使用您自己的批次ID，請提出下列要求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含物件的 `_links` 裝載。 物件內 `_links` 有新 `href` 的API呼叫作為其值。 複製此值以繼續下一步。

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

使用 `href` 上一步驟中的值做為API呼叫，提出新的GET請求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 資料集檔案ID會在上一步 `href` 驟的值中 [傳回](#retrieve-the-next-api-call-with-your-batch-id)。 也可在對象類型下 `data` 的陣列中訪問 `dataSetFileId`。 |

**請求**

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
| `_links.self.href` | 用於下載目錄中檔案的GET要求URL。 |


複製數 `href` 組中任何檔案對象的值， `data` 然後繼續執行下一步。

## 下載您的檔案資料

若要下載檔案資料，請對您在上一步驟中復 `"href"` 制的檔案值提出GET [要求](#retrieving-your-files)。

>[!NOTE] 如果您直接在命令列中提出此請求，可能會提示您在請求標題後新增輸出。 以下請求範例使用 `--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 資料集檔案ID會從上一步 `href` 驟的值中 [傳回](#retrieve-the-next-api-call-with-your-batch-id)。 |
| `{FILE_NAME}` | 檔案的名稱。 |

**請求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP] 在您提出GET請求前，請確定您位於要儲存檔案的正確目錄或資料夾中。

**回應**

回應會下載您在目前目錄中要求的檔案。 在此範例中，檔案名稱為&quot;filename.parce&quot;。

![終端](../images/download-scores/response.png)

## 下載使用客戶AI設定的區段 {#segment}

另一種下載分數資料的方式是將讀者匯出至資料集。 分段工作成功完成(屬性的值為 `status` 「成功」)後，您可將對象匯出至資料集，供您存取及操作。 若要進一步瞭解區段，請造訪區 [段總覽](../../../segmentation/home.md)。

>[!IMPORTANT] 為了運用此匯出方法，資料集需要啟用即時客戶設定檔。

區 [段評估指南中的](../../../segmentation/tutorials/evaluate-a-segment.md) 「匯出區段」區段涵蓋匯出觀眾資料集的必要步驟。 本指南概述並提供下列範例：

- **建立目標資料集：** 建立資料集以容納觀眾成員。
- **在資料集中產生觀眾設定檔：** 根據區段工作的結果，以XDM個別描述檔填入資料集。
- **監視導出進度：** 檢查導出進程的當前進度。
- **讀取受眾資料：** 擷取代表觀眾成員的產生的XDM個人設定檔。

## 後續步驟

本檔案概述下載客戶AI分數所需的步驟。 您現在可以繼續瀏覽其他 [智慧型服務](../../home.md) 和參考線。
