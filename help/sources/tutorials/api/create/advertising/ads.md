---
keywords: Experience Platform；首頁；熱門主題；google adwords;GoogleAdWords;adwords
solution: Experience Platform
title: 使用流服務API建立GoogleAdWords基連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到GoogleAdWords。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# 建立 [!DNL Google AdWords] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Google AdWords] 連接器位於beta中。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Google AdWords] (以下簡稱：[!DNL AdWords]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL AdWords] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL AdWords]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientCustomerId` | 客戶端客戶ID [!DNL AdWords] 帳戶。 |
| `developerToken` | 與管理器帳戶關聯的開發者令牌。 |
| `refreshToken` | 從獲取的刷新令牌 [!DNL Google] 授權訪問 [!DNL AdWords]。 |
| `clientId` | 的客戶端ID [!DNL Google] 用於獲取刷新令牌的應用程式。 |
| `clientSecret` | 客戶機密碼 [!DNL Google] 用於獲取刷新令牌的應用程式。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL AdWords] 為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

有關這些值的詳細資訊，請參閱 [GoogleAdWords文檔](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL AdWords] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL AdWords]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
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
| `auth.params.clientCustomerID` | 您的客戶端客戶ID [!DNL AdWords] 帳戶。 |
| `auth.params.developerToken` | 您的開發人員令牌 [!DNL AdWords] 帳戶。 |
| `auth.params.refreshToken` | 您的刷新令牌 [!DNL AdWords] 帳戶。 |
| `auth.params.clientID` | 您的客戶端ID [!DNL AdWords] 帳戶。 |
| `auth.params.clientSecret` | 你的客戶機密碼 [!DNL AdWords] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL Google AdWords] 連接規範ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Google AdWords] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/advertising.md)
