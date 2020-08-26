---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立HP Vertica連接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 3%

---


# 使用 [!DNL Vertica] API [!DNL Flow Service] 建立HP連接器

>[!NOTE]
>
>HP接 [!DNL Vertica] 口處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成將HP連接至的 [!DNL Vertica] 步驟 [!DNL Experience Platform]。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

- [來源](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時提供使用服務來建構、對應及增強傳入資料的 [!DNL Platform] 能力。
- [沙盒](https://docs.adobe.com/content/help/zh-Hant/experience-platform/sandbox/home.html): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用API成功連 [!DNL Vertica] 接至 [!DNL Flow Service] HP。

### 收集必要的認證

要與HP [!DNL Flow Service] 連接，您必 [!DNL Vertica]須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到HP實例的連接字串 [!DNL Vertica] 。 HP的連接字串模式 [!DNL Vertica] 是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | 建立連線所需的識別碼。 HP的固定連接規範ID [!DNL Vertica] 為： `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

有關獲取連接字串的詳細資訊，請參 [閱此HP Vertica文檔](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括源連接器）都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

- 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個HP帳戶只需要一 [!DNL Vertica] 個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立HP連接， [!DNL Vertica] 必須在POST請求中提供其唯一連接規範ID。 HP的連接規範ID [!DNL Vertica] 為 `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。

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
| `auth.params.connectionString` | 與您的HP帳戶關聯的連線 [!DNL Vertica] 字串。 HP的連接字串模 [!DNL Vertica] 式是： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | HP連接 [!DNL Vertica] 規範ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 後續步驟

在本教程中，您已使用 [!DNL Vertica] API建立HP連線，並 [!DNL Flow Service] 已取得連線的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使 [用Flow Service API來探索資料庫](../../explore/database-nosql.md)。
