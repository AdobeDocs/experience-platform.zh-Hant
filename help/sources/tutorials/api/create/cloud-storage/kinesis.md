---
keywords: Experience Platform；首頁；熱門主題；Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: 使用流程服務API建立Amazon Kinesis來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Amazon Kinesis來源。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: fe7c498542cc0dd5f53bc3a434ab34d62e449048
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 1%

---

# 使用流服務API建立[!DNL Amazon Kinesis]源連接

本教學課程會逐步帶您了解使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)將[!DNL Amazon Kinesis]（以下稱為「[!DNL Kinesis]」）連線至Experience Platform的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功將[!DNL Kinesis]連線至Platform。

### 收集所需憑據

為了使[!DNL Flow Service]與[!DNL Amazon Kinesis]帳戶連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 存取金鑰ID是用來驗證[!DNL Kinesis]帳戶至Platform的存取金鑰組的一半。 |
| `secretKey` | 秘密存取金鑰是用來驗證[!DNL Kinesis]帳戶至Platform的存取金鑰組的另一半。 |
| `region` | [!DNL Kinesis]帳戶的地區。 有關地區的詳細資訊，請參閱[將IP位址新增至允許清單](../../../../ip-address-allow-list.md)的指南。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Kinesis]連接規範ID為：`86043421-563b-46ec-8e6c-e23184711bf6`。 |

有關[!DNL Kinesis]訪問密鑰以及如何生成這些密鑰的詳細資訊，請參閱本[[!DNL AWS] 指南，以管理IAM用戶的訪問密鑰](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

建立源連接的第一步是驗證[!DNL Kinesis]源並生成基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Kinesis]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.accessKeyId` | [!DNL Kinesis]帳戶的訪問密鑰ID。 |
| `auth.params.secretKey` | [!DNL Kinesis]帳戶的秘密訪問密鑰。 |
| `auth.params.region` | [!DNL Kinesis]帳戶的地區。 |
| `connectionSpec.id` | [!DNL Kinesis]連接規範ID:`86043421-563b-46ec-8e6c-e23184711bf6` |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接 {#source}

來源連線會建立並管理資料擷取所在之外部來源的連線。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 來源連線例項是租用戶和IMS組織專屬的。

要建立源連接，請向[!DNL Flow Service] API的`/sourceConnections`端點發出POST請求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可提供的選用值，用於包含來源連線的詳細資訊。 |
| `baseConnectionId` | 在上一步中生成的[!DNL Kinesis]源的基本連接ID。 |
| `connectionSpec.id` | [!DNL Kinesis]的固定連接規範ID。 此ID為：`86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 您要擷取的[!DNL Kinesis]資料格式。 目前，唯一支援的資料格式是`json`。 |
| `params.stream` | 要提取記錄的資料流的名稱。 |
| `params.dataType` | 此參數會定義正在擷取的資料類型。 支援的資料類型包括：`raw`和`xdm`。 |
| `params.reset` | 此參數會定義資料的讀取方式。 使用`latest`開始從最新資料中讀取，並使用`earliest`開始從流中第一個可用資料中讀取。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在下一個教程中建立資料流時需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Kinesis]來源連線。 您可以在[的下一個教程中使用此源連接ID，以使用 [!DNL Flow Service] API](../../collect/streaming.md)建立流資料流。
