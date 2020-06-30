---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流服務API建立Amazon Kinesis連接器
topic: overview
translation-type: tm+mt
source-git-commit: 11431ffcfc2204931fe3e863bfadc7878a40b49c
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---


# 使用流 [!DNL Amazon Kinesis] 程服務API建立連接器

>[!NOTE]
>連接 [!DNL Amazon Kineses] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至帳戶 [!DNL Experience Platform] 的步 [!DNL Amazon Kinesis] 驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用API成功連 [!DNL Amazon Kinesis] 線至帳 [!DNL Flow Service] 戶。

### 收集必要的認證

若要連 [!DNL Flow Service] 接您的帳戶， [!DNL Amazon Kinesis] 您必須提供下列連線屬性的值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 您帳戶的存取金鑰 [!DNL Kinesis] ID。 |
| `secretKey` | 您帳戶的機密存取 [!DNL Kinesis] 金鑰。 |
| `region` |  | 您帳戶的地 [!DNL Kinesis] 區。 |
| `connectionSpec.id` | 連 [!DNL Kinesis] 接規範ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

有關這些值的詳細資訊，請參 [閱本Kinesis文檔](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Flow Service]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個帳戶只需要一個連 [!DNL Amazon Kinesis] 接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

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
            "specName": "Basic Authentication for Kinesis",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretKey": "secretKey"
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
| `auth.params.accessKeyId` | 您帳戶的存取金鑰 [!DNL Kinesis] ID。 |
| `auth.params.secretKey` | 您帳戶的機密存取 [!DNL Kinesis] 金鑰。 |
| `auth.params.region` | 您帳戶的地 [!DNL Kinesis] 區。 |
| `connectionSpec.id` | 連 [!DNL Kinesis] 接規範ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建 [!DNL Amazon Kinesis] 立連線，並且已取得唯一ID作為回應內文的一部分。 您可以使用此連線ID來 [探索雲端儲存空間，使用Flow Service API](../../explore/cloud-storage.md)。