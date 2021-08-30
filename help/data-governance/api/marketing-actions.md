---
keywords: Experience Platform；首頁；熱門主題；政策實作；行銷動作api;API型實作；資料控管
solution: Experience Platform
title: 行銷動作API端點
topic-legacy: developer guide
description: 在Adobe Experience Platform資料控管的情境下，行銷動作是Experience Platform資料使用者採取的動作，需要檢查是否有違反資料使用原則的行為。
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# 行銷動作端點

在Adobe Experience Platform [!DNL Data Governance]內容中的行銷動作是[!DNL Experience Platform]資料使用者採取的動作，需要檢查是否有違反資料使用原則的情況。

您可以使用原則服務API中的`/marketingActions`端點來管理貴組織的行銷動作。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需的重要標題資訊。

## 擷取行銷動作清單 {#list}

您可以分別向`/marketingActions/core`或`/marketingActions/custom`發出GET要求，以擷取核心或自訂行銷動作清單。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

下列請求會擷取您組織所維護的自訂行銷動作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回每個擷取行銷動作的詳細資訊，包括`name`和`href`。 `href`值用於在[建立資料使用原則時識別行銷動作](policies.md#create-policy)。

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `_page.count` | 傳回的行銷動作總數。 |
| `children` | 包含所擷取行銷動作詳細資訊的物件陣列。 |
| `name` | 行銷動作的名稱，在[查詢特定行銷動作時作為其唯一識別碼](#lookup)。 |
| `_links.self.href` | 行銷動作的URI參考，當[建立資料使用原則](policies.md#create-policy)時，可用來完成`marketingActionsRefs`陣列。 |

## 查詢特定的行銷動作 {#lookup}

您可以在GET請求的路徑中加入行銷動作的`name`屬性，以查詢特定行銷動作的詳細資訊。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要查詢之行銷動作的`name`屬性。 |

**要求**

下列請求會擷取名為`combineData`的自訂行銷動作。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件包含行銷動作的詳細資訊，包括定義資料使用政策](policies.md#create-policy)(`marketingActionsRefs`)時參考行銷動作所需的路徑(`_links.self.href`)。[

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## 建立或更新自訂行銷動作 {#create-update}

您可以在PUT請求的路徑中加入行銷動作的現有或預期名稱，以建立新的自訂行銷動作或更新現有的行銷動作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立或更新的行銷動作名稱。 如果系統中已存在具有提供名稱的行銷動作，則會更新該行銷動作。 如果不存在，則會為提供的名稱建立新的行銷動作。 |

**要求**

如果系統中尚未存在相同名稱的行銷動作，以下請求會建立名為`crossSiteTargeting`的新行銷動作。 如果`crossSiteTargeting`行銷動作確實存在，則此呼叫會改為根據裝載中提供的屬性更新該行銷動作。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立或更新的行銷動作名稱。 <br><br>**重要**:此屬性必須符 `{MARKETING_ACTION_NAME}` 合路徑中的，否則會發生HTTP 400(Bad Request)錯誤。換言之，一旦建立行銷動作後，其`name`屬性便無法變更。 |
| `description` | 可選的說明，可提供行銷動作的進一步內容。 |

**回應**

成功的回應會傳回行銷動作的詳細資訊。 如果更新了現有的行銷動作，回應會傳回HTTP狀態200（確定）。 如果已建立新的行銷動作，回應會傳回HTTP狀態201（已建立）。

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## 刪除自訂行銷動作 {#delete}

您可以在DELETE請求的路徑中加入自訂行銷動作名稱，以刪除自訂行銷動作。

>[!NOTE]
>
>無法刪除現有策略引用的行銷操作。 嘗試刪除其中一個行銷動作會導致HTTP 400(Bad Request)錯誤，以及包含參考行銷動作之所有原則ID的訊息。

**API格式**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要刪除之行銷動作的名稱。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200(OK)，並帶有空白回應內文。

您可以嘗試[查詢行銷動作](#look-up)以確認刪除。 如果從系統移除行銷動作，您應該會收到HTTP 404（找不到）錯誤。
