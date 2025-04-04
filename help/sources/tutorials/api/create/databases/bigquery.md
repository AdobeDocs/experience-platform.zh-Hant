---
title: 使用流量服務API將Google BigQuery連線至Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Google BigQuery。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API連線[!DNL Google BigQuery]至Experience Platform

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL Google BigQuery]資料庫連線至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

### 收集必要的認證

閱讀[[!DNL Google BigQuery] 驗證指南](../../../../connectors/databases/bigquery.md#prerequisites)以瞭解擷取[!DNL Google BigQuery]認證的詳細步驟。

## 在Azure上連線[!DNL Google BigQuery]至Experience Platform {#azure}

請閱讀下列步驟，以瞭解如何在Azure上將您的[!DNL Google BigQuery]來源連線至Experience Platform。

### 在Azure上的Experience Platform上為[!DNL Google BigQuery]建立基礎連線 {#azure-base}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Google BigQuery]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 使用基本驗證]

+++要求

下列要求使用基本驗證建立[!DNL Google BigQuery]的基本連線。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
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

+++

+++回應

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB 使用服務驗證]


+++要求

下列要求使用服務驗證為[!DNL Google BigQuery]建立基底連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection with service account",
      "description": "Google BigQuery connection with service account",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
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
| `auth.params.projectId` | 要查詢的預設[!DNL Google BigQuery]專案的專案識別碼。 針對。 |
| `auth.params.keyFileContent` | 用來驗證服務帳戶的金鑰檔案。 您必須在[!DNL Base64]中編碼金鑰檔案內容。 |
| `auth.params.largeResultsDataSetId` | （選用）啟用大型結果集支援所需的預先建立[!DNL Google BigQuery]資料集ID。 |

+++

+++回應

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## 將[!DNL Google BigQuery]連線到Amazon Web Services (AWS)上的Experience Platform {#aws}

請閱讀下列步驟，以瞭解如何將[!DNL Google BigQuery]資料庫連線至AWS上的Experience Platform。

### 在AWS上的Experience Platform上為[!DNL Google BigQuery]建立基礎連線

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立基底連線，將[!DNL Google BigQuery]連線至AWS上的Experience Platform。

+++選取以檢視範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.projectId` | 要查詢的預設[!DNL Google BigQuery]專案的專案識別碼。 針對。 |
| `auth.params.keyFileContent` | 用來驗證服務帳戶的金鑰檔案。 您必須在[!DNL Base64]中編碼金鑰檔案內容。 |
| `auth.params.datasetId` | 與您的[!DNL Google BigQuery]來源對應的資料集識別碼。 此ID代表資料表所在的位置。 |

+++

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的儲存空間時，需要此ID。

+++選取以檢視範例

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Google BigQuery]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
