---
keywords: Experience Platform;home;popular topics;google adwords;Google AdWords;adwords
solution: Experience Platform
title: 使用Flow Service API建立Google AdWords連接器
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將Experience Platform連接至Google AdWords的步驟。
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API建立[!DNL Google AdWords]連接器

>[!NOTE]
>
>[!DNL Google AdWords]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至[!DNL Google AdWords]的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至廣告。

### 收集必要的認證

要使[!DNL Flow Service]與AdWords連接，您必須為以下連接屬性提供值：

| **憑證** | **說明** |
| -------------- | --------------- |
| 客戶客戶ID | AdWords帳戶的客戶客戶ID。 |
| 開發人員Token | 與管理員帳戶關聯的開發人員Token。 |
| 重新整理Token | 從[!DNL Google]取得的重新整理Token，用於授權存取AdWords。 |
| 用戶端ID | 用於獲取刷新Token的[!DNL Google]應用程式的客戶端ID。 |
| 用戶端密碼 | 用於獲取刷新令牌的[!DNL Google]應用程式的客戶機密碼。 |
| 連接規範ID | 建立連線所需的唯一識別碼。 [!DNL Google AdWords]的連接規範ID為：`d771e9c1-4f26-40dc-8617-ce58c4b53702` |

如需這些值的詳細資訊，請參閱此[Google AdWords檔案](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Google AdWords]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```https
POST /connections
```

**請求**

要建立[!DNL Google AdWords]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Google AdWords]的連接規範ID為`d771e9c1-4f26-40dc-8617-ce58c4b53702`。

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
| `auth.params.clientCustomerID` | [!DNL AdWords]帳戶的客戶客戶ID。 |
| `auth.params.developerToken` | [!DNL AdWords]帳戶的開發人員Token。 |
| `auth.params.refreshToken` | [!DNL AdWords]帳戶的重新整理Token。 |
| `auth.params.clientID` | [!DNL AdWords]帳戶的用戶端ID。 |
| `auth.params.clientSecret` | [!DNL AdWords]帳戶的客戶機密碼。 |
| `connectionSpec.id` | [!DNL Google AdWords]連接規範ID:`d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時，需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Google AdWords]連接，並獲取了該連接的唯一ID值。 您可在下一個教學課程中使用此ID，同時學習如何使用Flow Service API[來探索廣告系統。](../../explore/advertising.md)
