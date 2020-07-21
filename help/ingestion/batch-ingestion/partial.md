---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform部分批次擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 1%

---



# 部分批次擷取

部分批次擷取是指能夠擷取包含錯誤的資料，最高可達到特定臨界值。 透過這項功能，使用者可以成功將所有正確的資料內嵌至Adobe Experience Platform，而其所有不正確的資料都會個別批次處理，以及為何無效的詳細資訊。

本檔案提供管理部分批次擷取的教學課程。

此外，本教學課 [程的附錄](#appendix) ，也提供部分批次擷取錯誤類型的參考。

## 快速入門

本教學課程需要對部分批次擷取所涉及的各種Adobe Experience Platform服務有相關的使用知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [批次擷取](./overview.md): 從資料檔 [!DNL Platform] 案（例如CSV和Parce）擷取和儲存資料的方法。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 組織客戶體驗資料 [!DNL Platform] 的標準化架構。

以下章節提供您成功呼叫API所需的其他資訊 [!DNL Platform] 。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

## 在API中啟用批次以擷取部分批次 {#enable-api}

>[!NOTE]
>
>本節說明如何使用API啟用批次以擷取部分批次。 如需使用UI的指示，請閱讀UI步 [驟中啟用批次以擷取部分批次](#enable-ui) 。

您可以建立啟用部分擷取的新批次。

若要建立新批次，請依照批次擷取開發人員指 [南中的步驟進行](./api-overview.md)。 在您達到「建 *立批次* 」步驟後，在請求內文中新增下列欄位：

```json
{
    ...
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
    ...
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允許生成有關 [!DNL Platform] 批的詳細錯誤消息的標籤。 |
| `partialIngestionPercentage` | 整個批失敗前可接受錯誤的百分比。 因此，在此示例中，最多5%的批可能是錯誤，否則將失敗。 |


## 在UI中啟用批次以擷取部分批次 {#enable-ui}

>[!NOTE]
>
>本節說明如何使用UI啟用批處理以進行部分批處理。 如果您已使用API啟用批次以擷取部分批次，則可跳至下一節。

若要透過 [!DNL Platform] UI啟用批次以進行部分擷取，您可以透過來源連線建立新批次、在現有資料集中建立新批次，或透過「[!UICONTROL Map CSV to XDM flow]」建立新批次。

### 建立新源連接 {#new-source}

要建立新源連接，請遵循「源」概述中列出的 [步驟](../../sources/home.md)。 在到達「資料 *[!UICONTROL 流詳細資訊]* 」步驟後 *[!UICONTROL ，請注意「部分]* 提取 *[!UICONTROL 」和「]* 錯誤診斷」欄位。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

「部 *[!UICONTROL 分擷取]* 」切換可讓您啟用或停用部分批次擷取的使用。

僅當 *[!UICONTROL Partial Ingestion（部分攝取）關]* 閉時，才會顯示 ** Error diagnostics（錯誤診斷）切換。 此功能可 [!DNL Platform] 產生有關您所擷取批次的詳細錯誤訊息。 如果已 *[!UICONTROL 開啟「部分擷取]* 」切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

「錯 *[!UICONTROL 誤閾值]* 」(Error threshold)允許您在整個批失敗之前設定可接受錯誤的百分比。 依預設，此值會設為5%。

### 使用現有資料集 {#existing-dataset}

若要使用現有資料集，請從選取資料集開始。 右側的側欄會填入資料集的相關資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

「部 *[!UICONTROL 分擷取]* 」切換可讓您啟用或停用部分批次擷取的使用。

僅當 *[!UICONTROL Partial Ingestion（部分攝取）關]* 閉時，才會顯示 ** Error diagnostics（錯誤診斷）切換。 此功能可 [!DNL Platform] 產生有關您所擷取批次的詳細錯誤訊息。 如果已 *[!UICONTROL 開啟「部分擷取]* 」切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

「錯 *[!UICONTROL 誤閾值]* 」(Error threshold)允許您在整個批失敗之前設定可接受錯誤的百分比。 依預設，此值會設為5%。

現在，您可以使用「新增資料」 **按鈕來上傳資料** ，而且會使用部分擷取來擷取資料。

### 使用「將[!UICONTROL CSV對應至XDM架構]」流程 {#map-flow}

若要使用「將[!UICONTROL CSV對應至XDM架構]」流程，請遵循「將CSV檔案對應」教學課程中 [所列的步驟](../tutorials/map-a-csv-file.md)。 一旦到達「添 *[!UICONTROL 加資料]* 」步驟 *[!UICONTROL ，請記下「部分提取」和「錯誤診斷」欄位]*** 。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

「部 *[!UICONTROL 分擷取]* 」切換可讓您啟用或停用部分批次擷取的使用。

僅當 *[!UICONTROL Partial Ingestion（部分攝取）關]* 閉時，才會顯示 ** Error diagnostics（錯誤診斷）切換。 此功能可 [!DNL Platform] 產生有關您所擷取批次的詳細錯誤訊息。 如果已 *[!UICONTROL 開啟「部分擷取]* 」切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

「錯 *[!UICONTROL 誤閾值]* 」(Error threshold)允許您在整個批失敗之前設定可接受錯誤的百分比。 依預設，此值會設為5%。

## 擷取部分批次擷取錯誤 {#retrieve-errors}

如果批包含失敗，您需要檢索這些失敗的錯誤資訊，以便重新收錄資料。

### 檢查狀態 {#check-status}

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
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
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

## 下一步 {#next-steps}

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
