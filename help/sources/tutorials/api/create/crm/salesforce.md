---
keywords: Experience Platform；首頁；熱門主題；Salesforce；salesforce
solution: Experience Platform
title: 使用流量服務API建立Salesforce基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Salesforce帳戶。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 27ad8812137502d0a636345852f0cae5d01c7b23
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 4%

---

# 建立 [!DNL Salesforce] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Salesforce] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用以下專案來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Platform] 至 [!DNL Salesforce] 帳戶使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線到 [!DNL Salesforce]，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | 的URL [!DNL Salesforce] 來源執行個體。 |
| `username` | 的使用者名稱 [!DNL Salesforce] 使用者帳戶。 |
| `password` | 的密碼 [!DNL Salesforce] 使用者帳戶。 |
| `securityToken` | 的安全性權杖 [!DNL Salesforce] 使用者帳戶。 |
| `apiVersion` | 選用)的REST API版本 [!DNL Salesforce] 您正在使用的例項。 API版本值必須使用小數點格式化。 例如，如果您使用API版本 `52`，則您必須輸入值為 `52.0` 如果此欄位留空，則Experience Platform將自動使用最新可用版本。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Salesforce] 為： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

如需開始使用的詳細資訊，請造訪 [此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，並提供您的 [!DNL Salesforce] 要求內文中的驗證認證。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立 [!DNL Salesforce]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Connection",
      "description": "Connection for Salesforce account",
      "auth": {
          "specName": "Basic Authentication",
          "params": {****
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Salesforce] 帳戶。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Salesforce] 帳戶。 |
| `auth.params.securityToken` | 與您的關聯的安全性權杖 [!DNL Salesforce] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Salesforce] 連線規格ID： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Salesforce] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以將CRM資料帶入Platform，使用 [!DNL Flow Service] API](../../collect/crm.md)
