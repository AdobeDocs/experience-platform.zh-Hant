---
keywords: Experience Platform；首頁；熱門主題；Oracle Service Cloud；Oracle Service Cloud
title: 使用流量服務API建立Oracle Service Cloud Source連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Oracle Service Cloud。
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立Oracle Service雲端來源連線

>[!WARNING]
>
>[!DNL Oracle Service Cloud]來源將於2025年6月底淘汰。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步帶您瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為Oracle Service Cloud建立基本連線。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至Oracle Service Cloud。

### 收集必要的認證

若要讓[!DNL Flow Service]連線至Oracle Service Cloud，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | Oracle Service Cloud例項的主機URL。 |
| `username` | 您的Oracle服務雲端使用者帳戶使用者名稱。 |
| `password` | 您的Oracle Service Cloud帳戶密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 Oracle Service Cloud的連線規格ID是： `ba5126ec-c9ac-11eb-b8bc-0242ac130003`。 |

如需驗證您的Oracle Service Cloud帳戶的詳細資訊，請參閱驗證](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html)的[[!DNL Oracle] 指南。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基礎連線ID，請在提供您的Oracle Service Cloud驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

以下請求會建立Oracle Service Cloud的基本連線：

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
| `auth.params.host` | Oracle Service Cloud例項的主機URL。 |
| `auth.params.username` | 與您的Oracle Service Cloud帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與您的Oracle Service Cloud帳戶相關聯的密碼。 |
| `connectionSpec.id` | Oracle服務雲端連線規格識別碼： `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立Oracle Service Cloud基本連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流，將客戶成功資料匯入Experience Platform](../../collect/customer-success.md)
