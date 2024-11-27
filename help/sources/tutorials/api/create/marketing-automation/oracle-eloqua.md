---
title: 使用流程服務API建立OracleEloqua基本連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連結至Oracle Eloqua。
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Oracle Eloqua]基本連線

>[!WARNING]
>
>[!DNL Oracle Eloqua]來源將於2025年6月底淘汰。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Oracle Eloqua]建立基礎連線的步驟。

## 快速入門

本指南需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)： Platform允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Platform提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Oracle Eloqua]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Oracle Eloqua]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| `endpoint` | [!DNL Oracle Eloqua]的端點。 |
| `username` | 您[!DNL Oracle Eloqua]帳戶的使用者名稱。 使用者名稱必須格式化為`siteName + \\ + username`，其中`siteName`是您用來登入[!DNL Oracle Eloqua]的公司名稱，`username`是您的使用者名稱。 例如，您的登入使用者名稱可以是： `adobe\\emily`。 |
| `password` | 與您的[!DNL Oracle Eloqua]使用者名稱對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Oracle Eloqua]來源的連線規格識別碼值固定為： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`。 |

如需[!DNL Oracle Eloqua]的驗證認證詳細資訊，請參閱驗證](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)的[[!DNL Oracle Eloqua] 指南。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Oracle Eloqua]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Oracle Eloqua]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `name` | [!DNL Oracle Eloqua]基本連線的名稱。 建議您提供描述性名稱，因為您可以使用此值來查詢基礎連線。 |
| `description` | （選擇性）您可以納入的屬性，以提供基礎連線的補充資訊。 |
| `auth.specName` | 用於連線的驗證型別。 |
| `auth.params.endpoint` | [!DNL Oracle Eloqua]伺服器的端點。 |
| `auth.params.username` | 包含與您[!DNL Oracle Eloqua]帳戶對應的網站名稱和使用者名稱的串連認證。 |
| `auth.params.password` | 與您的[!DNL Oracle Eloqua]帳戶對應的密碼。 |
| `connectionSpec.id` | [!DNL Oracle Eloqua]來源的連線規格識別碼值固定為： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Oracle Eloqua]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將行銷自動化資料帶入Platform](../../collect/marketing-automation.md)
