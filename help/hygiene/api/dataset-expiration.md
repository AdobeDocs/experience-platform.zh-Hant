---
title: 資料集過期API終結點
description: 資料衛生API中的/ttl端點允許您以寫程式方式計畫Adobe Experience Platform的資料集過期。
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 49ba5263c6dc8eccac2ffe339476cf316c68e486
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 6%

---

# 資料集過期終結點

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

的 `/ttl` 資料衛生API中的終結點允許您為Adobe Experience Platform的資料集安排過期日期。

資料集過期僅是一個延遲的定時刪除操作。 該資料集在過渡期間未受到保護，因此可以在其到期之前通過其他方式將其刪除。

>[!NOTE]
>
>儘管到期時間被指定為特定的即時時間，但在實際刪除開始之前，在到期後可能會延遲24小時。 一旦開始刪除，則可能需要七天時間才能從平台系統中刪除該資料集的所有跟蹤。

在實際啟動dataset-delete之前的任何時間，都可以取消到期或修改其觸發時間。 取消資料集到期後，可以通過設定新的到期日來重新開啟它。

資料集刪除一旦啟動，其到期作業將標籤為 `executing`不得進一步修改。 資料集本身可恢復長達七天，但只能通過通過Adobe服務請求啟動的手動過程。 在請求執行時，資料湖、身份服務和即時客戶配置檔案將開始單獨的進程，以從各自的服務中刪除資料集的內容。 從所有三個服務中刪除資料後，過期將標籤為 `executed`。

## 快速入門

本指南中使用的終結點是資料衛生API的一部分。 在繼續之前，請查看 [概述](./overview.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 清單資料集過期 {#list}

通過發出GET請求，可以列出組織的所有資料集過期時間。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 可選查詢參數清單，其中多個參數以 `&` 字元。 公共參數包括 `size` 和 `page` 用於分頁。 有關支援的查詢參數的完整清單，請參閱 [附錄部分](#query-params)。 |

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

成功的響應列出了結果的資料集過期時間。 以下示例已截斷空間。

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
| `results` | 包含返回的資料集過期的詳細資訊。 有關資料集過期屬性的詳細資訊，請參閱用於生成 [查找調用](#lookup)。 |
| `current_page` | 列出結果的當前頁。 |
| `total_pages` | 響應中的頁總數。 |
| `total_count` | 響應中資料集過期的總數。 |

{style=&quot;table-layout:auto&quot;&quot;

## 查找資料集過期 {#lookup}

您可以通過GET請求查找資料集過期。

**API格式**

```http
GET /ttl/{TTL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 要查找的資料集過期的ID。 |

{style=&quot;table-layout:auto&quot;&quot;

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

成功的響應返回資料集過期的詳細資訊。

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
| `datasetId` | 此到期日期所應用的資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的當前狀態。 |
| `expiry` | 刪除資料集的計畫日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳。 |
| `updatedBy` | 上次更新過期的用戶。 |

{style=&quot;table-layout:auto&quot;&quot;

## 建立資料集過期 {#create}

您可以通過POST請求為資料集建立過期日期。

**API格式**

```http
POST /ttl
```

**要求**

以下請求調度資料集 `5b020a27e7040801dedbf46e` 於2022年底刪除（格林尼治平均時間）。

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
| `datasetId` | 要為其安排到期日期的資料集的ID。 |
| `expiry` | 刪除資料集的時間的ISO 8601時間戳。 |

{style=&quot;table-layout:auto&quot;&quot;

**回應**

成功的響應將返回資料集到期的詳細資訊，如果更新了預先存在的到期，則HTTP狀態為200(OK)；如果沒有預先存在的到期，則返回201（已建立）。

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
| `datasetId` | 此到期日期所應用的資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的當前狀態。 |
| `expiry` | 刪除資料集的計畫日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳。 |
| `updatedBy` | 上次更新過期的用戶。 |

{style=&quot;table-layout:auto&quot;&quot;

## 更新資料集過期 {#update}

您可以通過PUT請求更新資料集過期。

**API格式**

```http
PUT /ttl/{TTL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 要修改的資料集過期的ID。 |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

以下請求更新資料集的到期時間 `5b020a27e7040801dedbf46e` 因此，它將於2023年底（格林尼治平均時間）到期。

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
| `expiry` | 刪除資料集的時間的ISO 8601時間戳。 |

{style=&quot;table-layout:auto&quot;&quot;

**回應**

成功的響應將返回更新的到期的詳細資訊。

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
| `datasetId` | 此到期日期所應用的資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的當前狀態。 |
| `expiry` | 刪除資料集的計畫日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳。 |
| `updatedBy` | 上次更新過期的用戶。 |

{style=&quot;table-layout:auto&quot;&quot;

## 取消資料集過期 {#delete}

可以通過發出DELETE請求來取消資料集過期。

**API格式**

```http
DELETE /ttl/{TTL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 要取消的資料集過期的ID。 |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

以下請求更新資料集的到期時間 `5b020a27e7040801dedbf46e` 因此，它將於2023年底（格林尼治平均時間）到期。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回資料集過期的詳細資訊，其中 `status` 屬性現在設定為 `cancelled`。

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
| `datasetId` | 此到期日期所應用的資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `status` | 資料集過期的當前狀態。 |
| `expiry` | 刪除資料集的計畫日期和時間。 |
| `updatedAt` | 上次更新到期時間的時間戳。 |
| `updatedBy` | 上次更新過期的用戶。 |

{style=&quot;table-layout:auto&quot;&quot;

## 檢索資料集過期的歷史記錄

可以使用查詢參數查找特定資料集過期的歷史記錄 `include=history` 查找請求中。 結果包括有關建立資料集過期、已應用的任何更新及其取消或執行（如果適用）的資訊。

**API格式**

```http
GET /ttl/{TTL_ID}?include=history
```

| 參數 | 說明 |
| --- | --- |
| `{TTL_ID}` | 要查找其歷史記錄的資料集過期的ID。 |

{style=&quot;table-layout:auto&quot;&quot;

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

成功的響應將返回資料集過期的詳細資訊， `history` 陣列提供其 `status`。 `expiry`。 `updatedAt`, `updatedBy` 每個記錄更新的屬性。

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
| `datasetId` | 此到期日期所應用的資料集的ID。 |
| `imsOrg` | 您組織的ID。 |
| `history` | 將過期更新的歷史記錄列為對象陣列，每個對象都包含 `status`。 `expiry`。 `updatedAt`, `updatedBy` 更新時到期的屬性。 |

{style=&quot;table-layout:auto&quot;&quot;

## 附錄

### 接受的查詢參數 {#query-params}

下表概述了當 [清單資料集過期](#list):

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `size` | 介於1和100之間的整數，它指示要返回的最大過期數。 預設為25。 | `size=50` |
| `page` | 一個整數，它指示要返回的過期頁。 | `page=3` |
| `status` | 以逗號分隔的狀態清單。 當包含時，響應將匹配當前狀態為列出狀態的資料集過期時間。 | `status=pending,cancelled` |
| `author` | 匹配過期時間 `created_by` 是搜索字串的匹配項。 如果搜索字串以 `LIKE` 或 `NOT LIKE`，其餘部分將視為SQL搜索模式。 否則，整個搜索字串將被視為必須完全匹配的文本字串 `created_by` 的子菜單。 | `author=LIKE %john%` |
| `createdDate` | 與在指定時間開始的24小時窗口中建立的過期時間匹配。<br><br>注意沒有時間的日期(如 `2021-12-07`)表示該天開始的日期時間。 因此， `createdDate=2021-12-07` 指2021年12月7日建立的任何期限， `00:00:00` 通 `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 匹配在指定時間或之後建立的過期時間。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 與在指定時間或之前建立的過期時間匹配。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 像 `createdDate` / `createdFromDate` / `createdToDate`，但與資料集到期的更新時間而不是建立時間匹配。<br><br>每次編輯時都會考慮更新過期，包括建立、取消或執行過期時。 | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 匹配在指定時間間隔內隨時取消的過期時間。 即使到期日稍後重新開啟（通過為同一資料集設定新的到期日），也會適用。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 匹配在指定時間間隔內完成的過期時間。 | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 匹配在指定時間間隔內將執行或已執行的過期時間。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;&quot;
