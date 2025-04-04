---
title: 使用資料衛生API刪除記錄
description: 瞭解如何以程式設計方式修正或刪除客戶在Adobe Experience Platform中儲存的個人資料。
role: Developer
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 5%

---

# 使用資料衛生API刪除記錄

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

資料衛生API可讓您以程式設計方式更正或刪除客戶儲存在Adobe Experience Platform中的個人資料。

您可以透過與[Privacy Service API](../../privacy-service/api/overview.md)相同的根路徑來存取API： `https://platform.adobe.io/data/core/privacy/`

## 快速入門

本節提供嘗試呼叫資料衛生API之前需要瞭解的核心概念簡介。

### 收集所需標頭的值

為了呼叫資料衛生API，您必須先收集您的驗證認證。 這些是用於存取Privacy Service API的相同認證。 請參閱[API總覽](./overview.md#getting-started)，為資料衛生API的每個必要標題產生值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* `Content-Type: application/json`

### 讀取範例 API 呼叫

本檔案提供範例API呼叫，示範如何格式化您的請求。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Experience Platform API快速入門手冊中[如何讀取範例API呼叫](../../landing/api-guide.md#sample-api)的相關章節。

## 建立刪除工作

您可以發出POST要求來建立刪除工作。

**API格式**

```http
POST /jobs
```

**要求**

要求裝載的結構類似於Privacy Service API](../../privacy-service/api/privacy-jobs.md#access-delete)中[刪除要求的結構。 它包含`users`陣列，其物件代表要刪除其資料的使用者。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `companyContexts` | 包含貴組織驗證資訊的陣列。 它必須包含具有下列屬性的單一物件： <ul><li>`namespace`：必須設定為`imsOrgID`。</li><li>`value`：您的組織識別碼。 這是`x-gw-ims-org-id`標頭中提供的相同值。</li></ul> |
| `users` | 一個陣列，包含您要刪除其資訊之至少一個使用者的集合。 每個使用者物件包含下列資訊： <ul><li>`key`：用於限定回應資料中個別工作ID的使用者識別碼。 最佳實務是為這個值選擇唯一且易於識別的字串，以便稍後參考或查詢。</li><li>`action`：列出要對使用者資料採取的所需動作的陣列。 必須包含單一字串值： `delete`。</li><li>`userIDs`：使用者的身分識別集合。 單一使用者可擁有的身分數量限製為九個。 每個身分都包含以下屬性： <ul><li>`namespace`：與識別碼關聯的[身分名稱空間](../../identity-service/features/namespaces.md)。 這可以是Experience Platform識別的[標準名稱空間](../../privacy-service/api/appendix.md#standard-namespaces)，也可以是您的組織定義的自訂名稱空間。 使用的名稱空間型別必須反映在`type`屬性中。</li><li>`value`：身分值。</li><li>`type`：若使用全域辨識的名稱空間，則必須設為`standard`；若使用貴組織定義的名稱空間，則必須設為`custom`。</li></ul></li></ul> |

{style="table-layout:auto"}

**回應**

成功的回應會傳回已建立工作的詳細資訊。

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
