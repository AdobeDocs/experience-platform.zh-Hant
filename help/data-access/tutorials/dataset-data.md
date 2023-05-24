---
keywords: Experience Platform；首頁；熱門主題；資料存取；資料存取api；查詢資料存取
solution: Experience Platform
title: 使用資料存取API查看資料集資料
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform的資料存取API查找、訪問和下載資料集中儲存的資料。 還將介紹資料存取API的一些獨特功能，如分頁和部分下載。
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# 使用 [!DNL Data Access] API

本文檔提供了一個逐步教程，介紹如何使用 [!DNL Data Access] API在Adobe Experience Platform。 您還將介紹 [!DNL Data Access] API，如分頁和部分下載。

## 快速入門

本教程需要瞭解如何建立和填充資料集。 查看 [資料集建立教程](../../catalog/datasets/create.md) 的子菜單。

以下各節提供了成功調用平台API所需的其他資訊。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

## 序列圖

本教程遵循以下序列圖中概述的步驟，突出介紹 [!DNL Data Access] API。</br>
![](../images/sequence_diagram.png)

的 [!DNL Catalog] API允許您檢索有關批處理和檔案的資訊。 的 [!DNL Data Access] API允許您通過HTTP以完整或部分下載方式訪問和下載這些檔案，具體取決於檔案的大小。

## 查找資料

開始使用 [!DNL Data Access] API，您需要標識要訪問的資料的位置。 在 [!DNL Catalog] API中，有兩個端點可用於瀏覽組織的元資料並檢索要訪問的批或檔案的ID:

- `GET /batches`:返回組織下的批清單
- `GET /dataSetFiles`:返回組織下的檔案清單

有關中端點的全面清單 [!DNL Catalog] API，請參閱 [API參考](https://www.adobe.io/experience-platform-apis/references/catalog/)。

## 檢索組織下的批清單

使用 [!DNL Catalog] API，您可以返回組織下的批清單：

**API格式**

```http
GET /batches
```

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括一個對象，該對象列出與組織相關的所有批，每個頂層值表示一個批。 單個批對象包含該特定批的詳細資訊。 已將以下響應最小化為空間。

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### 篩選批清單

為檢索特定用例的相關資料，通常需要篩選器來查找特定批。 參數可添加到 `GET /batches` 請求以篩選返回的響應。 以下請求將返回在特定資料集內指定時間後建立的所有批，並按建立時間排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 以毫秒為單位的開始時間戳（例如1514836799000）。 |
| `{DATASET_ID}` | 資料集標識符。 |
| `{SORT_BY}` | 按提供的值對響應進行排序。 比如說， `desc:created` 按建立日期按降序排序對象。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

在中，可找到參數和篩選器的完整清單 [目錄API參考](https://www.adobe.io/experience-platform-apis/references/catalog/)。

## 檢索屬於特定批的所有檔案的清單

現在，您擁有要訪問的批的ID，您可以使用 [!DNL Data Access] API，以獲取屬於該批的檔案清單。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試訪問的批的批標識符。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data._links.self.href` | 訪問此檔案的URL。 |

響應包含一個資料陣列，該陣列列出指定批處理中的所有檔案。 檔案由其檔案ID引用，該ID位於 `dataSetFileId` 的子菜單。

## 使用檔案ID訪問檔案

擁有唯一的檔案ID後，可以使用 [!DNL Data Access] 用於訪問檔案的特定詳細資訊的API，包括其名稱、大小（以位元組為單位）以及下載該檔案的連結。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 要訪問的檔案的標識符。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

根據檔案ID是否指向單個檔案或目錄，返回的資料陣列可能包含屬於該目錄的單個條目或檔案清單。 每個檔案元素都將包含詳細資訊，如檔案名、大小（以位元組為單位）以及下載檔案的連結。

**案例1:檔案ID指向單個檔案**

**回應**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
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

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | 檔案的名稱。 |
| `_links.self.href` | 下載檔案的URL。 |

**案例二：檔案ID指向目錄**

**回應**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `data._links.self.href` | 下載關聯檔案的URL。 |

此響應返回包含兩個獨立檔案(ID)的目錄 `{FILE_ID_2}` 和 `{FILE_ID_3}`。 在此方案中，您需要遵循每個檔案的URL才能訪問該檔案。

## 檢索檔案的元資料

可通過發出HEAD請求來檢索檔案的元資料。 這將返回檔案的元資料標頭，包括其大小（以位元組和檔案格式表示）。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的標識符。 |
| `{FILE_NAME}` | 檔案名（例如profiles.parce） |

**要求**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應標頭包含查詢檔案的元資料，包括：
- `Content-Length`:指示負載的大小（以位元組為單位）
- `Content-Type`:指示檔案類型。

## 訪問檔案的內容

您還可以使用 [!DNL Data Access] API。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的標識符。 |
| `{FILE_NAME}` | 檔案名（例如profiles.parce）。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回檔案的內容。

## 下載檔案的部分內容

的 [!DNL Data Access] API允許以塊形式下載檔案。 在 `GET /files/{FILE_ID}` 請求從檔案下載特定範圍的位元組。 如果未指定範圍，則API將預設下載整個檔案。

中的HEAD示例 [上一節](#retrieve-the-metadata-of-a-file) 指定特定檔案的大小（以位元組為單位）。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID} ` | 檔案的標識符。 |
| `{FILE_NAME}` | 檔案名（例如profiles.parce） |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 指定要下載的位元組範圍。 如果未指定此選項，API將下載整個檔案。 在此示例中，將下載前100個位元組。 |

**回應**

響應主體包括檔案的前100個位元組（如請求中的「範圍」標頭所指定）以及HTTP狀態206（部分內容）。 響應還包括以下標頭：

- 內容長度：100（返回的位元組數）
- 內容類型：application/parke(請求了Parke檔案，因此響應內容類型為 `parquet`)
- 內容範圍：位元組0-99/249058(請求的範圍(0-99)，佔位元組總數(249058))

## 配置API響應分頁

在 [!DNL Data Access] API已分頁。 預設情況下，每頁的最大條目數為100。 分頁參數可用於修改預設行為。

- `limit`:您可以使用「limit」參數根據您的要求指定每頁的條目數。
- `start`:偏移可以通過「開始」查詢參數設定。
- `&`:可以使用「和號」在單個調用中組合多個參數。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試訪問的批的批標識符。 |
| `{OFFSET}` | 用於啟動結果陣列的指定索引（例如，start=0） |
| `{LIMIT}` | 控制在結果陣列中返回的結果數（例如， limit=1） |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**:

響應包含 `"data"` 具有單個元素的陣列，由request參數指定 `limit=1`。 此元素是包含第一個可用檔案的詳細資訊的對象，由 `start=0` 參數（請記住，在基於零的編號中，第一個元素為「0」）。

的 `_links.next.href` 值包含指向響應下一頁的連結，在該頁中，您可以看到 `start` 參數已高級到 `start=1`。

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
