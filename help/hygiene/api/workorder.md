---
title: 工作單API終結點
description: 資料衛生API中的/workorder終結點允許您以寫程式方式管理標識的刪除任務。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# 工作單終結點

的 `/workorder` Data Heliscon API中的終結點允許您以寫程式方式管理Adobe Experience Platform中的記錄刪除請求。

>[!IMPORTANT]
>
>記錄刪除請求僅適用於已購買的組織 **Adobe醫療保健盾**。
>
>
>記錄刪除旨在用於資料清除、刪除匿名資料或資料最小化。 他們 **不** 用於與隱私法規(如一般資料保護法規(GDPR))相關的資料主題權限請求（合規性）。 對於所有符合性使用案例，使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 的雙曲餘切值。

## 快速入門

本指南中使用的終結點是資料衛生API的一部分。 在繼續之前，請查看 [概述](./overview.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 建立記錄刪除請求 {#create}

通過向Web站點發出POST請求，可以從單個資料集或所有資料集中刪除一個或多個標識 `/workorder` 端點。

**API格式**

```http
POST /workorder
```

**要求**

取決於 `datasetId` 在請求負載中提供，API調用將從所有資料集或您指定的單個資料集中刪除標識。 以下請求從特定資料集中刪除三個標識。

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
        "displayName": "Example Record Delete Request",
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
| `action` | 要執行的操作。 值必須設定為 `delete_identity` 刪除記錄。 |
| `datasetId` | 如果要從單個資料集刪除，則此值必須是有關資料集的ID。 如果要從所有資料集中刪除，請將值設定為 `ALL`。<br><br>如果指定單個資料集，則資料集的關聯體驗資料模型(XDM)架構必須定義主標識。 |
| `displayName` | 記錄刪除請求的顯示名稱。 |
| `description` | 記錄刪除請求的說明。 |
| `identities` | 一個陣列，包含您要刪除其資訊的至少一個用戶的標識。 每個身份由 [標識命名空間](../../identity-service/namespaces.md) 和值：<ul><li>`namespace`:包含單個字串屬性， `code`，表示標識名稱空間。 </li><li>`id`:標識值。</ul>如果 `datasetId` 指定單個資料集，每個實體 `identities` 必須使用與架構的主標識相同的標識名稱空間。<br><br>如果 `datasetId` 設定為 `ALL`，也請參見Wiki頁。 `identities` 陣列未限制到任何單個命名空間，因為每個資料集可能不同。 但是，您的請求仍受到組織可用的命名空間的約束，如報告所述 [身份服務](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)。 |

{style="table-layout:auto"}

**回應**

成功的響應返回記錄刪除的詳細資訊。

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
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用於稍後查看刪除的狀態。 |
| `orgId` | 您的組織 ID。 |
| `bundleId` | 此刪除順序與捆綁包關聯的ID，用於調試。 多個刪除訂單捆綁在一起，以便由下游服務處理。 |
| `action` | 工作單正在執行的操作。 對於記錄刪除，值為 `identity-delete`。 |
| `createdAt` | 建立刪除順序的時間戳。 |
| `updatedAt` | 上次更新刪除順序的時間戳。 |
| `status` | 刪除訂單的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
| `datasetId` | 受請求約束的資料集的ID。 如果請求針對所有資料集，則值將設定為 `ALL`。 |

{style="table-layout:auto"}

## 檢索記錄刪除的狀態(#lookup)

之後 [建立記錄刪除請求](#create)，可以使用GET請求檢查其狀態。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 的 `workorderId` 您正在查找的記錄刪除。 |

{style="table-layout:auto"}

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

成功的響應將返回刪除操作的詳細資訊，包括其當前狀態。

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
  "displayName": "Example Record Delete Request",
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
| `workorderId` | 刪除順序的ID。 這可用於稍後查看刪除的狀態。 |
| `orgId` | 您的組織 ID。 |
| `bundleId` | 此刪除順序與捆綁包關聯的ID，用於調試。 多個刪除訂單捆綁在一起，以便由下游服務處理。 |
| `action` | 工作單正在執行的操作。 對於記錄刪除，值為 `identity-delete`。 |
| `createdAt` | 建立刪除順序的時間戳。 |
| `updatedAt` | 上次更新刪除順序的時間戳。 |
| `status` | 刪除訂單的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
| `datasetId` | 受請求約束的資料集的ID。 如果請求針對所有資料集，則值將設定為 `ALL`。 |
| `productStatusDetails` | 列出與請求相關的下游進程的當前狀態的陣列。 每個陣列對象都包含以下屬性：<ul><li>`productName`:下游服務的名稱。</li><li>`productStatus`:來自下游服務的請求的當前處理狀態。</li><li>`createdAt`:服務發佈最近狀態的時間戳。</li></ul> |

## 更新記錄刪除請求

您可以更新 `displayName` 和 `description` 來刪除記錄。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 的 `workorderId` 您正在查找的記錄刪除。 |

{style="table-layout:auto"}

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
| `displayName` | 記錄刪除請求的更新顯示名稱。 |
| `description` | 記錄刪除請求的更新說明。 |

{style="table-layout:auto"}

**回應**

成功的響應返回記錄刪除的詳細資訊。

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
| `workorderId` | 刪除順序的ID。 這可用於稍後查看刪除的狀態。 |
| `orgId` | 您的組織 ID。 |
| `bundleId` | 此刪除順序與捆綁包關聯的ID，用於調試。 多個刪除訂單捆綁在一起，以便由下游服務處理。 |
| `action` | 工作單正在執行的操作。 對於記錄刪除，值為 `identity-delete`。 |
| `createdAt` | 建立刪除順序的時間戳。 |
| `updatedAt` | 上次更新刪除順序的時間戳。 |
| `status` | 刪除訂單的當前狀態。 |
| `createdBy` | 建立刪除順序的用戶。 |
| `datasetId` | 受請求約束的資料集的ID。 如果請求針對所有資料集，則值將設定為 `ALL`。 |
| `productStatusDetails` | 列出與請求相關的下游進程的當前狀態的陣列。 每個陣列對象都包含以下屬性：<ul><li>`productName`:下游服務的名稱。</li><li>`productStatus`:來自下游服務的請求的當前處理狀態。</li><li>`createdAt`:服務發佈最近狀態的時間戳。</li></ul> |

{style="table-layout:auto"}
