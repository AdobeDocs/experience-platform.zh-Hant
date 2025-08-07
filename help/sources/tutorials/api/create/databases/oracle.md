---
title: 使用流量服務API將Oracle DB連線至Experience Platform
description: 瞭解如何使用API將Oracle DB連結至Experience Platform。
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---

# 使用[!DNL Oracle DB] API連線[!DNL Flow Service]至Experience Platform

閱讀本指南，瞭解如何使用[!DNL Oracle DB]API[[!DNL Flow Service] 將您的](https://developer.adobe.com/experience-platform-apis/references/flow-service/)帳戶連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Oracle] API成功連線到[!DNL Flow Service]。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

### 收集必要的認證

閱讀[[!DNL Oracle DB] 總覽](../../../../connectors/databases/oracle.md#prerequisites)以取得驗證的相關資訊。

## 在Azure上連線[!DNL Oracle DB]至Experience Platform {#azure}

請閱讀下列步驟，以瞭解如何在Azure上將您的[!DNL Oracle DB]帳戶連線至Experience Platform。

### 在Azure上的Experience Platform上為[!DNL Oracle DB]建立基礎連線 {#azure-base}

基礎連線會將您的來源連結至Experience Platform，以儲存驗證詳細資料、連線狀態和唯一ID。 使用此ID來瀏覽來源檔案並識別要擷取的特定專案，包括其資料型別和格式。

**API格式**

```https
POST /connections
```

若要建立基底連線ID，請對`/connections`端點提出POST要求，並提供您的[!DNL Oracle DB]驗證認證作為要求引數的一部分。

**要求**

下列要求使用連線字串驗證為[!DNL Oracle DB]建立基礎連線。

+++檢視請求


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 用來連線到[!DNL Oracle DB]的連線字串。 [!DNL Oracle DB]連線字串模式為： `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL Oracle]連線規格識別碼： `d6b52d86-f0f8-475f-89d4-ce54c8527328`。 |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。

+++檢視回應

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## 將[!DNL Oracle DB]連線至Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

請閱讀下列步驟，以瞭解如何在AWS上將您的[!DNL Oracle DB]帳戶連結至Experience Platform。

### 在AWS上的Experience Platform上為[!DNL Oracle DB]建立基礎連線 {#aws-base}

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Oracle DB]的基礎連線，以連線至AWS上的Experience Platform。

+++檢視請求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.server` | [!DNL Oracle DB]伺服器的IP位址或主機名稱。 |
| `auth.params.port` | [!DNL Oracle DB]伺服器的連線埠號碼。 |
| `auth.params.database` | 您連線的[!DNL Oracle DB]執行個體名稱。 |
| `auth.params.username` | 與您的[!DNL Oracle DB]執行個體相關聯的使用者帳戶。 |
| `auth.prams.password` | 與您的[!DNL Oracle DB]使用者帳戶對應的密碼。 |
| `auth.params.schema` | 包含資料庫物件的綱要。 |
| `auth.params.sslMode` | 布林值，指出是否強制執行SSL測量。 |
| `connectionSpec.id` | 與[!DNL Oracle DB]來源對應的連線規格識別碼。 此ID值固定為： `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)和對應的識別碼。 您可以使用識別碼來[建立來源連線](../../collect/database-nosql.md#create-a-source-connection)，並使用`etag`來[更新您的帳戶](../../update.md)。

+++檢視回應

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## 建立[!DNL Oracle DB]資料的資料流

現在您已經成功連線[!DNL Oracle DB]帳戶，您現在可以[建立資料流，並將資料庫中的資料擷取到Experience Platform](../../collect/database-nosql.md)。