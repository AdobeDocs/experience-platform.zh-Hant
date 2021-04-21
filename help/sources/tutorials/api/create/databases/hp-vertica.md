---
keywords: Experience Platform;home；熱門主題；Vertica;vertica
solution: Experience Platform
title: 使用Flow Service API建立HP Vertica Source Connection
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將HP Vertica連線至Adobe Experience Platform。
exl-id: 37f831c1-7c82-462a-8338-a0bcaaf08cd1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API建立HP [!DNL Vertica]源連接

>[!NOTE]
>
>HP [!DNL Vertica]介面處於測試階段。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用[!DNL Flow Service] API來引導您完成將HP [!DNL Vertica]連接到[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時提供使用服務來建構、對應及增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](https://docs.adobe.com/content/help/zh-Hant/experience-platform/sandbox/home.html): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功連接到HP [!DNL Vertica]。

### 收集必要的認證

要使[!DNL Flow Service]與HP [!DNL Vertica]連接，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到HP [!DNL Vertica]實例的連接字串。 HP [!DNL Vertica]的連接字串模式是`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | 建立連線所需的識別碼。 HP [!DNL Vertica]的固定連接規範ID為：`a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

有關獲取連接字串的詳細資訊，請參閱[此HP Vertica文檔](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

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

連接指定源，並包含該源的憑據。 每個HP [!DNL Vertica]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

要建立HP [!DNL Vertica]連接，必須在POST請求中提供其唯一連接規範ID。 HP [!DNL Vertica]的連接規範ID為`a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 與HP [!DNL Vertica]帳戶關聯的連接字串。 HP [!DNL Vertica]的連接字串模式是：`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | HP [!DNL Vertica]連接規範ID:`a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了HP [!DNL Vertica]連接，並獲取了該連接的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使用流服務API](../../explore/database-nosql.md)來探索資料庫。[
