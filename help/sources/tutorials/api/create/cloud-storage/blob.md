---
keywords: Experience Platform;home;popular topics;Azure;azure blob;blob;Blob
solution: Experience Platform
title: 使用流程服務API建立Azure Blob連接器
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Azure Blob（以下稱為「Blob」）儲存空間的步驟。
translation-type: tm+mt
source-git-commit: fc6449d260ea7b96956689ce6c95c5e8b9002d89
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API建立[!DNL Azure Blob]連接器

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至[!DNL Azure Blob]（以下稱為「Blob」）儲存空間的步驟。

如果您希望使用[!DNL Experience Platform]中的用戶介面， [Azure Blob源連接器UI教程](../../../ui/create/cloud-storage/blob.md)提供了執行類似操作的逐步說明。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功連線至Blob儲存空間。

### 收集必要的認證

要使[!DNL Flow Service]與Blob儲存連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 訪問Blob儲存中的資料所需的連接字串。 Blob連接字串模式是：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 Blob的連接規範ID是：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

有關獲取連接字串的詳細資訊，請參閱[此Azure Blob文檔](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 「內容類型：application/json&quot;

## 建立連線

連接指定源，並包含該源的憑據。 每個Blob帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立Blob連接，其唯一連接規範ID必須作為POST請求的一部分提供。 Blob的連接規範ID為`4c10e202-c428-4796-9208-5f1f5732b1cf`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
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
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
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
| `auth.params.connectionString` | 訪問Blob儲存中的資料所需的連接字串。 Blob連接字串模式是：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | 點滴儲存連接規範ID是：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索您的儲存空間時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 後續步驟

在本教學課程中，您已使用API建立Blob連線，並且已取得唯一ID作為回應內文的一部分。 您可以使用此連線ID來探索使用Flow Service API[或](../../explore/cloud-storage.md)使用Flow Service API[收錄拼花資料的雲端儲存空間。](../../cloud-storage-parquet.md)