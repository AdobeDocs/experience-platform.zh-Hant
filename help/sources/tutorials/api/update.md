---
keywords: Experience Platform; home；熱門主題；流服務；更新連接
solution: Experience Platform
title: 使用流服務API更新連接資訊
topic: overview
type: Tutorial
description: 在某些情況下，可能需要更新現有源連接的詳細資訊。 Flow Service API可讓您新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---


# 使用Flow Service API更新連線資訊

在某些情況下，可能需要更新現有源連接的詳細資訊。 [!DNL Flow Service] 提供您新增、編輯和刪除現有批處理或串流連接詳細資料的能力，包括其名稱、說明和認證。

本教程介紹使用[[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)更新現有連接的詳細資訊和憑據的步驟。

## 快速入門

本教學課程要求您必須有有效的連線ID。 如果您沒有有效的連線ID，請從[來源概觀](../../home.md)中選取您選擇的連接器，然後依照本教學課程嘗試前所述的步驟進行。

本教學課程也要求您對Adobe Experience Platform的下列元件有正確的認識：

* [來源](../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功更新連線的資訊。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 查找連接詳細資訊

>[!NOTE]
>本教學課程以[Salesforce來源連接器](../../connectors/crm/salesforce.md)為例，但概述的步驟適用於任何[可用來源連接器](../../home.md)。

更新連線資訊的第一步是使用連線ID擷取連線詳細資訊。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要檢索的連接的唯一`id`值。 |

**請求**

以下內容會擷取您連線ID的相關資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回連線的目前詳細資料，包括其認證、唯一識別碼(`id`)和版本。

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

擁有現有連接ID後，請對[!DNL Flow Service] API執行PATCH請求。

>[!IMPORTANT]
>PATCH請求需要使用`If-Match`標題。 此標題的值是連線的唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要更新的連接的唯一`id`值。 |

**請求**

以下請求提供更新連線的新資訊。

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

成功的回應會傳回您的連線ID和更新的etag。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 查找更新的連接詳細資訊

您可以擷取您更新的相同連線ID，以便透過對[!DNL Flow Service] API提出GET要求來查看您所做的變更。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 要檢索的連接的唯一`id`值。 |

**請求**

下列請求會擷取有關您連線ID的更新資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您連線ID的更新詳細資訊，包括其新名稱、說明和版本。

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1598038319627,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "Test salesforce connection",
            "description": "A test salesforce connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{NEW_SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "salesforce-connector-username"
                }
            },
            "version": "\"3600e378-0000-0200-0000-5f40212f0000\"",
            "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
        }
    ]
}
```

## 後續步驟

在本教程中，您已使用[!DNL Flow Service] API更新了與連接相關的憑據和資訊。 有關使用源連接器的詳細資訊，請參閱[源概述](../../home.md)。
