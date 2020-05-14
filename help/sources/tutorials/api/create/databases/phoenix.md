---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Phoenix連接器
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---


# 使用Flow Service API建立Phoenix連接器

>[!NOTE]
>菲尼克斯連接器是測試版。 功能和檔案可能會有所變更。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Phoenix資料庫連接至Experience Platform的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的額外資訊，以便使用Flow Service API成功連線至Phoenix。

### 收集必要的認證

為了讓Flow Service與Phoenix連接，您必須提供下列連線屬性的值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | Phoenix伺服器的IP地址或主機名。 |
| `username` | 您用來存取Phoenix伺服器的使用者名稱。 |
| `password` | 與用戶對應的密碼。 |
| `port` | Phoenix伺服器用於監聽客戶端連接的TCP埠。 如果您連線至Azure HDInsights，請將連接埠指定為443。 |
| `httpPath` | 對應於Phoenix伺服器的部分URL。 如果使用Azure HDInsights叢集，請指定/hbasephoenix0。 |
| `enableSsl` | 布林值。 指定是否使用SSL加密與伺服器的連線。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 Phoenix的連接規範ID是： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有關開始使用的更多資訊，請參 [閱這份Phoenix檔案](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

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

連接指定源，並包含該源的憑據。 每個Phoenix帳戶只需要一個連線，因為它可用來建立多個來源連接器，以匯入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

為了建立Phoenix連線，其唯一連線規格ID必須作為POST要求的一部分提供。 菲尼克斯的連接規範ID為 `102706fb-a5cd-42ee-afe0-bc42f017ff43`。

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
| `auth.params.host` | 菲尼克斯伺服器的主機。 |
| `auth.params.username` | 與您的Phoenix連線關聯的使用者名稱。 |
| `auth.params.password` | 與您的Phoenix連線關聯的密碼。 |
| `auth.params.port` | Phoenix連接的TCP埠。 |
| `auth.params.httpPath` | Phoenix連線的部分http路徑。 |
| `auth.params.enableSsl` | 此布爾值指定是否使用SSL加密與伺服器的連接。 |
| `connectionSpec.id` | Phoenix連接規範ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 後續步驟

在本教學課程中，您已使用Flow Service API建立Phoenix連線，並取得連線的唯一ID值。 在下一個教學課程中，您可以使用此ID來學習如何使 [用Flow Service API來探索資料庫](../../explore/database-nosql.md)。