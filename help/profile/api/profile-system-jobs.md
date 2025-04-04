---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 設定檔系統作業API端點
type: Documentation
description: Adobe Experience Platform可讓您從設定檔存放區中刪除資料集或批次，以移除不再需要或錯誤新增的即時客戶設定檔資料。 這需要使用設定檔API來建立設定檔系統作業或刪除請求。
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 2%

---

# 設定檔系統作業端點（刪除請求）

>[!IMPORTANT]
>
>在Microsoft Azure和Amazon Web Services (AWS)上執行的Adobe Experience Platform實作有下列端點。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。

Adobe Experience Platform可讓您從多個來源擷取資料，並為個別客戶建立強大的設定檔。 擷取到[!DNL Experience Platform]的資料儲存在[!DNL Data Lake]中，如果已為設定檔啟用資料集，則該資料也會儲存在[!DNL Real-Time Customer Profile]資料存放區中。 有時候，可能有必要從設定檔存放區中刪除與資料集相關聯的設定檔資料，以移除不再需要或錯誤新增的資料。 這需要使用[!DNL Real-Time Customer Profile] API來建立[!DNL Profile]系統作業或「刪除請求」。

>[!NOTE]
>
>如果您嘗試從[!DNL Data Lake]刪除資料集或批次，請造訪[目錄服務總覽](../../catalog/home.md)以取得詳細資訊。

## 快速入門

本指南中使用的API端點是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在繼續之前，請先檢閱[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience Platform API所需必要標題的重要資訊。

## 檢視刪除請求 {#view}

刪除請求是長期執行的非同步程式，這表示您的組織可能同時執行多個刪除請求。 若要檢視貴組織目前執行的所有刪除請求，您可以對`/system/jobs`端點執行GET請求。

您也可以使用選用的查詢引數，以篩選回應中傳回的刪除請求清單。 若要使用多個引數，請使用&amp;符號(`&`)分隔每個引數。

**API格式**

>[!AVAILABILITY]
>
>在Microsoft Azure上使用Experience Platform時，下列查詢引數僅&#x200B;**可用**。
>
>在AWS上使用此端點時，前100個系統作業會根據其建立日期以降序傳回。

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 根據請求的建立時間，位移傳回結果的頁面。 | `start=4` |
| `limit` | 限制傳回的結果數。 | `limit=10` |
| `page` | 根據請求的建立時間，傳回結果的特定頁面。 | `page=2` |
| `sort` | 以遞增(`asc`)或遞減(`desc`)順序依特定欄位排序結果。 傳回多個結果頁面時，排序引數無法運作。 | `sort=batchId:asc` |

**要求**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的以下要求不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 檢視系統作業的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>將此端點與AWS搭配使用時，您&#x200B;**必須**&#x200B;使用`x-sandbox-id`要求標頭，而非`x-sandbox-name`要求標頭。

+++ 檢視系統作業的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**回應**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的下列回應不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

成功的回應包括「children」陣列，每個刪除請求都有一個物件，其中包含該請求的詳細資訊。

+++ 檢視刪除請求的成功回應

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `_page.count` | 要求總數。 此回應已因空間而遭截斷。 |
| `_page.next` | 如果存在額外的結果頁面，請將[查詢請求](#view-a-specific-delete-request)中的ID值取代為提供的`"next"`值，以檢視下一頁的結果。 |
| `jobType` | 正在建立的工作型別。 在此情況下，它一律會傳回`"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值包括`"NEW"`、`"PROCESSING"`、`"COMPLETED"`和`"ERROR"`。 |
| `metrics` | 物件包含已處理的記錄數(`"recordsProcessed"`)、要求已處理的秒數時間，或要求完成所需的時間(`"timeTakenInSec"`)。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的回應會傳回一個陣列，其中包含每個系統請求的物件。

+++ 檢視系統請求的成功回應

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `requestId` | 系統作業的ID。 |
| `requestType` | 系統作業的型別。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系統作業的狀態。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含批次和/或系統作業之資料集ID的物件。 |

+++

>[!ENDTABS]

## 建立刪除請求 {#create-a-delete-request}

初始化新的刪除請求是透過POST請求完成至`/systems/jobs`端點，其中要刪除的資料集或批次識別碼會提供在請求內文中。

### 刪除資料集和相關聯的設定檔資料

若要從設定檔存放區中刪除資料集及與資料集相關聯的所有設定檔資料，必須在POST請求內文中包含資料集ID。 此動作將會刪除指定資料集的所有資料。 [!DNL Experience Platform]可讓您根據記錄和時間序列結構描述來刪除資料集。

**API格式**

```http
POST /system/jobs
```

**要求**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的以下要求不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 刪除資料集的範例請求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| 屬性 | 說明 |
| -------- | ----------- |
| `dataSetId` | 您要刪除的資料集ID。 |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>將此端點與AWS搭配使用時，您&#x200B;**必須**&#x200B;使用`x-sandbox-id`要求標頭，而非`x-sandbox-name`要求標頭。

+++ 刪除資料集的範例請求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| 屬性 | 說明 |
| -------- | ----------- |
| `dataSetId` | 您要刪除的資料集ID。 |

>[!ENDTABS]

**回應**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的下列回應不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

成功的回應會傳回新建立的刪除請求的詳細資料，包括請求的不重複、系統產生的唯讀ID。 這可用來查閱請求並檢查其狀態。 在建立時請求的`status`是`"NEW"`，直到它開始處理為止。 回應中的`dataSetId`應符合要求中傳送的`dataSetId`。

+++ 建立刪除請求的成功回應。

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的唯一刪除請求唯讀ID。 |
| `dataSetId` | 資料集的ID，如POST要求中所指定。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的回應會傳回新建立的系統要求的詳細資料。

+++ 建立刪除請求的成功回應。

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `requestId` | 系統作業的ID。 |
| `requestType` | 系統作業的型別。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系統作業的狀態。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含批次和/或系統作業之資料集ID的物件。 |

+++

>[!ENDTABS]

### 刪除批次

要刪除批次，批次ID必須包含在POST請求正文中。 請注意，您無法刪除以記錄結構描述為基礎的資料集批次。 只能刪除以時間序列結構描述為基礎的資料集批次。

>[!NOTE]
>
> 您無法刪除根據記錄結構描述之資料集的批次，因為記錄型別資料集批次會覆寫先前的記錄，因此無法「復原」或刪除。 根據記錄結構描述移除資料集錯誤批次影響的唯一方法是，使用正確的資料重新內嵌批次，以覆寫不正確的記錄。

如需有關記錄和時間序列行為的詳細資訊，請檢閱[!DNL XDM System]總覽中有關XDM資料行為](../../xdm/home.md#data-behaviors)的[區段。

**API格式**

```http
POST /system/jobs
```

**要求**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的以下要求不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 刪除批次的範例請求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| 屬性 | 說明 |
| -------- | ----------- |
| `datasetId` | 您要刪除之批次的資料集ID。 |
| `batchId` | 您要刪除之批次的ID。 |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>將此端點與AWS搭配使用時，您&#x200B;**必須**&#x200B;使用`x-sandbox-id`要求標頭，而非`x-sandbox-name`要求標頭。

+++ 刪除批次的範例請求。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| 屬性 | 說明 |
| -------- | ----------- |
| `datasetId` | 您要刪除之批次的資料集ID。 |
| `batchId` | 您要刪除之批次的ID。 |

>[!ENDTABS]

**回應**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的下列回應不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

成功的回應會傳回新建立的刪除請求的詳細資料，包括請求的不重複、系統產生的唯讀ID。 這可用來查閱請求並檢查其狀態。 在建立時請求的`"status"`是`"NEW"`，直到它開始處理為止。 回應中的`"batchId"`值應符合要求中傳送的`"batchId"`值。

+++ 建立刪除請求的成功回應。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的唯一刪除請求唯讀ID。 |
| `datasetId` | 指定資料集的識別碼。 |
| `batchId` | 批次的ID，如POST請求中所指定。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的回應會傳回新建立的系統要求的詳細資料。

+++ 建立刪除請求的成功回應。

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `requestId` | 系統作業的ID。 |
| `requestType` | 系統作業的型別。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系統作業的狀態。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含批次和/或系統作業之資料集ID的物件。 |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>在Microsoft Azure上使用Experience Platform時，下列功能僅&#x200B;**可用**。

如果您嘗試起始記錄資料集批次的刪除請求，您將會遇到400層級的錯誤，類似以下情況：

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## 檢視特定的刪除請求 {#view-a-specific-delete-request}

若要檢視特定刪除請求，包括其狀態等詳細資訊，您可以對`/system/jobs`端點執行查詢(GET)請求，並在路徑中包含刪除請求的ID。

**API格式**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | 您要檢視之刪除請求的ID。 |

**要求**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的以下要求不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ 檢視設定檔工作的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>將此端點與AWS搭配使用時，您&#x200B;**必須**&#x200B;使用`x-sandbox-id`要求標頭，而非`x-sandbox-name`要求標頭。

+++ 檢視設定檔工作的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**回應**

>[!IMPORTANT]
>
>Azure和AWS執行個體之間的下列回應不同。

>[!BEGINTABS]

>[!TAB Microsoft Azure]

回應會提供刪除請求的詳細資訊，包括其更新狀態。 回應中的刪除要求ID （`"id"`值）應與要求路徑中傳送的ID相符。

+++ 檢視刪除請求的成功回應。

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| 屬性 | 說明 |
| ---------- | ----------- |
| `jobType` | 正在建立的工作型別，在此情況下，一律會傳回`"DELETE"`。 |
| `status` | 刪除請求的狀態。 可能的值包括`NEW`、`PROCESSING`、`COMPLETED`和`ERROR`。 |
| `metrics` | 陣列，包含已處理的記錄數(`"recordsProcessed"`)以及處理要求所需的秒數，或是完成要求所需的時間(`"timeTakenInSec"`)。 |

+++

>[!TAB Amazon Web Services (AWS)]

成功的回應會傳回指定系統要求的詳細資料。

+++ 檢視刪除請求的成功回應。

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `requestId` | 系統作業的ID。 |
| `requestType` | 系統作業的型別。 可能的值包括`BACKFILL_TTL`、`DELETE_EE_BATCH`和`TRUNCATE_DATASET`。 |
| `status` | 系統作業的狀態。 可能的值包括`NEW`、`SUCCESS`、`ERROR`、`FAILED`和`IN-PROGRESS`。 |
| `properties` | 包含批次和/或系統作業之資料集ID的物件。 |

+++

>[!ENDTABS]

刪除請求狀態為`"COMPLETED"`後，您可以嘗試使用資料存取API存取已刪除的資料，以確認資料已刪除。 如需如何使用資料存取API存取資料集和批次的指示，請檢閱[資料存取檔案](../../data-access/home.md)。

## 移除刪除請求

>[!AVAILABILITY]
>
>此端點在Adobe Experience Platform的Azure執行個體中僅&#x200B;**支援**，而在AWS執行個體中則是&#x200B;**不支援**。

[!DNL Experience Platform]可讓您刪除先前的請求，這可能對許多原因有用，包括刪除工作未完成或卡在處理階段中。 若要移除刪除請求，您可以對`/system/jobs`端點執行DELETE請求，並將您要移除之刪除請求的ID加入請求路徑。

**API格式**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | 您要移除之刪除請求的ID。 |

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的刪除請求會傳回HTTP狀態200 （確定）和空白的回應內文。 您可以透過執行GET請求來確認請求已刪除，以依據其ID檢視刪除請求。 這會傳回HTTP狀態404 （找不到），指出刪除請求已移除。

## 後續步驟

現在您已經知道從[!DNL Experience Platform]內的[!DNL Profile store]刪除資料集和批次所涉及的步驟，您可以安全地刪除已錯誤新增或您的組織不再需要的。 請注意，刪除請求無法復原，因此您應該僅刪除確信現在不需要且未來不需要的資料。
