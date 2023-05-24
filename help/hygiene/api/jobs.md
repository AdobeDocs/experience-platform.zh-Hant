---
title: 使用資料衛生API刪除記錄
description: 瞭解如何以寫程式方式更正或刪除客戶在Adobe Experience Platform儲存的個人資料。
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

資料衛生API允許您以寫程式方式更正或刪除客戶在Adobe Experience Platform儲存的個人資料。

您可以通過與 [Privacy ServiceAPI](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## 快速入門

本節介紹在嘗試調用資料衛生API之前需要瞭解的核心概念。

### 收集所需標題的值

要調用資料衛生API，必須先收集身份驗證憑據。 這些是用於訪問Privacy ServiceAPI的相同憑據。 請參閱 [API概述](./overview.md#getting-started) 為資料衛生API的每個必需標頭生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* `Content-Type: application/json`

### 讀取示例API調用

本文檔提供了一個示例API調用，以演示如何格式化請求。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/api-guide.md#sample-api) 的FTP伺服器連接設定。

## 建立刪除作業

您可以通過發出POST請求來建立刪除作業。

**API格式**

```http
POST /jobs
```

**要求**

請求負載的結構與請求負載的結構類似 [刪除Privacy ServiceAPI中的請求](../../privacy-service/api/privacy-jobs.md#access-delete)。 它包括 `users` 其對象表示要刪除其資料的用戶的陣列。

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
| `companyContexts` | 包含組織驗證資訊的陣列。 它必須包含具有以下屬性的單個對象： <ul><li>`namespace`:必須設定為 `imsOrgID`。</li><li>`value`:您的組織ID。 此值與 `x-gw-ims-org-id` 標題。</li></ul> |
| `users` | 包含至少一個要刪除其資訊的用戶集合的陣列。 每個用戶對象都包含以下資訊： <ul><li>`key`:用於限定響應資料中的單獨作業ID的用戶的標識符。 最好為此值選擇一個唯一且易於識別的字串，以便以後可以引用或查找它。</li><li>`action`:一個陣列，它列出了對用戶資料執行的所需操作。 必須包含單個字串值： `delete`。</li><li>`userIDs`:用戶的標識集合。 單個用戶可以擁有的標識數限制為9。 每個標識都包含以下屬性： <ul><li>`namespace`:的 [標識命名空間](../../identity-service/namespaces.md) 與ID關聯。 這可以是 [標準命名空間](../../privacy-service/api/appendix.md#standard-namespaces) 平台識別，或者它可以是您的組織定義的自定義命名空間。 使用的命名空間類型必須反映在 `type` 屬性。</li><li>`value`:標識值。</li><li>`type`:必須設定為 `standard` 如果使用全局識別的命名空間，或 `custom` 使用由組織定義的命名空間。</li></ul></li></ul> |

{style="table-layout:auto"}

**回應**

成功的響應將返回已建立作業的詳細資訊。

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
