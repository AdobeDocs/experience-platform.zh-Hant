---
keywords: Experience Platform；首頁；熱門主題；Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: 使用流程服務API建立Amazon Kinesis來源連線
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至Amazon Kinesis來源。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# 建立 [!DNL Amazon Kinesis] 源連接（使用流服務API）

本教學課程會逐步引導您完成連線步驟 [!DNL Amazon Kinesis] (下稱「[!DNL Kinesis]&quot;)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可分割單一 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL Kinesis] 到使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Amazon Kinesis] 帳戶，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 存取金鑰ID是用來驗證您的 [!DNL Kinesis] 帳戶至Platform。 |
| `secretKey` | 秘密訪問密鑰是用於驗證您的 [!DNL Kinesis] 帳戶至Platform。 |
| `region` | 您的 [!DNL Kinesis] 帳戶。 請參閱 [新增IP位址至允許清單](../../../../ip-address-allow-list.md) 以取得地區的詳細資訊。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 此 [!DNL Kinesis] 連接規範ID為： `86043421-563b-46ec-8e6c-e23184711bf6`. |

如需 [!DNL Kinesis] 存取金鑰及其產生方式，請參閱 [[!DNL AWS] 管理IAM用戶訪問密鑰的指南](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

建立源連接的第一步是驗證您的 [!DNL Kinesis] 源和生成基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Kinesis] 驗證憑證作為要求參數的一部分。

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
| `auth.params.accessKeyId` | 您 [!DNL Kinesis] 帳戶。 |
| `auth.params.secretKey` | 您的 [!DNL Kinesis] 帳戶。 |
| `auth.params.region` | 您的 [!DNL Kinesis] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Kinesis] 連接規範ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**回應**

成功的回應會傳回新建立之基本連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接 {#source}

來源連線會建立並管理資料擷取所在之外部來源的連線。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 來源連線例項是租用戶和IMS組織專屬的。

若要建立來源連線，請向 `/sourceConnections` 端點 [!DNL Flow Service] API。

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
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可提供的選用值，用於包含來源連線的詳細資訊。 |
| `baseConnectionId` | 您的 [!DNL Kinesis] 在上一步驟中生成的源。 |
| `connectionSpec.id` | 的固定連接規範ID [!DNL Kinesis]. 此ID為： `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 格式 [!DNL Kinesis] 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |
| `params.stream` | 要提取記錄的資料流的名稱。 |
| `params.dataType` | 此參數會定義正在擷取的資料類型。 支援的資料類型包括： `raw` 和 `xdm`. |
| `params.reset` | 此參數會定義資料的讀取方式。 使用 `latest` 從最新資料開始讀取，並使用 `earliest` 從資料流中的第一個可用資料開始讀取。 |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在下一個教程中建立資料流時需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Kinesis] 源連接使用 [!DNL Flow Service] API。 您可以在下一個教學課程中使用此來源連線ID [使用 [!DNL Flow Service] API](../../collect/streaming.md).
