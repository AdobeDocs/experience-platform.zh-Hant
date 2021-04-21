---
keywords: Experience Platform；首頁；熱門主題；Azure資料湖儲存Gen2;azure資料湖儲存；Azure
solution: Experience Platform
title: 使用流式服務API建立Azure資料湖儲存Gen2來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連接至Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure] Data Lake Storage Gen2源連接

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至[!DNL Azure] Data Lake Storage Gen2（以下稱為「ADLS Gen2」）的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功建立ADLS Gen2來源連線。

### 收集必要的認證

要使[!DNL Flow Service]連接到ADLS Gen2，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `url` | 地址URL。 |
| `servicePrincipalId` | 應用程式的用戶端ID。 |
| `servicePrincipalKey` | 應用程式的金鑰。 |
| `tenant` | 包含您應用程式的租用戶資訊。 |

有關這些值的詳細資訊，請參閱[此ADLS Gen2文檔](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個ADLS Gen2帳戶只需要一個連線，因為它可用來建立多個來源連接器，以匯入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

要建立ADLS-Gen2連接，必須在POST請求中提供其唯一連接規範ID。 ADLS-Gen2的連接規範ID為`0ed90a81-07f4-4586-8190-b40eccef1c5a`。

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
| `auth.params.servicePrincipalId` | ADLS Gen2帳戶的服務主體ID。 |
| `auth.params.servicePrincipalKey` | ADLS Gen2帳戶的服務主要金鑰。 |
| `auth.params.tenant` | ADLS Gen2帳戶的租用戶資訊。 |
| `connectionSpec.id` | ADLS Gen2連接規範ID:`0ed90a81-07f4-4586-8190-b40eccef1c5a1`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下個步驟中探索您的雲端儲存空間時，需要此ID。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建立ADLS Gen2連線，並取得唯一ID作為回應內文的一部分。 您可以使用此連線ID來探索使用Flow Service API](../../explore/cloud-storage.md)或[使用Flow Service API](../../cloud-storage-parquet.md)來內嵌Parce資料的雲端儲存空間。[
