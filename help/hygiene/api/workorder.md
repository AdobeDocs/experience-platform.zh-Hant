---
title: 工單API端點
description: 資料衛生API中的/workorder端點可讓您以程式設計方式管理身分的刪除任務。
badgeBeta: label="Beta" type="Informative"
role: Developer
badge: Beta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: bf819d506b0ee6f3aba6850f598ee46f16695dfa
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 1%

---

# 工單端點 {#work-order-endpoint}

資料衛生API中的`/workorder`端點可讓您以程式設計方式管理Adobe Experience Platform中的記錄刪除請求。

>[!IMPORTANT]
> 
>「記錄刪除」功能目前在Beta中，僅可在&#x200B;**限定的版本**&#x200B;中使用。 並非所有客戶都可使用。 記錄刪除請求僅適用於有限版本中的組織。
>
>記錄刪除旨在用於資料清理、匿名資料移除或資料最小化。 它們&#x200B;**不**&#x200B;用於資料主體權利要求（法規遵循），因為與一般資料保護規範(GDPR)等隱私權法規相關。 對於所有規範使用案例，請改用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 快速入門

本指南中使用的端點屬於資料衛生API。 在繼續之前，請先檢閱[總覽](./overview.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 建立記錄刪除請求 {#create}

您可以向`/workorder`端點發出POST要求，從單一資料集或所有資料集中刪除一或多個身分。

>[!IMPORTANT]
> 
>每個月可提交的不重複身分記錄刪除總數有不同的限制。 這些限制是以您的授權合約為基礎。 已購買Adobe Real-time Customer Data Platform和Adobe Journey Optimizer所有版本的組織，每個月最多可提交100,000筆身分記錄刪除。 已購買&#x200B;**AdobeHealthcare Shield**&#x200B;或&#x200B;**AdobePrivacy &amp; Security Shield**&#x200B;的組織每個月最多可提交600,000個身分記錄刪除。<br>透過UI[&#128279;](../ui/record-delete.md)的單一記錄刪除請求可讓您一次提交10,000個ID。 用於刪除記錄的API方法允許一次提交100,000個ID。<br>最佳實務是每個請求提交儘可能多的ID，以您的ID限製為限。 當您要刪除大量ID時，應避擴音交小量ID或每個記錄刪除請求使用一個單一ID。

**API格式**

```http
POST /workorder
```

>[!NOTE]
>
>資料生命週期請求只能根據主要身分或身分對應修改資料集。 要求必須指定主要身分，或提供身分對應。

**要求**

根據請求承載中提供的`datasetId`值，API呼叫將會從您指定的所有資料集或單一資料集中刪除身分。 以下請求會從特定資料集中刪除三個身分。

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
| `action` | 要執行的動作。 記錄刪除的值必須設定為`delete_identity`。 |
| `datasetId` | 如果您要從單一資料集中刪除，此值必須是相關資料集的ID。 如果您要從所有資料集中刪除，請將值設定為`ALL`。<br><br>如果您指定單一資料集，該資料集的相關聯Experience Data Model (XDM)結構描述必須定義主要身分。 如果資料集沒有主要身分，則必須有身分對應，資料生命週期請求才能修改資料集。<br>如果身分對應存在，則會顯示為名為`identityMap`的頂層欄位。<br>請注意，資料集列的身分對應中可能有許多身分，但只能將一個標示為主要身分。 必須包含`"primary": true`以強制`id`符合主要身分。 |
| `displayName` | 記錄刪除請求的顯示名稱。 |
| `description` | 記錄刪除請求的說明。 |
| `identities` | 陣列，包含您要刪除其資訊之至少一個使用者的身分識別。 每個身分都由[身分名稱空間](../../identity-service/features/namespaces.md)和一個值組成：<ul><li>`namespace`：包含單一字串屬性`code`，代表身分名稱空間。 </li><li>`id`：身分值。</ul>如果`datasetId`指定了單一資料集，`identities`下的每個實體都必須使用與結構描述主要身分相同的身分名稱空間。<br><br>如果`datasetId`設為`ALL`，則`identities`陣列不受限於任何單一名稱空間，因為每個資料集可能不同。 但是，如[Identity服務](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)所報告，您的要求仍受限於貴組織可用的名稱空間。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回記錄刪除的詳細資料。

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
| `workorderId` | 刪除順序的ID。 這可用於稍後查詢刪除狀態。 |
| `orgId` | 您的組織ID。 |
| `bundleId` | 與此刪除順序相關聯的套件組合ID，用於偵錯。 多個刪除訂單會整合在一起，由下游服務處理。 |
| `action` | 工單正在執行的動作。 對於記錄刪除，值為`identity-delete`。 |
| `createdAt` | 建立刪除順序時的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的目前狀態。 |
| `createdBy` | 建立刪除訂單的使用者。 |
| `datasetId` | 受限於請求的資料集的ID。 如果要求適用於所有資料集，則值將設為`ALL`。 |

{style="table-layout:auto"}

## 擷取記錄刪除的狀態 {#lookup}

在您[建立記錄刪除請求](#create)之後，您可以使用GET請求檢查其狀態。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 您正在查詢的記錄刪除`workorderId`。 |

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
| `workorderId` | 刪除順序的ID。 這可用於稍後查詢刪除狀態。 |
| `orgId` | 您的組織ID。 |
| `bundleId` | 與此刪除順序相關聯的套件組合ID，用於偵錯。 多個刪除訂單會整合在一起，由下游服務處理。 |
| `action` | 工單正在執行的動作。 對於記錄刪除，值為`identity-delete`。 |
| `createdAt` | 建立刪除順序時的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的目前狀態。 |
| `createdBy` | 建立刪除訂單的使用者。 |
| `datasetId` | 受限於請求的資料集的ID。 如果要求適用於所有資料集，則值將設為`ALL`。 |
| `productStatusDetails` | 一個陣列，列出與請求相關的下游處理序的目前狀態。 每個陣列物件包含下列屬性：<ul><li>`productName`：下游服務的名稱。</li><li>`productStatus`：下游服務要求的目前處理狀態。</li><li>`createdAt`：服務發佈最新狀態的時間戳記。</li></ul> |

## 更新記錄刪除請求

您可以藉由提出PUT要求來更新記錄刪除的`displayName`和`description`。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 您正在查詢的記錄刪除`workorderId`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X PUT \
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

成功的回應會傳回記錄刪除的詳細資料。

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 刪除順序的ID。 這可用於稍後查詢刪除狀態。 |
| `orgId` | 您的組織ID。 |
| `bundleId` | 與此刪除順序相關聯的套件組合ID，用於偵錯。 多個刪除訂單會整合在一起，由下游服務處理。 |
| `action` | 工單正在執行的動作。 對於記錄刪除，值為`identity-delete`。 |
| `createdAt` | 建立刪除順序時的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的目前狀態。 |
| `createdBy` | 建立刪除訂單的使用者。 |
| `datasetId` | 受限於請求的資料集的ID。 如果要求適用於所有資料集，則值將設為`ALL`。 |
| `productStatusDetails` | 一個陣列，列出與請求相關的下游處理序的目前狀態。 每個陣列物件包含下列屬性：<ul><li>`productName`：下游服務的名稱。</li><li>`productStatus`：下游服務要求的目前處理狀態。</li><li>`createdAt`：服務發佈最新狀態的時間戳記。</li></ul> |

{style="table-layout:auto"}
