---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform部分批次擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---



# 部分批次擷取（測試版）

部分批次擷取是指能夠擷取包含錯誤的資料，最高可達到特定臨界值。 透過這項功能，使用者可以成功將所有正確的資料內嵌至Adobe Experience Platform，而其所有不正確的資料都會個別批次處理，以及為何無效的詳細資訊。

本檔案提供管理部分批次擷取的教學課程。

此外，本教學課 [程的附錄](#appendix) ，也提供部分批次擷取錯誤類型的參考。

>[!IMPORTANT]
>
>此功能僅存在於使用API。 請連絡您的團隊，以取得此功能。

## 快速入門

本教學課程需要對部分批次擷取所涉及的各種Adobe Experience Platform服務有相關的使用知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [批次擷取](./overview.md): Platform從資料檔案（例如CSV和Parke）擷取和儲存資料的方法。
- [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。

以下章節提供您成功呼叫平台API所需的其他資訊。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

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

## 在API中啟用資料集以進行部分批次擷取

<!-- >[!NOTE] This section describes enabling a dataset for partial batch ingestion using the API. For instructions on using the UI, please read the [enable a dataset for partial batch ingestion in the UI](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) step. -->

您可以建立新的資料集，或修改啟用部分擷取的現有資料集。

若要建立新資料集，請依照建立資料集教學 [課程中的步驟進行](../../catalog/api/create-dataset.md)。 在您到達「建 *立資料集* 」步驟後，在請求內文中新增下列欄位：

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `errorThresholdPercentage` | 整個批失敗前可接受錯誤的百分比。 |

同樣地，若要修改現有資料集，請依照目錄開發人員指 [南中的步驟](../../catalog/api/update-object.md)。

在資料集中，您需要新增上述標籤。

<!-- ## Enable a dataset for partial batch ingestion in the UI

>[!NOTE]
>
>This section describes enabling a dataset for partial batch ingestion using the UI. If you have already enabled a dataset for partial batch ingestion using the API, you can skip ahead to the next section.

To enable a dataset for partial ingestion through the Platform UI, click **Datasets** in the left navigation. You can either [create a new dataset](#create-a-new-dataset-with-partial-batch-ingestion-enabled) or [modify an existing dataset](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Create a new dataset with partial batch ingestion enabled

To create a new dataset, follow the steps in the [dataset user guide](../../catalog/datasets/user-guide.md). Once you reach the *Configure dataset* step, take note of the *Partial Ingestion* and *Error Diagnostics* fields.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error Diagnostics* toggle only appears when the *Partial Ingestion* toggle is off. This feature allows Platform to generate detailed error messages about your ingested batches. If the *Partial Ingestion* toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%.

### Modify an existing dataset to enable partial batch ingestion

To modify an existing dataset, select the dataset you want to modify. The sidebar on the right populates with information about the dataset. 

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%. -->

## 擷取部分批次擷取錯誤

如果批包含失敗，您需要檢索這些失敗的錯誤資訊，以便重新收錄資料。

### 檢查狀態

要檢查收錄批的狀態，您必須在GET請求的路徑中提供批的ID。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 檢查狀態的批的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含批次狀態的詳細資訊。

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

如果批次發生錯誤並啟用錯誤診斷，則狀態會是「成功」，並在可下載的錯誤檔案中提供錯誤的詳細資訊。

## 後續步驟

本教學課程涵蓋如何建立或修改資料集以啟用部分批次擷取。 如需批次擷取的詳細資訊，請閱讀批次擷取開 [發人員指南](./api-overview.md)。

## 部分批次擷取錯誤類型 {#appendix}

部分批次擷取在擷取資料時有四種不同的錯誤類型。

- [無法讀取的檔案](#unreadable)
- [無效的結構或標題](#schemas-headers)
- [不可分的行](#unparsable)
- [無效的XDM轉換](#conversion)

### 無法讀取的檔案 {#unreadable}

如果接受的批具有無法讀取的檔案，則批的錯誤將附加到批本身。 有關檢索失敗批的詳細資訊，請參閱檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 無效的結構或標題 {#schemas-headers}

如果所收錄的批具有無效的方案或無效標題，則批的錯誤將附加在批本身上。 有關檢索失敗批的詳細資訊，請參閱檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 不可分的行 {#unparsable}

如果接受的批處理具有不可分割的行，則批處理的錯誤將儲存在檔案中，該檔案可以使用下面概述的端點進行訪問。

**API格式**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 從 `id` 中檢索錯誤資訊的批的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含不可分列的詳細資料。

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### 無效的XDM轉換 {#conversion}

如果接收的批具有無效的XDM轉換，則批的錯誤將儲存在可通過以下端點訪問的檔案中。

**API格式**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 從 `id` 中檢索錯誤資訊的批的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含XDM轉換失敗的詳細資訊。

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
