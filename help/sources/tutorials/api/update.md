---
keywords: Experience Platform；首頁；熱門主題；流量服務；更新帳戶
solution: Experience Platform
title: 使用流量服務API更新帳戶
topic-legacy: overview
type: Tutorial
description: 本教學課程涵蓋使用流量服務API更新帳戶詳細資訊和憑證的步驟。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 2%

---

# 使用流量服務API更新帳戶

在某些情況下，可能需要更新現有源連接的詳細資訊。 [!DNL Flow Service] 可讓您新增、編輯和刪除現有批次或串流連線的詳細資訊，包括其名稱、說明和憑證。

本教學課程涵蓋使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新連線的詳細資訊和憑證的步驟。

## 快速入門

本教學課程要求您具備現有連線和有效的連線ID。 如果您沒有現有連接，請從[sources overview](../../home.md)中選擇您的選擇源，並遵循在嘗試本教程之前概述的步驟。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功更新連接。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的區段。

### 收集必要標題的值

若要呼叫Platform API，您必須先完成[authentication教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有資源，包括屬於[!DNL Flow Service]的資源，都會隔離至特定虛擬沙箱。 對Platform API提出的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 查找連接詳細資訊

更新連線的第一步，是使用連線ID擷取其詳細資訊。 若要擷取連線的目前詳細資料，請在提供您要更新之連線的連線ID時，向[!DNL Flow Service] API提出GET要求。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要檢索的連接的唯一`id`值。 |

**要求**

下列要求會擷取您連線的相關資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回連接的當前詳細資訊，包括其憑據、唯一標識符(`id`)和版本。 更新連線需要版本值。

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

若要更新連線的名稱、說明和憑證，請對[!DNL Flow Service] API執行PATCH請求，同時提供您的連線ID、版本，以及您要使用的新資訊。

>[!IMPORTANT]
>
>提出PATCH請求時需要`If-Match`標題。 此標題的值是您要更新的連線的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要更新的連接的唯一`id`值。 |

**要求**

以下請求會提供新名稱和說明，以及一組新的憑證，以更新您的連線。

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
| `op` | 用來定義更新連線所需動作的操作呼叫。 操作包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回連線ID和更新的etag。 您可以在提供連線ID時，向[!DNL Flow Service] API提出GET要求，以驗證更新。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API更新與連線相關聯的認證和資訊。 有關使用源連接器的詳細資訊，請參閱[源概述](../../home.md)。
