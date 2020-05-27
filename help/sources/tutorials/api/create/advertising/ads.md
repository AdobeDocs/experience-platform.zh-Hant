---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API建立Google AdWords連接器
topic: overview
translation-type: tm+mt
source-git-commit: 00f785577999d2ec3147a3cc2b8edd1028be2471
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---


# 使用Flow Service API建立Google AdWords連接器

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Google AdWords的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用Flow Service API成功連線至廣告。

### 收集必要的認證

為了讓流式服務與AdWords連線，您必須提供下列連線屬性的值：

| **憑證** | **說明** |
| -------------- | --------------- |
| 客戶客戶ID | AdWords帳戶的客戶客戶ID。 |
| 開發人員Token | 與管理員帳戶關聯的開發人員Token。 |
| 重新整理Token | 從Google取得的重新整理Token，以授權存取AdWords。 |
| 用戶端ID | 用來取得重新整理Token之Google應用程式的用戶端ID。 |
| 用戶端密碼 | 用來取得重新整理Token之Google應用程式的用戶端密碼。 |
| 連接規範ID | 建立連線所需的唯一識別碼。 Google AdWords的連線規格ID為： `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

如需這些值的詳細資訊，請參閱此 [Google AdWords檔案](https://developers.google.com/adwords/api/docs/guides/authentication)。

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

連接指定源，並包含該源的憑據。 每個Google AdWords帳戶只需要一個連線，因為它可用於建立多個來源連接器，以匯入不同的資料。

**API格式**

```https
POST /connections
```

**請求**

若要建立Google AdWords連線，其唯一連線規格ID必須作為POST要求的一部分提供。 Google AdWords的連線規格ID為 `221c7626-58f6-4eec-8ee2-042b0226f03b`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | 您AdWords帳戶的客戶客戶ID。 |
| `auth.params.developerToken` | 您AdWords帳戶的開發人員代號。 |
| `auth.params.refreshToken` | 您AdWords帳戶的重新整理Token。 |
| `auth.params.clientID` | 您AdWords帳戶的用戶端ID。 |
| `auth.params.clientSecret` | 您AdWords帳戶的客戶機密碼。 |
| `connectionSpec.id` | Google AdWords連線規格ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

在本教學課程中，您已使用Flow Service API建立Google AdWords連線，並取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，學習如何使 [用Flow Service API來探索廣告系統](../../explore/advertising.md)。
