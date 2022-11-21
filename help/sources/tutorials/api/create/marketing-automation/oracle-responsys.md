---
keywords: Experience Platform；首頁；熱門主題；oracle;
title: （測試版）使用流量服務API建立OracleResponsys Base連線
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至OracleResponsys。
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# （測試版）建立 [!DNL Oracle Responsys] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Oracle Responsys] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Oracle Responsys] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解Platform的下列元件：

* [來源](../../../../home.md):Platform可讓您從各種來源擷取資料，同時能使用來建構、加上標籤，以及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Platform提供可將單一 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Oracle Responsys] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Oracle Responsys]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| --- | --- |
| `endpoint` | 您的 [!DNL Oracle Responsys] 例項。 |
| `clientId` | 您 [!DNL Oracle Responsys] 例項。 |
| `clientSecret` | 您的用戶端密碼 [!DNL Oracle Responsys] 例項。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID的值 [!DNL Oracle Responsys] 來源固定為： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

有關的身份驗證憑據的詳細資訊 [!DNL Oracle Responsys]，請參閱 [[!DNL Oracle Responsys] 驗證指南](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Oracle Responsys] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `name` | 您的 [!DNL Oracle Responsys] 基本連接。 建議您提供描述性名稱，因為您可以使用此值來查詢基本連線。 |
| `description` | （選用）您可包含的屬性，用於提供基礎連線的補充資訊。 |
| `auth.specName` | 用於連接的驗證類型。 |
| `auth.params.endpoint` | 您的 [!DNL Oracle Responsys] 伺服器。 |
| `auth.params.clientId` | 您 [!DNL Oracle Responsys] 例項。 |
| `auth.params.clientSecret` | 您的用戶端密碼 [!DNL Oracle Responsys] 例項。 |
| `connectionSpec.id` | 連接規範ID的值 [!DNL Oracle Responsys] 來源固定為： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**回應**

成功的回應會傳回新建立之基本連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Oracle Responsys] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
