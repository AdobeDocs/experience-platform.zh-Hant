---
keywords: Experience Platform；首頁；熱門主題；PayPal連接器；paypal;Paypal
solution: Experience Platform
title: 使用流量服務API建立PayPal基本連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將PayPal連線至Adobe Experience Platform。
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 6b6bd67e70267e81c144c37549b0dcba20534eb6
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL PayPal]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL PayPal]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL PayPal]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL PayPal]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL PayPal]實例的URL。 (預設值：api.sandbox.paypal.com)。 |
| `clientId` | 與您的[!DNL PayPal]應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的[!DNL PayPal]應用程式相關聯的用戶端密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL PayPal]的連接規範ID為：`221c7626-58f6-4eec-8ee2-042b0226f03b` |

有關入門的詳細資訊，請參閱[此PayPal文檔](https://developer.paypal.com/docs/api/overview/#get-credentials)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL PayPal]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL PayPal]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL PayPal]實例的URL。 |
| `auth.params.clientId` | 與您的[!DNL PayPal]實例相關聯的用戶端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL PayPal]實例關聯的客戶端密碼。 |
| `connectionSpec.id` | [!DNL PayPal]連接規範ID:`221c7626-58f6-4eec-8ee2-042b0226f03b`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL PayPal]連線，並取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，同時了解如何使用流量服務API](../../explore/payments.md)探索付款應用程式。[
