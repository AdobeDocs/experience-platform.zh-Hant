---
title: 資料集過期API端點
description: 資料衛生API中的/ttl端點可讓您以程式設計方式在Adobe Experience Platform中排程資料集有效期。
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 20d616463469a4d78fe0e7b6be0ec76b293789d6
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 2%

---

# 資料集到期端點

此 `/ttl` 資料衛生API中的端點可讓您為Adobe Experience Platform中的資料集排程到期日。

資料集到期時間只是計時延遲的刪除作業。 資料集在過渡期間不受保護，因此在到期之前可能會以其他方式刪除。

>[!NOTE]
>
>雖然到期時間指定為特定即時，但在實際刪除開始之前，到期後最多可能有24小時的延遲。 開始刪除後，可能需要長達七天的時間，資料集的所有追蹤才會從Platform系統中移除。

在實際起始資料集刪除作業之前，您可以隨時取消到期日或修改其觸發時間。 取消資料集到期日後，您可以設定新的到期日，以重新開啟資料集。

開始刪除資料集後，其到期工作將標籤為 `executing`，且可能不會進一步變更。 資料集本身最多可以復原七天，但必須透過Adobe服務要求啟動的手動程式進行。 請求執行時，Data Lake、Identity Service和即時客戶設定檔會開始個別程式，從各自的服務中移除資料集的內容。 從所有三項服務中刪除資料後，到期日將標籤為 `completed`.

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更任何可能會將資料擷取至該資料集的資料流程，讓您的下游工作流程不會受到負面影響。

## 快速入門

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱 [API指南](./overview.md) 以瞭解CRUD作業所需的標頭、錯誤訊息、Postman集合，以及如何讀取範例API呼叫的相關資訊。

>[!IMPORTANT]
>
>呼叫資料衛生API時，您必須使用 — H `x-sandbox-name: {SANDBOX_NAME}` 標頭。

## 列出資料集有效期 {#list}

您可以發出GET要求，列出貴組織的所有資料集有效期。 查詢引數可用來篩選適當結果的回應。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 選擇性查詢引數清單，多個引數由下列專案分隔： `&` 個字元。 常見引數包括 `limit` 和 `page` 以作分頁之用。 如需支援的查詢引數完整清單，請參閱 [附錄部分](#query-params). |

{style="table-layout:auto"}

**要求**

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
>此 `ttlId` 在回應中亦稱為 `{DATASET_EXPIRATION_ID}`. 兩者都會參照資料集到期的唯一識別碼。

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| 屬性 | 說明 |
| --- | --- |
| `total_count` | 與清單呼叫的引數相符的資料集到期計數。 |
| `results` | 包含傳回資料集有效期的詳細資訊。 如需資料集到期屬性的詳細資訊，請參閱回應一節，以發出 [查詢呼叫](#lookup). |

{style="table-layout:auto"}

## 查詢資料集有效期 {#lookup}

若要查詢資料集有效期，請使用以下任一專案發出GET請求： `{DATASET_ID}` 或 `{DATASET_EXPIRATION_ID}`.

>[!IMPORTANT]
>
>此 `{DATASET_EXPIRATION_ID}` 稱為 `ttlId` 在回應中。 兩者都會參照資料集到期的唯一識別碼。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其有效期的資料集ID。 |
| `{DATASET_EXPIRATION_ID}` | 資料集過期時間的ID。 |

{style="table-layout:auto"}

**要求**

以下請求會查詢資料集的到期詳細資料 `62759f2ede9e601b63a2ee14`：

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
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期時間的ID。 |
| `datasetId` | 此到期適用於的資料集ID。 |
| `datasetName` | 此到期適用於的資料集的顯示名稱。 |
| `sandboxName` | 目標資料集所在之沙箱的名稱。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集到期的目前狀態。 |
| `expiry` | 刪除資料集的預定日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳記。 |
| `updatedBy` | 上次更新到期日的使用者。 |
| `displayName` | 到期要求的顯示名稱。 |
| `description` | 到期要求的說明。 |

{style="table-layout:auto"}

### 目錄到期標籤

使用時 [目錄API](../../catalog/api/getting-started.md) 若要查詢資料集詳細資訊，如果資料集有「作用中」有效期限，則會列在「作用中」底下 `tags.adobe/hygiene/ttl`.

以下JSON代表來自目錄之資料集詳細資料的截斷回應，其到期值為 `32503680000000`. 標籤的值會將到期編碼為自Unix紀元開始以來的整數毫秒數。

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

為確保資料在指定期間後從系統中移除，請以ISO 8601格式提供資料集ID和到期日與時間，以排程特定資料集的到期日。

若要建立資料集有效期，請執行如下所示的POST請求，並在裝載中提供下列提及的值。

>[!NOTE]
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
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| 屬性 | 說明 |
| --- | --- |
| `datasetId` | **必填** 您要為其排程到期的目標資料集ID。 |
| `expiry` | **必填** ISO 8601格式的日期和時間。 如果字串沒有明確的時區位移，則會假設時區為UTC。 系統內的資料有效期限是根據提供的到期值所設定。<br>注意：<ul><li>如果資料集已存在資料集有效期，請求將失敗。</li><li>此日期和時間必須至少為 **未來24小時**.</li></ul> |
| `displayName` | 資料集到期要求的選用顯示名稱。 |
| `description` | 到期要求的選擇性說明。 |

**回應**

成功的回應會傳回HTTP 201 （已建立）狀態和資料集到期的新狀態。

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期時間的ID。 |
| `datasetId` | 此到期適用於的資料集ID。 |
| `datasetName` | 此到期適用於的資料集的顯示名稱。 |
| `sandboxName` | 目標資料集所在之沙箱的名稱。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集到期的目前狀態。 |
| `expiry` | 刪除資料集的預定日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳記。 |
| `updatedBy` | 上次更新到期日的使用者。 |
| `displayName` | 到期要求的顯示名稱。 |
| `description` | 到期要求的說明。 |

如果資料集已存在資料集有效期，則會出現400 （錯誤請求） HTTP狀態。 如果資料集過期時間不存在（或您無權存取資料集），失敗的回應會傳回404 （找不到） HTTP狀態。

## 更新資料集有效期 {#update}

若要更新資料集的到期日，請使用PUT請求和 `ttlId`. 您可以更新 `displayName`， `description`、和/或 `expiry` 資訊。

>[!NOTE]
>
>如果您變更到期日和時間，未來必須至少為24小時。 此強制的延遲提供您取消或重新排程到期日的機會，並避免任何意外遺失資料。

**API格式**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | 您要變更的資料集有效期ID。 注意：這稱為 `ttlId` 在回應中。 |

**要求**

以下請求會重新排程資料集到期日 `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` 於2024年底發生（格林威治標準時間）。 如果找到現有的資料集有效期，則會以新的資料集更新該有效期 `expiry` 值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `expiry` | **必填** ISO 8601格式的日期和時間。 如果字串沒有明確的時區位移，則會假設時區為UTC。 系統內的資料有效期限是根據提供的到期值所設定。 相同資料集的任何先前到期時間戳記都會取代為您提供的新到期值。 此日期和時間必須至少為 **未來24小時**. |
| `displayName` | 到期要求的顯示名稱。 |
| `description` | 到期要求的選擇性說明。 |

{style="table-layout:auto"}

**回應**

如果更新了預先存在的到期時間，則成功的回應會傳回資料集到期時間的新狀態和HTTP狀態200 （確定）。

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期時間的ID。 |
| `datasetId` | 此到期適用於的資料集ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集到期的目前狀態。 |
| `expiry` | 刪除資料集的預定日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳記。 |
| `updatedBy` | 上次更新到期日的使用者。 |

{style="table-layout:auto"}

如果資料集過期時間不存在，失敗的回應會傳回404 （找不到） HTTP狀態。

## 取消資料集有效期 {#delete}

您可以發出DELETE要求來取消資料集到期日。

>[!NOTE]
>
>僅限狀態為的資料集有效期 `pending` 可以取消。 嘗試取消已執行或已取消的到期時傳回HTTP 404錯誤。

**API格式**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{EXPIRATION_ID}` | 此 `ttlId` 要取消的資料集到期日。 |

{style="table-layout:auto"}

**要求**

以下請求會取消ID為的資料集有效期 `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`：

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容），以及過期時間 `status` 屬性已設定為 `cancelled`.

## 擷取資料集的到期狀態歷史記錄 {#retrieve-expiration-history}

若要查詢特定資料集的到期狀態歷史記錄，請使用 `{DATASET_ID}` 和 `include=history` 查詢請求中的查詢引數。 結果包括關於建立資料集有效期、已套用的任何更新，及其取消或執行（如果適用）的資訊。 您也可以使用 `{DATASET_EXPIRATION_ID}` 以擷取資料集到期狀態歷史記錄。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}?include=history
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其到期歷程記錄的資料集ID。 |
| `{DATASET_EXPIRATION_ID}` | 資料集過期時間的ID。 注意：這稱為 `ttlId` 在回應中。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集到期日的詳細資料，其中包含 `history` 提供詳細資訊的陣列 `status`， `expiry`， `updatedAt`、和 `updatedBy` 其每個記錄的更新的屬性。

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期時間的ID。 |
| `datasetId` | 此到期適用於的資料集ID。 |
| `datasetName` | 此到期適用於的資料集的顯示名稱。 |
| `sandboxName` | 目標資料集所在之沙箱的名稱。 |
| `displayName` | 到期要求的顯示名稱。 |
| `description` | 到期要求的說明。 |
| `imsOrg` | 您組織的ID。 |
| `history` | 以物件陣列形式列出到期日更新的歷史記錄，每個物件包含 `status`， `expiry`， `updatedAt`、和 `updatedBy` 更新時到期的屬性。 |

{style="table-layout:auto"}

## 附錄

### 接受的查詢引數 {#query-params}

下表概述在下列情況下可用的查詢引數： [列出資料集有效期](#list)：

>[!NOTE]
>
>此 `description`， `displayName`、和 `datasetName` 引數都包含依據LIKE值搜尋的能力。 這表示您可以搜尋字串「Name1」，以尋找名為「Name123」、「Name183」、「DisplayName1234」的排程資料集有效期。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `author` | 比對下列專案的有效期 `created_by` 是搜尋字串的相符專案。 如果搜尋字串的開頭為 `LIKE` 或 `NOT LIKE`，其餘會視為SQL搜尋模式。 否則，整個搜尋字串會被視為必須完全符合的整個內容的常值字串。 `created_by` 欄位。 | `author=LIKE %john%`、`author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 符合在指定間隔內任何時間取消的到期日。 即使稍後重新開啟到期日（為相同資料集設定新的到期日），這亦適用。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 符合在指定間隔內完成的到期日。 | `completedToDate=2021-11-11-06:00` |
| `createdDate` | 符合在指定時間開始的24小時視窗中建立的到期日。<br><br>請注意，沒有時間的日期(例如 `2021-12-07`)代表當天開始的日期時間。 因此， `createdDate=2021-12-07` 是指任何在2021年12月7日建立的到期日，來自 `00:00:00` 到 `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 比對在指定時間或之後建立的到期日。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 比對在指定時間或之前建立的到期日。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | 符合套用至特定資料集的到期日。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | 符合資料集名稱包含所提供搜尋字串的到期日。 相符專案不區分大小寫。 | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | 符合顯示名稱包含所提供搜尋字串的到期日。 相符專案不區分大小寫。 | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | 根據確切的執行日期、執行的結束日期或執行的開始日期來篩選結果。 它們可用來擷取與特定日期、特定日期之前或特定日期之後執行作業相關聯的資料或記錄。 | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 符合指定間隔內即將執行或已執行的到期日。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | 介於1到100之間的整數，表示要傳回的最大到期次數。 預設為25。 | `limit=50` |
| `orderBy` | 此 `orderBy` 查詢引數指定API傳回結果的排序順序。 使用它可根據一或多個欄位來排列資料，以遞增(ASC)或遞減(DESC)順序排列。 使用+或 — 首碼分別表示ASC、DESC。 接受下列值： `displayName`， `description`， `datasetName`， `id`， `updatedBy`， `updatedAt`， `expiry`， `status`. | `-datasetName` |
| `orgId` | 比對組織ID與引數相符的資料集有效期。 此值預設為 `x-gw-ims-org-id` 標頭，並會忽略，除非請求提供服務權杖。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | 整數，指出要傳回的過期頁面。 | `page=3` |
| `sandboxName` | 符合沙箱名稱與引數完全相符的資料集有效期。 在請求的 `x-sandbox-name` 標頭。 使用 `sandboxName=*` 以納入所有沙箱的資料集有效期。 | `sandboxName=dev1` |
| `search` | 符合指定字串與到期ID完全相符或為的到期 **包含** 在下列任一欄位中：<br><ul><li>作者</li><li>顯示名稱</li><li>說明</li><li>顯示名稱</li><li>資料集名稱</li></ul> | `search=TESTING` |
| `status` | 以逗號分隔的狀態清單。 包含後，回應會比對資料集有效期，其目前狀態在所列資料集有效期中。 | `status=pending,cancelled` |
| `ttlId` | 符合具有特定ID的到期要求。 | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 按讚 `createdDate` / `createdFromDate` / `createdToDate`，但符合資料集到期日的更新時間，而不是建立時間。<br><br>每次編輯時都會視為更新到期日，包括建立、取消或執行的時間。 | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

