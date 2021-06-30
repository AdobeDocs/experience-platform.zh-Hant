---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；Google雲端儲存空間；Google;Google
solution: Experience Platform
title: 使用流程服務API建立Google雲端儲存基礎連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Google雲端儲存空間帳戶。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Google Cloud Storage]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Google Cloud Storage]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至Google雲端儲存空間帳戶。

### 收集所需憑據

為了使[!DNL Flow Service]與[!DNL Google Cloud Storage]帳戶連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 61個字元的英數字串，用於向Platform驗證[!DNL Google Cloud Storage]帳戶。 |
| `secretAccessKey` | 40個字元的base-64編碼字串，用於向Platform驗證您的[!DNL Google Cloud Storage]帳戶。 |

如需這些值的詳細資訊，請參閱[Google雲端儲存空間HMAC索引鍵](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有關如何生成您自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱[[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Google Cloud Storage]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL Google Cloud Storage]建立基本連接：

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
| `auth.params.accessKeyId` | 與您的[!DNL Google Cloud Storage]帳戶相關聯的存取金鑰ID。 |
| `auth.params.secretAccessKey` | 與[!DNL Google Cloud Storage]帳戶相關聯的秘密訪問密鑰。 |
| `connectionSpec.id` | [!DNL Google Cloud Storage]連接規範ID:`32e8f412-cdf7-464c-9885-78184cb113fd` |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

依照本教學課程，您已使用API建立[!DNL Google Cloud Storage]連線，且在回應內文中已取得唯一ID。 您可以使用此連線ID來使用流量服務API](../../explore/cloud-storage.md)或[使用流量服務API](../../cloud-storage-parquet.md)內嵌Parquet資料，以探索雲儲存空間。[
