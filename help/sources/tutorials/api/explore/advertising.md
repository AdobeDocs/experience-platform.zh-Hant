---
keywords: Experience Platform；首頁；熱門主題；廣告系統；Advertising系統
solution: Experience Platform
title: 使用流量服務API探索Advertising系統
description: 流量服務是用來收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。 本教學課程使用Flow Service API來探索廣告系統。
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API探索廣告系統

建立基礎連線後，您現在可以使用唯一的基礎連線ID來導覽並探索來源的資料結構和內容。 這可讓您在建立資料流並將其帶到Adobe Experience Platform之前，識別特定專案及其各自的資料型別和格式。

此教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)來探索廣告系統。

## 快速入門

>[!IMPORTANT]
>
>本教學課程需要您擁有廣告來源的唯一基本連線ID。 如果您沒有此ID，請參閱有關[將廣告來源連線至Experience Platform](../../api/create/advertising/ads.md)的教學課程。

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至廣告系統。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../landing/api-guide.md)指南。

## 探索您的資料表

使用廣告系統的基本連線，您可以執行GET請求來探索資料表。 使用以下呼叫來尋找您要檢查或擷取至[!DNL Experience Platform]的資料表的路徑。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 廣告系統之基本連線的ID。 |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應是從到廣告系統的大量表格。 尋找您要帶入[!DNL Experience Platform]的資料表並記下其`path`屬性，因為您必須在下個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 檢查表格的結構

若要從廣告系統檢查表格的結構，請在將表格路徑指定為查詢引數時執行GET要求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 您的廣告系統的連線ID。 |
| `{TABLE_PATH}` | 廣告系統內的表格路徑。 |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
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
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## 後續步驟

依照本教學課程，您已探索您的廣告系統，找到您要帶入[!DNL Experience Platform]的表格路徑，並取得有關其結構的資訊。 您可以在下個教學課程中使用此資訊，從您的廣告系統[收集資料並將其帶入Experience Platform](../collect/advertising.md)。
