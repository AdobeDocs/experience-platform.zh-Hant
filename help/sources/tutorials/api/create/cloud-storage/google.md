---
title: 使用流服務API建立Google雲儲存基連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Google雲儲存帳戶。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Google Cloud Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Google Cloud Storage] 帳戶，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 61個字元的字母數字字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。 |
| `secretAccessKey` | 一個40個字元、基64編碼的字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。 |
| `bucketName` | 您的名稱 [!DNL Google Cloud Storage] 桶。 如果要提供對雲儲存中特定子資料夾的訪問權限，則必須指定儲存段名稱。 |
| `folderPath` | 要提供訪問權限的資料夾的路徑。 |

有關這些值的詳細資訊，請參見 [Google雲儲存HMAC密鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的子菜單。 有關如何生成您自己的訪問密鑰ID和密鑰訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Google Cloud Storage] 身份驗證憑據作為請求參數的一部分。

>[!TIP]
>
>在此步驟中，您還可以通過定義儲存段名稱和子資料夾路徑來指定帳戶可以訪問的子資料夾。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Google Cloud Storage]:

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
| `auth.params.accessKeyId` | 與您的 [!DNL Google Cloud Storage] 帳戶。 |
| `auth.params.secretAccessKey` | 與您的 [!DNL Google Cloud Storage] 帳戶。 |
| `auth.params.bucketName` | 您的名稱 [!DNL Google Cloud Storage] 桶。 如果要提供對雲儲存中特定子資料夾的訪問權限，則必須指定儲存段名稱。 |
| `auth.params.folderPath` | 要提供訪問權限的資料夾的路徑。 |
| `connectionSpec.id` | 的 [!DNL Google Cloud Storage] 連接規範ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽雲儲存資料時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Google Cloud Storage] 使用API和唯一ID進行連接，作為響應體的一部分。 您可以使用此連接ID [使用流服務API瀏覽雲儲存](../../explore/cloud-storage.md)。
