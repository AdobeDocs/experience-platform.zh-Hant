---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api
solution: Experience Platform
title: '使用API管理資料使用量標籤 '
topic-legacy: developer guide
description: 資料集服務API可讓您套用及編輯資料集的使用量標籤。 此API是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# 使用API管理資料使用量標籤

本檔案提供如何使用[!DNL Policy Service] API和[!DNL Dataset Service] API管理資料使用量標籤的步驟。

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)提供數個端點，可讓您建立和管理貴組織的資料使用量標籤。

[!DNL Dataset Service] API可讓您套用及編輯資料集的使用量標籤。 這是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的[!DNL Catalog Service] API不同。

## 快速入門

閱讀本指南之前，請依照目錄開發人員指南中[快速入門小節](../../catalog/api/getting-started.md)中概述的步驟，收集必要憑證，以呼叫[!DNL Platform] API。

若要呼叫本檔案中概述的[!DNL Dataset Service]端點，您必須具有特定資料集的唯一`id`值。 如果您沒有此值，請參閱[列出目錄物件](../../catalog/api/list-objects.md)的指南，以尋找現有資料集的ID。

## 列出所有標籤 {#list-labels}

使用[!DNL Policy Service] API，您可以分別對`/labels/core`或`/labels/custom`發出GET要求，以列出所有`core`或`custom`標籤。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**要求**

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

成功的回應會傳回從系統擷取的自訂標籤清單。 由於對`/labels/custom`提出了上述範例要求，因此下方的回應只會顯示自訂標籤。

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

## 查找標籤 {#look-up-label}

您可以在[!DNL Policy Service] API的GET請求路徑中加入該標籤的`name`屬性，以查找特定標籤。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 您要查詢的自訂標籤的`name`屬性。 |

**要求**

如路徑所示，下列請求會擷取自訂標籤`L2`。

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

## 建立或更新自訂標籤 {#create-update-label}

若要建立或更新自訂標籤，您必須向[!DNL Policy Service] API提出PUT要求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 自訂標籤的`name`屬性。 如果具有此名稱的自訂標籤不存在，則會建立新標籤。 如果確實存在，則會更新該標籤。 |

**要求**

以下請求建立新標籤`L3`，該標籤旨在描述包含與客戶選定付款計畫相關資訊的資料。

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
| `name` | 標籤的唯一字串識別碼。 此值可用於查詢，並將標籤套用至資料集和欄位，因此建議使用它簡短明瞭。 |
| `category` | 標籤的類別。 雖然您可以為自訂標籤建立自己的類別，但如果您希望標籤顯示在UI中，則強烈建議您使用`Custom`。 |
| `friendlyName` | 標籤的好記名稱，用於顯示用途。 |
| `description` | （選用）提供進一步內容之標籤的說明。 |

**回應**

成功的回應會傳回自訂標籤的詳細資訊，如果現有標籤更新，則會傳回HTTP代碼200(OK)，如果建立新標籤，則會傳回201(Created)。

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

## 查找資料集的標籤 {#look-up-dataset-labels}

您可以向[!DNL Dataset Service] API提出GET要求，以查找已套用至現有資料集的資料使用量標籤。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回已套用至資料集的資料使用量標籤。

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
| `labels` | 已套用至資料集的資料使用量標籤清單。 |
| `optionalLabels` | 資料集內已套用資料使用標籤的個別欄位清單。 需要下列子屬性：<br/><br/>`option`:包含欄位[!DNL Experience Data Model](XDM)屬性的物件。 需要下列三個屬性：<ul><li>`id`:與欄 `$id` 位關聯的架構的URI值。</li><li>`contentType`:指示架構的格式和版本。如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。</li><li>`schemaPath`:相關結構屬性的路徑，以JSON Pointer語法 [撰](../../landing/api-fundamentals.md#json-pointer) 寫。</li></ul>`labels`:您要新增至欄位的資料使用量標籤清單。 |

- id:資料集所根據之XDM架構的URI $id值。
- contentType:指示架構的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。
- schemaPath:以[JSON指標](../../landing/api-fundamentals.md#json-pointer)語法撰寫的相關架構屬性路徑。

## 將標籤套用至資料集 {#apply-dataset-labels}

您可以在[!DNL Dataset Service] API的POST或PUT請求的裝載中提供資料集，以建立資料集的標籤集。 使用其中一種方法會覆寫任何現有標籤，並以裝載中提供的標籤取代這些標籤。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 為建立標籤的資料集的唯一`id`值。 |

**要求**

下列POST請求會將一系列標籤新增至資料集，以及該資料集內的特定欄位。 有效負載中提供的欄位與PUT要求所需的欄位相同。

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
| `labels` | 您要新增至資料集的資料使用量標籤清單。 |
| `optionalLabels` | 資料集內您要新增標籤的任何個別欄位清單。 此陣列中的每個項目必須具有下列屬性：<br/><br/>`option`:包含欄位[!DNL Experience Data Model](XDM)屬性的物件。 需要下列三個屬性：<ul><li>`id`:與欄 `$id` 位關聯的架構的URI值。</li><li>`contentType`:指示架構的格式和版本。如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。</li><li>`schemaPath`:相關結構屬性的路徑，以JSON Pointer語法 [撰](../../landing/api-fundamentals.md#json-pointer) 寫。</li></ul>`labels`:您要新增至欄位的資料使用量標籤清單。 |

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

您可以向[!DNL Dataset Service] API提出DELETE請求，移除套用至資料集的標籤。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要移除其標籤之資料集的唯一`id`值。 |

**要求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應HTTP狀態200（確定），表示標籤已移除。 您可以透過個別呼叫[查找資料集的現有標籤](#look-up-dataset-labels)以確認此情況。

## 後續步驟

閱讀本檔案後，您便學會了如何使用API管理資料使用量標籤。

在資料集和欄位層級新增資料使用量標籤後，您就可以開始將資料內嵌至[!DNL Experience Platform]。 若要深入了解，請先閱讀[資料擷取檔案](../../ingestion/home.md)。

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱[資料使用原則概述](../policies/overview.md)。

如需在[!DNL Experience Platform]中管理資料集的詳細資訊，請參閱[資料集概述](../../catalog/datasets/overview.md)。