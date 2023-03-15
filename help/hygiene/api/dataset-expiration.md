---
title: 資料集過期API端點
description: 資料衛生API中的/ttl端點可讓您以程式設計方式排程Adobe Experience Platform中的資料集到期日。
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 2%

---

# 資料集過期端點

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**.

此 `/ttl` 資料衛生API中的端點可讓您排程Adobe Experience Platform中資料集的到期日。

資料集過期只是延遲刪除作業。 過渡期間不會保護資料集，因此在資料集過期前，可能會以其他方式刪除資料集。

>[!NOTE]
>
>儘管將過期指定為特定及時，但在實際刪除開始之前，在過期後可能會延遲24小時。 開始刪除後，最多可能需要七天時間，資料集的所有追蹤才會從Platform系統中移除。

在實際啟動資料集刪除之前，您可以隨時取消過期時間或修改其觸發時間。 取消資料集的有效期後，您可以設定新的到期日以重新開啟資料集。

資料集刪除一旦開始，其過期作業即會標示為 `executing`，且不可進一步變更。 資料集本身最多可復原七天，但只能透過透過Adobe服務請求起始的手動程式進行。 請求執行時，資料湖、Identity Service和即時客戶設定檔會開始個別的程式，從各自的服務中移除資料集的內容。 從這三項服務中刪除資料後，過期時間會標示為 `executed`.

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更可能會將資料內嵌至該資料集的任何資料流，以免對下游工作流程造成負面影響。

## 快速入門

本指南中使用的端點是資料衛生API的一部分。 繼續之前，請檢閱 [概述](./overview.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 列出資料集有效期 {#list}

您可以提出GET要求，列出貴組織的所有資料集有效期。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 選用的查詢參數清單，多個參數以 `&` 字元。 常見參數包括 `size` 和 `page` 分頁用途。 如需支援查詢參數的完整清單，請參閱 [附錄](#query-params). |

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

成功的回應會列出產生的資料集有效期。 下列範例已截斷空格。

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
| `totalRecords` | 符合清單呼叫參數的資料集過期計數。 |
| `ttlDetails` | 包含傳回資料集有效期的詳細資料。 如需資料集有效期屬性的詳細資訊，請參閱 [查閱呼叫](#lookup). |

{style="table-layout:auto"}

## 查詢資料集的有效期 {#lookup}

您可以透過GET請求查詢資料集的有效期。

**API格式**

```http
GET /ttl/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其有效期的資料集ID。 |

{style="table-layout:auto"}

**要求**

下列請求會查詢資料集的到期日詳細資料 `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集有效期的詳細資訊。

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
| `workorderId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的目前狀態。 |
| `expiry` | 刪除資料集的排程日期和時間。 |
| `updatedAt` | 上次更新過期時間的時間戳記。 |
| `updatedBy` | 上次更新過期的使用者。 |
| `displayName` | 過期請求的顯示名稱。 |
| `description` | 過期請求的說明。 |

{style="table-layout:auto"}

### 目錄過期標籤

使用 [目錄API](../../catalog/api/getting-started.md) 若要查詢資料集詳細資訊，如果資料集的有效期限為 `tags.adobe/hygiene/ttl`.

下列JSON代表來自目錄之資料集詳細資料的截斷回應，其過期值為 `32503680000000`. 標籤的值會將到期時間編碼為自Unix紀元開始以來的整數毫秒數。

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

## 建立或更新資料集的有效期 {#create-or-update}

您可以透過PUT請求建立或更新資料集的到期日。

**API格式**

```http
PUT /ttl/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要排程有效期的資料集ID。 |

**要求**

下列請求會排程資料集 `5b020a27e7040801dedbf46e` 於2022年底刪除（格林威治標準時間）。 如果資料集找不到任何現有的有效期，系統就會建立新的有效期。 如果資料集已有待定的過期時間，該過期時間會以新的 `expiry` 值。

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
| `expiry` | 刪除資料集時的ISO 8601時間戳記。 |
| `displayName` | 過期請求的顯示名稱。 |
| `description` | 過期請求的可選說明。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回資料集有效期的詳細資料，如果已更新預先存在的有效期，則會傳回HTTP狀態200(OK)；如果沒有預先存在的有效期，則會傳回201（已建立）。

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
| `workorderId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的目前狀態。 |
| `expiry` | 刪除資料集的排程日期和時間。 |
| `updatedAt` | 上次更新過期時間的時間戳記。 |
| `updatedBy` | 上次更新過期的使用者。 |

{style="table-layout:auto"}

## 取消資料集過期 {#delete}

您可以提出DELETE要求，以取消資料集的過期時間。

>[!NOTE]
>
>僅限狀態為 `pending` 可以取消。 嘗試取消已執行或已取消的過期時間會傳回HTTP 404錯誤。

**API格式**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{EXPIRATION_ID}` | 此 `workorderId` 取消的資料集過期時間。 |

{style="table-layout:auto"}

**要求**

下列請求會以ID取消資料集的有效期 `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容），且過期的 `status` 屬性設為 `cancelled`.

## 擷取資料集的到期狀態記錄

您可以使用查詢參數來查詢特定資料集的到期狀態記錄 `include=history` 在查詢請求中。 結果包含關於資料集過期時間、已套用的任何更新，以及其取消或執行（如果適用）的相關資訊。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其有效期記錄的資料集ID。 |

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

成功的回應會傳回資料集有效期的詳細資料，並附上 `history` 陣列提供其詳細資訊 `status`, `expiry`, `updatedAt`，和 `updatedBy` 屬性。

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
| `workorderId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `datasetName` | 此有效期適用的資料集的顯示名稱。 |
| `sandboxName` | 目標資料集所在的沙箱名稱。 |
| `displayName` | 過期請求的顯示名稱。 |
| `description` | 過期請求的說明。 |
| `imsOrg` | 您組織的ID。 |
| `history` | 以對象陣列形式列出過期的更新歷史記錄，每個對象都包含 `status`, `expiry`, `updatedAt`，和 `updatedBy` 屬性。 |

{style="table-layout:auto"}

## 附錄

### 接受的查詢參數 {#query-params}

下表概述了當 [清單資料集過期時間](#list):

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `size` | 介於1和100之間的整數，表示要返回的最大過期數。 預設為25。 | `size=50` |
| `page` | 指出要傳回過期頁面的整數。 | `page=3` |
| `orgId` | 相符項目：組織ID與參數的相符的到期資料集。 此值預設為 `x-gw-ims-org-id` 標題，則會忽略和，除非請求提供服務代號。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | 以逗號分隔的狀態清單。 包含時，回應會比對目前狀態為所列之資料集的有效期。 | `status=pending,cancelled` |
| `author` | 相符項目：過期時間 `created_by` 是搜尋字串的相符項目。 如果搜索字串的開頭為 `LIKE` 或 `NOT LIKE`，其餘將視為SQL搜尋模式。 否則，整個搜尋字串會視為文字字串，而字串必須完全符合 `created_by` 欄位。 | `author=LIKE %john%` |
| `sandboxName` | 相符項目：沙箱名稱與引數完全相符的資料集有效期。 預設為請求的沙箱名稱 `x-sandbox-name` 頁首。 使用 `sandboxName=*` 納入所有沙箱的資料集有效期。 | `sandboxName=dev1` |
| `datasetId` | 比對套用至特定資料集的有效期。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | 相符項目：從指定時間開始，在24小時視窗中建立的到期日。<br><br>請注意沒有時間的日期(例如 `2021-12-07`)表示當天開始的日期時間。 因此， `createdDate=2021-12-07` 是指2021年12月7日建立的任何到期日，從 `00:00:00` through `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 相符項目：在指定時間或之後建立的有效期。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 相符項目：在指定時間或之前建立的有效期。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 贊 `createdDate` / `createdFromDate` / `createdToDate`，但會比對資料集到期日的更新時間（而非建立時間）。<br><br>每次編輯時都會考慮更新過期時間，包括建立、取消或執行過期時間。 | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 符合在指定間隔內隨時取消的到期時間。 即使日後重新開啟過期時間（針對相同資料集設定新的過期時間），也會套用此規則。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 相符項目：在指定間隔內完成的到期日。 | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 在指定間隔內，將執行或已執行的過期時間相符。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
