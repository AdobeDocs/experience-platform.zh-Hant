---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料存取概述
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 2%

---


# 使用資料存取API查詢資料集資料

本檔案提供逐步教學課程，其中涵蓋如何使用Adobe Experience Platform中的資料存取API來尋找、存取及下載儲存在資料集中的資料。 您也將會瞭解資料存取API的一些獨特功能，例如分頁和部分下載。

## 快速入門

本教學課程旨在瞭解如何建立和填入資料集。 如需詳細 [資訊，請參閱資料集建立教學課程](../../catalog/datasets/create.md) 。

以下章節提供您必須知道的其他資訊，以便成功呼叫平台API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型： application/json

## 序列圖

本教學課程依循下列順序圖中概述的步驟，反白顯示資料存取API的核心功能。</br>
![](../images/sequence_diagram.png)

目錄API可讓您擷取有關批次和檔案的資訊。 資料存取API可讓您透過HTTP存取和下載這些檔案，視檔案大小而定，為完整或部分下載。

## 找出資料

開始使用資料存取API之前，您必須先識別您要存取的資料位置。 在目錄API中，有兩個端點可用來瀏覽組織的中繼資料並擷取您要存取的批次或檔案ID:

- `GET /batches`: 返回組織下的批清單
- `GET /dataSetFiles`: 傳回組織下的檔案清單

如需目錄API中端點的完整清單，請參閱 [API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

## 擷取IMS組織下的批次清單

使用目錄API，您可以在組織下傳回批次清單：

**API格式**

```http
GET /batches
```

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括一個對象，該對象列出與IMS組織相關的所有批，每個頂層值代表一個批。 個別批對象包含該特定批的詳細資訊。 以下響應已最小化。

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
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

### 篩選批次清單

通常需要篩選器才能找到特定批，以便檢索特定使用案例的相關資料。 可將參數新增至請 `GET /batches` 求，以篩選傳回的回應。 以下請求將返回在特定資料集內指定時間之後建立的所有批，並按建立時間排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 開始時間戳記（以毫秒為單位，例如1514836799000）。 |
| `{DATASET_ID}` | 資料集識別碼。 |
| `{SORT_BY}` | 依提供的值排序回應。 例如，按創 `desc:created` 建日期以降序排序對象。 |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

您可在目錄API參考中找到參數和篩選器的 [完整清單](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

## 檢索屬於特定批的所有檔案的清單

現在您擁有要存取之批次的ID，可使用資料存取API來取得屬於該批次的檔案清單。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試存取之批次的批次識別碼。 |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

回應包含一個資料陣列，列出指定批次中的所有檔案。 檔案由其檔案ID引用，該檔案ID位於欄位 `dataSetFileId` 下。

## 使用檔案ID訪問檔案

擁有唯一的檔案ID後，您就可以使用資料存取API來存取檔案的特定詳細資訊，包括檔案名稱、檔案大小（以位元組為單位），以及下載檔案的連結。

**API格式**

```http
GET /files/{FILE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 您要存取之檔案的識別碼。 |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

根據檔案ID指向單個檔案或目錄，返回的資料陣列可能包含屬於該目錄的單個條目或檔案清單。 每個檔案元素都包含詳細資訊，例如檔案名稱、檔案大小（以位元組為單位），以及下載檔案的連結。

**案例1: 檔案ID指向單一檔案**

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

**案例2: 檔案ID指向目錄**

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
| `data._links.self.href` | 下載相關檔案的URL。 |

此回應會傳回包含兩個獨立檔案的目錄，其中包含ID `{FILE_ID_2}` 和 `{FILE_ID_3}`。 在此案例中，您必須遵循每個檔案的URL才能存取檔案。

## 擷取檔案的中繼資料

您可以通過發出HEAD請求來檢索檔案的元資料。 這會傳回檔案的中繼資料標題，包括其大小（位元組）和檔案格式。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的識別碼。 |
| `{FILE_NAME`} | 檔案名稱（例如profiles.parce） |

**請求**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應標題包含查詢檔案的中繼資料，包括：
- `Content-Length`: 以位元組表示裝載的大小
- `Content-Type`: 指示檔案類型。

## 存取檔案內容

您也可以使用資料存取API存取檔案的內容。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的識別碼。 |
| `{FILE_NAME`} | 檔案名稱（例如profiles.parce）。 |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回檔案的內容。

## 下載檔案的部分內容

資料存取API允許以區塊下載檔案。 在從檔案下載特定位元組范 `GET /files/{FILE_ID}` 圍的請求期間，可指定範圍標題。 如果未指定範圍，API預設會下載整個檔案。

上一節中的HEAD [示例](#retrieve-the-metadata-of-a-file) ，以位元組為單位提供特定檔案的大小。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_ID} ` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parce） |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 指定要下載的位元組範圍。 如果未指定，API將下載整個檔案。 在此範例中，將下載前100個位元組。 |

**回應**

回應內文包含檔案的前100位元組（如請求中的「範圍」標題所指定），以及HTTP狀態206（部分內容）。 回應也包含下列標題：

- 內容長度： 100（傳回的位元組數）
- 內容類型： application/parec（請求的是拼花檔案，因此響應內容類型是拼花的）
- 內容範圍： 位元組0-99/249058(請求的範圍(0-99)，佔位元組總數(249058))

## 設定API回應分頁

資料存取API中的回應會編頁。 依預設，每頁的登入點數上限為100。 分頁參數可用於修改預設行為。

- `limit`: 您可以使用「限制」參數，根據您的需求指定每頁的登入次數。
- `start`: 偏移可以由&quot;start&quot;查詢參數設定。
- `&`: 您可以使用和符號，在單一呼叫中結合多個參數。

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
| `{LIMIT}` | 控制在結果陣列中傳回多少結果（例如，limit=1） |

**請求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**:

回應包含一個 `"data"` 包含單一元素的陣列，如請求參數所指定 `limit=1`。 此元素是包含第一個可用檔案詳細資料的物件，如請求中的參數所指 `start=0` 定（請記住，在零編號中，第一個元素是&quot;0&quot;）。

該 `_links.next.href` 值包含下一頁回應的連結，您可在此看到參 `start` 數已進階至 `start=1`。

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
