---
keywords: Experience Platform；首頁；熱門主題；資料攝取；批處理；啟用資料集；批處理攝取概述；概述；批處理攝取概述；
solution: Experience Platform
title: 批處理接收API概述
description: Adobe Experience Platform批處理接收API允許您將資料作為批處理檔案接收到平台。 正在攝取的資料可以是來自CRM系統中的平面檔案（如Parke檔案）的配置檔案資料，或符合「體驗資料模型」(XDM)註冊表中已知模式的資料。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# 批處理接收API概述

Adobe Experience Platform批處理接收API允許您將資料作為批處理檔案接收到平台。 所攝取的資料可以是來自平面檔案（如Parke檔案）的配置檔案資料，也可以是符合該檔案中已知模式的資料 [!DNL Experience Data Model] (XDM)註冊表。

的 [批處理接收API參考](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 提供了有關這些API調用的其他資訊。

下圖概述了批處理接收過程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 快速入門

本指南中使用的API端點是 [批處理接收API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

### [!DNL Data Ingestion] 先決條件

- 要上載的資料必須採用Parke或JSON格式。
- 在 [[!DNL Catalog services]](../../catalog/home.md)。
- Parke檔案的內容必須與上載到的資料集的架構的子集相匹配。
- 驗證後使用您唯一的訪問令牌。

### 批量攝取最佳做法

- 建議的批大小介於256 MB和100 GB之間。
- 每個批最多應包含1500個檔案。

### 批處理接收約束

批處理資料接收存在一些限制：

- 每批的最大檔案數：1500
- 最大批大小：100 GB
- 每行的最大屬性或欄位數：10000
- 每用戶每分鐘的最大批次數：138

>[!NOTE]
>
>要上載大於512MB的檔案，需要將檔案分成較小的塊。 有關上載大檔案的說明，請參見 [此文檔的大檔案上載部分](#large-file-upload---create-file)。

### 類型

在接收資料時，瞭解如何 [!DNL Experience Data Model] (XDM)架構有效。 有關XDM欄位類型如何映射到不同格式的詳細資訊，請閱讀 [架構註冊表開發人員指南](../../xdm/api/getting-started.md)。

在接收資料時具有一定的靈活性 — 如果類型與目標架構中的類型不匹配，則資料將轉換為表示的目標類型。 如果無法，則將用 `TypeCompatibilityException`。

例如，JSON和CSV都沒有 `date` 或 `date-time` 的雙曲餘切值。 因此，這些值使用 [ISO 8061格式化字串](https://www.iso.org/iso-8601-date-and-time-format.html) (「2018-07-10T15:05:59.000-08:00&quot;)或Unix時間（以毫秒為單位）格式化，並在接收時轉換為目標XDM類型。

下表顯示了在接收資料時支援的轉換。

| 入站（行）與目標（列） | 字串 | 位元組 | 短 | 整數 | 龍 | 雙倍 | 日期 | 日期-時間 | 物件 | 地圖 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字串 | X | X | X | X | X | X | X | X |  |  |
| 位元組 | X | X | X | X | X | X |  |  |  |  |
| 短 | X | X | X | X | X | X |  |  |  |  |
| 整數 | X | X | X | X | X | X |  |  |  |  |
| 龍 | X | X | X | X | X | X | X | X |  |  |
| 雙倍 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| 日期-時間 |  |  |  |  |  |  |  | X |  |  |
| 物件 |  |  |  |  |  |  |  |  | X | X |
| 地圖 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>布爾值和陣列不能轉換為其他類型。

## 使用 API

的 [!DNL Data Ingestion] API允許您將資料作為批（資料單元，由一個或多個要作為單個單元被接收的檔案組成）接收到 [!DNL Experience Platform] 分三個基本步驟：

1. 建立新批。
2. 將檔案上載到與資料的XDM架構匹配的指定資料集。
3. 發出批次結束的信號。

## 建立批

在將資料添加到資料集之前，必須將其連結到批處理，該批處理稍後將上載到指定的資料集。

```http
POST /batches
```

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `datasetId` | 要將檔案上載到的資料集的ID。 |

**雷龐塞**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 剛建立的批的ID（用於後續請求）。 |
| `relatedObjects.id` | 要將檔案上載到的資料集的ID。 |

## 檔案上載

成功建立新批以進行上載後，可以將檔案上載到特定資料集。

可以使用「小檔案上載API」上載檔案。 但是，如果檔案太大且超出網關限制（如延長超時、超出正文大小的請求以及其他限制），則可以切換到「大檔案上載API」。 此API以塊形式上載檔案，並使用「大檔案上載完成API」調用將資料縫合在一起。

>[!NOTE]
>
>批處理接收可用於增量更新配置檔案儲存中的資料。 有關詳細資訊，請參閱 [更新批](#patch-a-batch) 的 [批量攝取顯影劑指南](api-overview.md)。

>[!INFO]
>
>以下示例使用 [阿帕奇鑲木地板](https://parquet.apache.org/docs/) 的雙曲餘切值。 在中可找到使用JSON檔案格式的示例 [批量攝取顯影劑指南](api-overview.md)。

### 小檔案上載

一旦建立了批處理，就可以將資料上載到預先存在的資料集。  正在上載的檔案必須與其引用的XDM架構匹配。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 要上載檔案的資料集的ID。 |
| `{FILE_NAME}` | 在資料集中看到的檔案的名稱。 |

**要求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上載到資料集中的檔案的路徑和檔案名。 |

**雷龐塞**

```JSON
#Status 200 OK, with empty response body
```

### 大檔案上載 — 建立檔案

要上載大檔案，必須將檔案拆分為較小的塊，並一次上載一個。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 正在接收檔案的資料集的ID。 |
| `{FILE_NAME}` | 在資料集中看到的檔案的名稱。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**雷龐塞**

```JSON
#Status 201 CREATED, with empty response body
```

### 大檔案上載 — 上載後續部件

建立檔案後，可以通過重複的PATCH請求來上載所有後續的區塊，這對檔案的每個部分都是一個請求。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 要將檔案上載到的資料集的ID。 |
| `{FILE_NAME}` | 在資料集中看到的檔案的名稱。 |

**要求**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上載到資料集中的檔案的路徑和檔案名。 |

**雷龐塞**

```JSON
#Status 200 OK, with empty response
```

## 信號批量完成

在所有檔案都上載到批後，可以發出批完成的信號。 通過這樣， [!DNL Catalog] 為已完成的檔案建立資料集檔案條目，並與上面生成的批關聯。 的 [!DNL Catalog] 然後將批處理標籤為成功，這將觸發下游流以接收可用資料。

**要求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上載到資料集的批的ID。 |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**雷龐塞**

```JSON
#Status 200 OK, with empty response
```

## 檢查批狀態

等待檔案上載到批時，可以檢查批的狀態以查看其進度。

**API格式**

```http
GET /batch/{BATCH_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 正在檢查的批的ID。 |

**要求**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**雷龐塞**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{USER_ID}` | 建立或更新批的用戶的ID。 |

的 `"status"` 欄位顯示請求的批的當前狀態。 批可具有以下狀態之一：

## 批處理接收狀態

| 狀態 | 說明 |
| ------ | ----------- |
| 已放棄 | 批未在預期時間範圍內完成。 |
| 中止 | 中止操作已 **明確** 已調用（通過批接收API）指定批。 一旦批處於「已載入」狀態，則無法中止該批。 |
| 作用中 | 批已成功升級，可用於下游衝減。 此狀態可與「成功」互換使用。 |
| 已刪除 | 批的資料已完全刪除。 |
| 已失敗 | 由錯誤配置和/或錯誤資料導致的終端狀態。 失敗批處理的資料將 **不** 出現。 此狀態可與「失敗」互換使用。 |
| 非活動 | 批已成功升級，但已還原或已過期。 批不再可用於下游衝減。 |
| 已載入 | 批的資料已完成，批已準備好進行升級。 |
| 正在載入 | 正在上載此批的資料，且該批當前正在 **不** 準備升職。 |
| 正在重試 | 正在處理此批的資料。 但是，由於系統或暫時性錯誤，批失敗 — 因此，將重試此批。 |
| 已轉移 | 批的升級進程的暫存階段已完成，並且已運行接收作業。 |
| 預備 | 正在處理批的資料。 |
| 停止 | 正在處理批的資料。 但是，批升級在多次重試後已停止。 |
