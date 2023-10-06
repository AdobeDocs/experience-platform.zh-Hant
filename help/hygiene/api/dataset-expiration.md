---
title: 資料集過期API端點
description: 資料衛生API中的/ttl端點可讓您以程式設計方式在Adobe Experience Platform中排程資料集有效期。
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 2%

---

# 資料集到期端點

此 `/ttl` 資料衛生API中的端點可讓您為Adobe Experience Platform中的資料集排程到期日。

資料集到期時間只是計時延遲的刪除作業。 資料集在過渡期間不受保護，因此在到期之前可能會以其他方式刪除。

>[!NOTE]
>
>雖然到期時間指定為特定即時，但在實際刪除開始之前，到期後最多可能有24小時的延遲。 開始刪除後，可能需要長達七天的時間，資料集的所有追蹤才會從Platform系統中移除。

在實際起始資料集刪除作業之前，您可以隨時取消到期日或修改其觸發時間。 取消資料集到期日後，您可以設定新的到期日，以重新開啟資料集。

開始刪除資料集後，其到期工作將標籤為 `executing`，且可能不會進一步變更。 資料集本身最多可以復原七天，但必須透過Adobe服務要求啟動的手動程式進行。 請求執行時，Data Lake、Identity Service和即時客戶設定檔會開始個別程式，從各自的服務中移除資料集的內容。 從所有三項服務中刪除資料後，到期日將標籤為 `executed`.

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更任何可能會將資料擷取至該資料集的資料流程，讓您的下游工作流程不會受到負面影響。

## 快速入門

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱 [概述](./overview.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需標題的重要資訊。

## 列出資料集有效期 {#list}

您可以發出GET要求，列出貴組織的所有資料集有效期。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 選擇性查詢引數清單，多個引數由下列專案分隔： `&` 個字元。 常見引數包括 `size` 和 `page` 以作分頁之用。 如需支援的查詢引數完整清單，請參閱 [附錄部分](#query-params). |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會列出產生的資料集有效期。 下列範例的空格已截斷。

```json
{
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `totalRecords` | 與清單呼叫的引數相符的資料集到期計數。 |
| `ttlDetails` | 包含傳回資料集有效期的詳細資訊。 如需資料集到期屬性的詳細資訊，請參閱回應一節，以發出 [查詢呼叫](#lookup). |

{style="table-layout:auto"}

## 查詢資料集有效期 {#lookup}

您可以透過GET請求查詢資料集到期日。

**API格式**

```http
GET /ttl/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其有效期的資料集ID。 |

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
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 資料集過期時間的ID。 |
| `datasetId` | 此到期適用於的資料集ID。 |
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

## 建立或更新資料集有效期 {#create-or-update}

您可以透過PUT請求建立或更新資料集的到期日。

**API格式**

```http
PUT /ttl/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要為其排程到期的資料集ID。 |

**要求**

下列請求會排程資料集 `5b020a27e7040801dedbf46e` ，並於2022年底（格林威治標準時間）刪除。 如果資料集找不到現有的有效期，則會建立新的有效期。 如果資料集已有暫止的到期日，則會將該到期日更新為新的到期日 `expiry` 值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `expiry` | 要刪除資料集的時間的ISO 8601時間戳記。 |
| `displayName` | 到期要求的顯示名稱。 |
| `description` | 到期要求的選擇性說明。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回資料集到期日的詳細資料，如果更新了預先存在的到期日，則HTTP狀態為200 （確定），如果沒有預先存在的到期日，則傳回201 （建立）。

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 資料集過期時間的ID。 |
| `datasetId` | 此到期適用於的資料集ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集到期的目前狀態。 |
| `expiry` | 刪除資料集的預定日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳記。 |
| `updatedBy` | 上次更新到期日的使用者。 |

{style="table-layout:auto"}

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
| `{EXPIRATION_ID}` | 此 `workorderId` 要取消的資料集到期日。 |

{style="table-layout:auto"}

**要求**

以下請求會取消ID為的資料集有效期 `SD5cfd7a11b25543a9bcd9ef647db3d8df`：

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容），以及過期時間 `status` 屬性已設定為 `cancelled`.

## 擷取資料集的到期狀態歷史記錄

您可以使用查詢引數查詢特定資料集的到期狀態歷史記錄 `include=history` 在查詢請求中。 結果包括關於建立資料集有效期、已套用的任何更新，及其取消或執行（如果適用）的資訊。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其到期歷程記錄的資料集ID。 |

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
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 資料集過期時間的ID。 |
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

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `size` | 介於1到100之間的整數，表示要傳回的最大到期次數。 預設為25。 | `size=50` |
| `page` | 整數，指出要傳回的過期頁面。 | `page=3` |
| `orgId` | 比對組織ID與引數相符的資料集有效期。 此值預設為 `x-gw-ims-org-id` 標頭，並會忽略，除非請求提供服務權杖。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | 以逗號分隔的狀態清單。 包含後，回應會比對資料集有效期，其目前狀態在所列資料集有效期中。 | `status=pending,cancelled` |
| `author` | 比對下列專案的有效期 `created_by` 是搜尋字串的相符專案。 如果搜尋字串的開頭為 `LIKE` 或 `NOT LIKE`，其餘會視為SQL搜尋模式。 否則，整個搜尋字串會被視為必須完全符合的整個內容的常值字串。 `created_by` 欄位。 | `author=LIKE %john%` |
| `sandboxName` | 符合沙箱名稱與引數完全相符的資料集有效期。 在請求的 `x-sandbox-name` 標頭。 使用 `sandboxName=*` 以納入所有沙箱的資料集有效期。 | `sandboxName=dev1` |
| `datasetId` | 符合套用至特定資料集的到期日。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | 符合在指定時間開始的24小時視窗中建立的到期日。<br><br>請注意，沒有時間的日期(例如 `2021-12-07`)代表當天開始的日期時間。 因此， `createdDate=2021-12-07` 是指任何在2021年12月7日建立的到期日，來自 `00:00:00` 到 `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 比對在指定時間或之後建立的到期日。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 比對在指定時間或之前建立的到期日。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 按讚 `createdDate` / `createdFromDate` / `createdToDate`，但符合資料集到期日的更新時間，而不是建立時間。<br><br>每次編輯時都會視為更新到期日，包括建立、取消或執行的時間。 | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 符合在指定間隔內任何時間取消的到期日。 即使稍後重新開啟到期日（為相同資料集設定新的到期日），這亦適用。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 符合在指定間隔內完成的到期日。 | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 符合指定間隔內即將執行或已執行的到期日。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
