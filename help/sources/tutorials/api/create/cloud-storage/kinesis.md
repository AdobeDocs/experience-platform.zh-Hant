---
keywords: Experience Platform；首頁；熱門主題；Kinesis;kinesis;AmazonKinesis;amazon kinesis
solution: Experience Platform
title: 使用流服務API建立AmazonKinesis源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至AmazonKinesis帳戶。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 2%

---

# 使用流服務API建立[!DNL Amazon Kinesis]源連接

>[!NOTE]
>
>[!DNL Amazon Kineses]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至[!DNL Amazon Kinesis]帳戶的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至[!DNL Amazon Kinesis]帳戶。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Amazon Kinesis]帳戶連接，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | [!DNL Kinesis]帳戶的存取金鑰ID。 |
| `secretKey` | [!DNL Kinesis]帳戶的機密存取金鑰。 |
| `region` | [!DNL Kinesis]帳戶的地區。 |
| `connectionSpec.id` | [!DNL Kinesis]連接規範ID:`86043421-563b-46ec-8e6c-e23184711bf6` |

有關這些值的詳細資訊，請參閱[本Kinesis文檔](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Amazon Kinesis]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

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
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region: "{REGION}
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
| `auth.params.accessKeyId` | [!DNL Kinesis]帳戶的存取金鑰ID。 |
| `auth.params.secretKey` | [!DNL Kinesis]帳戶的機密存取金鑰。 |
| `auth.params.region` | [!DNL Kinesis]帳戶的地區。 如需地區的詳細資訊，請參閱[IP位址允許清單](../../../../ip-address-allow-list.md)上的檔案 |
| `connectionSpec.id` | [!DNL Kinesis]連接規範ID:`86043421-563b-46ec-8e6c-e23184711bf6` |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建立[!DNL Amazon Kinesis]連線，並取得唯一ID做為回應內文的一部分。 您可以使用此連線ID來使用Flow Service API](../../collect/streaming.md)收集串流資料。[
