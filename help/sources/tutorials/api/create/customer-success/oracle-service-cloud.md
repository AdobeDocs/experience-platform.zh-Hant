---
keywords: Experience Platform；首頁；熱門主題；Oracle服務雲端；oracle服務雲端
title: 使用流程服務API建立Oracle服務雲端來源連線
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Oracle服務雲端。
source-git-commit: 078a266967cd7b0818f958283a58a8af4c886a21
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# （測試版）使用建立Oracle服務雲端來源連線 [!DNL Flow Service] API

>[!NOTE]
>
>oracle服務雲端來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成使用以下步驟，為Oracle服務雲建立基本連線： [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用成功連線至Oracle服務雲端 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 若要與Oracle服務雲端連線，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 您的Oracle服務雲例項的主機URL。 |
| `username` | 您的Oracle服務雲端使用者帳戶的使用者名稱。 |
| `password` | 您的Oracle服務雲端帳戶的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 oracle服務雲的連接規範ID為： `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

如需驗證Oracle服務雲端帳戶的詳細資訊，請參閱 [[!DNL Oracle] 驗證指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點，同時提供您的Oracle服務雲端驗證憑證，作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求會為Analytics Service Cloud建立基礎連線：Oracle服務雲端

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 您的Oracle服務雲例項的主機URL。 |
| `auth.params.username` | 與您的Oracle服務雲端帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與您的Oracle服務雲端帳戶相關聯的密碼。 |
| `connectionSpec.id` | oracle服務雲連接規範ID: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

依照本教學課程，您已使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/customer-success.md)
