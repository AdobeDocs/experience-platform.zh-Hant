---
title: 使用流服務API建立Azure Blob基連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# 建立 [!DNL Azure Blob] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Azure Blob] (以下簡稱：[!DNL Blob]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功建立 [!DNL Blob] 源連接使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Blob] 儲存，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 包含驗證所需的授權資訊的字串 [!DNL Blob] Experience Platform。 的 [!DNL Blob] 連接字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有關連接字串的詳細資訊，請參閱 [!DNL Blob] 文檔 [配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)。 |
| `sasUri` | 可用作連接的備用身份驗證類型的共用訪問簽名URI [!DNL Blob] 帳戶。 的 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 有關詳細資訊，請參閱 [!DNL Blob] 文檔 [共用訪問簽名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)。 |
| `container` | 要指定訪問權限的容器的名稱。 使用 [!DNL Blob] 源，您可以提供容器名稱來指定用戶對所選子資料夾的訪問權限。 |
| `folderPath` | 要提供訪問權限的資料夾的路徑。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Blob] 為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

的 [!DNL Blob] 源支援連接字串和共用訪問簽名(SAS)驗證。 共用訪問簽名(SAS)URI允許對您的 [!DNL Blob] 帳戶。 您可以使用SAS建立不同訪問度的身份驗證憑據，因為基於SAS的身份驗證允許您設定權限、開始日期和到期日期以及對特定資源的設定。

在此步驟中，您還可以通過定義容器名稱和子資料夾的路徑來指定帳戶可以訪問的子資料夾。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Blob] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

>[!BEGINTABS]

>[!TAB 連接字串]

以下請求為 [!DNL Blob] 使用基於連接字串的身份驗證：

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
| `auth.params.connectionString` | 訪問Blob儲存中的資料所需的連接字串。 Blob連接字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | Blob儲存連接規範ID為： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!TAB SAS URI身份驗證]

建立 [!DNL Blob] blob連接使用共用訪問簽名URI，向POST請求 [!DNL Flow Service] API，同時為 [!DNL Blob] `sasUri`。

以下請求為 [!DNL Blob] 使用共用訪問簽名URI:

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
| `auth.params.connectionString` | 訪問您的資料所需的SAS URI [!DNL Blob] 儲存。 的 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`。 |
| `connectionSpec.id` | 的 [!DNL Blob] 儲存連接規範ID為： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!ENDTABS]

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Blob] 使用API和唯一ID進行連接，作為響應體的一部分。 您可以使用此連接ID [使用流服務API瀏覽雲儲存](../../explore/cloud-storage.md)。
