---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 行銷動作
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---


# 行銷動作

在Adobe Experience Platform資料治理範圍內的行銷行動，是資料消費者採取的行動，需要檢查是否有違反資料使用政策的行為。 [!DNL Experience Platform]

在API中處理行銷動作時，您必須使用端 `/marketingActions` 點。

## 列出所有行銷動作

若要檢視所有行銷動作的清單，您可以向指定容器提出GET `/marketingActions/core` 要求 `/marketingActions/custom` ，或傳回指定容器的所有原則。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**請求**

下列請求會傳回由IMS組織定義之所有自訂行銷動作的清單。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件提供容器(`count`)中的行銷動作總數，而陣列包含每個行銷動作的詳細資料，包括 `children` 行銷動 `name``href` 作的和。 建立資料使`_links.self.href`用策略時，此路徑( `marketingActionsRefs` )用 [於完成陣列](policies.md#create-policy)。

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
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

## 查看特定的行銷動作

您也可以執行查閱(GET)請求，以檢視特定行銷動作的詳細資訊。 這是使用行銷 `name` 動作來完成。 如果名稱未知，則可使用先前顯示的清單(GET)請求找到名稱。

**API格式**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件包含行銷動作的詳細資訊，包括定義資料使用政策(`_links.self.href`)時參考行銷動作所需的路徑(`marketingActionsRefs`)。

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

## 建立或更新行銷動作

API [!DNL Policy Service] 可讓您定義自己的行銷動作，並更新現有的行銷動作。 建立和更新都是使用PUT作業來建立行銷動作名稱。

**API格式**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**請求**

在後續的請求中，請注意 `name` 請求裝載中的與API呼叫 `{marketingActionName}` 中的相同。 與唯 `id` 讀和系統產生的原則不同，建立行銷動作需要您在建立行銷動作時 __ ，提供預期的行銷動作名稱。

>[!NOTE] 無法在呼叫 `{marketingActionName}` 中提供，將導致405錯誤（不允許使用方法），因為您不允許直接對端點執行PUT `/marketingActions/custom` 。 此外，如果 `name` 裝載中的不符合路徑中 `{marketingActionName}` 的，您會收到400錯誤（錯誤請求）。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**回應**

如果成功建立，您會收到HTTP狀態201（已建立），回應主體將包含新建立之行銷動作的詳細資訊。 回 `name` 應中的應符合在請求中傳送的內容。

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

## 刪除行銷動作

您可以將DELETE請求傳送至您要移除的行銷 `{marketingActionName}` 動作，以刪除行銷動作。

>[!NOTE] 您無法刪除現有政策所參照的行銷動作。 嘗試這麼做會產生400錯誤（錯誤請求），並出現錯誤訊息，其中包含任何原則（或原則）的 `id` （或多個ID），其中包含您嘗試刪除之行銷動作的參考。

**API格式**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**請求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

如果行銷動作已成功刪除，則回應內文將會空白，並顯示HTTP狀態200（確定）。

您可以嘗試查閱(GET)行銷動作，以確認刪除。 您應會收到HTTP狀態404（找不到）以及「找不到」錯誤訊息，因為行銷動作已移除。
