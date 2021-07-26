---
keywords: Experience Platform；首頁；熱門主題；salesforce marketing cloud;SalesforceMarketing Cloud
solution: Experience Platform
title: 使用流服務API建立SalesforceMarketing Cloud基礎連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至SalesforceMarketing Cloud。
source-git-commit: 56458ed6e74a76e2787ab3b9f1409b11556bdee2
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Salesforce Marketing Cloud]基本連線

>[!NOTE]
>
>[!DNL Salesforce Marketing Cloud]源位於測試版。 有關使用測試版標籤的來源的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Salesforce Marketing Cloud]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

以下章節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Salesforce Marketing Cloud]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Salesforce Marketing Cloud]連接，必須提供以下連接屬性：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子網域。 |
| `clientId` | 與您的[!DNL Salesforce Marketing Cloud]應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的[!DNL Salesforce Marketing Cloud]應用程式相關聯的用戶端密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Salesforce Marketing Cloud]的連接規範ID為：`cea1c2a08-b722-11eb-8529-0242ac130003`。 |

有關入門的詳細資訊，請參閱此[[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Salesforce Marketing Cloud]驗證憑證作為要求內文的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

以下請求為[!DNL Salesforce Marketing Cloud]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的[!DNL Salesforce Marketing Cloud]應用程式相關聯的用戶端ID。 |
| `auth.params.clientSecret` | 與您的[!DNL Salesforce Marketing Cloud]應用程式相關聯的用戶端密碼。 |
| `connectionSpec.id` | [!DNL Salesforce Marketing Cloud]連接規範ID:`cea1c2a08-b722-11eb-8529-0242ac130003`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Salesforce Marketing Cloud]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/marketing-automation.md)探索行銷自動化系統時，您可以在下一個教學課程中使用此連線ID。[
