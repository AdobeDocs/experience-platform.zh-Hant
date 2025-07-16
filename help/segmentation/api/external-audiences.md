---
title: 外部對象API端點
description: 瞭解如何使用外部對象API，以從Adobe Experience Platform建立、更新、啟用和刪除外部對象。
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 4%

---


# 外部受眾端點

外部受眾可讓您將設定檔資料從外部來源上傳到Adobe Experience Platform。 您可以使用Segmentation Service API中的`/external-audience`端點來將外部對象擷取到Experience Platform、檢視詳細資料並更新外部對象，以及刪除外部對象。

## 快速入門

>[!IMPORTANT]
>
>本指南中的端點會加上前置詞`/core/ais`，而不是`/core/ups`。

若要使用Experience Platform API，您必須已完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程，提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要一個標頭，以指定將執行操作的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 建立外部對象 {#create-audience}

您可以對`/external-audience/`端點發出POST要求，以建立外部對象。

**API格式**

```http
POST /external-audience/
```

**要求**

+++ 建立外部受眾的範例要求。

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `name` | 字串 | 外部對象的名稱。 |
| `description` | 字串 | 適用於外部對象的說明（選用）。 |
| `customAudienceId` | 字串 | 外部對象的選用識別碼。 |
| `fields` | 物件陣列 | 欄位清單及其資料型別。 建立欄位清單時，您可以新增下列專案： <ul><li>`name`： **必要**&#x200B;屬於外部對象規格的欄位名稱。</li><li>`type`： **必要**&#x200B;進入欄位的資料型別。 支援的值包括`string`、`number`、`long`、`integer`、`date` (`2025-05-13`)、`datetime` (`2025-05-23T20:19:00+00:00`)和`boolean`。</li>`identityNs`： **身分欄位需要**&#x200B;身分欄位使用的名稱空間。 支援的值包含所有有效的名稱空間，例如`ECID`或`email`.li><li>`labels`： *選擇性*&#x200B;欄位的存取控制標籤陣列。 在[資料使用標籤字彙表](/help/data-governance/labels/reference.md)中找到有關可用存取控制標籤的更多資訊。 </li></ul> |
| `sourceSpec` | 物件 | 包含外部對象所在資訊的物件。 使用此物件時，您&#x200B;**必須**&#x200B;包含下列資訊： <ul><li>`path`： **必要**：來源內外部對象或包含外部對象的資料夾的位置。</li><li>`type`： **必要**&#x200B;您要從來源擷取的物件型別。 此值可以是`file`或`folder`。</li><li>`sourceType`： *選擇性*&#x200B;您要擷取的來源型別。 目前唯一支援的值是`Cloud Storage`。</li><li>`cloudType`： *選擇性*&#x200B;雲端儲存的型別（根據來源型別）。 支援的值包括`S3`、`DLZ`、`GCS`和`SFTP`。</li><li>`baseConnectionId`：基礎連線的識別碼，由您的來源提供者提供。 如果使用&#x200B;**、**&#x200B;或`cloudType`的`S3`值，則此值為`GCS`必要`SFTP`。 如需詳細資訊，請閱讀[來源聯結器總覽](../../sources/home.md)li></ul> |
| `ttlInDays` | 整數 | 外部對象的資料有效期（天）。 此值可以設定從1到90。 依預設，資料到期日設為30天。 |
| `audienceType` | 字串 | 外部對象的對象型別。 目前僅支援`people`。 |
| `originName` | 字串 | **必要**&#x200B;對象來源。 這會指出受眾的來源。 對於外部對象，您應該使用`CUSTOM_UPLOAD`。 |
| `namespace` | 字串 | 對象的名稱空間。 預設情況下，此值設定為`CustomerAudienceUpload`。 |
| `labels` | 字串陣列 | 套用至外部對象的存取控制標籤。 在[資料使用標籤字彙表](/help/data-governance/labels/reference.md)中找到有關可用存取控制標籤的更多資訊。 |
| `tags` | 字串陣列 | 您要套用至外部對象的標籤。 您可以在[管理標籤指南](/help/administrative-tags/ui/managing-tags.md)中找到標籤的詳細資訊。 |

+++

**回應**

成功的回應會傳回HTTP狀態202以及您新建立的外部對象的詳細資料。

+++ 建立外部對象時的範例回應。

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `operationId` | 字串 | 作業的ID。 您之後可以使用此ID來擷取對象建立的狀態。 |
| `operationDetails` | 物件 | 此物件包含您提交以建立外部對象之要求的詳細資料。 |
| `name` | 字串 | 外部對象的名稱。 |
| `description` | 字串 | 外部對象的說明。 |
| `fields` | 物件陣列 | 欄位清單及其資料型別。 此陣列會決定您在外部對象中需要哪些欄位。 |
| `sourceSpec` | 物件 | 包含外部對象所在資訊的物件。 |
| `ttlInDays` | 整數 | 外部對象的資料有效期（天）。 此值可以設定從1到90。 依預設，資料到期日設為30天。 |
| `audienceType` | 字串 | 外部對象的對象型別。 |
| `originName` | 字串 | **必要**&#x200B;對象來源。 這會指出受眾的來源。 |
| `namespace` | 字串 | 對象的名稱空間。 |
| `labels` | 字串陣列 | 套用至外部對象的存取控制標籤。 在[資料使用標籤字彙表](/help/data-governance/labels/reference.md)中找到有關可用存取控制標籤的更多資訊。 |


+++

## 擷取對象建立狀態 {#retrieve-status}

您可以對`/external-audiences/operations`端點發出GET要求，並提供您從建立外部對象回應中收到的作業ID，藉此擷取外部對象提交狀態。

**API格式**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{OPERATION_ID}` | 您要擷取之作業的`id`值。 |

**要求**

+++ 擷取外部對象操作狀態的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及外部對象任務狀態的詳細資料。

+++ 擷取外部對象任務狀態時的範例回應。

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `operationId` | 字串 | 您要擷取的作業ID。 |
| `status` | 字串 | 作業的狀態。 這可以是下列其中一個值： `SUCCESS`、`FAILED`、`PROCESSING`。 |
| `operationDetails` | 物件 | 包含對象詳細資料的物件。 |
| `audienceId` | 字串 | 作業正在提交的外部對象ID。 |
| `createdBy` | 字串 | 建立外部對象之使用者的ID。 |
| `createdAt` | 長紀元時間戳記 | 提交建立外部對象請求時的時間戳記（以秒為單位）。 |
| `updatedBy` | 字串 | 上次更新對象的使用者ID。 |
| `updatedAt` | 長紀元時間戳記 | 上次更新對象的時間戳記（以秒為單位）。 |

+++

## 更新外部對象 {#update-audience}

>[!NOTE]
>
>若要使用下列端點，您必須擁有外部對象的`audienceId`。 您可從對`audienceId`端點的成功呼叫取得您的`GET /external-audiences/operations/{OPERATION_ID}`。

您可以對`/external-audience`端點發出PATCH要求，並在要求路徑中提供對象的ID，以更新外部對象的欄位。

使用此端點時，您可以更新以下欄位：

- 客群說明
- 欄位層級存取控制標籤
- 對象層級存取控制標籤

使用此端點&#x200B;**更新欄位會取代**&#x200B;您要求的欄位內容。

**API格式**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**要求**

+++ 更新外部對象說明的範例要求。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `description` | 字串 | 外部對象的更新說明。 |

此外，您可以更新下列引數：

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `labels` | 陣列 | 一個陣列，包含對象的更新存取標籤清單。 在[資料使用標籤字彙表](/help/data-governance/labels/reference.md)中找到有關可用存取控制標籤的更多資訊。 |
| `fields` | 物件陣列 | 一個陣列，包含外部對象的欄位及其相關標籤。 只有列於PATCH請求中的欄位才會更新。 在[資料使用標籤字彙表](/help/data-governance/labels/reference.md)中找到有關可用存取控制標籤的更多資訊。 |
| `ttlInDays` | 整數 | 外部對象的資料有效期（天）。 此值可以設定從1到90。 |

+++

**回應**

成功的回應會傳回HTTP狀態200以及已更新外部對象的詳細資料。

+++ 更新外部對象說明時的範例回應。

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## 開始對象內嵌 {#start-audience-ingestion}

>[!IMPORTANT]
>
>如果先前的對象內嵌已在進行中，您&#x200B;**無法**&#x200B;開始外部對象的新內嵌。

>[!NOTE]
>
>若要使用下列端點，您必須擁有外部對象的`audienceId`。 您可從對`audienceId`端點的成功呼叫取得您的`GET /external-audiences/operations/{OPERATION_ID}`。

您可以在提供對象ID時，透過向下列端點發出POST請求來開始對象擷取。

**API格式**

```http
POST /external-audience/{AUDIENCE_ID}/run
```

**要求**

以下請求會觸發外部對象的擷取執行。

+++ 開始受眾擷取的範例要求。

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/run \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | 紀元時間戳記 | **必要**&#x200B;指定流程執行的開始時間範圍，以選取要處理的檔案。 |
| `dataFilterEndTime` | 紀元時間戳記 | 指定流程執行的結束時間範圍，以選取要處理的檔案。 |
| `differentialIngestion` | 布林值 | 此欄位會根據自上次擷取以來的差異，判斷擷取是否為部分擷取，或是完整受眾擷取。 預設值為`true`。 |

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含擷取執行的詳細資訊。

+++ 開始對象擷取時的範例回應。

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `audienceName` | 字串 | 您正在開始內嵌回合的對象名稱。 |
| `audienceId` | 字串 | 對象的ID。 |
| `runId` | 字串 | 您啟動的內嵌執行ID。 |
| `differentialIngestion` | 布林值 | 此欄位會根據自上次擷取以來的差異，或根據完整對象擷取來判斷擷取是否為部分擷取。 |
| `dataFilterStartTime` | 紀元時間戳記 | 指定流程執行的開始時間，以選取已處理檔案的範圍。 |
| `dataFilterEndTime` | 紀元時間戳記 | 指定流程執行的結束時間範圍，以選取已處理的檔案。 |
| `createdAt` | 長紀元時間戳記 | 提交建立外部對象請求時的時間戳記（以秒為單位）。 |
| `createdBy` | 字串 | 建立外部對象之使用者的ID。 |

+++

## 擷取特定對象擷取狀態 {#retrieve-ingestion-status}

您可以在提供對象和執行ID的同時，透過向以下端點發出GET請求來擷取對象擷取狀態。

**API格式**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**要求**

以下請求會擷取外部對象的擷取狀態。

+++ 擷取外部對象擷取狀態的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及外部對象擷取的詳細資料。

+++ 擷取外部對象擷取時的範例回應。

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `audienceName` | 字串 | 對象名稱。 |
| `audienceId` | 字串 | 對象的ID。 |
| `runId` | 字串 | 擷取回合的ID。 |
| `status` | 字串 | 擷取執行的狀態。 可能的狀態包括`SUCCESS`和`FAILED`。 |
| `differentialIngestion` | 布林值 | 此欄位會根據自上次擷取以來的差異，或根據完整對象擷取來判斷擷取是否為部分擷取。 |
| `dataFilterStartTime` | 紀元時間戳記 | 指定流程執行的開始時間，以選取已處理檔案的範圍。 |
| `dataFilterEndTime` | 紀元時間戳記 | 指定流程執行的結束時間範圍，以選取已處理的檔案。 |
| `createdAt` | 長紀元時間戳記 | 提交建立外部對象請求時的時間戳記（以秒為單位）。 |
| `createdBy` | 字串 | 建立外部對象之使用者的ID。 |
| `details` | 物件陣列 | 包含擷取回合詳細資料的物件。 <ul><li>`stage`：擷取執行的階段。 這可以是`DATASET_INGEST`或`PROFILE_STORE_INGEST`，代表資料湖擷取和設定檔擷取。</li><li>`status`：階段上的擷取狀態。 可能的狀態包括`SUCCESS`和`FAILED`。</li><li>`flowRunId`：階段擷取流程執行的識別碼。</li></ul> |

+++

## 列出對象擷取狀態 {#list-ingestion-statuses}

您可以在提供對象ID時，透過向下列端點發出GET請求來擷取所選外部對象的所有擷取狀態。 可以包含多個引數，以&amp;符號(`&`)分隔。

**API格式**

下列端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數來協助您聚焦於結果。

```http
GET /external-audience/{AUDIENCE_ID}/runs
GET /external-audience/{AUDIENCE_ID}/runs?{QUERY_PARAMETERS}
```

**查詢引數**

+++ 可用查詢引數的清單。

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `limit` | 回應中傳回的專案數上限。 此值的範圍介於1到40之間。 預設的限制設為20。 | `limit=30` |
| `sortBy` | 傳回專案的排序順序。 您可以依`name`或`ingestionTime`排序。 此外，您可以新增`-`符號來依&#x200B;**遞減**&#x200B;順序排序，而非&#x200B;**遞增**&#x200B;順序。 依預設，專案會依`ingestionTime`遞減排序。 | `sortBy=name` |
| `property` | 此篩選器可決定要顯示哪些對象擷取執行。 您可以篩選下列屬性： <ul><li>`name`：可讓您依對象名稱篩選。 如果使用此屬性，您可以使用`=`、`!=`、`=contains`或`!=contains`來比較。 </li><li>`ingestionTime`：可讓您依據擷取時間篩選。 如果使用此屬性，您可以使用`>=`或`<=`來比較。</li><li>`status`：可讓您依據擷取回合的狀態進行篩選。 如果使用此屬性，您可以使用`=`、`!=`、`=contains`或`!=contains`來比較。 </li></ul> | `property=ingestionTime<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++

**要求**

以下請求會擷取外部對象的所有擷取狀態。

+++ 取得對象擷取狀態清單的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定外部對象的擷取狀態清單。

+++ 擷取對象擷取狀態清單時的範例回應。

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        }
    ],
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
}
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `runs` | 物件 | 一個物件，其中包含屬於對象的擷取執行清單。 您可以在[擷取擷取狀態區段](#retrieve-ingestion-status)中找到有關這個物件的詳細資訊。 |
| `_page` | 物件 | 包含結果清單分頁資訊的物件。 |

+++

## 刪除外部對象 {#delete-audience}

您可以在提供對象ID時，透過向下列端點發出DELETE請求來刪除外部對象。

**API格式**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**要求**

以下請求會刪除指定的外部對象。

+++ 刪除外部對象的範例請求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態204和空白的回應本文。

## 後續步驟 {#next-steps}

閱讀本指南後，您現在已更能瞭解如何使用Experience Platform API建立、管理和刪除外部對象。 若要瞭解如何搭配Experience Platform UI使用外部對象，請閱讀[Audience Portal檔案](../ui/audience-portal.md)。

## 附錄 {#appendix}

下節列出使用外部對象API時可用的錯誤代碼。

| 平台錯誤代碼 | 狀態代碼 | 訊息 | 說明 |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | 由於驗證請求時發生錯誤，導致發生錯誤請求。 |
| 100911-400 | 400 | `BAD_REQUEST` | 提供了無效的權杖。 |
| 100920-401 | 401 | `UNAUTHORIZED` | 缺少標頭。 |
| 100921-401 | 401 | `UNAUTHORIZED` | 提供了無效的`imsOrgId`。 |
| 100922-401 | 401 | `UNAUTHORIZED` | 您無權使用外部對象API。 |
| 100940-404 | 404 | `NOT_FOUND` | 找不到請求的對象。 |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | 對象已存在。 |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | 請求結構有效，但由於邏輯或語意錯誤而無法處理。 |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | 在系統中處理請求時發生問題。 |
| 100970-502 | 502 | `BAD_GATEWAY` | 下游相依性有問題。 |
