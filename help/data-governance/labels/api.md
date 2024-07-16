---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api
solution: Experience Platform
title: 使用API管理資料使用標籤
description: 資料集服務API可讓您套用及編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 2%

---


# 使用API管理資料使用標籤

本檔案提供如何使用[!DNL Policy Service] API和[!DNL Dataset Service] API管理資料使用標籤的步驟。

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)提供數個端點，可讓您建立和管理組織的資料使用標籤。

[!DNL Dataset Service] API可讓您套用及編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的[!DNL Catalog Service] API不同。

## 快速入門

在閱讀本指南之前，請依照目錄開發人員指南的[快速入門區段](../../catalog/api/getting-started.md)中概述的步驟，收集呼叫[!DNL Platform] API所需的認證。

若要呼叫本檔案中概述的[!DNL Dataset Service]端點，您必須具有特定資料集的唯一`id`值。 如果您沒有這個值，請參閱[目錄物件清單](../../catalog/api/list-objects.md)上的指南，以尋找現有資料集的ID。

## 列出所有標籤 {#list-labels}

使用[!DNL Policy Service] API，您可以分別向`/labels/core`或`/labels/custom`發出GET要求，列出所有`core`或`custom`標籤。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**要求**

以下請求列出在您的組織下建立的所有自訂標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回從系統擷取的自訂標籤清單。 由於上述範例要求是向`/labels/custom`發出，因此下列回應只會顯示自訂標籤。

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

## 查詢標籤 {#look-up-label}

您可以在[!DNL Policy Service] API的GET要求路徑中包含該標籤的`name`屬性，以查詢特定標籤。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 您要查閱之自訂標籤的`name`屬性。 |

**要求**

下列要求會擷取自訂標籤`L2`，如路徑中所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回自訂標籤的詳細資料。

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

## 建立或更新自訂標籤 {#create-update-label}

若要建立或更新自訂標籤，您必須向[!DNL Policy Service] API發出PUT要求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 自訂標籤的`name`屬性。 如果使用此名稱的自訂標籤不存在，則會建立新標籤。 如果標籤確實存在，則會更新該標籤。 |

**要求**

下列請求會建立新標籤`L3`，此標籤旨在說明包含與客戶所選付款計畫相關資訊的資料。

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
| `name` | 適用於標籤的唯一字串識別碼。 此值用於查詢目的，並將標籤套用至資料集和欄位，因此建議該值簡短明瞭。 |
| `category` | 標籤的類別。 雖然您可以建立自己的自訂標籤類別，但如果您想要標籤顯示在UI中，強烈建議您使用`Custom`。 |
| `friendlyName` | 標籤的易記名稱，用於顯示目的。 |
| `description` | （選用）標籤說明，提供更多相關情境。 |

**回應**

成功的回應會傳回自訂標籤的詳細資料，如果更新現有標籤，則傳回HTTP代碼為200 （確定），如果建立新標籤，則傳回201 （建立）。

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

## 查詢資料集的標籤 {#look-up-dataset-labels}

您可以向[!DNL Dataset Service] API發出GET要求，查詢已套用至現有資料集的資料使用標籤。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其標籤的資料集的唯一`id`值。 |

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

成功的回應會傳回已套用至資料集的資料使用標籤。

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
| `labels` | 已套用至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中已套用資料使用標籤的個別欄位清單。 需要下列子屬性： <br/><br/>`option`：包含欄位[!DNL Experience Data Model] (XDM)屬性的物件。 需要下列三個屬性：<ul><li>`id`：與欄位關聯之結構描述的URI `$id`值。</li><li>`contentType`：表示結構描述的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。</li><li>`schemaPath`：相關結構描述屬性的路徑，以[JSON指標](../../landing/api-fundamentals.md#json-pointer)語法撰寫。</li></ul>`labels`：您要新增至欄位的資料使用標籤清單。 |

- ID：資料集所根據之XDM結構描述的URI $id值。
- contentType：指出結構描述的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。
- schemaPath：相關結構描述屬性的路徑，以[JSON指標](../../landing/api-fundamentals.md#json-pointer)語法撰寫。

## 將標籤套用至資料集 {#apply-dataset-labels}

您可以在[!DNL Dataset Service] API的POST或PUT要求裝載中提供這些標籤，藉此為資料集建立一組標籤。 使用其中一個方法會覆寫任何現有標籤，並以承載中提供的標籤取代。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您正在建立標籤的資料集的唯一`id`值。 |

**要求**

以下POST請求會將一系列標籤新增至資料集，以及該資料集內的特定欄位。 承載中提供的欄位與PUT請求所需的欄位相同。

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
| `labels` | 您要新增到資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中您要新增標籤的任何個別欄位清單。 此陣列中的每個專案都必須具備下列屬性： <br/><br/>`option`：包含欄位[!DNL Experience Data Model] (XDM)屬性的物件。 需要下列三個屬性：<ul><li>`id`：與欄位關聯之結構描述的URI `$id`值。</li><li>`contentType`：表示結構描述的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。</li><li>`schemaPath`：相關結構描述屬性的路徑，以[JSON指標](../../landing/api-fundamentals.md#json-pointer)語法撰寫。</li></ul>`labels`：您要新增至欄位的資料使用標籤清單。 |

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

## 從資料集中移除標籤 {#remove-dataset-labels}

您可以透過向[!DNL Dataset Service] API發出DELETE要求來移除套用至資料集的標籤。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要移除其標籤的資料集的唯一`id`值。 |

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

成功的回應HTTP狀態200 （確定），表示標籤已移除。 您可以[在個別呼叫中查詢資料集的現有標籤](#look-up-dataset-labels)以確認這一點。

## 後續步驟

閱讀本檔案後，您已瞭解如何使用API管理資料使用標籤。

在資料集和欄位層級新增資料使用標籤後，您就可以開始將資料內嵌到[!DNL Experience Platform]中。 若要深入瞭解，請先閱讀[資料擷取檔案](../../ingestion/home.md)。

您現在還可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱[資料使用原則概觀](../policies/overview.md)。

如需在[!DNL Experience Platform]中管理資料集的詳細資訊，請參閱[資料集總覽](../../catalog/datasets/overview.md)。