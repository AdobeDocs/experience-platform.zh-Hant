---
keywords: Experience Platform；首頁；熱門主題；流式服務；更新帳戶
solution: Experience Platform
title: 使用流服務API更新帳戶
type: Tutorial
description: 本教程介紹了使用流服務API更新帳戶的詳細資訊和憑據的步驟。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 使用流服務API更新帳戶

在某些情況下，可能需要更新現有源連接的詳細資訊。 [!DNL Flow Service] 使您能夠添加、編輯和刪除現有批處理或流連接的詳細資訊，包括其名稱、說明和憑據。

本教程介紹使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本教程要求您具有現有連接和有效的連接ID。 如果沒有現有連接，請從 [源概述](../../home.md) 在嘗試本教程之前，請按照上述步驟操作。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

## 查找連接詳細資訊

更新連接的第一步是使用連接ID檢索其詳細資訊。 要檢索連接的當前詳細資訊，請向 [!DNL Flow Service] 提供要更新的連接的連接ID時的API。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 獨特 `id` 要檢索的連接的值。 |

**要求**

以下請求檢索有關連接的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回連接的當前詳細資訊，包括其憑據、唯一標識符(`id`)和版本。 更新連接需要版本值。

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## 更新連接

要更新連接的名稱、說明和憑據，請向 [!DNL Flow Service] 提供連接ID、版本和要使用的新資訊時的API。

>[!IMPORTANT]
>
>的 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是要更新的連接的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 獨特 `id` 要更新的連接的值。 |

**要求**

以下請求提供了新名稱和說明以及一組新的憑據，以更新您的連接。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| 參數 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新連接所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回連接ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供連接ID。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 後續步驟

通過學完本教程，您已使用 [!DNL Flow Service] API。 有關使用源連接器的詳細資訊，請參見 [源概述](../../home.md)。
