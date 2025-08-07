---
title: 資料集過期API端點
description: 資料衛生API中的/ttl端點可讓您以程式設計方式在Adobe Experience Platform中排程資料集有效期。
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# 資料集到期端點

使用資料衛生API中的`/ttl`端點來排程Adobe Experience Platform中的資料集何時應該刪除。

資料集到期時間是延遲的刪除作業。 資料集在過渡期間不受保護，並可能在排程到期之前透過其他方法刪除。

>[!NOTE]
>
>雖然到期時間指定為特定即時，但在實際刪除開始之前，到期後最多可能有24小時的延遲。 開始刪除後，可能需要長達七天的時間，資料集的所有追蹤才會從Experience Platform系統中移除。

刪除開始前，您可以取消到期日或變更其排程時間。 若要重新開啟已取消的到期日，請設定新的到期日。

刪除開始後，到期工作將標籤為`executing`且無法再修改。 資料集最多可以復原七天，但必須透過手動Adobe服務請求進行。 在刪除期間，Data Lake、Identity Service和即時客戶設定檔會分別移除資料集內容。 刪除完成時，到期日會標示為`completed`。

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更任何可能會將資料擷取至該資料集的資料流程，讓您的下游工作流程不會受到負面影響。

進階資料生命週期管理支援透過資料集到期端點進行資料集刪除，以及使用主要身分透過[工單端點](./workorder.md)進行的識別碼刪除（列層級資料）。 您也可以透過Experience Platform UI管理[資料集有效期](../ui/dataset-expiration.md)和[記錄刪除](../ui/record-delete.md)。 如需詳細資訊，請參閱連結的檔案。

>[!NOTE]
>
>資料生命週期不支援批次刪除。

## 快速入門

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱[API指南](./overview.md)，以瞭解CRUD作業、錯誤訊息、Postman集合的必要標頭，以及如何讀取範例API呼叫的相關資訊。

>[!IMPORTANT]
>
>呼叫資料衛生API時，您必須使用 — H `x-sandbox-name: {SANDBOX_NAME}`標頭。

## 列出資料集有效期 {#list}

您可以透過向`/ttl`端點發出GET請求，列出為貴組織設定的所有資料集有效期。

使用查詢引數篩選結果，以僅傳回符合您條件的到期日。 每個結果都包含每個資料集到期日的狀態和設定詳細資訊。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 選擇性查詢引數清單，具有多個以`&`字元分隔的引數。 常見的引數包括`limit`和`page`以用於分頁目的。 如需支援的查詢引數完整清單，請參閱[附錄區段](#query-params)支援的查詢引數完整清單。 最常用的引數包含於下文及附錄中。 |
| `author` | 依最近更新或建立資料集過期時間的使用者篩選。 支援類似SQL的模式（例如，`LIKE %john%`）。 |
| `datasetId` | 依特定資料集ID篩選有效期。 |
| `datasetName` | 資料集名稱相符專案的不區分大小寫的篩選器。 |
| `status` | 以逗號分隔的狀態清單篩選： `pending`， `executing`， `cancelled`， `completed`。 |
| `expiryDate` | 篩選具有特定到期日的到期日。 |
| `limit` | 指定要傳回的結果數量上限（1-100，預設值： 25）。 |
| `page` | 使用從零開始的索引（預設頁面大小：50，最大值：100）將結果分頁。 |

{style="table-layout:auto"}

**要求**

下列請求會擷取在2021年8月1日之前更新，且上次更新者名稱符合「Jane Doe」的使用者之所有資料集有效期。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會列出產生的資料集有效期。 下列範例的空格已截斷。

>[!IMPORTANT]
>
>回應中的`ttlId`也稱為`{DATASET_EXPIRATION_ID}`。 兩者都會參照資料集到期的唯一識別碼。

```json
{
  "results": [
    {
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| 屬性 | 說明 |
| --- | --- |
| `results` | 資料集到期設定的陣列。 |
| `ttlId` | 資料集到期設定的唯一識別碼。 |
| `datasetId` | 與此設定相關之資料集的唯一識別碼。 |
| `datasetName` | 資料集的名稱。 |
| `sandboxName` | 設定此資料集有效期的沙箱。 |
| `displayName` | 到期設定的易讀名稱。 |
| `description` | 到期設定的說明。 |
| `imsOrg` | 您的唯一組織識別碼。 |
| `status` | 到期的目前狀態。 其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 排程的到期日期和時間（ISO 8601格式）。 |
| `updatedAt` | 此組態上次更新的時間戳記。 |
| `updatedBy` | 上次更新設定之使用者或服務的識別碼和電子郵件。 |
| `current_page` | 目前結果頁面的索引（從零開始）。 |
| `total_pages` | 可用的結果頁總數。 |
| `total_count` | 傳回的資料集到期設定記錄總數。 |

{style="table-layout:auto"}

## 查詢資料集有效期 {#lookup}

透過提出使用資料集到期ID或資料集ID作為路徑引數的GET請求，擷取特定資料集到期設定的詳細資料。

>[!IMPORTANT]
>
>您可以在路徑中提供資料集到期日ID （例如`SD-xxxxxx-xxxx`）或資料集ID。 回應中的`ttlId`是資料集到期的唯一識別碼。

**API格式**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| 參數 | 說明 |
| --- | --- |
| `{ID}` | 資料集到期設定的唯一識別碼。 您可以提供資料集有效期ID或資料集ID。 |
| `include` | （選擇性）如果設為`history`，則回應會包含設定的`history`陣列和變更事件。 |

{style="table-layout:auto"}

**要求**

下列要求會查詢資料集`62759f2ede9e601b63a2ee14`的到期詳細資料：

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集到期日的詳細資料。

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集到期設定的唯一識別碼。 |
| `datasetId` | 資料集的唯一識別碼。 |
| `datasetName` | 資料集的名稱。 |
| `sandboxName` | 設定資料集有效期的沙箱。 |
| `displayName` | 適用於資料集到期設定的易讀名稱。 |
| `description` | 資料集到期設定的說明。 |
| `imsOrg` | 您與此設定相關聯的唯一組織識別碼。 |
| `status` | 資料集到期設定的目前狀態。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 資料集的已排程到期時間戳記（ISO 8601格式）。 |
| `updatedAt` | 最近更新的時間戳記。 |
| `updatedBy` | 上次更新資料集到期日之使用者或服務的識別碼和電子郵件。 |

{style="table-layout:auto"}

### 目錄到期標籤

使用[目錄API](../../catalog/api/getting-started.md)查詢資料集詳細資料時，如果資料集有效到期，則會列在`tags.adobe/hygiene/ttl`下。

下列JSON針對到期值為`32503680000000`的資料集顯示截斷的目錄API回應。 標籤會將到期編碼為自Unix紀元以來的毫秒數。

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## 建立資料集有效期 {#create}

建立新的資料集到期設定，以定義資料集到期並符合刪除資格。\
提供資料集ID、到期日或日期時間（ISO 8601格式）、顯示名稱及（選擇性）說明。

>[!NOTE]
>
>有效期值可能是日期(YYYY-MM-DD)或日期和時間(YYYY-MM-DDTHH:MM:SSZ)。 如果您只提供日期，系統會使用當天的午夜UTC (00:00:00Z)。 到期日必須在未來至少24小時。

若要建立資料集有效期，請傳送POST要求，如下所示。

>[!TIP]
>
>如果您收到404錯誤，請確定請求沒有其他正斜線。 結尾斜線可能會導致POST要求失敗。

**API格式**

```http
POST /ttl
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `datasetId` | **必要。**&#x200B;要套用到期日之資料集的唯一識別碼。 |
| `expiry` | **必要。** ISO 8601格式的到期日期和時間。 這會定義系統內的資料有效期限。 如果只提供日期，則預設為UTC午夜(00:00:00Z)。 到期日&#x200B;**在未來**&#x200B;必須至少為24小時。 <br>**附註**：<ul><li>如果資料集已存在資料集有效期，請求將失敗。</li></ul> |
| `displayName` | **必要。**&#x200B;適用於資料集到期設定的可讀取名稱。 |
| `description` | 資料集到期設定的選擇性說明。 |

**回應**

成功的回應會傳回HTTP 201 （已建立）狀態和新的資料集到期設定。

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 適用於已建立資料集到期設定的唯一識別碼。 |
| `datasetId` | 資料集的唯一識別碼。 |
| `datasetName` | 資料集的名稱。 |
| `sandboxName` | 設定此資料集有效期的沙箱。 |
| `displayName` | 資料集到期設定的顯示名稱。 |
| `description` | 資料集到期設定的說明。 |
| `imsOrg` | 您與此設定相關聯的唯一組織識別碼。 |
| `status` | 資料集到期設定的目前狀態。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 資料集的已排程到期時間戳記。 |
| `updatedAt` | 最近更新的時間戳記。 |
| `updatedBy` | 上次更新資料集到期設定之使用者或服務的識別碼和電子郵件。 |

如果資料集已存在資料集有效期，則會出現400 （錯誤請求） HTTP狀態。 如果資料集不存在或您無權存取資料集，則會出現404 （找不到） HTTP狀態。

## 更新資料集到期日設定 {#update}

若要更新現有的資料集到期組態，請向`/ttl/DATASET_EXPIRATION_ID`發出PUT請求。 您只能更新設定的`displayName`、`description`和`expiry`欄位。 只有在到期狀態為`pending`時才允許更新。

>[!NOTE]
>
>`expiry`欄位接受日期(YYYY-MM-DD)或日期和時間(YYYY-MM-DDTHH:MM:SSZ)。 如果只提供日期，系統會使用當天的午夜UTC (00:00:00Z)。 到期日&#x200B;**在未來**&#x200B;必須至少為24小時。

**API格式**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | 資料集到期設定的唯一識別碼。 **注意**：這稱為回應中的`ttlId`。 |

**要求**

下列要求會更新資料集有效期`SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`的到期日、顯示名稱和描述：

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `displayName` | （選用）適用於資料集到期設定的全新人類可讀名稱。 |
| `description` | （選用）資料集到期設定的新說明。 |
| `expiry` | （選用）新的到期日或ISO 8601格式的日期和時間。 如果只提供日期，則預設為UTC午夜。 到期日必須在未來&#x200B;**至少24小時**。 |

>[!NOTE]
>
>請求中必須提供這些欄位中的至少一個。

**回應**

成功的回應會傳回HTTP狀態200 （確定）和更新的資料集到期設定。

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 已更新資料集到期設定的唯一識別碼。 |
| `datasetId` | 資料集的唯一識別碼。 |
| `datasetName` | 資料集的名稱。 |
| `sandboxName` | 設定此資料集有效期的沙箱。 |
| `displayName` | 資料集到期設定的顯示名稱。 |
| `description` | 資料集到期設定的說明。 |
| `imsOrg` | 與此設定相關聯的組織ID。 |
| `status` | 資料集到期設定的目前狀態。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 資料集的已排程到期時間戳記。 |
| `updatedAt` | 最近更新的時間戳記。 |
| `updatedBy` | 上次更新資料集到期設定之使用者或服務的識別碼和電子郵件。 |

{style="table-layout:auto"}

如果資料集過期時間不存在，失敗的回應會傳回404 （找不到） HTTP狀態。

## 取消資料集有效期 {#delete}

藉由向`/ttl/{ID}`發出DELETE要求，取消擱置的資料集到期組態。

>[!NOTE]
>
>只能取消處於`pending`狀態的資料集有效期。 嘗試取消已經是`executing`、`completed`或`cancelled`的到期會傳回HTTP 400 （錯誤請求）。

**API格式**

```http
DELETE /ttl/{ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ID}` | 資料集到期設定的唯一識別碼。 您可以提供資料集有效期ID或資料集ID。 |

{style="table-layout:auto"}

**要求**

下列要求會取消ID為`SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`的資料集有效期：

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200 （確定）和已取消的資料集到期設定。 不是到期的`status`屬性設定為`cancelled`。

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| 屬性 | 說明 |
|---|---|
| `ttlId` | 已刪除資料集到期設定的唯一識別碼。 |
| `datasetId` | 資料集的唯一識別碼。 |
| `datasetName` | 資料集的名稱。 |
| `sandboxName` | 設定此資料集有效期的沙箱。 |
| `displayName` | 資料集到期設定的顯示名稱。 |
| `description` | 資料集到期設定的說明。 |
| `imsOrg` | 您與此設定相關聯的唯一組織識別碼。 |
| `status` | 資料集到期設定的目前狀態。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 資料集的已排程到期時間戳記。 |
| `updatedAt` | 最近更新的時間戳記。 |
| `updatedBy` | 上次更新資料集到期設定之使用者或服務的識別碼和電子郵件。 |

**範例400 （錯誤請求）回應**

嘗試取消具有`executing`、`completed`或`cancelled`到期組態的資料集時發生400錯誤。

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>嘗試取消已經是`completed`或`cancelled`的資料集到期時，會發生404錯誤。

## 附錄

### 接受的查詢引數 {#query-params}

下表概述[列出資料集有效期](#list)時可用的查詢引數：

>[!NOTE]
>
>`description`、`displayName`和`datasetName`引數都包含依據LIKE值搜尋的能力。 這表示您可以搜尋字串「Name1」，以尋找名為「Name123」、「Name183」、「DisplayName1234」的排程資料集有效期。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `author` | 使用`author`查詢引數來尋找最近更新資料集到期日的人員。 如果自建立後未進行任何更新，則會符合到期的原始建立者。 此引數符合`created_by`欄位與搜尋字串對應的有效期。<br>如果搜尋字串的開頭為`LIKE`或`NOT LIKE`，其餘部分會視為SQL搜尋模式。 否則，會將整個搜尋字串視為必須完全符合`created_by`欄位之整個內容的常值字串。 | `author=LIKE %john%`、`author=John Q. Public` |
| `datasetId` | 符合套用至特定資料集的到期日。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | 符合資料集名稱包含所提供搜尋字串的到期日。 相符專案不區分大小寫。 | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | 符合顯示名稱包含所提供搜尋字串的到期日。 相符專案不區分大小寫。 | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | 根據確切的執行日期、執行的結束日期或執行的開始日期來篩選結果。 它們可用來擷取與特定日期、特定日期之前或特定日期之後執行作業相關聯的資料或記錄。 | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | 符合在指定日期的24小時期間內發生的到期。 | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | 符合指定間隔內即將執行或已執行的到期日。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | 介於1到100之間的整數，表示要傳回的最大到期次數。 預設為25。 | `limit=50` |
| `orderBy` | `orderBy`查詢引數指定API傳回結果的排序順序。 使用它可根據一或多個欄位來排列資料，以遞增(ASC)或遞減(DESC)順序排列。 使用+或 — 首碼分別表示ASC、DESC。 接受下列值： `displayName`、`description`、`datasetName`、`id`、`updatedBy`、`updatedAt`、`expiry`、`status`。 | `-datasetName` |
| `orgId` | 比對組織ID與引數相符的資料集有效期。 此值預設為`x-gw-ims-org-id`標頭的值，除非請求提供服務權杖，否則會忽略此值。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | 整數，指出要傳回的過期頁面。 | `page=3` |
| `sandboxName` | 符合沙箱名稱與引數完全相符的資料集有效期。 預設為請求的`x-sandbox-name`標頭中的沙箱名稱。 使用`sandboxName=*`包含所有沙箱的資料集有效期。 | `sandboxName=dev1` |
| `search` | 符合指定字串與有效期ID完全相符或是&#x200B;**包含**&#x200B;於下列任何欄位中的有效期：<br><ul><li>作者</li><li>顯示名稱</li><li>說明</li><li>顯示名稱</li><li>資料集名稱</li></ul> | `search=TESTING` |
| `status` | 以逗號分隔的狀態清單。 包含後，回應會比對資料集有效期，其目前狀態在所列資料集有效期中。 | `status=pending,cancelled` |
| `ttlId` | 符合具有特定ID的到期要求。 | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | 符合在指定日期的24小時視窗中更新的有效期。 | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | 符合在指定時間開始的24小時視窗中更新的有效期。<br><br>每次編輯時都會將到期視為已更新，包括建立、取消或執行的時間。 | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

