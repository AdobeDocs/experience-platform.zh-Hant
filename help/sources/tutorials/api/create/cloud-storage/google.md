---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；google雲端儲存空間；google;Google
solution: Experience Platform
title: 使用流程服務API建立Google雲端儲存基礎連線
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Google雲端儲存空間帳戶。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Google Cloud Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用成功連線至Google雲端儲存空間帳戶 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Google Cloud Storage] 帳戶，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 |
| `secretAccessKey` | 40個字元的base-64編碼字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 |

如需這些值的詳細資訊，請參閱 [Google雲端儲存HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何生成您自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Google Cloud Storage] 驗證憑證作為要求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL Google Cloud Storage]:

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
                "secretAccessKey": "secretAccessKey"
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
| `connectionSpec.id` | 此 [!DNL Google Cloud Storage] 連接規範ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Google Cloud Storage] 已透過API與唯一ID取得連線，並成為回應內文的一部分。 您可將此連線ID用於 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
