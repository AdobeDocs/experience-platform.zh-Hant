---
keywords: Experience Platform；首頁；熱門主題；資料存取；資料存取api；查詢資料存取
solution: Experience Platform
title: 使用資料存取API檢視資料集資料
type: Tutorial
description: 了解如何使用Adobe Experience Platform中的「資料存取API」來尋找、存取和下載資料集內儲存的資料。 此外，我們也會介紹您使用資料存取API的部分獨特功能，例如分頁和部分下載。
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# 使用 [!DNL Data Access] API

本檔案提供逐步教學課程，說明如何使用 [!DNL Data Access] API(Adobe Experience Platform)。 此外，我們也會介紹 [!DNL Data Access] API，例如分頁和部分下載。

## 快速入門

本教學課程需要先深入了解如何建立和填入資料集。 請參閱 [資料集建立教學課程](../../catalog/datasets/create.md) 以取得更多資訊。

以下小節提供您需要了解的其他資訊，以便成功呼叫Platform API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 序列圖

本教學課程依照下列序列圖中概述的步驟，強調說明 [!DNL Data Access] API。</br>
![](../images/sequence_diagram.png)

此 [!DNL Catalog] API可讓您擷取批次和檔案的相關資訊。 此 [!DNL Data Access] API可讓您根據檔案大小，透過HTTP以完整或部分下載方式存取和下載這些檔案。

## 找出資料

開始使用之前 [!DNL Data Access] API，您必須識別要存取的資料位置。 在 [!DNL Catalog] API中，有兩個端點可用來瀏覽組織的中繼資料，以及擷取您要存取的批次或檔案ID:

- `GET /batches`:傳回組織下的批次清單
- `GET /dataSetFiles`:傳回組織下的檔案清單

若要取得 [!DNL Catalog] API，請參閱 [API參考](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 擷取組織下的批次清單

使用 [!DNL Catalog] API，您可以在組織下傳回批次清單：

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

回應包含一個物件，列出與組織相關的所有批次，每個頂層值代表一個批次。 單個批對象包含該特定批的詳細資訊。 已針對空間最小化以下響應。

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

### 篩選批次清單

通常需要篩選器才能找到特定批次，才能擷取特定使用案例的相關資料。 參數可新增至 `GET /batches` 請求，以篩選傳回的回應。 以下請求將返回在指定時間後建立的所有批，在特定資料集內，按建立時間排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 開始時間戳記(如1514836799000)，單位為毫秒。 |
| `{DATASET_ID}` | 資料集識別碼。 |
| `{SORT_BY}` | 依提供的值排序回應。 例如， `desc:created` 按建立日期的降序對對象進行排序。 |

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

您可以在 [目錄API參考](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 檢索屬於特定批的所有檔案的清單

現在您擁有要存取的批次ID，即可使用 [!DNL Data Access] API，以取得屬於該批次的檔案清單。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試訪問的批的批的批標識符。 |

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

回應包含一個資料陣列，列出指定批次中的所有檔案。 檔案由其檔案ID參照，可在 `dataSetFileId` 欄位。

## 使用檔案ID存取檔案

擁有唯一的檔案ID後，即可使用 [!DNL Data Access] API可存取檔案的特定詳細資訊，包括名稱、位元組大小，以及下載檔案的連結。

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

根據檔案ID指向單個檔案還是目錄，返回的資料陣列可能包含一個條目或屬於該目錄的檔案清單。 每個檔案元素都包含詳細資訊，例如檔案名稱、位元組大小，以及下載檔案的連結。

**案例1:檔案ID指向單一檔案**

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

**案例2:檔案ID指向目錄**

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

此回應會傳回包含兩個獨立檔案（含ID）的目錄 `{FILE_ID_2}` 和 `{FILE_ID_3}`. 在此案例中，您必須遵循每個檔案的URL才能存取檔案。

## 擷取檔案的中繼資料

您可以提出HEAD要求，以擷取檔案的中繼資料。 這會傳回檔案的中繼資料標題，包括其大小（位元組）和檔案格式。

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

回應標題包含查詢檔案的中繼資料，包括：
- `Content-Length`:指示有效負載的大小（以位元組為單位）
- `Content-Type`:指示檔案的類型。

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

成功的回應會傳回檔案的內容。

## 下載檔案的部分內容

此 [!DNL Data Access] API允許以區塊下載檔案。 範圍標題可在 `GET /files/{FILE_ID}` 請求從檔案下載特定範圍的位元組。 如果未指定範圍，API預設會下載整個檔案。

中的HEAD範例 [上一節](#retrieve-the-metadata-of-a-file) 提供特定檔案的大小（以位元組為單位）。

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
| `Range: bytes=0-99` | 指定要下載的位元組範圍。 若未指定，API將下載整個檔案。 在此範例中，將下載前100個位元組。 |

**回應**

回應內文包含檔案的前100個位元組（如要求中的「範圍」標題所指定），以及HTTP狀態206（部分內容）。 回應也包含下列標題：

- 內容長度：100（傳回的位元組數）
- 內容類型：application/parquet(請求了Parquet檔案，因此響應內容類型為 `parquet`)
- 內容範圍：位元組0-99/249058(請求的範圍(0-99)，位元組總數中的位元組數(249058))

## 設定API回應分頁

回應 [!DNL Data Access] API會編頁。 依預設，每頁的登入次數上限為100。 可使用分頁參數來修改預設行為。

- `limit`:您可以使用「limit」參數，根據您的需求指定每頁的登入次數。
- `start`:位移可由「開始」查詢參數設定。
- `&`:您可以使用&amp;符號，在單一呼叫中結合多個參數。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試訪問的批的批的批標識符。 |
| `{OFFSET}` | 要啟動結果陣列的指定索引（例如，start=0） |
| `{LIMIT}` | 控制結果陣列中傳回的結果數（例如，limit=1） |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**:

回應包含 `"data"` 陣列，如要求參數所指定 `limit=1`. 此元素是物件，包含第一個可用檔案的詳細資訊，如 `start=0` 參數（請記住，在以零為基礎的編號中，第一個元素是「0」）。

此 `_links.next.href` 值包含下一頁回應的連結，您可在此看到 `start` 參數進階至 `start=1`.

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
