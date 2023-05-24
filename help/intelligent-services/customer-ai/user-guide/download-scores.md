---
keywords: Experience Platform；下載分數；客戶ai；熱門主題；導出；客戶ai下載；客戶ai得分
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 在客戶AI中下載分數
description: 客戶AI允許您下載Parfect檔案格式的分數。
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# 在客戶AI中下載分數

本文檔是下載客戶AI分數的指南。

## 快速入門

客戶AI允許您下載Parfect檔案格式的分數。 本教程要求您閱讀並完成下載的「客戶AI分數」部分 [開始](../getting-started.md) 的子菜單。

此外，為了訪問客戶AI的分數，您需要有一個具有成功運行狀態的服務實例可用。 要建立新服務實例，請訪問 [配置客戶AI實例](./configure.md)。 如果您最近建立了一個服務實例，但該實例仍在訓練和評分，請允許它24小時才能完成運行。

目前，下載客戶AI分數有兩種方法：

1. 如果要在單個層下載分數和/或未啟用即時客戶配置檔案，請首先導航至 [查找您的資料集ID](#dataset-id)。
2. 如果啟用了配置檔案並希望下載使用客戶AI配置的段，請導航至 [下載配置有客戶AI的網段](#segment)。

## 查找您的資料集ID {#dataset-id}

在您的服務實例中，按一下 *更多操作* 從右上角導航下拉，然後選擇 **[!UICONTROL 訪問分數]**。

![更多操作](../images/insights/more-actions.png)

此時將出現一個新對話框，其中包含下載分數文檔和當前實例的資料集ID的連結。 將資料集ID複製到剪貼簿，然後繼續下一步。

![資料集 ID](../images/download-scores/access-scores.png)

## 檢索批ID {#retrieve-your-batch-id}

使用上一步中的資料集ID，需要調用目錄API以檢索批ID。 此API調用使用附加查詢參數，以返回最新成功的批，而不是屬於您組織的批的清單。 要返回附加批，請將限制查詢參數的編號增加到希望返回的所需金額。 有關可用查詢參數類型的詳細資訊，請訪問上的指南 [使用查詢參數篩選目錄資料](../../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 「訪問分數」對話框中可用的資料集ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含批ID對象的負載。 在本示例中，返回對象的鍵值為批ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 複製批ID以在下次API調用中使用。

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

## 使用批ID檢索下一個API調用 {#retrieve-the-next-api-call-with-your-batch-id}

一旦您擁有了批ID，您就可以發出新的GET請求 `/batches`。 該請求返回用作下一個API請求的連結。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步中檢索的批ID [檢索批ID](#retrieve-your-batch-id)。 |

**要求**

使用您自己的批ID，發出以下請求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含 `_links` 的雙曲餘切值。 在 `_links` 對象是 `href` 將新API調用作為其值。 複製此值以繼續執行下一步。

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

## 檢索檔案 {#retrieving-your-files}

使用 `href` 作為API調用在上一步中獲得的值，請發出新的GET請求以檢索檔案目錄。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在中返回dataSetFile ID `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id)。 在 `data` 對象類型下的陣列 `dataSetFileId`。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包含一個資料陣列，該陣列可能具有一個條目，或者包含屬於該目錄的檔案清單。 下面的示例包含檔案清單，並已壓縮可讀性。 在此方案中，您需要遵循每個檔案的URL才能訪問該檔案。

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


複製 `href` 值 `data` 陣列，然後繼續下一步。

## 下載檔案資料

要下載檔案資料，請向 `"href"` 上一步中複製的值 [正在檢索檔案](#retrieving-your-files)。

>[!NOTE]
>
>如果您直接在命令行中發出此請求，可能會提示您在請求標題後添加輸出。 以下請求示例使用 `--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在中返回dataSetFile ID `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id)。 |
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
>在發出GET請求之前，請確保您所在的目錄或資料夾正確。

**回應**

響應將下載您在當前目錄中請求的檔案。 在本示例中，檔案名為&quot;filename.parmet&quot;。

![終端](../images/download-scores/response.png)

## 下載使用客戶AI配置的網段 {#segment}

下載分數資料的另一種方法是將受眾導出到資料集。 分段作業成功完成後( `status` 屬性為「成功」)，您可以將受眾導出到資料集，在該資料集中可以訪問並對其執行操作。 要瞭解有關細分的詳細資訊，請訪問 [分段概述](../../../segmentation/home.md)。

>[!IMPORTANT]
>
>為了利用此導出方法，需要為資料集啟用即時客戶配置檔案。

的 [導出段](../../../segmentation/tutorials/evaluate-a-segment.md) 段評估指南中的一節介紹了導出受眾資料集所需的步驟。 本指南概括介紹並提供了以下示例：

- **建立目標資料集：** 建立資料集以容納受眾成員。
- **在資料集中生成受眾配置檔案：** 根據段作業的結果，使用XDM單個配置檔案填充資料集。
- **監視導出進度：** 檢查導出進程的當前進度。
- **讀取受眾資料：** 檢索表示受眾成員的生成的XDM個人配置檔案。

## 後續步驟

本文檔概述了下載客戶AI分數所需的步驟。 現在，您可以繼續瀏覽其他 [智慧服務](../../home.md) 以及提供的嚮導。
