---
keywords: Experience Platform；首頁；熱門主題；bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: 使用Flow Service API建立Google BigQuery Base連線
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Google BigQuery。
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 建立 [!DNL Google BigQuery] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Google BigQuery] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Google BigQuery] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Google BigQuery] 若要使用Platform，您必須提供下列OAuth 2.0驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `project` | 預設的專案ID [!DNL Google BigQuery] 要查詢的專案。 |
| `clientID` | 用來產生重新整理Token的ID值。 |
| `clientSecret` | 用於產生重新整理Token的密碼值。 |
| `refreshToken` | 從中取得的重新整理代號 [!DNL Google] 用於授權存取 [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | 預先建立  [!DNL Google BigQuery] 啟用對大型結果集的支援所需的資料集ID。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Google BigQuery] 為： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

如需這些值的詳細資訊，請參閱 [[!DNL Google BigQuery] 檔案](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Google BigQuery] 驗證憑證作為要求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Google BigQuery]:

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
| `auth.params.project` | 預設的專案ID [!DNL Google BigQuery] 要查詢的專案。 反對。 |
| `auth.params.clientId` | 用來產生重新整理Token的ID值。 |
| `auth.params.clientSecret` | 用於產生重新整理Token的用戶端值。 |
| `auth.params.refreshToken` | 從中取得的重新整理代號 [!DNL Google] 用於授權存取 [!DNL Google BigQuery]. |
| `connectionSpec.id` | 此 [!DNL Google BigQuery] 連接規範ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**回應**

成功的回應會傳回新建立連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Google BigQuery] 基本連接使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
