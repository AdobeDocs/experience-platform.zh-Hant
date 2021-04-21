---
keywords: Experience Platform;home；熱門主題；流服務；更新帳戶
solution: Experience Platform
title: 使用流程服務API更新帳戶
topic-legacy: overview
type: Tutorial
description: 本教學課程涵蓋使用Flow Service API更新帳戶詳細資訊和認證的步驟。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---

# 使用流程服務API更新帳戶

在某些情況下，可能需要更新現有源連接的詳細資訊。 [!DNL Flow Service] 提供您新增、編輯和刪除現有批處理或串流連接詳細資料的能力，包括其名稱、說明和認證。

本教程介紹使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)更新連接的詳細資訊和憑據的步驟。

## 快速入門

本教學課程要求您擁有現有的連線和有效的連線ID。 如果您沒有現有連線，請從[來源概觀](../../home.md)中選擇您的選擇來源，然後依照本教學課程之前概述的步驟進行。

本教學課程還要求您對Adobe Experience Platform的以下部分有切實的瞭解：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功更新連線。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 查找連接詳細資訊

更新連線的第一步是使用連線ID擷取其詳細資訊。 要檢索連接的當前詳細資訊，請在提供要更新的連接的連接ID時向[!DNL Flow Service] API發出GET請求。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要檢索的連接的唯一`id`值。 |

**要求**

下列請求會擷取您連線的相關資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回連線的目前詳細資料，包括其認證、唯一識別碼(`id`)和版本。 更新連線時需要版本值。

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

若要更新連線的名稱、說明和認證，請在提供您的連線ID、版本和您要使用的新資訊時，對[!DNL Flow Service] API執行PATCH要求。

>[!IMPORTANT]
>
>發出PATCH請求時，`If-Match`標題是必需的。 此標題的值是您要更新之連線的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要更新的連接的唯一`id`值。 |

**要求**

以下請求提供新的名稱和說明，以及一組新的認證，以更新您的連線。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | 用於定義更新連接所需操作的操作調用。 運營包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的參數路徑。 |
| `value` | 您要用來更新參數的新值。 |

**回應**

成功的回應會傳回您的連線ID和更新的etag。 您可以在提供連線ID時，向[!DNL Flow Service] API提出GET要求，以驗證更新。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 後續步驟

在本教程中，您已使用[!DNL Flow Service] API更新了與連接相關的憑據和資訊。 有關使用源連接器的詳細資訊，請參閱[源概述](../../home.md)。
