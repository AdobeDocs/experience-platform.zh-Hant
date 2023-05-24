---
keywords: Experience Platform；首頁；熱門主題；資料管理；資料使用標籤api；策略服務api
solution: Experience Platform
title: 使用API管理資料使用標籤
description: 資料集服務API允許您應用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的目錄服務API是分開的。
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# 使用API管理資料使用標籤

本文檔提供了有關如何使用 [!DNL Policy Service] API和 [!DNL Dataset Service] API。

的 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 提供了多個端點，允許您為組織建立和管理資料使用標籤。

的 [!DNL Dataset Service] API允許您應用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與 [!DNL Catalog Service] 管理資料集元資料的API。

## 快速入門

在閱讀本指南之前，請遵循中概述的步驟 [入門部分](../../catalog/api/getting-started.md) 在目錄開發人員指南中，收集調用所需的憑據 [!DNL Platform] API。

為了呼叫 [!DNL Dataset Service] 本文檔中概述的端點，必須具有唯一性 `id` 特定資料集的值。 如果沒有此值，請參閱上的指南 [列出目錄對象](../../catalog/api/list-objects.md) 查找現有資料集的ID。

## 列出所有標籤 {#list-labels}

使用 [!DNL Policy Service] API，您可以列出所有 `core` 或 `custom` 標籤：發出GET請求 `/labels/core` 或 `/labels/custom`的下界。

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

## 查找標籤 {#look-up-label}

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

## 建立或更新自定義標籤 {#create-update-label}

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

## 查找資料集的標籤 {#look-up-dataset-labels}

通過向Web站點發出GET請求，您可以查找已應用到現有資料集的資料使用標籤 [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 獨特 `id` 要查找其標籤的資料集的值。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回已應用到資料集的資料使用標籤。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `labels` | 已應用到資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中具有應用資料使用標籤的各個欄位的清單。 需要以下子屬性：<br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)欄位的屬性。 需要以下三個屬性：<ul><li>`id`:URI `$id` 與欄位關聯的架構的值。</li><li>`contentType`:指示架構的格式和版本。 請參閱 [架構版本](../../xdm/api/getting-started.md#versioning) 的子菜單。</li><li>`schemaPath`:有關的架構屬性的路徑，寫入 [JSON指針](../../landing/api-fundamentals.md#json-pointer) 語法。</li></ul>`labels`:要添加到欄位的資料使用標籤清單。 |

- id:資料集所基於的XDM架構的URI $id值。
- 內容類型：指示架構的格式和版本。 請參閱 [架構版本](../../xdm/api/getting-started.md#versioning) 的子菜單。
- schemaPath:有關的架構屬性的路徑，寫入 [JSON指針](../../landing/api-fundamentals.md#json-pointer) 語法。

## 將標籤應用於資料集 {#apply-dataset-labels}

通過將標籤提供到POST或PUT請求的負載中，可以為資料集建立一組標籤 [!DNL Dataset Service] API。 使用這些方法中的任一方法覆蓋任何現有標籤，並用負載中提供的標籤替換它們。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 獨特 `id` 要為其建立標籤的資料集的值。 |

**要求**

以下POST請求將一系列標籤添加到資料集以及該資料集中的特定欄位。 負載中提供的欄位與PUT請求所需的欄位相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `labels` | 要添加到資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中要向其添加標籤的任何單個欄位的清單。 此陣列中的每個項都必須具有以下屬性：<br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)欄位的屬性。 需要以下三個屬性：<ul><li>`id`:URI `$id` 與欄位關聯的架構的值。</li><li>`contentType`:指示架構的格式和版本。 請參閱 [架構版本](../../xdm/api/getting-started.md#versioning) 的子菜單。</li><li>`schemaPath`:有關的架構屬性的路徑，寫入 [JSON指針](../../landing/api-fundamentals.md#json-pointer) 語法。</li></ul>`labels`:要添加到欄位的資料使用標籤清單。 |

**回應**

成功的響應返回已添加到資料集的標籤。

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## 從資料集中刪除標籤 {#remove-dataset-labels}

可以通過向Web站點發出DELETE請求來刪除應用於資料集的標籤 [!DNL Dataset Service] API。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 獨特 `id` 要刪除其標籤的資料集的值。 |

**要求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應HTTP狀態200(OK)，表示標籤已被刪除。 你可以 [查找現有標籤](#look-up-dataset-labels) 以確認此情況。

## 後續步驟

通過閱讀此文檔，您已學會了如何使用API管理資料使用標籤。

在資料集和欄位級別添加資料使用標籤後，您就可以開始將資料插入 [!DNL Experience Platform]。 要瞭解更多資訊，請從閱讀 [資料攝取文檔](../../ingestion/home.md)。

您現在還可以根據已應用的標籤定義資料使用策略。 有關詳細資訊，請參見 [資料使用策略概述](../policies/overview.md)。

有關在中管理資料集的詳細資訊 [!DNL Experience Platform]，請參見 [資料集概述](../../catalog/datasets/overview.md)。