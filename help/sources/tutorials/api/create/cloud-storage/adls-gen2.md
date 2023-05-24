---
keywords: Experience Platform；首頁；熱門主題；Azure資料湖儲存Gen2;azure資料湖儲存；Azure
solution: Experience Platform
title: 使用流服務API建立Azure Data Lake Storage Gen2基本連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# 建立 [!DNL Azure Data Lake Storage Gen2] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Azure Data Lake Storage Gen2] （下稱「ADLS Gen2」）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個平台實例分區到單獨的虛擬環境中，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 要連接到ADLS Gen2，必須提供以下連接屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | ADLS Gen2的終結點。 端點模式為： `https://<accountname>.dfs.core.windows.net`。 |
| `servicePrincipalId` | 應用程式的客戶端ID。 |
| `servicePrincipalKey` | 應用程式的密鑰。 |
| `tenant` | 包含應用程式的租戶資訊。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 ADLS Gen2的連接規範ID為： `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`。 |

有關這些值的詳細資訊，請參閱 [此ADLS第2代文檔](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 端點，同時將ADLS Gen2身份驗證憑據作為請求參數的一部分提供。

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
| `auth.params.url` | ADLS Gen2帳戶的URL終結點。 |
| `auth.params.servicePrincipalId` | ADLS Gen2帳戶的服務主體ID。 |
| `auth.params.servicePrincipalKey` | ADLS Gen2帳戶的服務主密鑰。 |
| `auth.params.tenant` | ADLS Gen2帳戶的租戶資訊。 |
| `connectionSpec.id` | ADLS Gen2連接規範ID: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 後續步驟

按照本教程，您已使用API建立了ADLS Gen2連接，並且作為響應體的一部分獲得了唯一ID。 您可以使用此連接ID [使用流服務API瀏覽雲儲存](../../explore/cloud-storage.md)。
