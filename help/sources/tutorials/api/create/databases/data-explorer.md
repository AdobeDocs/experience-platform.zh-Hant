---
keywords: Experience Platform；首頁；熱門主題；Azure AzureData Explorer;AzureData Explorer;AzureData Explorer
solution: Experience Platform
title: 使用流服務API建立Azure AzureData Explorer基連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將AzureData Explorer連接到Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 1e2644b7d83a0bcb7175f27d7c4859c0efba4060
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 建立 [!DNL Azure Azure Data Explorer] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Azure Data Explorer] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。


## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Azure Data Explorer] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Azure Data Explorer]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | 的端點 [!DNL Azure Data Explorer] 伺服器。 |
| `database` | 名稱 [!DNL Azure Data Explorer] 資料庫。 |
| `tenant` | 用於連接到的唯一租戶ID [!DNL Azure Data Explorer] 資料庫。 |
| `servicePrincipalId` | 用於連接到的唯一服務主體ID [!DNL Azure Data Explorer] 資料庫。 |
| `servicePrincipalKey` | 用於連接到的唯一服務主體密鑰 [!DNL Azure Data Explorer] 資料庫。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Azure Data Explorer] 是 `0479cc14-7651-4354-b233-7480606c2ac3`。 |

有關入門的詳細資訊，請參閱此 [[!DNL Azure Data Explorer] 文檔](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Azure Data Explorer] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Azure Data Explorer]:

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
| `auth.params.database` | 名稱 [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.tenant` | 用於連接到的唯一租戶ID [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.servicePrincipalId` | 用於連接到的唯一服務主體ID [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.servicePrincipalKey` | 用於連接到的唯一服務主體密鑰 [!DNL Azure Data Explorer] 資料庫。 |
| `connectionSpec.id` | 的 [!DNL Azure Data Explorer] 連接規範ID: `0479cc14-7651-4354-b233-7480606c2ac3`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Azure Data Explorer] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
