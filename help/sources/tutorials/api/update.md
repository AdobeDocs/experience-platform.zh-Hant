---
title: 使用流程服務API更新帳戶
description: 本教學課程涵蓋使用Flow Service API更新帳戶詳細資訊和認證的步驟。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---

# 使用流程服務API更新帳戶

在某些情況下，可能需要更新現有基礎連線的詳細資料。 [!DNL Flow Service]可讓您新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。

本教學課程涵蓋使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新連線的詳細資訊和認證的步驟。

>[!TIP]
>
>當需要更新時，您不需要建立新的基礎連線。 您對基本連線所做的任何變更都會反映在關聯的資料流中。

## 快速入門

本教學課程需要您具備現有的連線和有效的連線ID。 如果您沒有現有的連線，請從[來源概觀](../../home.md)中選取您選擇的來源，並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../landing/api-guide.md)指南。

## 查詢連線詳細資料

更新連線的第一個步驟是使用連線ID擷取其詳細資訊。 若要擷取您連線的目前詳細資料，請在提供您要更新的連線的連線ID時，向[!DNL Flow Service] API提出GET要求。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您要擷取的連線的唯一`id`值。 |

**要求**

以下請求會擷取有關您連線的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您連線的目前詳細資料，包括其認證、唯一識別碼(`id`)和版本。 更新您的連線需要版本值。

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

## 更新連線

若要更新連線的名稱、說明和認證，請對[!DNL Flow Service] API執行PATCH要求，同時提供您的連線ID、版本以及您要使用的新資訊。

>[!IMPORTANT]
>
>發出PATCH請求時需要`If-Match`標頭。 此標頭的值是您要更新之連線的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您要更新的連線的唯一`id`值。 |

**要求**

以下請求提供新的名稱和說明，以及一組新的認證，用於更新您的連線。

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
| `op` | 用於定義更新連線所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 要更新之引數的路徑。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您的連線ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的連線ID。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 後續步驟

依照本教學課程，您已更新使用[!DNL Flow Service] API與您連線相關聯的認證和資訊。 如需使用來源聯結器的詳細資訊，請參閱[來源概觀](../../home.md)。
