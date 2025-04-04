---
title: 使用Flow Service API建立PathFactory基本連線
description: 瞭解如何使用流量服務API針對Experience Platform驗證您的PathFactory帳戶。
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL PathFactory]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

閱讀本檔案以瞭解如何使用[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)為[!DNL PathFactory]建立基礎連線。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

以下章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL PathFactory]。

### 收集必要的認證 {#gather-credentials}

若要在Experience Platform上存取PathFactory帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| 使用者名稱 | 您的[!DNL PathFactory]帳戶使用者名稱。 這對於在系統中識別您的帳戶至關重要。 |
| 密碼 | 與您的[!DNL PathFactory]帳戶關聯的密碼。 請確定此功能安全無虞，以防止未經授權的存取。 |
| 網域 | 與您的[!DNL PathFactory]帳戶關聯的網域。 這通常是指您[!DNL PathFactory] URL中的唯一識別碼。 |
| 存取權杖 | 用於API驗證的唯一Token，以確保您的系統與[!DNL PathFactory]之間的安全通訊。 |
| api端點 | 存取資料的特定API端點：訪客、工作階段和頁面檢視。 每個端點都對應到您可以擷取的不同資料集。 **注意：**&#x200B;這些資料已由[!DNL PathFactory]預先定義，而且是您想要存取的特定資料： <ul><li>**訪客端點**： `/api/public/v3/data_lake_apis/visitors.json`</li><li>**工作階段端點**： `/api/public/v3/data_lake_apis/sessions.json`</li><li>**頁面檢視端點**： `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

如需如何保護和使用您的認證，以及如何取得和重新整理您的存取Token的詳細資訊，請造訪[[!DNL PathFactory] 支援中心](https://support.pathfactory.com/categories/adobe/)。 此資源提供管理認證的完整指南，並確保有效且安全的API整合。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL PathFactory]驗證認證作為要求內文的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL PathFactory]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的[!DNL PathFactory]應用程式關聯的使用者端識別碼。 |
| `auth.params.clientSecret` | 與您的[!DNL PathFactory]應用程式關聯的使用者端密碼。 |
| `connectionSpec.id` | [!DNL PathFactory]連線規格識別碼： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

**回應**

成功的回應會傳回新建立的連線，包括其唯一的連線識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL PathFactory]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將行銷自動化資料帶入Experience Platform](../../collect/marketing-automation.md)
