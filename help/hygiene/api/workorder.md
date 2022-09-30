---
title: 工作單API端點
description: 資料衛生API中的/workorder端點可讓您以程式設計方式管理消費者身分識別的刪除工作。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 4%

---

# 工作單端點

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買Analytics Healthcare Shield的組織。

此 `/workorder` 資料衛生API中的端點可讓您以程式設計方式管理Adobe Experience Platform中的消費者刪除請求。

## 快速入門

本指南中使用的端點是資料衛生API的一部分。 繼續之前，請檢閱 [概述](./overview.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 建立消費者刪除請求 {#delete-consumers}

您可以對 `/workorder` 端點。

**API格式**

```http
POST /workorder
```

**要求**

視 `datasetId` 在請求裝載中提供，API呼叫會從所有資料集或您指定的單一資料集中刪除消費者身分識別。 下列請求會從特定資料集中刪除三個消費者身分識別。

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
        "displayName": "Example Consumer Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
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
| `action` | 要執行的動作。 值必須設為 `delete_identity` 針對消費者刪除。 |
| `datasetId` | 如果您要從單一資料集刪除，此值必須是相關資料集的ID。 如果您要從所有資料集刪除，請將值設為 `ALL`.<br><br>如果您指定單一資料集，資料集的相關Experience Data Model(XDM)結構必須已定義主要身分。 |
| `displayName` | 消費者刪除請求的顯示名稱。 |
| `description` | 消費者刪除請求的說明。 |
| `identities` | 一個陣列，包含至少一個要刪除其資訊的用戶的標識。 每個身分都由 [身分命名空間](../../identity-service/namespaces.md) 和值：<ul><li>`namespace`:包含單一字串屬性， `code`，代表身分識別命名空間。 </li><li>`id`:身分值。</ul>若 `datasetId` 指定單一資料集，每個實體位於 `identities` 必須使用與架構的主要身分相同的身分命名空間。<br><br>若 `datasetId` 設為 `ALL`, `identities` 陣列不受限於任何單一命名空間，因為每個資料集可能不同。 不過，您的要求仍受到組織可用的命名空間限制，如 [Identity服務](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回消費者刪除的詳細資訊。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用來稍後查詢刪除的狀態。 |
| `orgId` | 您的組織ID。 |
| `bundleId` | 此刪除順序關聯的套件ID，用於調試。 多個刪除訂單捆綁在一起，由下游服務處理。 |
| `action` | 由工作單執行的操作。 若為消費者刪除，則值為 `identity-delete`. |
| `createdAt` | 建立刪除順序時的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
| `datasetId` | 受要求約束的資料集ID。 如果要求適用於所有資料集，則值會設為 `ALL`. |

{style=&quot;table-layout:auto&quot;}

## 檢索消費者刪除的狀態(#lookup)

之後 [建立消費者刪除請求](#delete-consumers)，您可以使用GET請求來檢查其狀態。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 此 `workorderId` 您正在查詢的消費者刪除。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回刪除操作的詳細資訊，包括其目前狀態。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用來稍後查詢刪除的狀態。 |
| `orgId` | 您的組織ID。 |
| `bundleId` | 此刪除順序關聯的套件ID，用於調試。 多個刪除訂單捆綁在一起，由下游服務處理。 |
| `action` | 由工作單執行的操作。 若為消費者刪除，則值為 `identity-delete`. |
| `createdAt` | 建立刪除順序時的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
| `datasetId` | 受要求約束的資料集ID。 如果要求適用於所有資料集，則值會設為 `ALL`. |
| `productStatusDetails` | 列出與請求相關之下遊程式的目前狀態的陣列。 每個陣列物件都包含下列屬性：<ul><li>`productName`:下游服務的名稱。</li><li>`productStatus`:來自下游服務的請求的目前處理狀態。</li><li>`createdAt`:服務張貼最新狀態的時間戳記。</li></ul> |

## 更新消費者刪除請求

您可以更新 `displayName` 和 `description` 以透過提出PUT請求刪除消費者。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 此 `workorderId` 您正在查詢的消費者刪除。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `displayName` | 消費者刪除請求的顯示名稱已更新。 |
| `description` | 消費者刪除請求的更新說明。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回消費者刪除的詳細資訊。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用來稍後查詢刪除的狀態。 |
| `orgId` | 您的組織ID。 |
| `bundleId` | 此刪除順序關聯的套件ID，用於調試。 多個刪除訂單捆綁在一起，由下游服務處理。 |
| `action` | 由工作單執行的操作。 若為消費者刪除，則值為 `identity-delete`. |
| `createdAt` | 建立刪除順序時的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
| `datasetId` | 受要求約束的資料集ID。 如果要求適用於所有資料集，則值會設為 `ALL`. |
| `productStatusDetails` | 列出與請求相關之下遊程式的目前狀態的陣列。 每個陣列物件都包含下列屬性：<ul><li>`productName`:下游服務的名稱。</li><li>`productStatus`:來自下游服務的請求的目前處理狀態。</li><li>`createdAt`:服務張貼最新狀態的時間戳記。</li></ul> |

{style=&quot;table-layout:auto&quot;}
