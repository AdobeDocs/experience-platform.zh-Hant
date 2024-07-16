---
keywords: Experience Platform；首頁；熱門主題；原則執行；行銷動作API；API型執行；資料治理
solution: Experience Platform
title: 行銷動作API端點
description: 在Adobe Experience Platform資料控管的內容中，行銷動作是Experience Platform資料消費者採取的動作，需要檢查其是否違反資料使用原則。
role: Developer
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---

# 行銷動作端點

在Adobe Experience Platform資料控管內容中的行銷動作是[!DNL Experience Platform]資料消費者採取的動作，需要檢查其是否違反資料使用原則。

您可以使用原則服務API中的`/marketingActions`端點來管理組織的行銷動作。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 擷取行銷動作清單 {#list}

您可以分別向`/marketingActions/core`或`/marketingActions/custom`發出GET要求，以擷取核心或自訂行銷動作清單。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

下列請求會擷取貴組織維護的自訂行銷動作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回每個已擷取行銷動作的詳細資料，包括其`name`和`href`。 `href`值是用來在[建立資料使用原則](policies.md#create-policy)時識別行銷動作。

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `children` | 一個物件陣列，其中包含已擷取行銷動作的詳細資訊。 |
| `name` | 行銷動作的名稱，在[查詢特定行銷動作](#lookup)時，做為其唯一識別碼。 |
| `_links.self.href` | 行銷動作的URI參考，當[建立資料使用原則](policies.md#create-policy)時，可用來完成`marketingActionsRefs`陣列。 |

## 查詢特定行銷動作 {#lookup}

您可以在GET要求的路徑中包含行銷動作的`name`屬性，以查閱特定行銷動作的詳細資料。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要查閱之行銷動作的`name`屬性。 |

**要求**

下列要求會擷取名為`combineData`的自訂行銷動作。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件包含行銷動作的詳細資料，包括在[定義資料使用原則](policies.md#create-policy) (`marketingActionsRefs`)時參考行銷動作所需的路徑(`_links.self.href`)。

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
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

您可以在PUT請求的路徑中包含行銷動作的現有或預期名稱，以建立新的自訂行銷動作或更新現有行銷動作。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立或更新之行銷動作的名稱。 如果系統中已存在具有所提供名稱的行銷動作，則會更新該行銷動作。 如果不存在，則會針對提供的名稱建立新的行銷動作。 |

**要求**

下列要求會建立名為`crossSiteTargeting`的新行銷動作，前提是系統中不存在相同名稱的行銷動作。 如果`crossSiteTargeting`行銷動作確實存在，此呼叫會根據承載中提供的屬性來更新該行銷動作。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立或更新之行銷動作的名稱。 <br><br>**重要**：此屬性必須符合路徑中的`{MARKETING_ACTION_NAME}`，否則會發生HTTP 400 （錯誤請求）錯誤。 換言之，一旦建立行銷動作，就無法變更其`name`屬性。 |
| `description` | 選用的說明，可提供行銷動作的進一步內容。 |

**回應**

成功的回應會傳回行銷動作的詳細資料。 如果更新了現有的行銷動作，回應會傳回HTTP狀態200 （確定）。 如果建立了新的行銷動作，回應會傳回HTTP狀態201 （已建立）。

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
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

您可以在DELETE請求的路徑中包含自訂行銷動作的名稱，以刪除該動作。

>[!NOTE]
>
>無法刪除現有原則參照的行銷動作。 嘗試刪除其中一個行銷動作將導致HTTP 400 （錯誤請求）錯誤以及包含參考行銷動作之所有原則ID的訊息。

**API格式**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要刪除的行銷動作名稱。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200 （確定），並帶有空白回應內文。

您可以嘗試[查詢行銷動作](#look-up)，以確認刪除。 如果行銷動作已從系統中移除，您應該會收到HTTP 404 （找不到）錯誤。
