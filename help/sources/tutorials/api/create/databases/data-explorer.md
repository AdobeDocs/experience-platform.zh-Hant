---
keywords: Experience Platform；首頁；熱門主題；AzureData Explorer；資料瀏覽器；Data Explorer
solution: Experience Platform
title: 使用流程服務API建立AzureData Explorer來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將AzureData Explorer連接至Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Data Explorer]來源連線

>[!NOTE]
>
>[!DNL Azure Data Explorer]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Azure Data Explorer](以下稱為「Data Explorer」)連接至[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至[!DNL Data Explorer]。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Data Explorer]連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `endpoint` | [!DNL Data Explorer]伺服器的端點。 |
| `database` | [!DNL Data Explorer]資料庫的名稱。 |
| `tenant` | 用來連線至[!DNL Data Explorer]資料庫的唯一租用戶ID。 |
| `servicePrincipalId` | 用於連接[!DNL Data Explorer]資料庫的唯一服務承擔者ID。 |
| `servicePrincipalKey` | 用於連接[!DNL Data Explorer]資料庫的唯一服務主體密鑰。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL Data Explorer]的連接規範ID為`0479cc14-7651-4354-b233-7480606c2ac3`。 |

有關入門的詳細資訊，請參閱[本Data Explorer文檔](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Data Explorer]帳戶只需一個連接器，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

要建立[!DNL Data Explorer]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Data Explorer]的連接規範ID為`0479cc14-7651-4354-b233-7480606c2ac3`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.endpoint` | [!DNL Data Explorer]伺服器的端點。 |
| `auth.params.database` | [!DNL Data Explorer]資料庫的名稱。 |
| `auth.params.tenant` | 用來連線至[!DNL Data Explorer]資料庫的唯一租用戶ID。 |
| `auth.params.servicePrincipalId` | 用於連接[!DNL Data Explorer]資料庫的唯一服務承擔者ID。 |
| `auth.params.servicePrincipalKey` | 用於連接[!DNL Data Explorer]資料庫的唯一服務主體密鑰。 |
| `connectionSpec.id` | [!DNL Data Explorer]連接規範ID:`0479cc14-7651-4354-b233-7480606c2ac3`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Data Explorer]連接，並獲取了該連接的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使用流服務API](../../explore/database-nosql.md)來探索資料庫。[
