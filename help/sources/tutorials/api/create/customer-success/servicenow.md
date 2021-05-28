---
keywords: Experience Platform；首頁；熱門主題；servicenow;ServiceNow
solution: Experience Platform
title: 使用流服務API建立ServiceNow源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至ServiceNow伺服器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL ServiceNow]源連接

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API引導您完成將[!DNL Experience Platform]連接到[!DNL ServiceNow]伺服器的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL ServiceNow]伺服器。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL ServiceNow]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow]伺服器的端點。 |
| `username` | 用於連接到[!DNL ServiceNow]伺服器進行身份驗證的用戶名。 |
| `password` | 連接到[!DNL ServiceNow]伺服器以進行身份驗證的密碼。 |

有關入門的詳細資訊，請參閱[此ServiceNow文檔](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL ServiceNow]帳戶只需一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

若要建立[!DNL ServiceNow]連線，必須在POST請求中提供其唯一連線規格ID。 [!DNL ServiceNow]的連接規範ID為`eb13cb25-47ab-407f-ba89-c0125281c563`。

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

| 屬性 | 說明 |
| ------------- | --------------- |
| `auth.params.server` | [!DNL ServiceNow]伺服器的端點。 |
| `auth.params.username` | 用於連接到[!DNL ServiceNow]伺服器進行身份驗證的用戶名。 |
| `auth.params.password` | 連接到[!DNL ServiceNow]伺服器以進行身份驗證的密碼。 |
| `connectionSpec.id` | 與[!DNL ServiceNow]關聯的連接規範ID。 |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個步驟中探索您的CRM系統時需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL ServiceNow]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/customer-success.md)探索客戶成功系統時，您可以在下一個教學課程中使用此連線ID。[
