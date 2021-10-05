---
title: 資料衛生API(Alpha)
description: 了解如何以程式設計方式修正或刪除客戶在Adobe Experience Platform中儲存的個人資料。
hide: true
hidefromtoc: true
source-git-commit: dfe9c1ef826bc769a82938223029cd41c066c221
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 資料衛生API(Alpha)

>[!IMPORTANT]
>
>資料衛生API目前位於Alpha中，而您的組織可能尚未取得存取權。 本檔案所述的功能可能會有所變更。

資料衛生API可讓您以程式設計方式修正或刪除客戶儲存在Adobe Experience Platform中的個人資料。 與Privacy ServiceAPI不同，這些操作不需要與法律隱私權法規相關聯，而且可單純用於保持資料乾淨和準確。

## 快速入門

本節提供在嘗試呼叫資料衛生API前，您需先了解的核心概念的簡介。

### 收集必要標題的值

若要呼叫資料衛生API，您必須先收集驗證憑證。 這些是用來存取Privacy ServiceAPI的相同憑證。 請依照Privacy ServiceAPI的[快速入門手冊](./api/getting-started.md)，為資料衛生API的每個必要標題產生值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

### 讀取範例API呼叫

本檔案提供範例API呼叫，以示範如何設定請求格式。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience PlatformAPI快速入門手冊中的[如何讀取範例API呼叫](../landing/api-guide.md#sample-api)一節。

## 建立刪除作業

您可以提出POST請求，以建立刪除作業。

**API格式**

```http
POST /jobs
```

**要求**

請求裝載的結構與Privacy ServiceAPI](./api/privacy-jobs.md#access-delete)中的[delete請求的結構類似。 它包括`users`陣列，其對象表示要刪除其資料的用戶。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{IMS_ORG}"
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
| `companyContexts` | 包含貴組織驗證資訊的陣列。 它必須包含具有下列屬性的單一物件： <ul><li>`namespace`:必須設為 `imsOrgID`。</li><li>`value`:您的IMS組織ID。這與`x-gw-ims-org-id`標題中提供的值相同。</li></ul> |
| `users` | 一個陣列，其中包含至少一個要刪除其資訊的用戶的集合。 每個使用者物件包含下列資訊： <ul><li>`key`:用來限定回應資料中個別作業ID的使用者識別碼。最佳實務是為此值選擇可輕鬆識別的唯一字串，以便日後參考或查閱。</li><li>`action`:列出對使用者資料採取之所需動作的陣列。必須包含單一字串值：`delete`。</li><li>`userIDs`:使用者的身分集合。單一使用者可擁有的身分數目上限為九。 每個身分包含下列屬性： <ul><li>`namespace`:與 [ID](../identity-service/namespaces.md) 相關聯的身分名稱。這可以是Platform所識別的[標準命名空間](./api/appendix.md#standard-namespaces)，也可以是您的組織所定義的自訂命名空間。 使用的命名空間類型必須反映在`type`屬性中。</li><li>`value`:身分值。</li><li>`type`:如果使用全域 `standard` 辨識的命名空間，或使用 `custom` 組織定義的命名空間，則必須設為。</li></ul></li></ul> |

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
