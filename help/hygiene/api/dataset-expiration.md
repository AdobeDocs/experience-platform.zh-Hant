---
title: 資料集過期API端點
description: 資料衛生API中的/ttl端點可讓您以程式設計方式排程Adobe Experience Platform中的資料集到期日。
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 6%

---

# 資料集過期端點

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

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

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會列出產生的資料集有效期。 下列範例已截斷空格。

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| 屬性 | 說明 |
| --- | --- |
| `results` | 包含傳回資料集有效期的詳細資料。 如需資料集有效期屬性的詳細資訊，請參閱 [查閱呼叫](#lookup). |
| `current_page` | 列出結果的當前頁。 |
| `total_pages` | 回應中的總頁數。 |
| `total_count` | 回應中的資料集過期總數。 |

{style=&quot;table-layout:auto&quot;}

## 查詢資料集的有效期 {#lookup}

您可以透過GET請求查詢資料集的有效期。

**API格式**

```http
GET /ttl/{TTL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 您要查詢的資料集有效期ID。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集有效期的詳細資訊。

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的目前狀態。 |
| `expiry` | 刪除資料集的排程日期和時間。 |
| `updatedAt` | 上次更新過期時間的時間戳記。 |
| `updatedBy` | 上次更新過期的使用者。 |

{style=&quot;table-layout:auto&quot;}

## 建立資料集過期時間 {#create}

您可以透過POST請求為資料集建立到期日。

**API格式**

```http
POST /ttl
```

**要求**

下列請求會排程資料集 `5b020a27e7040801dedbf46e` 於2022年底刪除（格林威治標準時間）。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `datasetId` | 您要排程到期日的資料集ID。 |
| `expiry` | 刪除資料集時的ISO 8601時間戳記。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回資料集有效期的詳細資料，如果已更新預先存在的有效期，則會傳回HTTP狀態200(OK)；如果沒有預先存在的有效期，則會傳回201（已建立）。

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的目前狀態。 |
| `expiry` | 刪除資料集的排程日期和時間。 |
| `updatedAt` | 上次更新過期時間的時間戳記。 |
| `updatedBy` | 上次更新過期的使用者。 |

{style=&quot;table-layout:auto&quot;}

## 更新資料集過期時間 {#update}

您可以透過PUT請求更新資料集的有效期。

**API格式**

```http
PUT /ttl/{TTL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 您要修改的資料集過期時間ID。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會更新資料集的有效期 `5b020a27e7040801dedbf46e` 因此，它將於2023年底到期（格林威治標準時間）。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `expiry` | 刪除資料集時的ISO 8601時間戳記。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回更新過期的詳細資訊。

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的目前狀態。 |
| `expiry` | 刪除資料集的排程日期和時間。 |
| `updatedAt` | 上次更新過期時間的時間戳記。 |
| `updatedBy` | 上次更新過期的使用者。 |

{style=&quot;table-layout:auto&quot;}

## 取消資料集過期 {#delete}

您可以提出DELETE要求，以取消資料集的過期時間。

**API格式**

```http
DELETE /ttl/{TTL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 您要取消的資料集過期時間ID。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會更新資料集的有效期 `5b020a27e7040801dedbf46e` 因此，它將於2023年底到期（格林威治標準時間）。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集有效期的詳細資料，及其 `status` 屬性現在設為 `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `ttlId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的目前狀態。 |
| `expiry` | 刪除資料集的排程日期和時間。 |
| `updatedAt` | 上次更新過期時間的時間戳記。 |
| `updatedBy` | 上次更新過期的使用者。 |

{style=&quot;table-layout:auto&quot;}

## 擷取資料集過期的歷史記錄

您可以使用查詢參數來查詢特定資料集有效期的歷史記錄 `include=history` 在查詢請求中。 結果包含關於資料集過期時間、已套用的任何更新，以及其取消或執行（如果適用）的相關資訊。

**API格式**

```http
GET /ttl/{TTL_ID}?include=history
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 您要查詢其歷史記錄的資料集過期時間ID。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集有效期的詳細資料，並附上 `history` 陣列提供其詳細資訊 `status`, `expiry`, `updatedAt`，和 `updatedBy` 屬性。

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
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
| `ttlId` | 資料集過期的ID。 |
| `datasetId` | 此過期時間所套用之資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `history` | 以對象陣列形式列出過期的更新歷史記錄，每個對象都包含 `status`, `expiry`, `updatedAt`，和 `updatedBy` 屬性。 |

{style=&quot;table-layout:auto&quot;}

## 附錄

### 接受的查詢參數 {#query-params}

下表概述了當 [清單資料集過期時間](#list):

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `size` | 介於1和100之間的整數，表示要返回的最大過期數。 預設為25。 | `size=50` |
| `page` | 指出要傳回過期頁面的整數。 | `page=3` |
| `status` | 以逗號分隔的狀態清單。 包含時，回應會比對目前狀態為所列之資料集的有效期。 | `status=pending,cancelled` |
| `author` | 相符項目：過期時間 `created_by` 是搜尋字串的相符項目。 如果搜索字串的開頭為 `LIKE` 或 `NOT LIKE`，其餘將視為SQL搜尋模式。 否則，整個搜尋字串會視為文字字串，而字串必須完全符合 `created_by` 欄位。 | `author=LIKE %john%` |
| `createdDate` | 相符項目：從指定時間開始，在24小時視窗中建立的到期日。<br><br>請注意沒有時間的日期(例如 `2021-12-07`)表示當天開始的日期時間。 因此， `createdDate=2021-12-07` 是指2021年12月7日建立的任何到期日，從 `00:00:00` through `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 相符項目：在指定時間或之後建立的有效期。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 相符項目：在指定時間或之前建立的有效期。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 贊 `createdDate` / `createdFromDate` / `createdToDate`，但會比對資料集到期日的更新時間（而非建立時間）。<br><br>每次編輯時都會考慮更新過期時間，包括建立、取消或執行過期時間。 | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 符合在指定間隔內隨時取消的到期時間。 即使日後重新開啟過期時間（針對相同資料集設定新的過期時間），也會套用此規則。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 相符項目：在指定間隔內完成的到期日。 | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 在指定間隔內，將執行或已執行的過期時間相符。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
