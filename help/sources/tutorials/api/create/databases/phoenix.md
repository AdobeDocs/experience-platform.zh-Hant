---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Phoenix連接器
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# 使用 [!DNL Phoenix] API建立連 [!DNL Flow Service] 接器

>[!NOTE]
>連接 [!DNL Phoenix] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成將資料庫連線至的 [!DNL Phoenix] 步驟 [!DNL Experience Platform]。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 [!DNL Phoenix][!DNL Flow Service] API成功連線至。

### 收集必要的認證

要連接 [!DNL Flow Service] ，必須為以 [!DNL Phoenix]下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 伺服器的IP地址或主 [!DNL Phoenix] 機名。 |
| `username` | 您用來存取伺服器的使用者 [!DNL Phoenix] 名稱。 |
| `password` | 與用戶對應的密碼。 |
| `port` | 伺服器用於監聽 [!DNL Phoenix] 客戶機連接的TCP埠。 如果您連線至 [!DNL Azure] HDInsights，請將埠指定為443。 |
| `httpPath` | 與伺服器對應的部分 [!DNL Phoenix] URL。 如果使用HDInsights叢集，請指 [!DNL Azure] 定/hbasephoenix0。 |
| `enableSsl` | 布林值。 指定是否使用SSL加密與伺服器的連線。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 的連接規範ID [!DNL Phoenix] 為： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有關開始使用的更多資訊，請參 [閱這份Phoenix檔案](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

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

連接指定源，並包含該源的憑據。 每個帳戶只需要一個連 [!DNL Phoenix] 接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立連接，必 [!DNL Phoenix] 須在POST請求中提供其唯一連接規範ID。 的連接規範ID [!DNL Phoenix] 為 `102706fb-a5cd-42ee-afe0-bc42f017ff43`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 伺服器的主 [!DNL Phoenix] 機。 |
| `auth.params.username` | 與您的連線相關聯的使用 [!DNL Phoenix] 者名稱。 |
| `auth.params.password` | 與您的連線相關聯的 [!DNL Phoenix] 密碼。 |
| `auth.params.port` | 連接的TCP端 [!DNL Phoenix] 口。 |
| `auth.params.httpPath` | 您連線的部分http [!DNL Phoenix] 路徑。 |
| `auth.params.enableSsl` | 此布爾值指定是否使用SSL加密與伺服器的連接。 |
| `connectionSpec.id` | 連 [!DNL Phoenix] 接規範ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 後續步驟

在本教學課程中，您已使 [!DNL Phoenix] 用 [!DNL Flow Service] API建立連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使 [用Flow Service API來探索資料庫](../../explore/database-nosql.md)。