---
keywords: Experience Platform；首頁；熱門主題；Azure;azure blob;blob;Blob
solution: Experience Platform
title: 使用流服務API建立Azure Blob基本連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Blob]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Azure Blob]基本連線（以下稱為「[!DNL Blob]」）的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便使用[!DNL Flow Service] API成功建立[!DNL Blob]源連接。

### 收集所需憑據

為了使[!DNL Flow Service]與[!DNL Blob]儲存連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 包含驗證[!DNL Blob]以Experience Platform所需的授權資訊的字串。 [!DNL Blob]連接字串模式為：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有關連接字串的詳細資訊，請參見有關[配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)的此[!DNL Blob]文檔。 |
| `sasUri` | 可用作連接[!DNL Blob]帳戶的替代身份驗證類型的共用訪問簽名URI。 [!DNL Blob] SAS URI模式為：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`有關詳細資訊，請參見有關[共用訪問簽名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)的此[!DNL Blob]文檔。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Blob]的連接規範ID為：`d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Blob]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

### 使用基於連接字串的身份驗證建立[!DNL Blob]基本連接

若要使用連線字串式驗證建立[!DNL Blob]基本連線，請在提供[!DNL Blob] `connectionString`時，向[!DNL Flow Service] API提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

以下請求使用基於連接字串的身份驗證為[!DNL Blob]建立基本連接：

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
| `auth.params.connectionString` | 存取Blob儲存中的資料所需的連線字串。 Blob連線字串模式為：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | Blob儲存連接規範ID為：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### 使用共用訪問簽名URI建立[!DNL Blob]基本連接

共用訪問簽名(SAS)URI允許對[!DNL Blob]帳戶進行安全委派授權。 您可以使用SAS建立具有不同訪問權限的身份驗證憑據，因為基於SAS的身份驗證允許您設定權限、開始日期和到期日，以及對特定資源的調配。

要使用共用訪問簽名URI建立[!DNL Blob] blob連接，請向[!DNL Flow Service] API發出POST請求，同時為[!DNL Blob] `sasUri`提供值。

**API格式**

```http
POST /connections
```

**要求**

以下請求使用共用訪問簽名URI為[!DNL Blob]建立基連接：

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

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 後續步驟

依照本教學課程，您已使用API建立[!DNL Blob]連線，且在回應內文中已取得唯一ID。 您可以使用此連線ID來使用流量服務API](../../explore/cloud-storage.md)或[使用流量服務API](../../cloud-storage-parquet.md)內嵌Parquet資料，以探索雲儲存空間。[
