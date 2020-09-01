---
keywords: Experience Platform;home;popular topics;google adwords;Google AdWords;adwords
solution: Experience Platform
title: 使用Flow Service API建立Google AdWords連接器
topic: overview
description: 本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Google AdWords的步驟。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---


# 使用 [!DNL Google AdWords] API建立連 [!DNL Flow Service] 接器

>[!NOTE]
>
>連接 [!DNL Google AdWords] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至的 [!DNL Experience Platform] 步驟 [!DNL Google AdWords]。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 [!DNL Flow Service] API成功連線至廣告。

### 收集必要的認證

若要連 [!DNL Flow Service] 接AdWords，您必須提供下列連線屬性的值：

| **憑證** | **說明** |
| -------------- | --------------- |
| 客戶客戶ID | AdWords帳戶的客戶客戶ID。 |
| 開發人員Token | 與管理員帳戶關聯的開發人員Token。 |
| 重新整理Token | 從授權存取AdWords [!DNL Google] 所取得的重新整理Token。 |
| 用戶端ID | 用於取得重新整理 [!DNL Google] Token之應用程式的用戶端ID。 |
| 用戶端密碼 | 用來取得重新整理Token [!DNL Google] 之應用程式的用戶端密碼。 |
| 連接規範ID | 建立連線所需的唯一識別碼。 的連接規範ID [!DNL Google AdWords] 為： `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

如需這些值的詳細資訊，請參閱此 [Google AdWords檔案](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個帳戶只需要一個連 [!DNL Google AdWords] 接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```https
POST /connections
```

**請求**

下列請求會建立新的AdWords連線，由裝載中提供的屬性設定：


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
| `auth.params.clientCustomerID` | 您帳戶的客戶客戶ID [!DNL AdWords] 。 |
| `auth.params.developerToken` | 您帳戶的開發人員 [!DNL AdWords] 代號。 |
| `auth.params.refreshToken` | 您帳戶的重新整理 [!DNL AdWords] Token。 |
| `auth.params.clientID` | 您帳戶的用戶端 [!DNL AdWords] ID。 |
| `auth.params.clientSecret` | 您帳戶的客戶機 [!DNL AdWords] 密碼。 |
| `connectionSpec.id` | 連 [!DNL Google AdWords] 接規範ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

在本教學課程中，您已使 [!DNL Google AdWords] 用 [!DNL Flow Service] API建立連線，並取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，學習如何使 [用Flow Service API來探索廣告系統](../../explore/advertising.md)。
