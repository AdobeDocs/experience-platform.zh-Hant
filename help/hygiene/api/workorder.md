---
title: 記錄刪除工單
description: 瞭解如何使用資料衛生API中的/workorder端點，以管理Adobe Experience Platform中的記錄刪除工單。 本指南涵蓋配額、處理時間表及API使用情形。
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 4f4b668c2b29228499dc28b2c6c54656e98aaeab
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 1%

---

# 記錄刪除工單 {#work-order-endpoint}

使用資料衛生API中的`/workorder`端點在Adobe Experience Platform中建立、檢視和管理記錄刪除工單。 工單可讓您控制、監控及追蹤資料集中的資料移除作業，協助您維持資料品質，並支援組織的資料控管標準。

>[!IMPORTANT]
>
>記錄刪除工單用於資料清理、匿名資料移除或資料最小化。 **請勿根據GDPR等隱私權法規對資料主體權利請求使用記錄刪除工單。**&#x200B;針對規範使用案例，請使用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 快速入門

開始之前，請參閱[總覽](./overview.md)以瞭解必要的標頭、如何讀取範例API呼叫，以及到何處尋找相關檔案。

## 配額與處理時間表 {#quotas}

記錄刪除工單受每日和每月識別碼提交限制的約束，此限制由您組織的授權權益決定。 這些限制同時適用於UI和API型記錄刪除請求。

>[!NOTE]
>
>您每天最多可以提交&#x200B;**1,000,000個識別碼**，但前提是剩餘的每月配額允許。 如果您的每月上限少於100萬，則每日提交內容不能超過該上限。

### 依產品的每月提交權利 {#quota-limits}

下表顯示產品和權益層級的識別碼提交限制。 對於每種產品，每月上限是兩個值中較小者：固定的識別碼上限，或與授權資料量繫結的百分比型臨界值。

| 產品 | 權益說明 | 每月上限（以較小者為準） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不含Privacy and Security Shield或Healthcare Shield附加元件 | 2,000,000個識別碼或可定址對象的5% |
| Real-Time CDP或Adobe Journey Optimizer | 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 15,000,000個識別碼或10%的可定址對象 |
| Customer Journey Analytics | 不含Privacy and Security Shield或Healthcare Shield附加元件 | 每百萬個CJA權益列有2,000,000個識別碼或100個識別碼 |
| Customer Journey Analytics | 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 每百萬個CJA權益列有15,000,000個識別碼或200個識別碼 |

>[!NOTE]
>
>根據組織的實際可定址對象或CJA列權益，大多陣列織的每月限制會較低。

>[!NOTE]
>
>配額在每個日曆月的第一天重設。 未使用的配額&#x200B;**不會**&#x200B;延續。

>[!NOTE]
>
>配額使用量是以貴組織針對&#x200B;**已提交識別碼**&#x200B;的每月授權為基礎。 配額不是由系統護欄強制執行，但可能被監視和檢閱。\
>記錄刪除工單容量是&#x200B;**共用服務**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何適用的Shield附加元件的最高權益。

### 處理識別碼提交的時間表 {#sla-processing-timelines}

提交之後，系統會根據您的權益層次，將記錄刪除工單排入佇列並進行處理。

| 產品與權益說明 | 佇列持續時間 | 最大處理時間(SLA) |
|------------------------------------|---------------------|-------------------------------|
| 不含Privacy and Security Shield或Healthcare Shield附加元件 | 最多15天 | 30 天 |
| 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 通常為24小時 | 15 天 |

如果您的組織需要更高的限制，請聯絡您的Adobe代表以要求軟體權利檔案審查。

>[!TIP]
>
>若要檢查您目前的配額使用量或權利階層，請參閱[配額參考指南](../api/quota.md)。

## 清單記錄刪除工單 {#list}

擷取貴組織中資料衛生作業的記錄刪除工單的分頁清單。 使用查詢引數篩選結果。 每個工單記錄都包含動作型別（例如`identity-delete`）、狀態、相關資料集和使用者詳細資訊，以及稽核中繼資料。

**API格式**

```http
GET /workorder
```

下表說明可用於列出記錄刪除工單的查詢引數。

| 查詢引數 | 說明 |
| --------------- | ------------|
| `search` | 跨欄位區分大小寫的部分相符（萬用字元搜尋）：author、displayName、description或datasetName。 也符合確切的到期ID。 |
| `type` | 依工單型別篩選結果（例如，`identity-delete`）。 |
| `status` | 以逗號分隔的工作單狀態清單。 狀態值區分大小寫。<br>列舉： `received`，`validated`，`submitted`，`ingested`，`completed`，`failed` |
| `author` | 尋找最近更新工單的人員（或原始建立者）。 接受常值或SQL模式。 |
| `displayName` | 工單顯示名稱不區分大小寫。 |
| `description` | 工作單說明的相符專案不區分大小寫。 |
| `workorderId` | 工單ID的完全相符。 |
| `sandboxName` | 要求中使用的沙箱名稱完全相符，或使用`*`包含所有沙箱。 |
| `fromDate` | 依在此日期或之後建立的工作單進行篩選。 需要設定`toDate`。 |
| `toDate` | 依在此日期或之前建立的工作單進行篩選。 需要設定`fromDate`。 |
| `filterDate` | 僅傳回在此日期建立、更新或變更狀態的工作單。 |
| `page` | 要傳回的頁面索引（從0開始）。 |
| `limit` | 每頁結果數上限（1-100，預設： 25）。 |
| `orderBy` | 結果的排序順序。 使用`+`或`-`首碼進行遞增/遞減。 範例：`orderBy=-datasetName`。 |
| `properties` | 要根據結果包含的其他欄位清單（以逗號分隔）。 選填。 |


**要求**

下列請求會擷取所有已完成的記錄刪除工單，限製為每頁兩次：

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回記錄刪除工單的分頁清單。

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

下表說明回應中的特性。

| 屬性 | 說明 |
| --- | --- |
| `results` | 刪除工單物件的記錄陣列。 每個物件都包含下列欄位。 |
| `workorderId` | 記錄刪除工單的唯一識別碼。 |
| `orgId` | 您的唯一組織識別碼。 |
| `bundleId` | 包含此記錄刪除工單的組合的唯一識別碼。 套裝可讓下游服務將多個刪除訂單分組並一起處理。 |
| `action` | 工單中要求的動作型別。 |
| `createdAt` | 建立工單時的時間戳記。 |
| `updatedAt` | 上次更新工單時的時間戳記。 |
| `operationCount` | 工單中包含的作業數。 |
| `targetServices` | 工單的目標服務清單。 |
| `status` | 工單的目前狀態。 可能的值為： `received`、`validated`、`submitted`、`ingested`、`completed`和`failed`。 |
| `createdBy` | 建立工作單之使用者的電子郵件和識別碼。 |
| `datasetId` | 與工單相關之資料集的唯一識別碼。 如果要求套用至所有資料集，此欄位將會設為「全部」。 |
| `datasetName` | 與工單相關聯的資料集名稱。 |
| `displayName` | 適用於工單的可讀取標籤。 |
| `description` | 工單用途的說明。 |
| `total` | 符合查詢的記錄刪除工單總數。 |
| `count` | 刪除目前頁面中工單的記錄數。 |
| `_links` | 分頁與導覽連結。 |
| `next` | 下一頁具有`href` （字串）和`templated` （布林值）的物件。 |
| `page` | 具有`href` （字串）和`templated` （布林值）的物件，用於頁面導覽。 |

{style="table-layout:auto"}

## 建立記錄刪除工單 {#create}

若要從單一資料集或所有資料集中刪除與一或多個身分相關聯的記錄，請對`/workorder`端點發出POST要求。

工單會以非同步方式處理，並在提交後顯示在工單清單中。

>[!TIP]
>
>透過API提交的每個記錄刪除工單最多可包含&#x200B;**100,000個身分**。 針對每個請求提交儘可能多的身分，以發揮最大效率。 避免大量提交作業，例如單一ID工單。

**API格式**

```http
POST /workorder
```

>[!NOTE]
>
>您只能從關聯XDM結構描述定義主要身分或身分對應的資料集中刪除記錄。

>[!NOTE]
>
>如果您嘗試為已有有效到期日的資料集建立記錄刪除工作單，請求會傳回HTTP 400 （錯誤請求）。有效到期日是任何尚未完成的已排程刪除。

**要求**

以下請求會從特定資料集中刪除與指定電子郵件地址相關聯的所有記錄。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

下表說明建立記錄刪除工單的特性。

| 屬性 | 說明 |
| --- | --- |
| `displayName` | 此記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |
| `action` | 記錄刪除工單所要求的動作。 若要刪除與指定識別相關聯的記錄，請使用`delete_identity`。 |
| `datasetId` | 資料集的唯一識別碼。 使用特定資料集的資料集ID，或使用`ALL`來鎖定所有資料集。 資料集必須具有主要身分或身分對應。 如果身分對應存在，則會顯示為名為`identityMap`的頂層欄位。<br>請注意，資料集列的身分對應中可能有許多身分，但只能將一個標示為主要身分。 必須包含`"primary": true`以強制`id`符合主要身分。 |
| `namespacesIdentities` | 物件陣列，每個都包含：<br><ul><li> `namespace`：物件具有`code`屬性，指定了身分名稱空間（例如，「email」）。</li><li> `IDs`：要刪除此名稱空間的一組身分值。</li></ul>身分識別名稱空間會提供身分識別資料的內容。 您可以使用Experience Platform提供的標準名稱空間或建立您自己的名稱空間。 若要深入瞭解，請參閱[身分名稱空間檔案](../../identity-service/features/namespaces.md)和[身分識別服務API規格](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)。 |

**回應**

成功的回應會傳回新記錄刪除工單的詳細資料。

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

下表說明回應中的特性。

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 記錄刪除工單的唯一識別碼。 使用此值可查詢刪除的狀態或詳細資訊。 |
| `orgId` | 您的唯一組織識別碼。 |
| `bundleId` | 包含此記錄刪除工單的組合的唯一識別碼。 套裝可讓下游服務將多個刪除訂單分組並一起處理。 |
| `action` | 記錄刪除工單中請求的動作型別。 |
| `createdAt` | 建立工單時的時間戳記。 |
| `updatedAt` | 上次更新工單時的時間戳記。 |
| `operationCount` | 工單中包含的作業數。 |
| `targetServices` | 記錄刪除工單的目標服務清單。 |
| `status` | 記錄刪除工單的目前狀態。 |
| `createdBy` | 建立記錄刪除工作單之使用者的電子郵件和識別碼。 |
| `datasetId` | 資料集的唯一識別碼。 如果要求適用於所有資料集，則值將設為`ALL`。 |
| `datasetName` | 此記錄刪除工單的資料集名稱。 |
| `displayName` | 記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |

{style="table-layout:auto"}

>[!NOTE]
>
>記錄刪除工單的動作屬性目前在API回應中為`identity-delete`。 如果API變更為使用不同的值（例如`delete_identity`），本檔案將會相應地更新。

## 擷取特定記錄刪除工單的詳細資料 {#lookup}

向`/workorder/{WORKORDER_ID}`發出GET要求，擷取特定記錄刪除工單的資訊。 回應包括動作型別、狀態、關聯的資料集和使用者資訊，以及稽核中繼資料。

**API格式**

```http
GET /workorder/{WORKORDER_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 您所查詢之記錄刪除工單的唯一識別碼。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回指定記錄刪除工單的詳細資料。

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

下表說明回應中的特性。

| 屬性 | 說明 |
| --- | --- |
| `workorderId` | 記錄刪除工單的唯一識別碼。 |
| `orgId` | 您組織的唯一識別碼。 |
| `bundleId` | 包含此記錄刪除工單的組合的唯一識別碼。 套裝可讓下游服務將多個刪除訂單分組並一起處理。 |
| `action` | 記錄刪除工單中請求的動作型別。 |
| `createdAt` | 建立工單時的時間戳記。 |
| `updatedAt` | 上次更新工單時的時間戳記。 |
| `operationCount` | 工單中包含的作業數。 |
| `targetServices` | 受此記錄刪除工單影響的目標服務清單。 |
| `status` | 記錄刪除工單的目前狀態。 |
| `createdBy` | 建立記錄刪除工作單之使用者的電子郵件和識別碼。 |
| `datasetId` | 與工單相關之資料集的唯一識別碼。 |
| `datasetName` | 與工單相關聯的資料集名稱。 |
| `displayName` | 記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |

## 更新記錄刪除工單

藉由對`name`端點發出PUT要求，更新記錄刪除工作順序的`description`和`/workorder/{WORKORDER_ID}`。

**API格式**

```http
PUT /workorder/{WORKORDER_ID}
```

下表說明此請求的引數。

| 參數 | 說明 |
| --- | --- |
| `{WORK_ORDER_ID}` | 您要更新的記錄刪除工單的唯一識別碼。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

下表說明您可以更新的特性。

| 屬性 | 說明 |
| --- | --- |
| `name` | 記錄刪除工作單的更新後可讀取標籤。 |
| `description` | 記錄刪除工單的更新說明。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回更新的工單請求。

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
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
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | 記錄刪除工單的唯一識別碼。 |
| `orgId` | 您組織的唯一識別碼。 |
| `bundleId` | 包含此記錄刪除工單的組合的唯一識別碼。 套裝可讓下游服務將多個刪除訂單分組並一起處理。 |
| `action` | 記錄刪除工單中請求的動作型別。 |
| `createdAt` | 建立工單時的時間戳記。 |
| `updatedAt` | 上次更新工單時的時間戳記。 |
| `operationCount` | 工單中包含的作業數。 |
| `targetServices` | 受此記錄刪除工單影響的目標服務清單。 |
| `status` | 記錄刪除工單的目前狀態。 可能的值為： `received`、`validated`、`submitted`、`ingested`、`completed`和`failed`。 |
| `createdBy` | 建立記錄刪除工作單之使用者的電子郵件和識別碼。 |
| `datasetId` | 與記錄刪除工單相關之資料集的唯一識別碼。 |
| `datasetName` | 與記錄刪除工單關聯的資料集名稱。 |
| `displayName` | 記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |
| `productStatusDetails` | 列出請求下游處理序目前狀態的陣列。 每個物件包含：<ul><li>`productName`：下游服務的名稱。</li><li>`productStatus`：下游服務的目前處理狀態。</li><li>`createdAt`：服務發佈最新狀態時的時間戳記。</li></ul>將工單提交至下游服務以開始處理之後，即可使用此屬性。 |

{style="table-layout:auto"}
