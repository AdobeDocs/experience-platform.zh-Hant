---
title: 使用流量服務API建立Amazon Kinesis Source連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Amazon Kinesis來源。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 3%

---

# 使用流程服務API建立[!DNL Amazon Kinesis]來源連線

>[!IMPORTANT]
>
>[!DNL Amazon Kinesis]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，將[!DNL Amazon Kinesis] （以下稱為&quot;[!DNL Kinesis]&quot;）連線至Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一[!DNL Experience Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功將[!DNL Kinesis]連線至Experience Platform。

### 收集必要的認證

為了讓[!DNL Flow Service]與您的[!DNL Amazon Kinesis]帳戶連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 存取金鑰ID是用來向Experience Platform驗證您[!DNL Kinesis]帳戶的存取金鑰組的一半。 |
| `secretKey` | 秘密存取金鑰是用來向Experience Platform驗證您[!DNL Kinesis]帳戶的存取金鑰組的另一半。 |
| `region` | 您的[!DNL Kinesis]帳戶的地區。 如需有關地區的詳細資訊，請參閱[將IP位址新增至允許清單](../../../../ip-address-allow-list.md)的指南。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Kinesis]連線規格識別碼為： `86043421-563b-46ec-8e6c-e23184711bf6`。 |

有關[!DNL Kinesis]存取金鑰以及如何產生這些金鑰的詳細資訊，請參閱此[[!DNL AWS] IAM使用者存取金鑰管理指南](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

建立來源連線的第一個步驟是驗證您的[!DNL Kinesis]來源並產生基本連線識別碼。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Kinesis]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 您[!DNL Kinesis]帳戶的存取金鑰識別碼。 |
| `auth.params.secretKey` | 您的[!DNL Kinesis]帳戶的秘密存取金鑰。 |
| `auth.params.region` | 您的[!DNL Kinesis]帳戶的地區。 |
| `connectionSpec.id` | [!DNL Kinesis]連線規格識別碼： `86043421-563b-46ec-8e6c-e23184711bf6` |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立來源連線 {#source}

來源連線會建立和管理與擷取資料的外部來源的連線。 來源連線包含資料來源、資料格式以及建立資料流所需的來源連線ID等資訊。 租使用者和組織專屬的來源連線例項。

若要建立來源連線，請對[!DNL Flow Service] API的`/sourceConnections`端點提出POST要求。

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以提供的選用值，包含來源連線的詳細資訊。 |
| `baseConnectionId` | 在上一步中產生的[!DNL Kinesis]來源的基本連線識別碼。 |
| `connectionSpec.id` | [!DNL Kinesis]的固定連線規格識別碼。 此ID為： `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 您要擷取的[!DNL Kinesis]資料格式。 目前唯一支援的資料格式為`json`。 |
| `params.stream` | 要從中提取記錄的資料流的名稱。 |
| `params.dataType` | 此引數會定義所擷取的資料型別。 支援的資料型別包括： `raw`和`xdm`。 |
| `params.reset` | 此引數會定義資料的讀取方式。 使用`latest`開始讀取最近的資料，並使用`earliest`開始讀取資料流中第一個可用的資料。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在下一個教學課程中，需要此ID才能建立資料流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>在您建立或更新串流資料流後，需要短暫暫停資料擷取5分鐘，以防止任何可能的資料遺失或資料中斷情況。

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Kinesis]來源連線。 您可以在下一個教學課程中使用此來源連線ID來[使用 [!DNL Flow Service] API](../../collect/streaming.md)建立串流資料流。
