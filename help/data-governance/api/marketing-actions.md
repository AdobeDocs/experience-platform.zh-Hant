---
keywords: Experience Platform;home；熱門主題；策略實施；行銷操作api；基於API的實施；資料治理
solution: Experience Platform
title: 行銷動作API端點
topic-legacy: developer guide
description: 在「Adobe Experience Platform資料治理」的背景下，行銷行動是Experience Platform資料消費者採取的行動，需要檢查是否違反資料使用策略。
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---

# 行銷動作端點

在Adobe Experience Platform[!DNL Data Governance]中的行銷動作是[!DNL Experience Platform]資料使用者採取的動作，需要檢查資料使用政策是否違規。

您可以使用原則服務API中的`/marketingActions`端點，管理組織的行銷動作。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 擷取行銷動作清單{#list}

您可以分別對`/marketingActions/core`或`/marketingActions/custom`提出GET請求，以擷取核心或自訂行銷動作的清單。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

下列請求會擷取您組織維護的自訂行銷動作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回每個擷取之行銷動作的詳細資料，包括其`name`和`href`。 `href`值用於在[建立資料使用原則](policies.md#create-policy)時識別行銷動作。

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
| `children` | 包含擷取之行銷動作詳細資料的物件陣列。 |
| `name` | 行銷動作的名稱，在[尋找特定行銷動作](#lookup)時，此名稱會當作其唯一識別碼。 |
| `_links.self.href` | 行銷動作的URI參考，當[建立資料使用原則](policies.md#create-policy)時，可用來完成`marketingActionsRefs`陣列。 |

## 查找特定行銷動作{#lookup}

您可以在請求路徑中加入行銷動作的`name`屬性，以查閱特定行銷動作的詳細資訊。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要尋找之行銷動作的`name`屬性。 |

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

回應物件包含行銷動作的詳細資訊，包括當[定義資料使用政策](policies.md#create-policy)(`marketingActionsRefs`)時參考行銷動作所需的路徑(`_links.self.href`)。

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

## 建立或更新自訂行銷動作{#create-update}

您可以建立新的自訂行銷動作，或更新現有的行銷動作，方法是將行銷動作的現有或預期名稱納入PUT請求的路徑。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立或更新之行銷動作的名稱。 如果系統中已存在具有提供名稱的行銷動作，則會更新該行銷動作。 如果不存在，則會為提供的名稱建立新的行銷動作。 |

**要求**

下列請求會建立名為`crossSiteTargeting`的新行銷動作，前提是系統中尚未有相同名稱的行銷動作。 如果`crossSiteTargeting`行銷動作確實存在，此呼叫會根據裝載中提供的屬性更新該行銷動作。

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
| `name` | 要建立或更新之行銷動作的名稱。 <br><br>**重要**:此屬性必須符合路 `{MARKETING_ACTION_NAME}` 徑中的，否則會發生HTTP 400（錯誤請求）錯誤。換言之，行銷動作一經建立，其`name`屬性便無法變更。 |
| `description` | 可選說明，提供行銷動作的進一步內容。 |

**回應**

成功的回應會傳回行銷動作的詳細資料。 如果已更新現有的行銷動作，回應會傳回HTTP狀態200（確定）。 如果建立了新的行銷動作，回應會傳回HTTP狀態201（已建立）。

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

## 刪除自訂行銷動作{#delete}

您可以將自訂行銷動作的名稱加入DELETE請求的路徑中，以刪除該動作。

>[!NOTE]
>
>無法刪除現有原則所參照的行銷動作。 嘗試刪除其中一個行銷動作，會導致HTTP 400（不當請求）錯誤，並產生訊息，其中包含參考行銷動作之所有原則的ID。

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

成功的回應會傳回HTTP狀態200(OK)，其回應內文為空白。

您可以嘗試[尋找行銷動作](#look-up)來確認刪除。 如果行銷動作已從系統移除，您應該會收到HTTP 404（找不到）錯誤。
