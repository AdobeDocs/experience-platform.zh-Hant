---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流程服務API建立Azure Blob連接器
topic: overview
translation-type: tm+mt
source-git-commit: 7ffe560f455973da3a37ad102fbb8cc5969d5043
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# 使用流程服務API建立Azure Blob連接器

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Azure Blob（以下稱為「Blob」）儲存空間的步驟。

如果您想要在Experience Platform中使用使用者介面， [](../../../ui/create/cloud-storage/blob-s3.md) Azure Blob或Amazon S3來源連接器UI教學課程會提供執行類似動作的逐步指示。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用Flow Service API成功連線至Blob儲存空間。

### 收集必要的認證

要使流服務與您的Blob儲存連接，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 訪問Blob儲存中的資料所需的連接字串。 |

如需快速入門的詳細資訊，請造 [訪此Azure Blob檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於流服務的資源）都會隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個Blob帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Blob Connection",
        "description": "Cnnection for an Azure Blob account",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | Blob儲存的連接字串。 |
| `connectionSpec.id` | 點滴儲存連接規範ID: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的儲存空間時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建立Blob連線，並且已取得唯一ID作為回應內文的一部分。 您可以使用此連線ID來 [探索使用Flow Service API的雲端儲存空間](../../explore/cloud-storage.md) ，或 [使用Flow Service API內嵌鑲木地板資料](../../cloud-storage-parquet.md)。