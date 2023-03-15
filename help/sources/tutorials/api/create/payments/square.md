---
keywords: Experience Platform；首頁；熱門主題；方塊；方塊
title: 使用流量服務API建立方形基連接
description: 了解如何使用Flow Service API將Square連線至Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 建立 [!DNL Square] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Square] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Square] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Square]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| --- | --- |
| `host` | 的URL [!DNL Square] 例項。 |
| `clientId` | 與您的 [!DNL Square] 帳戶。 |
| `clientSecret` | 與您的 [!DNL Square] 帳戶。 |
| `accessToken` | 存取權杖可用來驗證您的 [!DNL Square] 帳戶（驗證OAuth 2.0）。 存取權杖可從 [!DNL Square]. |
| `refreshToken` | 當您目前的存取權杖過期時，會使用重新整理權杖來產生新的存取權杖。 可從取得重新整理代號 [!DNL Square]. |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Square] 為： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

如需這些憑證以及如何取得的詳細資訊，請參閱 [[!DNL Square] OAuth相關檔案](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Square] 驗證憑證作為要求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 的URL [!DNL Square] 例項。 |
| `auth.params.clientId` | 與您的 [!DNL Square] 帳戶。 |
| `auth.params.clientSecret` | 與您的 [!DNL Square] 帳戶。 |
| `auth.params.accessToken` | 存取權杖可用來驗證您的 [!DNL Square] 帳戶（驗證OAuth 2.0）。 存取權杖可從 [!DNL Square]. |
| `auth.params.refreshToken` | 當您目前的存取權杖過期時，會使用重新整理權杖來產生新的存取權杖。 可從取得重新整理代號 [!DNL Square]. |
| `connectionSpec.id` | 此 [!DNL Square] 連接規範ID: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**回應**

成功的回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Square] 使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何 [使用Flow Service API探索支付應用程式](../../explore/payments.md).
