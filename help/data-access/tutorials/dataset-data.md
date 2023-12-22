---
keywords: Experience Platform；首頁；熱門主題；資料存取；資料存取api；查詢資料存取
solution: Experience Platform
title: 使用資料存取API檢視資料集資料
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform的資料存取API，尋找、存取及下載儲存在資料集中的資料。 本檔案會介紹資料存取API的一些獨特功能，例如分頁和部分下載。
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 9144a5f4cce88fc89973a7fea6d69384cc5f4ba1
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 7%

---

# 檢視資料集資料，使用 [!DNL Data Access] API

使用本逐步教學課程，瞭解如何使用尋找、存取及下載儲存在資料集中的資料。 [!DNL Data Access] Adobe Experience Platform中的API。 本檔案將介紹 [!DNL Data Access] API，例如分頁和部分下載。

## 快速入門

本教學課程需要您深入瞭解如何建立和填入資料集。 請參閱 [資料集建立教學課程](../../catalog/datasets/create.md) 以取得詳細資訊。

以下章節提供成功呼叫Platform API所需瞭解的其他資訊。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集所需標頭的值

若要呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](../../landing/api-authentication.md). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，以指定進行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- Content-Type： application/json

## 序列圖

本教學課程遵循下列順序圖中所概述的步驟，重點說明 [!DNL Data Access] API。

![資料存取API核心功能的順序圖。](../images/sequence_diagram.png)

若要擷取批次和檔案的相關資訊，請使用 [!DNL Catalog] API。 若要透過HTTP存取及下載這些檔案，並做為完整或部分下載專案，視檔案大小而定，請使用 [!DNL Data Access] API。

## 找出資料

開始使用之前 [!DNL Data Access] API，您必須識別要存取之資料的位置。 在 [!DNL Catalog] API的環境中，有兩個端點可用來瀏覽組織的中繼資料，以及擷取您要存取之批次或檔案的ID：

- `GET /batches`：傳回組織下的批次清單
- `GET /dataSetFiles`：傳回組織底下的檔案清單

如需中端點的完整清單 [!DNL Catalog] API，請參閱 [API參考](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## 擷取組織下的批次清單

使用 [!DNL Catalog] api下，您可以傳回組織下的批次清單：

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

回應中包含一個物件，列出與組織相關的所有批次，每個最上層值代表批次。 個別批次物件包含該特定批次的詳細資訊。 以下的回應已最小化空間。

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

### 篩選批次清單 {#filter-batches-list}

篩選器通常需要尋找特定批次以擷取特定使用案例的相關資料。 引數可新增至 `GET /batches` 請求篩選傳回的回應。 以下請求會傳回指定時間後建立的所有批次（在特定資料集中），依其建立時間排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 以毫秒為單位的開始時間戳記(例如1514836799000)。 |
| `{DATASET_ID}` | 資料集識別碼。 |
| `{SORT_BY}` | 依提供的值排序回應。 例如， `desc:created` 依建立日期遞減排序物件。 |

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

引數和篩選器的完整清單可在以下網址找到： [目錄API參考](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## 擷取屬於特定批次的所有檔案清單

現在您已取得要存取之批次的ID，可以使用 [!DNL Data Access] 此API用於取得屬於該批次的檔案清單。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試存取之批次的批次識別碼。 |

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
| `data._links.self.href` | 存取此檔案的URL。 |

回應包含列出指定批次中所有檔案的資料陣列。 參照檔案的檔案ID位於 `dataSetFileId` 欄位。

## 使用檔案ID存取檔案 {#access-file-with-file-id}

有了唯一的檔案ID後，您就可以使用 [!DNL Data Access] 存取檔案特定詳細資料的API，包括其名稱、位元組大小以及下載連結。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 您要存取之檔案的識別碼。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

視檔案ID指向個別檔案或目錄而定，傳回的資料陣列可能會包含單一專案或屬於該目錄的檔案清單。 每個檔案元素都包含檔案名稱、位元組大小等詳細資訊，以及下載檔案的連結。

**案例1：檔案ID指向單一檔案**

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

**案例2：檔案ID指向目錄**

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

此回應會傳回包含兩個個別檔案（具有ID）的目錄 `{FILE_ID_2}` 和 `{FILE_ID_3}`. 在此案例中，您必須追蹤每個檔案的URL才能存取該檔案。

## 擷取檔案的中繼資料

您可以發出HEAD要求來擷取檔案的中繼資料。 這會傳回檔案的中繼資料標題，包括其位元組大小和檔案格式。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parquet） |

**要求**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應標頭包含查詢檔案的中繼資料，包括：

- `Content-Length`：指出承載的大小（以位元組為單位）
- `Content-Type`：指出檔案型別。

## 存取檔案的內容

您也可以使用 [!DNL Data Access] API。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parquet）。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回檔案內容。

## 下載檔案的部分內容 {#download-partial-file-contents}

若要從檔案下載特定範圍的位元組，請在 `GET /files/{FILE_ID}` 要求給 [!DNL Data Access] API。 如果未指定範圍，API預設會下載整個檔案。

中的HEAD範例 [上一節](#retrieve-the-metadata-of-a-file) 會提供特定檔案的大小（位元組）。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID} ` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parquet） |

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
| `Range: bytes=0-99` | 指定要下載的位元組範圍。 如果未指定，API會下載整個檔案。 在此範例中，會下載前100個位元組。 |

**回應**

回應內文包含檔案的前100個位元組（如要求中的「Range」標頭所指定）以及HTTP狀態206 （部分內容）。 回應也包含下列標頭：

- Content-Length： 100 （傳回的位元組數）
- Content-type： application/parquet (已要求Parquet檔案，因此回應內容型別為 `parquet`)
- Content-Range：位元組0-99/249058 (要求的範圍(0-99)，位元組總數(249058))

## 設定API回應分頁 {#configure-response-pagination}

內的回應 [!DNL Data Access] API已分頁。 依預設，每頁的最大專案數為100。 您可以使用分頁引數修改預設行為。

- `limit`：您可以使用「limit」引數，根據您的要求指定每頁的專案數。
- `start`：位移可由「開始」查詢引數設定。
- `&`：您可以使用&amp;符號，在單一呼叫中組合多個引數。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試存取之批次的批次識別碼。 |
| `{OFFSET}` | 啟動結果陣列的指定索引（例如，start=0） |
| `{LIMIT}` | 控制結果陣列中傳回的結果數量（例如，limit=1） |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**:

回應包含 `"data"` 單一元素的陣列，如要求引數所指定 `limit=1`. 此元素是一個物件，包含第一個可用檔案的詳細資訊，由 `start=0` 請求中的引數（請記住，在以零開始的編號中，第一個元素為「0」）。

此 `_links.next.href` 值包含回應下一頁的連結，您可以在此看到 `start` 引數已進階至 `start=1`.

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
