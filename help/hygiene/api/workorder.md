---
title: 記錄刪除工單
description: 瞭解如何使用資料衛生API中的/workorder端點，以管理Adobe Experience Platform中的記錄刪除工單。 本指南涵蓋配額、處理時間表及API使用情形。
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 5ca3e4feae3096e41689610ac3afac7e93047149
workflow-type: tm+mt
source-wordcount: '3316'
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

下表顯示產品和權益層級的識別碼提交限制。 對於每種產品，每月上限是兩個值中較小者：固定的識別碼上限，或與授權資料量繫結的百分比型臨界值。 實際上，根據組織的實際可定址對象或Adobe Customer Journey Analytics列權益，大多陣列織的每月上限較低。

| 產品 | 權益說明 | 每月上限（以較小者為準） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不含Privacy and Security Shield或Healthcare Shield附加元件 | 2,000,000個識別碼或可定址對象的5% |
| Real-Time CDP或Adobe Journey Optimizer | 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 15,000,000個識別碼或10%的可定址對象 |
| Customer Journey Analytics | 不含Privacy and Security Shield或Healthcare Shield附加元件 | 每百萬個Customer Journey Analytics權益列有2,000,000個識別碼或100個識別碼 |
| Customer Journey Analytics | 搭配Privacy and Security Shield或Healthcare Shield附加元件 | 每百萬個Customer Journey Analytics權益列有15,000,000個識別碼或200個識別碼 |

>[!NOTE]
>
>- 配額在每個日曆月的第一天重設。 未使用的配額&#x200B;**不會**&#x200B;延續。
>- 配額使用量是以貴組織針對&#x200B;**已提交識別碼**&#x200B;的每月授權為基礎。 配額不是由系統護欄強制執行，但可能被監視和檢閱。
>- 記錄刪除工單容量是&#x200B;**共用服務**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何適用的Shield附加元件的最高權益。

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
        "identity",
        "ajo"
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
| `targetServices` | 處理刪除的目標服務集。 預設值取決於您組織的權益。 對於具有Real-Time CDP或Adobe Journey Optimizer的組織，預設為完整的支援服務集(`["datalake", "identity", "profile", "ajo"]`)。 對於僅限Customer Journey Analytics的組織（沒有即時客戶設定檔權利），唯一有效值為[&quot;datalake&quot;]。 |
| `status` | 工單的目前狀態。 可能的值為： `received`、`validated`、`submitted`、`ingested`、`completed`和`failed`。 |
| `createdBy` | 建立工作單之使用者的電子郵件和識別碼。 |
| `datasetId` | 工作順序所瞄準的資料集：單一資料集ID、以逗號分隔的資料集ID清單（多個資料集）或常值`ALL`。 當要求使用僅設定檔模式時，這個值為`ALL`。 |
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

若要從單一資料集、多個資料集或所有資料集中刪除與一或多個身分相關聯的記錄，請對`/workorder`端點發出POST要求。

工單會以非同步方式處理，並在提交後顯示在工單清單中。 自2026年3月Experience Platform發行版本起，所有客戶一般都能使用多資料集和僅限設定檔（目標服務）選項。

>[!TIP]
>
>透過API提交的每個記錄刪除工單最多可包含&#x200B;**100,000個身分**。 針對每個請求提交儘可能多的身分，以發揮最大效率。 避免大量提交作業，例如單一ID工單。

**API格式**

```http
POST /workorder
```

>[!IMPORTANT]
>
>記錄刪除工單僅在&#x200B;**主要身分**&#x200B;欄位上執行。 下列限制適用：
>
>- **資料集結構描述必須定義主要身分或身分對應。**&#x200B;您只能從關聯XDM結構描述定義主要身分或身分對應的資料集中刪除記錄。
>- **未掃描次要身分。**&#x200B;如果資料集包含多個身分欄位，則只會使用主要身分進行比對。 無法根據非主要身分定位或刪除記錄。
>- **略過沒有填入主要身分的記錄。**&#x200B;如果記錄未填入主要身分中繼資料，則無法刪除。
>- **在身分設定之前擷取的資料不合格。**&#x200B;如果主要身分欄位在資料擷取後新增到結構描述，則無法透過記錄刪除工作單來刪除先前擷取的記錄。

>[!NOTE]
>
>如果您嘗試為已有有效到期日的資料集建立記錄刪除工單，請求會傳回HTTP 400 （錯誤請求）。 有效到期是指任何尚未完成的排程刪除。

### 身分裝載格式（`namespacesIdentities`或`identities`）

要求內文必須包含下列&#x200B;**其中一個**。

| 格式 | 屬性 | 形狀 | 使用時機 |
|--------|----------|-------|-------------|
| **建議** | `namespacesIdentities` | 具有`namespace` （例如`{ "code": "email" }`）和`ids` （識別字串陣列）的物件陣列。 | 用於所有裝載，無論是手動建構或程式碼產生。 當許多身分共用相同的名稱空間時，這尤其能有效減少裝載大小。 |
| **也接受** | `identities` | 具有`namespace` （例如`{ "code": "email" }`）和單一`id` （字串）的物件陣列。 | 已接受以便回溯相容。 這是[csv至資料衛生轉換指令碼](#convert-id-lists-to-json-for-record-delete-requests)產生的格式。 此服務會在內部標準化此格式，因此產生的行為是相同的。 |

如果您傳送&#x200B;**兩個屬性**、**兩個屬性**，或為您包含的屬性提供&#x200B;**空陣列**，API會傳回&#x200B;**HTTP 400 （錯誤請求）**&#x200B;及下列其中一個訊息：

- **提供的兩個屬性：** `"Identities and NamespacesIdentities are not allowed at the same time"`
- **未提供或空白清單：** `"Identities are Empty for Delete Identity request."`

**要求**

以下請求會從特定資料集中刪除與指定電子郵件地址相關聯的所有記錄。 它使用建議的`namespacesIdentities`格式。

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
            "ids": [
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
| `datasetId` | 資料集的唯一識別碼。 值必須正好是下列其中之一：常值`ALL`、單一資料集ID，或以逗號分隔的兩個或多個資料集ID清單（例如`"id1,id2,id3"`）。 您無法將`ALL`與特定ID結合。 單一資料集請求的行為與先前相同，多資料集請求會從每個列出的資料集中刪除身分，並`ALL`鎖定每個資料集。 資料集必須具有主要身分或身分對應。 如果身分對應存在，則會顯示為名為`identityMap`的頂層欄位。<br>**注意**：資料集資料列的身分對應中可能有許多身分，但只能將一個標示為主要身分。 必須包含`"primary": true`以強制`id`符合主要身分。<br>使用`targetServices`進行僅設定檔刪除時，`datasetId`必須是`ALL`。 |
| `targetServices` | 選填。 指定應該處理刪除的服務。 預設值取決於您組織的權益。 依預設，具有Real-Time CDP或Adobe Journey Optimizer的組織會收到完整的支援服務集(`["datalake", "identity", "profile", "ajo"]`)。 擁有Customer Journey Analytics但沒有即時客戶設定檔權益的組織只能使用[&quot;datalake&quot;]。 若要將刪除限製為僅與設定檔相關的資料，並保留資料湖不變，請將此項設為`["identity", "profile", "ajo"]` （以任何順序）。 此僅設定檔模式需要Real-Time CDP或Adobe Journey Optimizer權益，且`datasetId`必須為`ALL`。 |
| `identities` | **只使用`identities`或`namespacesIdentities`其中之一。**&#x200B;物件陣列，每個具有`namespace` （具有`code`的物件，例如`"email"`）和`id` （單一識別字串）。 接受此項，以便回溯相容及由轉換指令碼產生。 此服務會在內部標準化此格式；行為相同。 請參閱上述[身分裝載格式](#identity-payload-format-identities-or-namespacesidentities)。 |
| `namespacesIdentities` | **只使用`identities`或`namespacesIdentities`其中之一。**&#x200B;物件陣列，每個具有`namespace` （具有`code`的物件，例如`"email"`）和`ids` （識別字串陣列）。 建議用於所有裝載。 當許多身分共用一個名稱空間時，`namespacesIdentities`屬性會更緊湊。 請參閱上述[身分裝載格式](#identity-payload-format-identities-or-namespacesidentities)。 識別名稱空間： [識別名稱空間檔案](../../identity-service/features/namespaces.md)，[識別服務API](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)。 |

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
    "identity",
    "ajo"
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
| `datasetId` | 資料集的唯一識別碼。 如果要求適用於所有資料集，則值將設為`ALL`。 對於多資料集請求，值會反映所提交的逗號分隔清單或單一ID。 |
| `datasetName` | 此記錄刪除工單的資料集名稱。 |
| `displayName` | 記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |

{style="table-layout:auto"}

回應`targetServices`值會回應您的要求，或在省略時顯示完整的預設設定（請參閱上方的回應表格）。

### 多資料集和僅限設定檔(API) {#multi-dataset-profile-only}

以下選項只能透過API使用，資料衛生UI中不支援。 這類許可權可控制哪些資料集和哪些服務會處理刪除，從而啟用多資料集提交和僅限設定檔的目標服務請求。

下表概述每個選項的請求內文和行為變更。

| 選項 | 要求內文變更 | 行為 |
|--------|---------------------|----------|
| **多個資料集** | 在`datasetId`中使用逗號分隔清單（例如`"id1,id2,id3"`）。 單一ID或`ALL`未變更。 | 身分會從列出的資料集中刪除（或是從`ALL`時的一個資料集，或是從所有資料集中刪除）。 |
| **僅設定檔（目標服務）** | 新增`targetServices`並包含`["identity", "profile", "ajo"]` （任何順序）。 需要`datasetId`： `"ALL"`。 | 只有身分、設定檔和Adobe Journey Optimizer會處理刪除；資料湖不會修改。 |

#### 多資料集請求

`datasetId`欄位會以逗號分割：使用單一ID （與之前相同的行為）、以逗號分隔的ID清單或常值`ALL`。 若要以一個工作順序從多個特定資料集中刪除身分，請提供逗號分隔清單：

```json
"datasetId": "6707eb36eef4d42ab86d9fbe,6643f00c16ddf51767fcf780"
```

接著會從每個列出的資料集中刪除身分。 單一資料集要求如常運作；使用`ALL`來鎖定每個資料集。 值必須剛好是下列其中一項： `ALL`、單一資料集ID，或兩個以上以逗號分隔的資料集ID （不將`ALL`與特定ID結合）。

#### 僅限設定檔（目標服務）

若要在保持資料湖不受影響時僅移除身分和設定檔相關資料，請以任意順序包含具有這三個值的`targetServices`： `identity`、`profile`和`ajo`。 明確包括身分、設定檔和AJO；排除資料湖。 在此模式中，`datasetId`必須是`ALL` （使用案例是完整設定檔刪除，而不是每個資料集片段）。

下列範例會建立僅設定檔記錄刪除工單：

```shell
curl -X POST \
  "https://platform.adobe.io/data/core/hygiene/workorder" \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
    "action": "delete_identity",
    "datasetId": "ALL",
    "displayName": "Profile-only delete for specified identity",
    "description": "Delete identity, profile, and AJO data only; datalake unchanged.",
    "targetServices": ["identity", "profile", "ajo"],
    "namespacesIdentities": [
      {
        "namespace": { "code": "email" },
        "ids": ["user@example.com"]
      }
    ]
  }'
```

多資料集或僅限設定檔要求的成功回應會遵循與其他工單回應相同的形狀。 傳回的`datasetId`和`targetServices`反映請求中的值（或省略`targetServices`時的完整預設清單），因此您可以確認已提交的內容。

>[!NOTE]
>
>記錄刪除工單的動作屬性目前在API回應中為`identity-delete`。 如果API變更為使用不同的值（例如`delete_identity`），本檔案將會相應地更新。

## 針對記錄刪除請求將ID清單轉換為JSON (#convert-id-lists-to-json-for-record-delete-requests)

當您的識別碼位於CSV、TSV或TXT檔案中時，使用轉換指令碼為`/workorder`端點產生必要的JSON裝載。 此方法在處理現有資料檔案時特別實用。 如需現成的指令碼和指示，請參閱[csv至資料衛生GitHub存放庫](https://github.com/perlmonger42/csv-to-data-hygiene)。

指令碼會輸出&#x200B;**`identities`**&#x200B;格式 — 每個具有`id`的物件一個`namespace`。 API接受此格式的現狀；您可以直接在POST內文中將產生的JSON傳送給`/workorder`，而不需要進行轉換。 建議的格式為&#x200B;**`namespacesIdentities`**；請參閱[建立記錄刪除工單](#create)和[身分裝載格式](#identity-payload-format-identities-or-namespacesidentities)。

### 產生JSON裝載

下列bash指令碼範例示範如何以Python或Ruby執行轉換指令碼：

>[!BEGINTABS]

>[!TAB 執行Python指令碼的範例]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB 執行Ruby指令碼的範例]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

下表說明bash指令碼中的引數。

| 參數 | 說明 |
| ---           | ---     |
| `verbose` | 啟用詳細資訊輸出。 |
| `column` | 包含要刪除之身分值的資料行的索引（以1為基礎）或標題名稱。 若未指定，則預設為第一欄。 |
| `namespace` | 傳遞給指令碼的身分名稱空間程式碼（例如，`email`）。 產生的JSON會在每個物件的`namespace.code`屬性中使用此專案。 |
| `dataset-id` | 資料集的唯一識別碼：單一ID、多個資料集使用逗號分隔的ID，或所有資料集使用`ALL`。 |
| `description` | 記錄刪除工單的說明。 |
| `output-dir` | 寫入輸出JSON裝載的目錄。 |

{style="table-layout:auto"}

以下範例顯示從CSV、TSV或TXT檔案轉換而來的成功JSON裝載。 它包含與指定名稱空間關聯的記錄，並用於刪除由電子郵件地址識別的記錄。

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

下表說明JSON裝載中的屬性。

| 屬性 | 說明 |
| ---          | ---     |
| `action` | 記錄刪除工單所要求的動作。 由轉換指令碼自動設定為`delete_identity`。 |
| `datasetId` | 資料集的唯一識別碼：單一ID、逗號分隔的ID或`ALL`。 |
| `displayName` | 此記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |
| `identities` | 物件陣列，每個都包含：<br><ul><li> `namespace`：物件具有`code`屬性，指定了身分名稱空間（例如，「email」）。</li><li> `id`：要刪除此名稱空間的身分值。</li></ul> |

{style="table-layout:auto"}

### 將產生的JSON資料提交至`/workorder`端點

指令碼輸出使用`identities`格式，API接受其原樣。 當您將`-d` POST要求傳送至`curl`端點時，請使用轉換的JSON裝載作為要求內文(`/workorder`)。 如需完整的請求選項和驗證規則，請參閱[建立記錄刪除工單](#create)。

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
| `datasetId` | 與工單相關之資料集的唯一識別碼（單一ID、逗號分隔的ID或`ALL`）。 |
| `datasetName` | 與工單相關聯的資料集名稱。 |
| `displayName` | 記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |

## 更新記錄刪除工單 {#update}

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
| `datasetId` | 與記錄刪除工作單相關之資料集的唯一識別碼（單一ID、逗號分隔的ID或`ALL`）。 |
| `datasetName` | 與記錄刪除工單關聯的資料集名稱。 |
| `displayName` | 記錄刪除工單的可讀取標籤。 |
| `description` | 記錄刪除工單的說明。 |
| `productStatusDetails` | 列出請求下游處理序目前狀態的陣列。 每個物件包含：<ul><li>`productName`：下游服務的名稱。</li><li>`productStatus`：下游服務的目前處理狀態。</li><li>`createdAt`：服務發佈最新狀態時的時間戳記。</li></ul>將工單提交至下游服務以開始處理之後，即可使用此屬性。 |

{style="table-layout:auto"}
