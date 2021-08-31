---
keywords: Experience Platform；首頁；熱門主題；Azure資料湖儲存Gen2;azure資料湖儲存；Azure
solution: Experience Platform
title: 使用流服務API建立Azure Data Lake Storage Gen2基本連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Data Lake Storage Gen2]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Azure Data Lake Storage Gen2]建立基本連線（以下稱為「ADLS Gen2」）的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便使用[!DNL Flow Service] API成功建立ADLS Gen2源連接。

### 收集所需憑據

為了使[!DNL Flow Service]連接到ADLS Gen2，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端點。 端點模式為：`https://<accountname>.dfs.core.windows.net`。 |
| `servicePrincipalId` | 應用程式的用戶端ID。 |
| `servicePrincipalKey` | 應用程式的密鑰。 |
| `tenant` | 包含您應用程式的租用戶資訊。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 ADLS Gen2的連接規範ID為：`0ed90a81-07f4-4586-8190-b40eccef1c5a`。 |

如需這些值的詳細資訊，請參閱[此ADLS Gen2檔案](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供ADLS Gen2驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為ADLS Gen2建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.url` | ADLS Gen2帳戶的URL端點。 |
| `auth.params.servicePrincipalId` | 您ADLS Gen2帳戶的服務主體ID。 |
| `auth.params.servicePrincipalKey` | ADLS Gen2帳戶的服務主體密鑰。 |
| `auth.params.tenant` | ADLS Gen2帳戶的租用戶資訊。 |
| `connectionSpec.id` | ADLS Gen2連接規範ID:`0ed90a81-07f4-4586-8190-b40eccef1c5a1`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 後續步驟

依照本教學課程，您已使用API建立ADLS Gen2連線，且在回應內文中已取得唯一ID。 您可以使用此連線ID來使用流量服務API](../../explore/cloud-storage.md)或[使用流量服務API](../../cloud-storage-parquet.md)內嵌Parquet資料，以探索雲儲存空間。[
