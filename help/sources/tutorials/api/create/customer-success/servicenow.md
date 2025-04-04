---
keywords: Experience Platform；首頁；熱門主題；servicenow；ServiceNow
solution: Experience Platform
title: 使用Flow Service API建立ServiceNow基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至ServiceNow伺服器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL ServiceNow]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Google ServiceNow]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL ServiceNow]伺服器。

### 收集必要的認證

為了讓[!DNL Flow Service]連線到[!DNL ServiceNow]，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow]伺服器的端點。 |
| `username` | 用來連線至[!DNL ServiceNow]伺服器以進行驗證的使用者名稱。 |
| `password` | 連線到[!DNL ServiceNow]伺服器以進行驗證的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL ServiceNow]的連線規格識別碼為： `eb13cb25-47ab-407f-ba89-c0125281c563`。 |

如需開始使用的詳細資訊，請參閱[此ServiceNow檔案](https://developer.servicenow.com/app.do#!/rest_api_doc？v=newyork&amp;id=r_TableAPI-GET)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL ServiceNow]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL ServiceNow]的基礎連線：

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
| `auth.params.server` | [!DNL ServiceNow]伺服器的端點。 |
| `auth.params.username` | 用來連線至[!DNL ServiceNow]伺服器以進行驗證的使用者名稱。 |
| `auth.params.password` | 連線到[!DNL ServiceNow]伺服器以進行驗證的密碼。 |
| `connectionSpec.id` | [!DNL ServiceNow]連線規格識別碼： `eb13cb25-47ab-407f-ba89-c0125281c563` |

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL ServiceNow]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流，將客戶成功資料匯入Experience Platform](../../collect/customer-success.md)
