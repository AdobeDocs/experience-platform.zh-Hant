---
keywords: Experience Platform；主題；熱門主題；Microsoft動態；microsoft動態；動態
solution: Experience Platform
title: 使用流服務API建立MicrosoftDynamics基連接
type: Tutorial
description: 瞭解如何使用流服務API將平台連接到MicrosoftDynamics帳戶。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# 建立 [!DNL Microsoft Dynamics] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Microsoft Dynamics] (以下簡稱：[!DNL Dynamics]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL Dynamics]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUri` | 您的服務URL [!DNL Dynamics] 實例。 |
| `username` | 您的用戶名 [!DNL Dynamics] 用戶帳戶。 |
| `password` | 您的密碼 [!DNL Dynamics] 帳戶。 |
| `servicePrincipalId` | 您的客戶端ID [!DNL Dynamics] 帳戶。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| `servicePrincipalKey` | 服務主密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Dynamics] 為： `38ad80fe-8b06-4938-94f4-d4ee80266b07`。 |

有關入門的詳細資訊，請訪問 [這個 [!DNL Dynamics] 文檔](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Dynamics] 身份驗證憑據作為請求參數的一部分。

### 建立 [!DNL Dynamics] 基本連接使用基本認證

建立 [!DNL Dynamics] 基本連接使用基本身份驗證，向POST請求 [!DNL Flow Service] API，同時為連接提供值 `serviceUri`。 `username`, `password`。

**API格式**

```http
POST /connections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的 [!DNL Dynamics] 實例。 |
| `auth.params.username` | 與您的 [!DNL Dynamics] 帳戶。 |
| `auth.params.password` | 與您的 [!DNL Dynamics] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL Dynamics] 連接規範ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中瀏覽CRM系統需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 建立 [!DNL Dynamics] 使用服務主體基於密鑰的認證的基連接

建立 [!DNL Dynamics] 基連接使用基於服務主體密鑰的POST，向服務主體請求 [!DNL Flow Service] API，同時為連接提供值 `serviceUri`。 `servicePrincipalId`, `servicePrincipalKey`。

**API格式**

```http
POST /connections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的 [!DNL Dynamics] 實例。 |
| `auth.params.servicePrincipalId` | 您的客戶端ID [!DNL Dynamics] 帳戶。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| `auth.params.servicePrincipalKey` | 服務主密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |
| `connectionSpec.id` | 的 [!DNL Dynamics] 連接規範ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中瀏覽CRM系統需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Microsoft Dynamics] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/crm.md)
