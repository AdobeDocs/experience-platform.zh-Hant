---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立HP Vertica連接器
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 3%

---


# 使用Flow Service API建立HP Vertica連接器

>[!NOTE]
>HP Vertica連接器正在測試中。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將HP Vertica連接至Experience Platform的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

- [來源](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、對應及增強傳入資料。
- [沙盒](https://docs.adobe.com/content/help/zh-Hant/experience-platform/sandbox/home.html): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用Flow Service API成功連線至HP Vertica。

### 收集必要的認證

要使Flow Service與HP Vertica連接，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到HP Vertica實例的連接字串。 HP Vertica的連接字串模式是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | 建立連線所需的識別碼。 HP Vertica的固定連接規範ID是： `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

有關獲取連接字串的詳細資訊，請參 [閱此HP Vertica文檔](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括來源連接器）都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

- 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個HP Vertica帳戶只需要一個連線，因為它可用來建立多個來源連接器以匯入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立HP Vertica連接，必須在POST請求中提供其唯一連接規範ID。 HP Vertica的連接規範ID為 `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。

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
| `auth.params.connectionString` | 與您的HP Vertica帳戶關聯的連線字串。 HP Vertica的連接字串模式是： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | HP Vertica連接規範ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 後續步驟

在本教學課程中，您已使用Flow Service API建立HP Vertica連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使 [用Flow Service API來探索資料庫](../../explore/database-nosql.md)。
