---
keywords: Experience Platform；首頁；熱門主題；行銷自動化
solution: Experience Platform
title: 使用流量服務API探索行銷自動化系統
description: 本教學課程使用Flow Service API來探索行銷自動化系統。
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 11%

---

# 使用[!DNL Flow Service] API探索行銷自動化系統

[!DNL Flow Service]用於收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。

此教學課程使用[!DNL Flow Service] API來探索行銷自動化系統。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至行銷自動化系統。

### 收集必要的認證

本教學課程需要您與您要擷取資料的協力廠商行銷自動化應用程式建立有效的連線。 有效的連線涉及您應用程式的連線規格ID和連線ID。 如需有關建立行銷自動化連線以及擷取這些值的詳細資訊，請參閱[將行銷自動化來源連線至Experience Platform](../../api/create/marketing-automation/hubspot.md)教學課程。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

## 探索您的資料表

使用行銷自動化系統的基礎連線，您可以透過執行GET請求來探索資料表。 使用以下呼叫來尋找您要檢查或擷取至[!DNL Experience Platform]的資料表的路徑。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 行銷自動化系統之基礎連線的ID。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應是來自行銷自動化系統的大量表格。 尋找您要帶入[!DNL Experience Platform]的資料表並記下其`path`屬性，因為您必須在下個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## 檢查表格的結構

若要從行銷自動化系統檢查表格結構，請在將表格路徑指定為查詢引數時執行GET要求。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 行銷自動化系統的連線ID。 |
| `{TABLE_PATH}` | 行銷自動化系統內的表格路徑。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回表格的結構。 有關每個資料表資料行的詳細資料位於`columns`陣列的元素中。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 後續步驟

依照本教學課程，您已探索您的行銷自動化系統，找到您要帶入[!DNL Experience Platform]的表格路徑，並取得有關其結構的資訊。 您可以在下個教學課程中使用此資訊，從行銷自動化系統[收集資料，並將其帶入Experience Platform](../collect/marketing-automation.md)。
