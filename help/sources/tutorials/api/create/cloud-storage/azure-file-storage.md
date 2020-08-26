---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用流程服務API建立Azure檔案儲存連接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---


# 使用 [!DNL Azure File Storage] API建立連 [!DNL Flow Service] 接器

>[!NOTE]
>
>連接 [!DNL Azure File Storage] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至的 [!DNL Azure File Storage] 步驟 [!DNL Experience Platform]。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 [!DNL Azure File Storage][!DNL Flow Service] API成功連線至。

### 收集必要的認證

要連接 [!DNL Flow Service] ，必須為以 [!DNL Azure File Storage]下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 您正在訪問 [!DNL Azure File Storag]的e實例的端點。 |
| `userId` | 對端點具有足夠訪問權限的 [!DNL Azure File Storage] 用戶。 |
| `password` | 實例的密 [!DNL Azure File Storage] 碼 |
| 連接規範ID | 建立連線所需的唯一識別碼。 的連接規範ID [!DNL Azure File Storage] 為： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

如需快速入門的詳細資訊，請參 [閱此Azure檔案儲存檔案](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Flow Service]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

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

下列請求會建立新 [!DNL Azure File Storage] 的連線，由裝載中提供的屬性設定：


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
| `auth.params.host` | 您正在訪問 [!DNL Azure File Storage] 的實例的端點。 |
| `auth.params.userId` | 對端點具有足夠訪問權限的 [!DNL Azure File Storage] 用戶。 |
| `auth.params.password` | 存取 [!DNL Azure File Storage] 金鑰。 |
| `connectionSpec.id` | 連 [!DNL Azure File Storage] 接規範ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

在本教學課程中，您已使 [!DNL Azure File Storage] 用 [!DNL Flow Service] API建立連線，並取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，同時學習如 [何使用Flow Service API來探索協力廠商雲端儲存空間](../../explore/cloud-storage.md)。
