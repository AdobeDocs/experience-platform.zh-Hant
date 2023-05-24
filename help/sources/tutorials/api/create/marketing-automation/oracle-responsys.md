---
keywords: Experience Platform；首頁；熱門主題；oracle;
title: (Beta)使用流服務API建立Oracle響應系統基連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Oracle響應系統。
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# (Beta)建立 [!DNL Oracle Responsys] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Oracle Responsys] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Oracle Responsys] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對平台的以下元件有良好的理解：

* [源](../../../../home.md):平台允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):平台提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接到所需的其他資訊 [!DNL Oracle Responsys] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Oracle Responsys]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| --- | --- |
| `endpoint` | 您的REST身份驗證終結點URL [!DNL Oracle Responsys] 實例。 |
| `clientId` | 您的客戶端ID [!DNL Oracle Responsys] 實例。 |
| `clientSecret` | 你的客戶機密碼 [!DNL Oracle Responsys] 實例。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID的值 [!DNL Oracle Responsys] 源固定為： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`。 |

有關的身份驗證憑據的詳細資訊 [!DNL Oracle Responsys]，請參見 [[!DNL Oracle Responsys] 認證指南](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Oracle Responsys] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Oracle Responsys]:

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
| `name` | 您的名稱 [!DNL Oracle Responsys] 基本連接。 建議提供描述性名稱，因為您可以使用此值查找基本連接。 |
| `description` | （可選）可包含的屬性，用於提供有關基本連接的補充資訊。 |
| `auth.specName` | 用於連接的驗證類型。 |
| `auth.params.endpoint` | 您的REST身份驗證終結點URL [!DNL Oracle Responsys] 伺服器。 |
| `auth.params.clientId` | 您的客戶端ID [!DNL Oracle Responsys] 實例。 |
| `auth.params.clientSecret` | 你的客戶機密碼 [!DNL Oracle Responsys] 實例。 |
| `connectionSpec.id` | 連接規範ID的值 [!DNL Oracle Responsys] 源固定為： `ff4274f2-c9a9-11eb-b8bc-0242ac130003`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Oracle Responsys] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)
