---
title: 工作單API終結點
description: 資料衛生API中的/workorder終結點允許您以寫程式方式管理使用者身份的刪除任務。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 4%

---

# 工作單終結點

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買Healthcare Shield的組織。

的 `/workorder` 通過資料衛生API中的終結點，您可以以寫程式方式管理Adobe Experience Platform的消費者標識的刪除任務。

## 快速入門

本指南中使用的終結點是資料衛生API的一部分。 在繼續之前，請查看 [概述](./overview.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 刪除標識 {#delete-identities}

您可以通過向以下對象發出POST請求，從單個資料集或所有資料集中刪除一個或多個使用者身份 `/workorder` 端點。

**API格式**

```http
POST /workorder
```

**要求**

取決於 `datasetId` 在請求負載中提供，API調用將從所有資料集或您指定的單個資料集中刪除使用者身份。 以下請求從特定資料集中刪除三個使用者身份。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `action` | 要執行的操作。 值必須設定為 `delete_identity` 刪除標識時。 |
| `datasetId` | 如果要從單個資料集刪除，則此值必須是有關資料集的ID。 如果要從所有資料集中刪除，請將值設定為 `ALL`。<br><br>如果指定單個資料集，則資料集的關聯體驗資料模型(XDM)架構必須定義主標識。 |
| `identities` | 一個陣列，包含您要刪除其資訊的至少一個用戶的標識。 每個身份由 [標識命名空間](../../identity-service/namespaces.md) 和值：<ul><li>`namespace`:包含單個字串屬性， `code`，表示標識名稱空間。 </li><li>`id`:標識值。</ul>如果 `datasetId` 指定單個資料集，每個實體 `identities` 必須使用與架構的主標識相同的標識名稱空間。<br><br>如果 `datasetId` 設定為 `ALL`，也請參見Wiki頁。 `identities` 陣列未限制到任何單個命名空間，因為每個資料集可能不同。 但是，您的請求仍受到組織可用的命名空間的約束，如報告所述 [身份服務](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回身份刪除的詳細資訊。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用於稍後查看刪除的狀態。 |
| `orgId` | 您組織的ID。 |
| `batchId` | 此刪除順序與關聯的批的ID，用於調試。 將多個刪除訂單捆綁到一個批中，以便由下游服務處理。 |
| `bundleOrdinal` | 將此刪除訂單捆綁到批中以進行下游處理時收到的順序。 用於調試。 |
| `payloadByteSize` | 建立此刪除順序的請求負載中提供的身份清單的大小（以位元組為單位）。 |
| `operationCount` | 此刪除順序應用於的標識數。 |
| `createdAt` | 建立刪除順序的時間戳。 |
| `responseMessage` | 系統返回的最新響應。 如果在處理過程中出錯，此值將是包含詳細錯誤資訊的JSON字串，以幫助您瞭解可能出錯的原因。 |
| `status` | 刪除訂單的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |

{style=&quot;table-layout:auto&quot;&quot;

## 列出所有身份刪除的狀態 {#list}

通過發出GET請求，可以列出所有身份刪除的狀態。

**API格式**

```http
GET /workorder?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMS}` | 清單調用的可選查詢參數清單，其中多個參數以 `&` 字元。 接受的查詢參數如下：<ul><li>`data`  — 一個布爾值，當設定為 `true`，包括為刪除訂單接收的所有附加請求和響應資料。 預設為 `false`。</li><li>`start`  — 搜索刪除順序的時間段開始的時間戳。</li><li>`end`  — 搜索刪除順序的時間段結束的時間戳。</li><li>`page`  — 要返回的特定響應頁。</li><li>`limit`  — 每頁要顯示的記錄數。</li></ul> |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回所有刪除操作的詳細資訊，包括其當前狀態。 下面的示例響應已被截斷為空間。

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `results` | 包含刪除訂單清單及其詳細資訊。 有關刪除順序屬性的詳細資訊，請參閱上一節中的示例響應 [查找刪除訂單](#lookup)。 |
| `total` | 基於當前篩選器找到的刪除訂單總數。 |
| `count` | 在響應的每頁上找到的刪除訂單總數。 |
| `_links` | 包含分頁資訊，幫助您瀏覽其餘響應：<ul><li>`next`:包含響應中下一頁的URL。</li><li>`page`:包含URL模板，用於訪問響應中的另一頁或調整在每頁返回的項目數。</li></ul> |

{style=&quot;table-layout:auto&quot;&quot;

## 檢索身份刪除的狀態(#lookup)

在將請求發送到 [刪除標識](#delete-identities)，可以使用GET請求檢查其狀態。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 的 `workorderId` 你正在查找的身份刪除。 |

{style=&quot;table-layout:auto&quot;&quot;

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回刪除操作的詳細資訊，包括其當前狀態。

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用於稍後查看刪除的狀態。 |
| `orgId` | 您組織的ID。 |
| `batchId` | 此刪除順序與關聯的批的ID，用於調試。 將多個刪除訂單捆綁到一個批中，以便由下游服務處理。 |
| `bundleOrdinal` | 將此刪除訂單捆綁到批中以進行下游處理時收到的順序。 用於調試。 |
| `payloadByteSize` | 建立此刪除順序的請求負載中提供的身份清單的大小（以位元組為單位）。 |
| `operationCount` | 此刪除順序應用於的標識數。 |
| `createdAt` | 建立刪除順序的時間戳。 |
| `responseMessage` | 系統返回的最新響應。 如果在處理過程中出錯，此值將是包含詳細錯誤資訊的JSON字串，以幫助您瞭解可能出錯的原因。 |
| `status` | 刪除訂單的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
