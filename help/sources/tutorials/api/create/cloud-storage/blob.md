---
title: 使用流程服務API建立Azure Blob基本連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure Blob]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程提供使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Azure Blob] （以下稱為「[!DNL Blob]」）建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功建立[!DNL Blob]來源連線。

### 收集必要的認證

為了讓[!DNL Flow Service]與您的[!DNL Blob]儲存裝置連線，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 連線字串驗證]

| 認證 | 說明 |
| --- | --- |
| `connectionString` | 字串，其中包含驗證[!DNL Blob]給Experience Platform所需的授權資訊。 [!DNL Blob]連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 如需有關連線字串的詳細資訊，請參閱[設定連線字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)上的此[!DNL Blob]檔案。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Blob]的連線規格識別碼為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

>[!TAB SAS URI驗證]

| 認證 | 說明 |
| --- | --- |
| `sasUri` | 共用存取簽章URI，可做為連線您的[!DNL Blob]帳戶的替代驗證型別。 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`如需詳細資訊，請參閱[共用存取簽章URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)上的此[!DNL Blob]檔案。 |
| `container` | 您要指定存取權的容器名稱。 使用[!DNL Blob]來源建立新帳戶時，您可以提供容器名稱，以指定使用者對您所選子資料夾的存取權。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Blob]的連線規格識別碼為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

>[!ENDTABS]

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

>[!TIP]
>
>建立後，您無法變更[!DNL Blob]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

[!DNL Blob]來源同時支援連線字串和共用存取簽章(SAS)驗證。 共用存取簽章(SAS) URI允許將安全授權委派給您的[!DNL Blob]帳戶。 您可以使用SAS建立具有不同存取許可權的驗證認證，因為以SAS為基礎的驗證可讓您設定許可權、開始和到期日期，以及配置給特定資源。

在此步驟中，您還可以透過定義容器名稱和子資料夾的路徑，指定您的帳戶將可以存取的子資料夾。

若要建立基底連線ID，請在提供您的[!DNL Blob]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

>[!BEGINTABS]

>[!TAB 連線字串]

下列要求會使用連線字串式驗證來建立[!DNL Blob]的基礎連線：

+++要求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
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

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 存取Blob儲存體中的資料所需的連線字串。 Blob連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | Blob儲存體連線規格識別碼為： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++回應

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB SAS URI驗證]

若要使用共用存取簽章URI來建立[!DNL Blob]連線，請對[!DNL Flow Service] API發出POST要求，同時為您的[!DNL Blob] `sasUri`提供值。

+++要求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
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

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 存取[!DNL Blob]存放區中的資料所需的SAS URI。 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`。 |
| `connectionSpec.id` | [!DNL Blob]儲存體連線規格識別碼為： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++回應

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## 後續步驟

依照本教學課程，您已使用API建立[!DNL Blob]連線，且已取得唯一ID作為回應本文的一部分。 您可以使用此連線ID來使用Flow Service API[&#128279;](../../explore/cloud-storage.md) 探索雲端儲存空間。
