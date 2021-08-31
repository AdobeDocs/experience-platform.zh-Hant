---
keywords: Experience Platform；首頁；熱門主題；Azure AzureData Explorer;AzureData Explorer;AzureData Explorer
solution: Experience Platform
title: 使用流服務API建立Azure AzureData Explorer基礎連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流程服務API將Azure AzureData Explorer連線至Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Azure Data Explorer]基本連線

>[!NOTE]
>
>[!DNL Azure Azure Data Explorer]連接器為測試版。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Azure Data Explore]基本連線的步驟。


## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Azure Data Explorer]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Azure Data Explorer]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | [!DNL Azure Data Explorer]伺服器的端點。 |
| `database` | [!DNL Azure Data Explorer]資料庫的名稱。 |
| `tenant` | 用於連接到[!DNL Azure Data Explorer]資料庫的唯一租戶ID。 |
| `servicePrincipalId` | 用於連接到[!DNL Azure Data Explorer]資料庫的唯一服務主體ID。 |
| `servicePrincipalKey` | 用於連接到[!DNL Azure Data Explorer]資料庫的唯一服務主體密鑰。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Azure Data Explorer]的連接規範ID為`0479cc14-7651-4354-b233-7480606c2ac3`。 |

有關入門的詳細資訊，請參閱此[[!DNL Azure Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Azure Data Explorer]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Azure Data Explorer]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.endpoint` | [!DNL Azure Data Explorer]伺服器的端點。 |
| `auth.params.database` | [!DNL Azure Data Explorer]資料庫的名稱。 |
| `auth.params.tenant` | 用於連接到[!DNL Azure Data Explorer]資料庫的唯一租戶ID。 |
| `auth.params.servicePrincipalId` | 用於連接到[!DNL Azure Data Explorer]資料庫的唯一服務主體ID。 |
| `auth.params.servicePrincipalKey` | 用於連接到[!DNL Azure Data Explorer]資料庫的唯一服務主體密鑰。 |
| `connectionSpec.id` | [!DNL Azure Data Explorer]連接規範ID:`0479cc14-7651-4354-b233-7480606c2ac3`。 |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Azure Data Explorer]連線，並取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何使用流量服務API](../../explore/database-nosql.md)探索資料庫。[
