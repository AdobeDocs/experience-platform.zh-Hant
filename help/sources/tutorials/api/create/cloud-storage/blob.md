---
title: 使用流量服務API連線Azure Blob儲存至Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# 使用API連線[!DNL Azure Blob Storage]至Experience Platform

閱讀本指南，瞭解如何使用[!DNL Azure Blobg Storage]API[[!DNL Flow Service] 將您的](https://developer.adobe.com/experience-platform-apis/references/flow-service/)帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

### 收集必要的認證

閱讀[[!DNL Azure Blob Storage] 總覽](../../../../connectors/cloud-storage/blob.md#authentication)以取得驗證的相關資訊。

## 將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform {#connect}

請閱讀下列步驟，以瞭解如何將[!DNL Azure Blob Storage]帳戶連線至Experience Platform。

### 建立基礎連線

>[!NOTE]
>
>建立後，您無法變更[!DNL Azure Blob Storage]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

基礎連線會將您的來源連結至Experience Platform，以儲存驗證詳細資料、連線狀態和唯一ID。 使用此ID來瀏覽來源檔案並識別要擷取的特定專案，包括其資料型別和格式。

您可以使用下列驗證型別，將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform：

* **帳戶金鑰驗證**：使用儲存體帳戶的存取金鑰來驗證並連線至您的[!DNL Azure Blob Storage]帳戶。
* **共用存取簽章(SAS)**：使用SAS URI提供您[!DNL Azure Blob Storage]帳戶中資源的委派、有限時間存取權。
* **以服務主體為基礎的驗證**：使用Azure Active Directory (AAD)服務主體（使用者端ID和密碼）來安全地驗證您的Azure Blob儲存帳戶。

**API格式**

```https
POST /connections
```

若要建立基礎連線ID，請對`/connections`端點提出POST要求，並提供您的驗證認證作為要求引數的一部分。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

若要使用帳戶金鑰驗證，請提供您`connectionString`、`container`和`folderPath`的值。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `connectionString` | 您的[!DNL Azure Blob Storage]帳戶的連線字串。 連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`。 |
| `container` | 儲存資料檔的[!DNL Azure Blob Storage]容器名稱。 |
| `folderPath` | 指定容器內檔案所在的路徑。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]來源的連線規格ID。 此ID已固定為： `4c10e202-c428-4796-9208-5f1f5732b1cf`。 |

>[!TAB 共用存取權簽章]

若要使用共用存取權簽章，請提供您`sasUri`、`container`和`folderPath`的值。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `sasUri` | 共用存取簽章URI，您可將其用作連線帳戶的替代驗證型別。 SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`。 |
| `container` | 儲存資料檔的[!DNL Azure Blob Storage]容器名稱。 |
| `folderPath` | 指定容器內檔案所在的路徑。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]來源的連線規格ID。 此ID已固定為： `4c10e202-c428-4796-9208-5f1f5732b1cf`。 |

>[!TAB 以服務主體為基礎的驗證]

若要透過以服務主體為基礎的驗證連線，請提供下列專案的值： `serviceEndpoint`、`servicePrincipalId`、`servicePrincipalKey`、`accountKind`、`tenant`、`container`以及`folderPath`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `serviceEndpoint` | [!DNL Azure Blob Storage]帳戶的端點URL。 通常格式為： `https://{ACCOUNT_NAME}.blob.core.windows.net`。 |
| `servicePrincipalId` | 用於驗證的Azure Active Directory (AAD)服務主體的使用者端/應用程式ID。 |
| `servicePrincipalKey` | 與Azure服務主體關聯的使用者端密碼或密碼。 |
| `accountKind` | [!DNL Azure Blob Storage]帳戶的型別。 通用值包括`StorageV2`、`BlobStorage`或`Storage`。 |
| `tenant` | 註冊服務主體的Azure Active Directory (AAD)租使用者ID。 |
| `container` | 儲存資料檔的[!DNL Azure Blob Storage]容器名稱。 |
| `folderPath` | 指定容器內檔案所在的路徑。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]來源的連線規格ID。 此ID已固定為： `4c10e202-c428-4796-9208-5f1f5732b1cf`。 |

>[!ENDTABS]

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## 後續步驟

依照本教學課程，您已使用API建立[!DNL Blob]連線，且已取得唯一ID作為回應本文的一部分。 您可以使用此連線ID來使用Flow Service API[ ](../../explore/cloud-storage.md)探索雲端儲存空間。
