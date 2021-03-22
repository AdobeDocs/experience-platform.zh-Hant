---
keywords: Experience Platform;home；熱門主題；Google雲端儲存；google雲端儲存；google;Google
solution: Experience Platform
title: 使用流程服務API建立Google雲端儲存來源連線
topic: 概述
type: 教學課程
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連接至Google雲端儲存空間帳戶。
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API建立[!DNL Google Cloud Storage]來源連線

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至[!DNL Google Cloud Storage]帳戶的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下章節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至Google雲端儲存空間帳戶。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Google Cloud Storage]帳戶連接，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| 存取金鑰ID | 用於向平台驗證[!DNL Google Cloud Storage]帳戶的61個字元英數字串。 |
| 機密存取金鑰 | 40個字元、基本64編碼的字串，用於向平台驗證您的[!DNL Google Cloud Storage]帳戶。 |

如需這些值的詳細資訊，請參閱[ Google Cloud Storage HMAC金鑰指南。 ](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)有關如何生成自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱[[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md)。

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

連接指定源，並包含該源的憑據。 每個[!DNL Google Cloud Storage]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立[!DNL Google Cloud Storage]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Google Cloud Storage]的連接規範ID為`32e8f412-cdf7-464c-9885-78184cb113fd`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.accessKeyId` | 與[!DNL Google Cloud Storage]帳戶關聯的存取金鑰ID。 |
| `auth.params.secretAccessKey` | 與[!DNL Google Cloud Storage]帳戶關聯的機密存取金鑰。 |
| `connectionSpec.id` | [!DNL Google Cloud Storage]連接規範ID:`32e8f412-cdf7-464c-9885-78184cb113fd` |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建立[!DNL Google Cloud Storage]連線，並取得唯一ID做為回應內文的一部分。 您可以使用此連線ID來探索使用Flow Service API](../../explore/cloud-storage.md)或[使用Flow Service API](../../cloud-storage-parquet.md)來內嵌Parce資料的雲端儲存空間。[