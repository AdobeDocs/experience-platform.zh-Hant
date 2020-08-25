---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 行銷動作
topic: developer guide
translation-type: tm+mt
source-git-commit: 12c53122d84e145a699a2a86631dc37ee0073578
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 2%

---


# 行銷動作端點

Adobe Experience Platform中的行銷行動是資料消費者採取的 [!DNL Data Governance]行動， [!DNL Experience Platform] 需要檢查資料使用政策是否違規。

您可以使用原則服務API中的端點，來管 `/marketingActions` 理組織的行銷動作。

## 快速入門

本指南中使用的API端點是 [[!DNL Policy Service] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在繼續之前，請先閱讀快速入門 [指南](./getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 擷取行銷動作清單 {#list}

您可以分別對或提出GET請求，以擷取核心或自訂行銷 `/marketingActions/core` 動作 `/marketingActions/custom`的清單。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**請求**

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

成功的回應會傳回每個擷取之行銷動作的詳細資料，包括其 `name` 和 `href`。 此 `href` 值用於識別建立資料使用 [原則時的行銷動作](policies.md#create-policy)。

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
| `name` | 行銷動作的名稱，在尋找特定行銷動作時， [會當做其唯一識別碼](#lookup)。 |
| `_links.self.href` | 行銷動作的URI參考，可用於建立資料使 `marketingActionsRefs` 用原則 [時完成陣列](policies.md#create-policy)。 |

## 查看特定的行銷動作 {#lookup}

您可將行銷動作的屬性加入GET請求的路徑中， `name` 以查閱特定行銷動作的詳細資訊。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您 `name` 要尋找之行銷動作的屬性。 |

**請求**

下列請求會擷取名為的自訂行銷動作 `combineData`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件包含行銷動作的詳細資訊，包括定義資料使用政策(`_links.self.href`)時參考行銷 [動作所需的路徑](policies.md#create-policy) (`marketingActionsRefs`)。

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

您可以建立新的自訂行銷動作，或更新現有的行銷動作，方法是將行銷動作的現有或預期名稱加入PUT請求的路徑中。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立或更新之行銷動作的名稱。 如果系統中已存在具有提供名稱的行銷動作，則會更新該行銷動作。 如果不存在，則會為提供的名稱建立新的行銷動作。 |

**請求**

下列請求會建立名為的新行銷動作 `crossSiteTargeting`，但系統中尚不存在同名的行銷動作。 如果行 `crossSiteTargeting` 銷動作確實存在，此呼叫會根據裝載中提供的屬性更新該行銷動作。

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
| `name` | 要建立或更新之行銷動作的名稱。 <br><br>**重要**:此屬性必須符 `{MARKETING_ACTION_NAME}` 合路徑中的，否則會發生HTTP 400（錯誤請求）錯誤。 換言之，一旦建立了行銷動作，就無法變 `name` 更其屬性。 |
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

## 刪除自訂行銷動作 {#delete}

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

**請求**

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

您可以嘗試尋找行銷動 [作以確認刪除](#look-up)。 如果行銷動作已從系統移除，您應該會收到HTTP 404（找不到）錯誤。
