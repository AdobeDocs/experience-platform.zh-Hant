---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流程服務API建立Azure檔案儲存連接器
topic: overview
translation-type: tm+mt
source-git-commit: 3a882656f93b86093b356be5dbc12b3e4321cfb8
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---


# 使用流程服務API建立Azure檔案儲存連接器

>[!NOTE]
>Azure檔案儲存連接器正在測試中。 功能和檔案可能會有所變更。

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Azure檔案儲存空間連接至Experience Platform的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用流程服務API成功連線至Azure檔案儲存。

### 收集必要的認證

為了讓流服務與Azure檔案儲存連接，您必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 您正在訪問的Azure檔案儲存實例的端點。 |
| `userId` | 對Azure檔案儲存端點具有足夠存取權的使用者。 |
| `password` | Azure檔案儲存例項的密碼 |
| 連接規範ID | 建立連線所需的唯一識別碼。 Azure檔案儲存區的連線規格ID為： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

如需快速入門的詳細資訊，請參 [閱此Azure檔案儲存檔案](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

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

連接指定源，並包含該源的憑據。 每個Azure檔案儲存帳戶只需要一個連線，因為它可用來建立多個來源連接器，以匯入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立Azure檔案儲存連接，必須在POST請求中提供其唯一連接規範ID。 Azure檔案儲存區的連線規格ID為 `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 您正在訪問的Azure檔案儲存實例的端點。 |
| `auth.params.userId` | 對Azure檔案儲存端點具有足夠存取權的使用者。 |
| `auth.params.password` | Azure檔案儲存存取金鑰。 |
| `connectionSpec.id` | Azure檔案儲存連線規格ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

在本教學課程中，您已使用流式服務API建立Azure檔案儲存連線，並取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，同時學習如 [何使用Flow Service API來探索協力廠商雲端儲存空間](../../explore/cloud-storage.md)。
