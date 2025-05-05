---
title: 使用流量服務API建立Google Cloud Storage基本連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Google雲端儲存空間帳戶。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL Google Cloud Storage]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Google Cloud Storage]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至Google雲端儲存空間帳戶。

### 收集必要的認證

為了讓[!DNL Flow Service]與您的[!DNL Google Cloud Storage]帳戶連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 61個字元的英數字串，用於向Experience Platform驗證您的[!DNL Google Cloud Storage]帳戶。 |
| `secretAccessKey` | 用於向Experience Platform驗證您的[!DNL Google Cloud Storage]帳戶的40個字元Base-64編碼字串。 |
| `bucketName` | 您的[!DNL Google Cloud Storage]儲存貯體的名稱。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，您必須指定儲存貯體名稱。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 |

如需這些值的詳細資訊，請參閱[Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 如需如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱[[!DNL Google Cloud Storage] 概觀](../../../../connectors/cloud-storage/google-cloud-storage.md)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Google Cloud Storage]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

>[!TIP]
>
>在此步驟中，您也可以定義貯體名稱和子資料夾的路徑，以指定您的帳戶將可以存取的子資料夾。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL Google Cloud Storage]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 與您的[!DNL Google Cloud Storage]帳戶關聯的存取金鑰識別碼。 |
| `auth.params.secretAccessKey` | 與您的[!DNL Google Cloud Storage]帳戶相關聯的秘密存取金鑰。 |
| `auth.params.bucketName` | 您的[!DNL Google Cloud Storage]儲存貯體的名稱。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，您必須指定儲存貯體名稱。 |
| `auth.params.folderPath` | 您要提供存取權的資料夾路徑。 |
| `connectionSpec.id` | [!DNL Google Cloud Storage]連線規格識別碼： `32e8f412-cdf7-464c-9885-78184cb113fd` |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中，探索您的雲端儲存空間資料需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

依照本教學課程，您已使用API建立[!DNL Google Cloud Storage]連線，且已取得唯一ID作為回應本文的一部分。 您可以使用此連線ID來使用Flow Service API[&#128279;](../../explore/cloud-storage.md) 探索雲端儲存空間。
