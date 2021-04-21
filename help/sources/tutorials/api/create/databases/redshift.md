---
keywords: Experience Platform；首頁；熱門主題；redshift；紅移；Amazon紅移；amazon紅移
solution: Experience Platform
title: 使用流服務API建立Amazon紅移源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform與Amazon紅移相連。
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Amazon Redshift]來源連線

>[!NOTE]
>
>[!DNL Amazon Redshift]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至[!DNL Amazon Redshift]（以下稱為&quot;[!DNL Redshift]&quot;）的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至[!DNL Redshift]。

### 收集必要的認證

要使[!DNL Flow Service]與[!DNL Redshift]連接，必須提供以下連接屬性：

| **憑證** | **說明** |
| -------------- | --------------- |
| `server` | 與[!DNL Redshift]帳戶關聯的伺服器。 |
| `username` | 與[!DNL Redshift]帳戶關聯的使用者名稱。 |
| `password` | 與[!DNL Redshift]帳戶關聯的密碼。 |
| `database` | 您正在訪問的[!DNL Redshift]資料庫。 |

有關開始使用的詳細資訊，請參閱[本Redshift文檔](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

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

連接指定源，並包含該源的憑據。 每個[!DNL Redshift]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

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
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.server` | 您的[!DNL Redshift]伺服器。 |
| `auth.params.database` | 與[!DNL Redshift]帳戶關聯的資料庫。 |
| `auth.params.password` | 與[!DNL Redshift]帳戶關聯的密碼。 |
| `auth.params.username` | 與[!DNL Redshift]帳戶關聯的使用者名稱。 |
| `connectionSpec.id` | 在上一步中檢索的[!DNL Redshift]帳戶的連接規範`id`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Redshift]連接，並獲取了該連接的唯一ID值。 在下一個教程中，您可以使用此連接ID來學習如何使用流服務API](../../explore/database-nosql.md)來瀏覽資料庫或NoSQL系統。[
