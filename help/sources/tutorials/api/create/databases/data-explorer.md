---
keywords: Experience Platform；首頁；熱門主題；Azure AzureData Explorer;AzureData Explorer;AzureData Explorer
solution: Experience Platform
title: 使用流服務API建立Azure AzureData Explorer基礎連接
type: Tutorial
description: 了解如何使用流程服務API將Azure AzureData Explorer連線至Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 建立 [!DNL Azure Azure Data Explorer] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Azure Data Explorer] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Azure Data Explorer] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Azure Data Explorer]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | 的端點 [!DNL Azure Data Explorer] 伺服器。 |
| `database` | 的名稱 [!DNL Azure Data Explorer] 資料庫。 |
| `tenant` | 用來連線至的不重複租用戶ID [!DNL Azure Data Explorer] 資料庫。 |
| `servicePrincipalId` | 用於連接到的唯一服務主體ID [!DNL Azure Data Explorer] 資料庫。 |
| `servicePrincipalKey` | 用於連接到的唯一服務主體密鑰 [!DNL Azure Data Explorer] 資料庫。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Azure Data Explorer] is `0479cc14-7651-4354-b233-7480606c2ac3`. |

如需快速入門的詳細資訊，請參閱 [[!DNL Azure Data Explorer] 檔案](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Azure Data Explorer] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
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
| `auth.params.endpoint` | 的端點 [!DNL Azure Data Explorer] 伺服器。 |
| `auth.params.database` | 的名稱 [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.tenant` | 用來連線至的不重複租用戶ID [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.servicePrincipalId` | 用於連接到的唯一服務主體ID [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.servicePrincipalKey` | 用於連接到的唯一服務主體密鑰 [!DNL Azure Data Explorer] 資料庫。 |
| `connectionSpec.id` | 此 [!DNL Azure Data Explorer] 連接規範ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Azure Data Explorer] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
