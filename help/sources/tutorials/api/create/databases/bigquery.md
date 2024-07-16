---
title: 使用流量服務API建立Google BigQuery基本連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Google BigQuery。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Google BigQuery]基本連線

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Google BigQuery]建立基礎連線的步驟。

## 快速入門

本指南需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Google BigQuery]。

### 收集必要的認證

為了讓[!DNL Flow Service]連線[!DNL Google BigQuery]至Platform，您必須提供下列OAuth 2.0驗證值：

| 認證 | 說明 |
| ---------- | ----------- |
| `project` | 要查詢的預設[!DNL Google BigQuery]專案的專案識別碼。 |
| `clientID` | 用來產生重新整理權杖的ID值。 |
| `clientSecret` | 用來產生重新整理權杖的密碼值。 |
| `refreshToken` | 從[!DNL Google]取得的重新整理權杖用於授權存取[!DNL Google BigQuery]。 |
| `largeResultsDataSetId` | 啟用大型結果集的支援所需的預先建立[!DNL Google BigQuery]資料集ID。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Google BigQuery]的連線規格識別碼為： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

如需這些值的詳細資訊，請參閱此[[!DNL Google BigQuery] 檔案](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Google BigQuery]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Google BigQuery]的基礎連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.project` | 要查詢的預設[!DNL Google BigQuery]專案的專案識別碼。 針對。 |
| `auth.params.clientId` | 用來產生重新整理權杖的ID值。 |
| `auth.params.clientSecret` | 用來產生重新整理權杖的使用者端值。 |
| `auth.params.refreshToken` | 從[!DNL Google]取得的重新整理權杖用於授權存取[!DNL Google BigQuery]。 |
| `connectionSpec.id` | [!DNL Google BigQuery]連線規格識別碼： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Google BigQuery]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶到Platform](../../collect/database-nosql.md)
