---
title: 使用流量服務API連線AWS Redshift至Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至AWS Redshift。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API連線[!DNL AWS Redshift]至Experience Platform

>[!IMPORTANT]
>
>[!DNL AWS Redshift]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL AWS Redshift]來源帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 在Azure上連線[!DNL AWS Redshift]至Experience Platform {#azure}

請閱讀下列步驟，以瞭解如何在Azure上將您的[!DNL AWS Redshift]來源連線至Experience Platform。

### 收集必要的認證

若要讓[!DNL Flow Service]與[!DNL AWS Redshift]連線，您必須提供下列連線屬性：

| 認證 | 說明 |
| `server` | [!DNL AWS Redshift]執行個體的伺服器名稱。 |
| `port` | [!DNL AWS Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| `username` | 與您的[!DNL AWS Redshift]帳戶相關聯的使用者名稱。 |
| `password` | 與使用者帳戶對應的密碼。 |
| `database` | 要從中擷取資料的[!DNL AWS Redshift]資料庫。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL AWS Redshift]的連線規格識別碼為`3416976c-a9ca-4bba-901a-1f08f66978ff`。 |

如需開始使用的詳細資訊，請參閱此[[!DNL AWS Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)。

### 在Azure [#azure-base]上的Experience Platform上為[!DNL AWS Redshift]建立基底連線

>[!NOTE]
>
>[!DNL Redshift]的預設編碼標準為Unicode。 無法變更此設定。

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL AWS Redshift]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

+++選取以檢視範例

下列要求會建立[!DNL AWS Redshift]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL AWS Redshift]執行個體的伺服器名稱。 |
| `auth.params.port` | [!DNL AWS Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| `auth.params.username` | 與您的[!DNL AWS Redshift]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與使用者帳戶對應的密碼。 |
| `auth.params.database` | 要從中擷取資料的[!DNL AWS Redshift]資料庫。 |
| `connectionSpec.id` | [!DNL AWS Redshift]連線規格識別碼： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**回應**

+++選取以檢視範例

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## 將[!DNL AWS Redshift]連線至AWS Web服務(AWS)上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在AWS Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何將[!DNL AWS Redshift]來源連線至AWS上的Experience Platform。

### 在AWS上的Experience Platform上為[!DNL AWS Redshift]建立基礎連線 {#aws-base}

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL AWS Redshift]的基礎連線：

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
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL AWS Redshift]執行個體的伺服器名稱。 |
| `auth.params.port` | [!DNL AWS Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| `auth.params.username` | 與您的[!DNL AWS Redshift]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與使用者帳戶對應的密碼。 |
| `auth.params.database` | 要從中擷取資料的[!DNL AWS Redshift]資料庫。 |
| `auth.params.schema` | 與您的[!DNL AWS Redshift]資料庫關聯的結構描述名稱。 您必須確保您要授與資料庫存取權的使用者也擁有此綱要的存取權。 |
| `connectionSpec.id` | [!DNL AWS Redshift]連線規格識別碼： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的儲存空間時，需要此ID。

+++選取以檢視範例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL AWS Redshift]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將資料庫資料帶入Experience Platform](../../collect/database-nosql.md)
