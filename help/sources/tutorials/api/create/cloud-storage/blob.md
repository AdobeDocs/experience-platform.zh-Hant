---
keywords: Experience Platform;home；熱門主題；Azure;azure blob;blob;Blob
solution: Experience Platform
title: 使用流服務API建立Azure Blob源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連接至Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Blob]來源連線

本教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)來引導您完成將[!DNL Azure Blob]（以下稱為「Blob」）連接至Adobe Experience Platform的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功建立[!DNL Blob]來源連線。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Blob]儲存設備連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 包含驗證[!DNL Blob]到Experience Platform所需的授權資訊的字串。 [!DNL Blob]連接字串模式是：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有關連接字串的詳細資訊，請參閱[配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)上的[!DNL Blob]文檔。 |
| `sasUri` | 共用訪問簽名URI，可用作連接[!DNL Blob]帳戶的替代驗證類型。 [!DNL Blob] SAS URI模式為：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`如需詳細資訊，請參閱[共用存取簽名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)上的此[!DNL Blob]檔案。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL Blob]的連接規範ID為：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Blob]帳戶只需要一個連接，因為它可用於建立多個資料流以導入不同的資料。

### 使用基於連接字串的驗證建立[!DNL Blob]連接

若要使用以連線字串為基礎的驗證來建立[!DNL Blob]連線，請在提供[!DNL Blob] `connectionString`時，向[!DNL Flow Service] API提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

要建立[!DNL Blob]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Blob]的連接規範ID為`4c10e202-c428-4796-9208-5f1f5732b1cf`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 訪問Blob儲存中的資料所需的連接字串。 Blob連接字串模式是：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | 點滴儲存連接規範ID是：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索您的儲存空間時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### 使用共用訪問簽名URI建立[!DNL Blob]連接

共用訪問簽名(SAS)URI允許對[!DNL Blob]帳戶進行安全委託授權。 您可以使用SAS來建立具有不同存取度的驗證憑證，因為以SAS為基礎的驗證可讓您設定權限、開始和到期日，以及特定資源的規定。

要使用共用訪問簽名URI建立[!DNL Blob]連接，請向[!DNL Flow Service] API發出POST請求，同時為[!DNL Blob] `sasUri`提供值。

**API格式**

```http
POST /connections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 訪問[!DNL Blob]儲存中的資料所需的SAS URI。 [!DNL Blob] SAS URI模式為：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`。 |
| `connectionSpec.id` | [!DNL Blob]儲存連接規範ID為：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索您的儲存空間時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建立[!DNL Blob]連線，並取得唯一ID做為回應內文的一部分。 您可以使用此連線ID來探索使用Flow Service API](../../explore/cloud-storage.md)或[使用Flow Service API](../../cloud-storage-parquet.md)來內嵌Parce資料的雲端儲存空間。[
