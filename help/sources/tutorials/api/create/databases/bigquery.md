---
keywords: Experience Platform；首頁；熱門主題；bigquery;Google;google;Google大查詢
solution: Experience Platform
title: 使用流服務API建立GoogleBigQuery基連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到GoogleBigQuery。
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 015a4fa06fc2157bb8374228380bb31826add37e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 建立 [!DNL Google BigQuery] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Google BigQuery] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Google BigQuery] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Google BigQuery] 在平台中，必須提供以下OAuth 2.0驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `project` | 預設項目ID [!DNL Google BigQuery] 要查詢的項目。 |
| `clientID` | 用於生成刷新令牌的ID值。 |
| `clientSecret` | 用於生成刷新令牌的密鑰值。 |
| `refreshToken` | 從獲取的刷新令牌 [!DNL Google] 用於授權訪問 [!DNL Google BigQuery]。 |
| `largeResultsDataSetId` | 預先建立的  [!DNL Google BigQuery] 為支援大型結果集而需要的資料集ID。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Google BigQuery] 為： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

有關這些值的詳細資訊，請參閱 [[!DNL Google BigQuery] 文檔](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Google BigQuery] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Google BigQuery]:

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
| `auth.params.project` | 預設項目ID [!DNL Google BigQuery] 要查詢的項目。 反對。 |
| `auth.params.clientId` | 用於生成刷新令牌的ID值。 |
| `auth.params.clientSecret` | 用於生成刷新令牌的客戶端值。 |
| `auth.params.refreshToken` | 從獲取的刷新令牌 [!DNL Google] 用於授權訪問 [!DNL Google BigQuery]。 |
| `connectionSpec.id` | 的 [!DNL Google BigQuery] 連接規範ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Google BigQuery] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
