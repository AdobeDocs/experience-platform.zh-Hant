---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2；azure data Lake儲存；Azure
solution: Experience Platform
title: 使用流量服務API建立Azure Data Lake Storage Gen2基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Data Lake Storage Gen2]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Azure Data Lake Storage Gen2] （以下稱為「ADLS Gen2」）建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一Experience Platform執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功建立ADLS Gen2來源連線。

### 收集必要的認證

為了讓[!DNL Flow Service]連線到ADLS Gen2，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端點。 端點模式為： `https://<accountname>.dfs.core.windows.net`。 |
| `servicePrincipalId` | 應用程式的使用者端ID。 |
| `servicePrincipalKey` | 應用程式的索引鍵。 |
| `tenant` | 包含您應用程式的租使用者資訊。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 ADLS Gen2的連線規格識別碼為： `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`。 |

如需這些值的詳細資訊，請參閱此ADLS Gen2檔案[&#128279;](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基礎連線ID，請在提供ADLS Gen2驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立ADLS Gen2的基本連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.url` | ADLS Gen2帳戶的URL端點。 |
| `auth.params.servicePrincipalId` | 您的ADLS Gen2帳戶的服務主體ID。 |
| `auth.params.servicePrincipalKey` | ADLS Gen2帳戶的服務主體金鑰。 |
| `auth.params.tenant` | 您ADLS Gen2帳戶的租使用者資訊。 |
| `connectionSpec.id` | ADLS Gen2連線規格識別碼： `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 後續步驟

依照本教學課程所述，您已使用API建立ADLS Gen2連線，且已取得唯一ID作為回應本文的一部分。 您可以使用此連線ID來使用Flow Service API[&#128279;](../../explore/cloud-storage.md) 探索雲端儲存空間。
