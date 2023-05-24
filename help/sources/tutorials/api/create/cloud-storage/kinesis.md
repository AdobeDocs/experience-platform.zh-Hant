---
keywords: Experience Platform；首頁；熱門主題；Kinesis;kinesis;AmazonKinesis;amazon kinesis
solution: Experience Platform
title: 使用流服務API建立AmazonKinesis源連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到AmazonKinesis源。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---

# 建立 [!DNL Amazon Kinesis] 使用流服務API的源連接

本教程將指導您完成連接的步驟 [!DNL Amazon Kinesis] (以下簡稱：[!DNL Kinesis]&quot;)到Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接所需的其他資訊 [!DNL Kinesis] 到使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 與 [!DNL Amazon Kinesis] 帳戶，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 訪問密鑰ID是用於驗證您的 [!DNL Kinesis] 帳戶到平台。 |
| `secretKey` | 密鑰訪問密鑰是用於驗證您的 [!DNL Kinesis] 帳戶到平台。 |
| `region` | 您的區域 [!DNL Kinesis] 帳戶。 請參閱上的指南 [將IP地址添加到允許清單](../../../../ip-address-allow-list.md) 的子菜單。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的 [!DNL Kinesis] 連接規範ID為： `86043421-563b-46ec-8e6c-e23184711bf6`。 |

有關 [!DNL Kinesis] 訪問密鑰以及如何生成密鑰，請參閱 [[!DNL AWS] 管理IAM用戶訪問密鑰的指南](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

建立源連接的第一步是驗證 [!DNL Kinesis] 源並生成基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Kinesis] 身份驗證憑據作為請求參數的一部分。

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
| `auth.params.accessKeyId` | 您的訪問密鑰ID [!DNL Kinesis] 帳戶。 |
| `auth.params.secretKey` | 您的機密訪問密鑰 [!DNL Kinesis] 帳戶。 |
| `auth.params.region` | 您的區域 [!DNL Kinesis] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL Kinesis] 連接規範ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立源連接 {#source}

源連接建立並管理與外部源的連接，該連接來自接收資料的位置。 源連接由資料源、資料格式和建立資料流所需的源連接ID等資訊組成。 源連接實例特定於租戶和組織。

要建立源連接，請向 `/sourceConnections` 端點 [!DNL Flow Service] API。

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以提供的可選值，以包含有關源連接的詳細資訊。 |
| `baseConnectionId` | 您的基本連接ID [!DNL Kinesis] 在上一步中生成的源。 |
| `connectionSpec.id` | 固定連接規範ID [!DNL Kinesis]。 此ID為： `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 格式 [!DNL Kinesis] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `params.stream` | 要從中提取記錄的資料流的名稱。 |
| `params.dataType` | 此參數定義正在攝取的資料的類型。 支援的資料類型包括： `raw` 和 `xdm`。 |
| `params.reset` | 此參數定義資料的讀取方式。 使用 `latest` 開始讀取最新資料，並使用 `earliest` 開始從流中的第一個可用資料讀取。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在下一教程中建立資料流時需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Kinesis] 源連接使用 [!DNL Flow Service] API。 您可以在下一教程中使用此源連接ID [使用 [!DNL Flow Service] API](../../collect/streaming.md)。
