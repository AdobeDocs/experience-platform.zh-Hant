---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 標籤API終結點
description: 瞭解如何使用策略服務API在Experience Platform中管理資料使用標籤。
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# 標籤端點

資料使用標籤允許您根據可能應用於該資料的使用策略對資料進行分類。 的 `/labels` 端點 [!DNL Policy Service API] 允許您以寫程式方式管理體驗應用程式中的資料用法標籤。

>[!NOTE]
>
>的 `/labels` 終結點僅用於檢索、建立和更新資料使用標籤。 有關如何使用API調用將標籤添加到資料集和欄位的步驟，請參閱上的指南 [管理資料集標籤](../labels/dataset-api.md)。

## 快速入門

本指南中使用的API終結點是 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 檢索標籤清單 {#list}

您可以列出所有 `core` 或 `custom` 標籤：發出GET請求 `/labels/core` 或 `/labels/custom`的下界。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**要求**

以下請求列出在您的組織下建立的所有自定義標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回從系統檢索到的自定義標籤的清單。 由於上面的示例請求是 `/labels/custom`，下面的響應僅顯示自定義標籤。

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## 查找標籤 {#look-up}

您可以通過包含該標籤來查找特定標籤 `name` GET請求到的路徑中的屬性 [!DNL Policy Service] API。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 的 `name` 要查找的自定義標籤的屬性。 |

**要求**

以下請求檢索自定義標籤 `L2`，如路徑中所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回自定義標籤的詳細資訊。

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## 建立或更新自定義標籤 {#create-update}

要建立或更新自定義標籤，必須向 [!DNL Policy Service] API。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 的 `name` 自定義標籤的屬性。 如果不存在具有此名稱的自定義標籤，則將建立新標籤。 如果確實存在，則將更新該標籤。 |

**要求**

以下請求將建立新標籤， `L3`，用於描述包含與客戶選定付款計畫相關資訊的資料。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 標籤的唯一字串標識符。 此值用於查找目的並將標籤應用於資料集和欄位，因此建議它簡短而簡潔。 |
| `category` | 標籤的類別。 雖然您可以為自定義標籤建立自己的類別，但強烈建議您使用 `Custom` 的子菜單。 |
| `friendlyName` | 用於顯示目的的標籤的友好名稱。 |
| `description` | （可選）標籤的說明，以提供更多上下文。 |

**回應**

成功的響應將返回自定義標籤的詳細資訊，如果更新了現有標籤，則HTTP代碼為200(OK)；如果建立了新標籤，則返回201（已建立）。

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## 後續步驟

本指南介紹了 `/labels` 策略服務API中的終結點。 有關如何將標籤應用於資料集和欄位的步驟，請參閱 [資料集標籤API指南](../labels/dataset-api.md)。
