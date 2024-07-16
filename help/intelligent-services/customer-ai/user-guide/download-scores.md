---
keywords: Experience Platform；下載分數；customer ai；熱門主題；匯出；匯出；customer ai下載；customer ai分數
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 在Customer AI中下載分數
description: Customer AI可讓您以Parquet檔案格式下載分數。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 在Customer AI中下載分數

本檔案可用作下載Customer AI分數的指南。

## 快速入門

Customer AI可讓您以Parquet檔案格式下載分數。 本教學課程要求您已閱讀並完成[快速入門](../getting-started.md)指南中的Customer AI分數下載區段。

此外，若要存取Customer AI的分數，您需要有可取得成功執行狀態的服務執行個體。 若要建立新的服務執行個體，請造訪[設定Customer AI執行個體](./configure.md)。 如果您最近已建立服務執行個體，但仍在訓練和評分中，請等待24小時讓執行完成。

目前，下載Customer AI分數有兩個方法：

1. 如果您想要下載個別層級的分數和/或未啟用即時客戶設定檔，請先導覽至[尋找您的資料集ID](#dataset-id)。
2. 如果您已啟用設定檔且想要下載您使用Customer AI設定的區段，請瀏覽至[下載使用Customer AI設定的區段](#segment)。

## 尋找您的資料集ID {#dataset-id}

在用於Customer AI深入分析的服務執行個體中，按一下右上方導覽列中的&#x200B;*更多動作*&#x200B;下拉式清單，然後選取&#x200B;**[!UICONTROL 存取分數]**。

![更多動作](../images/insights/more-actions.png)

隨即顯示新對話方塊，其中包含下載分數檔案的連結，以及目前執行個體的資料集ID。 將資料集ID複製到剪貼簿，然後繼續下一個步驟。

![資料集識別碼](../images/download-scores/access-scores.png)

## 擷取您的批次識別碼 {#retrieve-your-batch-id}

使用上一步的資料集ID，您需要呼叫目錄API以擷取批次ID。 此API呼叫使用其他查詢引數，以傳回最新的成功批次，而非屬於您組織的批次清單。 若要傳回其他批次，請將限制查詢引數的數字增加至您想要傳回的所需數量。 如需有關可用查詢引數型別的詳細資訊，請瀏覽有關[使用查詢引數篩選目錄資料](../../../catalog/api/filter-data.md)的指南。

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

成功的回應會傳回包含批次ID物件的裝載。 在此範例中，傳回物件的索引鍵值是批次識別碼`01E5QSWCAASFQ054FNBKYV6TIQ`。 複製您的批次ID以用於下一個API呼叫。

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

取得批次ID後，您就可以向`/batches`提出新的GET請求。 該請求會傳回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步中擷取的批次ID [擷取您的批次ID](#retrieve-your-batch-id)。 |

**要求**

使用您自己的批次ID提出以下請求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應傳回包含`_links`物件的裝載。 在`_links`物件中，是以新API呼叫作為其值的`href`。 複製此值以繼續執行下一個步驟。

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

使用您在上一步中取得的`href`值作為API呼叫，提出新的GET要求以擷取您的檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 資料集檔案識別碼是從[前一個步驟](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 它也可在物件型別`dataSetFileId`下的`data`陣列中存取。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含資料陣列，其中可能有單一專案，或屬於該目錄的檔案清單。 以下範例包含檔案清單，並經過壓縮以提高可讀性。 在此案例中，您需要遵循每個檔案的URL才能存取該檔案。

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
| `_links.self.href` | 用來下載目錄中檔案的GET要求URL。 |


複製`data`陣列中任何檔案物件的`href`值，然後繼續下一個步驟。

## 下載您的檔案資料

若要下載您的檔案資料，請對在先前步驟[擷取您的檔案](#retrieving-your-files)中複製的`"href"`值發出GET要求。

>[!NOTE]
>
>如果您直接在命令列中提出此請求，系統可能會提示您先在請求標頭後面新增輸出。 下列要求範例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 資料集檔案識別碼是從[前一個步驟](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中傳回。 |
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
>在發出GET請求之前，請確定您位於要儲存檔案的正確目錄或資料夾中。

**回應**

回應會將您要求的檔案下載到目前目錄中。 在此範例中，檔案名稱為「filename.parquet」。

![終端機](../images/download-scores/response.png)

## 下載使用Customer AI設定的區段 {#segment}

下載分數資料的替代方式是將對象匯出至資料集。 成功完成分段工作後（`status`屬性的值為「SUCCEEDED」），您就可以將對象匯出至資料集，以便對其進行存取和操作。 若要深入瞭解細分，請造訪[細分總覽](../../../segmentation/home.md)。

>[!IMPORTANT]
>
>若要使用此匯出方法，需要為資料集啟用「即時客戶設定檔」 。

區段評估指南中的[匯出區段](../../../segmentation/tutorials/evaluate-a-segment.md)區段涵蓋匯出對象資料集的必要步驟。 本指南概述並提供下列範例：

- **建立目標資料集：**&#x200B;建立資料集以保留對象成員。
- **在資料集中產生對象設定檔：**&#x200B;根據區段作業的結果，以XDM個別設定檔填入資料集。
- **監視匯出進度：**&#x200B;檢查目前匯出程式的進度。
- **讀取對象資料：**&#x200B;擷取代表對象成員的結果XDM個別設定檔。

## 後續步驟

本檔案概述下載Customer AI分數所需的步驟。 您現在可以繼續瀏覽提供的其他[智慧型服務](../../home.md)與指南。
