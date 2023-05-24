---
keywords: Experience Platform；首頁；熱門主題；ServiceNow;ServiceNow
solution: Experience Platform
title: 使用流服務API建立ServiceNow基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到ServiceNow伺服器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 建立 [!DNL ServiceNow] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Google ServiceNow] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接到 [!DNL ServiceNow] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL ServiceNow]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | 的端點 [!DNL ServiceNow] 伺服器。 |
| `username` | 用於連接到 [!DNL ServiceNow] 伺服器進行身份驗證。 |
| `password` | 連接到的密碼 [!DNL ServiceNow] 伺服器進行身份驗證。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL ServiceNow] 為： `eb13cb25-47ab-407f-ba89-c0125281c563`。 |

有關入門的詳細資訊，請參閱 [此ServiceNow文檔](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL ServiceNow] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL ServiceNow]:

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.server` | 您的終結點 [!DNL ServiceNow] 伺服器。 |
| `auth.params.username` | 用於連接到 [!DNL ServiceNow] 伺服器進行身份驗證。 |
| `auth.params.password` | 連接到的密碼 [!DNL ServiceNow] 伺服器進行身份驗證。 |
| `connectionSpec.id` | 的 [!DNL ServiceNow] 連接規範ID: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中瀏覽CRM系統需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL ServiceNow] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/customer-success.md)
