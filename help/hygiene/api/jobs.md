---
title: 使用資料衛生API刪除記錄
description: 了解如何以程式設計方式修正或刪除客戶在Adobe Experience Platform中儲存的個人資料。
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 使用資料衛生API刪除記錄

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

資料衛生API可讓您以程式設計方式修正或刪除客戶儲存在Adobe Experience Platform中的個人資料。

您可以透過與 [Privacy ServiceAPI](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## 快速入門

本節提供在嘗試呼叫資料衛生API前，您需先了解的核心概念的簡介。

### 收集必要標題的值

若要呼叫資料衛生API，您必須先收集驗證憑證。 這些是用來存取Privacy ServiceAPI的相同憑證。 請參閱 [API概述](./overview.md#getting-started) 為資料衛生API的每個必要標題產生值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

### 讀取範例API呼叫

本檔案提供範例API呼叫，以示範如何設定請求格式。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/api-guide.md#sample-api) (位於Experience PlatformAPI快速入門手冊中)。

## 建立刪除作業

您可以提出POST請求，以建立刪除作業。

**API格式**

```http
POST /jobs
```

**要求**

請求裝載的結構類似於 [刪除Privacy ServiceAPI中的請求](../../privacy-service/api/privacy-jobs.md#access-delete). 其中包含 `users` 陣列，其對象表示要刪除其資料的用戶。

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
| `companyContexts` | 包含貴組織驗證資訊的陣列。 它必須包含具有下列屬性的單一物件： <ul><li>`namespace`:必須設為 `imsOrgID`.</li><li>`value`:您的組織ID。 這與 `x-gw-ims-org-id` 頁首。</li></ul> |
| `users` | 一個陣列，其中包含至少一個要刪除其資訊的用戶的集合。 每個使用者物件包含下列資訊： <ul><li>`key`:用來限定回應資料中個別作業ID的使用者識別碼。 最佳實務是為此值選擇可輕鬆識別的唯一字串，以便日後參考或查閱。</li><li>`action`:列出對使用者資料採取之所需動作的陣列。 必須包含單一字串值： `delete`.</li><li>`userIDs`:使用者的身分集合。 單一使用者可擁有的身分數目上限為九。 每個身分包含下列屬性： <ul><li>`namespace`:此 [身分命名空間](../../identity-service/namespaces.md) 與ID相關聯。 這可以是 [標準命名空間](../../privacy-service/api/appendix.md#standard-namespaces) 可由Platform識別，或是由您的組織定義的自訂命名空間。 使用的命名空間類型必須反映在 `type` 屬性。</li><li>`value`:身分值。</li><li>`type`:必須設為 `standard` 如果使用全域識別的命名空間，或 `custom` 如果您使用的是組織定義的命名空間。</li></ul></li></ul> |

{style="table-layout:auto"}

**回應**

成功的回應會傳回已建立作業的詳細資訊。

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
