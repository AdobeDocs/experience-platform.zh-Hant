---
keywords: Experience Platform；首頁；熱門主題；資料治理；資料使用標籤api；策略服務api
solution: Experience Platform
title: '使用API管理資料使用標籤 '
topic: developer guide
description: 資料集服務API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的目錄服務API不同。
translation-type: tm+mt
source-git-commit: 4e75e3fbdcd480c384411c2f33bad5b2cdcc5c42
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---


# 使用API管理資料使用標籤

本檔案提供如何使用[!DNL Policy Service] API和[!DNL Dataset Service] API管理資料使用標籤的步驟。

[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)提供數個端點，可讓您為組織建立和管理資料使用標籤。

[!DNL Dataset Service] API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的[!DNL Catalog Service] API不同。

## 快速入門

在閱讀本指南之前，請依照目錄開發人員指南中[快速入門章節](../../catalog/api/getting-started.md)中概述的步驟，收集必要的認證以呼叫[!DNL Platform] API。

為了對本文檔中概述的[!DNL Dataset Service]端點進行調用，您必須具有特定資料集的唯一`id`值。 如果沒有此值，請參見[上列出目錄對象](../../catalog/api/list-objects.md)的指南，以查找現有資料集的ID。

## 列出所有標籤{#list-labels}

使用[!DNL Policy Service] API，您可以分別向`/labels/core`或`/labels/custom`發出GET請求，列出所有`core`或`custom`標籤。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**請求**

下列請求會列出您組織下建立的所有自訂標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回從系統檢索到的自定義標籤清單。 由於上述範例要求是對`/labels/custom`所做，因此下方的回應只會顯示自訂標籤。

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## 查找標籤{#look-up-label}

您可以在[!DNL Policy Service] API的GET請求路徑中加入該標籤的`name`屬性，以尋找特定標籤。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 您要查找的自訂標籤的`name`屬性。 |

**請求**

下列請求會擷取自訂標籤`L2`，如路徑所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回自訂標籤的詳細資訊。

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
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

## 建立或更新自訂標籤{#create-update-label}

若要建立或更新自訂標籤，您必須向[!DNL Policy Service] API提出PUT要求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 自訂標籤的`name`屬性。 如果沒有具有此名稱的自訂標籤，則會建立新標籤。 如果存在，則會更新該標籤。 |

**請求**

下列請求會建立新標籤`L3`，其目的在於說明包含客戶所選付款計畫相關資訊的資料。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 標籤的唯一字串識別碼。 此值用於查閱，並將標籤套用至資料集和欄位，因此建議使用它簡短且簡明。 |
| `category` | 標籤的類別。 雖然您可以為自訂標籤建立自己的類別，但強烈建議您使用`Custom`（如果您希望標籤顯示在UI中）。 |
| `friendlyName` | 標籤的好記名稱，用於顯示用途。 |
| `description` | （可選）標籤的說明，以提供更多內容。 |

**回應**

成功的回應會傳回自訂標籤的詳細資訊，如果已更新現有標籤，HTTP程式碼為200（確定）；如果已建立新標籤，則傳回201（已建立）。

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

## 查找資料集{#look-up-dataset-labels}的標籤

您可以向[!DNL Dataset Service] API提出GET請求，以查找已應用到現有資料集的資料使用標籤。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要尋找其標籤的資料集的唯一`id`值。 |

**請求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回已套用至資料集的資料使用標籤。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `labels` | 已套用至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集內已套用資料使用標籤的個別欄位清單。 需要下列子屬性：<br/><br/>`option`:包含欄位[!DNL Experience Data Model](XDM)屬性的對象。 需要下列三個屬性：<ul><li>`id`:與欄位 `$id` 關聯的架構的URI值。</li><li>`contentType`:指示方案的格式和版本。如需詳細資訊，請參閱XDM API指南中有關[架構版本控制](../../xdm/api/getting-started.md#versioning)的章節。</li><li>`schemaPath`:相關結構屬性的路徑，以 [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersyntax撰寫。</li></ul>`labels`:您要新增至欄位的資料使用標籤清單。 |

- id:資料集所依據之XDM架構的URI $id值。
- contentType:指示方案的格式和版本。 如需詳細資訊，請參閱XDM API指南中有關[架構版本控制](../../xdm/api/getting-started.md#versioning)的章節。
- schemaPath:相關架構屬性的路徑，以[JSON Pointer](../../landing/api-fundamentals.md#json-pointer)語法編寫。

## 將標籤套用至資料集{#apply-dataset-labels}

您可以在POST或PUT請求的裝載中提供標籤給[!DNL Dataset Service] API，為資料集建立標籤集。 使用其中一種方法會覆寫任何現有的標籤，並以裝載中提供的標籤來取代標籤。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您正在為其建立標籤的資料集的唯一`id`值。 |

**請求**

下列POST請求會將一系列標籤新增至資料集，以及該資料集內的特定欄位。 裝載中提供的欄位與PUT要求所需的欄位相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `labels` | 您要新增至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中您想新增標籤的任何個別欄位清單。 此陣列中的每個項目都必須具有以下屬性：<br/><br/>`option`:包含欄位[!DNL Experience Data Model](XDM)屬性的對象。 需要下列三個屬性：<ul><li>`id`:與欄位 `$id` 關聯的架構的URI值。</li><li>`contentType`:指示方案的格式和版本。如需詳細資訊，請參閱XDM API指南中有關[架構版本控制](../../xdm/api/getting-started.md#versioning)的章節。</li><li>`schemaPath`:相關結構屬性的路徑，以 [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersyntax撰寫。</li></ul>`labels`:您要新增至欄位的資料使用標籤清單。 |

**回應**

成功的回應會傳回已新增至資料集的標籤。

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

## 從資料集{#remove-dataset-labels}移除標籤

您可以對[!DNL Dataset Service] API提出DELETE請求，以移除套用至資料集的標籤。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要移除其標籤的資料集的唯一`id`值。 |

**請求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應HTTP狀態200（確定），表示標籤已移除。 您可以在個別呼叫中，[尋找資料集的現有標籤](#look-up-dataset-labels)以確認此點。

## 後續步驟

閱讀本檔案後，您便瞭解如何使用API管理資料使用標籤。

在資料集和欄位層級新增資料使用標籤後，您就可以開始將資料內嵌至[!DNL Experience Platform]。 若要進一步瞭解，請先閱讀[資料擷取檔案](../../ingestion/home.md)。

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱[資料使用政策概述](../policies/overview.md)。

有關在[!DNL Experience Platform]中管理資料集的詳細資訊，請參見[資料集概述](../../catalog/datasets/overview.md)。