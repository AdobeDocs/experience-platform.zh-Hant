---
keywords: Experience Platform；首頁；熱門主題；策略實施；市場營銷操作api；基於API的實施；資料治理
solution: Experience Platform
title: 市場營銷操作API終結點
description: 在「Adobe Experience Platform資料治理」的背景下，市場營銷行動是Experience Platform資料使用者採取的行動，需要檢查是否違反了資料使用策略。
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# 市場營銷操作終結點

在《Adobe Experience Platform資料治理》的背景下，營銷行動是一項 [!DNL Experience Platform] 資料使用者獲取的資料，需要檢查是否違反了資料使用策略。

您可以使用 `/marketingActions` 策略服務API中的終結點。

## 快速入門

本指南中使用的API端點是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 檢索市場營銷操作清單 {#list}

您可以通過發出GET請求來檢索核心或自定義市場營銷操作的清單 `/marketingActions/core` 或 `/marketingActions/custom`的下界。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**要求**

以下請求將檢索您的組織維護的自定義市場營銷操作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回每個檢索到的市場營銷操作的詳細資訊，包括其 `name` 和 `href`。 的 `href` 值用於在 [建立資料使用策略](policies.md#create-policy)。

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
| `_page.count` | 返回的市場營銷活動總數。 |
| `children` | 包含檢索到的市場營銷操作的詳細資訊的對象陣列。 |
| `name` | 市場營銷活動的名稱，在 [查找具體的營銷行動](#lookup)。 |
| `_links.self.href` | 市場營銷操作的URI引用，可用於完成 `marketingActionsRefs` 陣列 [建立資料使用策略](policies.md#create-policy)。 |

## 查找具體的營銷活動 {#lookup}

通過包括市場營銷活動的 `name` 屬性。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 的 `name` 要查找的市場營銷操作的屬性。 |

**要求**

以下請求檢索名為的自定義市場營銷操作 `combineData`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應對象包含市場營銷操作的詳細資訊，包括路徑(`_links.self.href`)需要參考市場推廣行動 [定義資料使用策略](policies.md#create-policy) (`marketingActionsRefs`)。

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

## 建立或更新自定義市場營銷活動 {#create-update}

您可以建立新的自定義市場營銷活動，或通過將市場營銷活動的現有或預期名稱包括在PUT請求的路徑中來更新現有的市場營銷活動。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立或更新的市場營銷操作的名稱。 如果系統中已存在具有提供名稱的市場營銷活動，則更新該市場營銷活動。 如果不存在，則為提供的名稱建立新的市場營銷操作。 |

**要求**

以下請求將建立名為 `crossSiteTargeting`，前提是系統中尚不存在同名的營銷操作。 如果 `crossSiteTargeting` 市場營銷操作確實存在，但此呼叫會根據負載中提供的屬性更新市場營銷操作。

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
| `name` | 要建立或更新的市場營銷操作的名稱。 <br><br>**重要**:此屬性必須與 `{MARKETING_ACTION_NAME}` 在路徑中，否則將出現HTTP 400（錯誤請求）錯誤。 換句話說，一旦建立了營銷活動， `name` 無法更改屬性。 |
| `description` | 可選說明，為市場營銷活動提供進一步的上下文。 |

**回應**

成功的響應將返回市場營銷操作的詳細資訊。 如果更新了現有的市場營銷操作，則響應將返回HTTP狀態200（確定）。 如果建立了新的市場營銷操作，則響應將返回HTTP狀態201（已建立）。

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

## 刪除自定義市場營銷操作 {#delete}

通過在DELETE請求的路徑中包含自定義市場營銷操作的名稱，可以刪除該操作。

>[!NOTE]
>
>無法刪除現有策略引用的市場營銷操作。 嘗試刪除這些市場營銷操作之一將導致HTTP 400（錯誤請求）錯誤，並導致包含引用市場營銷操作的所有策略的ID的消息。

**API格式**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要刪除的市場營銷操作的名稱。 |

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

成功的響應返回HTTP狀態200(OK)，返回的響應正文為空。

您可以通過嘗試 [查看營銷活動](#look-up)。 如果從系統中刪除了市場營銷操作，則應收到HTTP 404（未找到）錯誤。
