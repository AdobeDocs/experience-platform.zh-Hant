---
keywords: Experience Platform；首頁；熱門主題；Shopify;shopify；電子商務
solution: Experience Platform
title: 使用流量服務API建立Shopify連接器基本連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Shopify連線至Adobe Experience Platform。
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Shopify]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)建立[!DNL Shopify]基本連線（以下稱為「[!DNL Shopify]」）的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Sources]](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Shopify]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Shopify]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Shopify]伺服器的端點。 |
| `accessToken` | [!DNL Shopify]使用者帳戶的存取權杖。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Shopify]的連接規範ID為：`4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

有關入門的詳細資訊，請參閱此[Shopify authentication document](https://shopify.dev/concepts/about-apis/authentication)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Shopify]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL Shopify]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Shopify]伺服器的端點。 |
| `auth.params.accessToken` | [!DNL Shopify]使用者帳戶的存取權杖。 |
| `connectionSpec.id` | [!DNL Shopify]連接規範ID:`4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Shopify]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/ecommerce.md)探索電子商務連線時，您可以在下一個教學課程中使用此ID。[
