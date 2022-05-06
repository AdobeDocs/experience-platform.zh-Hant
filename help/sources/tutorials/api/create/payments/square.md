---
keywords: Experience Platform；首頁；熱門主題；方塊；方形
title: 使用流服務API建立方形基連接
description: 瞭解如何使用流服務API將Square連接到Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 建立 [!DNL Square] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Square] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個平台實例分區到單獨的虛擬環境中，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Square] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Square]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| --- | --- |
| `host` | 的URL [!DNL Square] 實例。 |
| `clientId` | 與您的 [!DNL Square] 帳戶。 |
| `clientSecret` | 與您的 [!DNL Square] 帳戶。 |
| `accessToken` | 訪問令牌用於驗證 [!DNL Square] OAuth 2.0身份驗證的帳戶。 可以從 [!DNL Square]。 |
| `refreshToken` | 刷新令牌用於在當前訪問令牌過期後生成新訪問令牌。 可從中獲取刷新令牌 [!DNL Square]。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Square] 為： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

有關這些憑據以及如何獲取這些憑據的詳細資訊，請參見 [[!DNL Square] OAuth文檔](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Square] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 的URL [!DNL Square] 實例。 |
| `auth.params.clientId` | 與您的 [!DNL Square] 帳戶。 |
| `auth.params.clientSecret` | 與您的 [!DNL Square] 帳戶。 |
| `auth.params.accessToken` | 訪問令牌用於驗證 [!DNL Square] OAuth 2.0身份驗證的帳戶。 可以從 [!DNL Square]。 |
| `auth.params.refreshToken` | 刷新令牌用於在當前訪問令牌過期後生成新訪問令牌。 可從中獲取刷新令牌 [!DNL Square]。 |
| `connectionSpec.id` | 的 [!DNL Square] 連接規範ID: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Square] 使用 [!DNL Flow Service] API，並已獲取連接的唯一ID值。 在學習如何 [使用流服務API瀏覽付款應用程式](../../explore/payments.md)。
