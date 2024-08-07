---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料型別登入；架構登入；資料型別；資料型別；資料型別；資料型別；建立
solution: Experience Platform
title: 資料型別API端點
description: 結構描述登入API中的/datatypes端點可讓您以程式設計方式管理體驗應用程式中的XDM資料型別。
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 2%

---

# 資料型別端點

資料型別在類別或結構描述欄位群組中的參考型別欄位使用方式，與基本常值欄位相同，主要差異在於資料型別可以定義多個子欄位。 雖然資料型別與欄位群組類似，因為其允許一致地使用多欄位結構，但資料型別較靈活，因為它們可以包含在架構結構中的任意位置，而欄位群組只能新增到根層級。 [!DNL Schema Registry] API中的`/datatypes`端點可讓您以程式設計方式管理體驗應用程式中的資料型別。

>[!NOTE]
>
>如果欄位定義為特定資料型別，則無法在另一個結構描述中以不同的資料型別建立相同的欄位。 此限制適用於您組織的租使用者。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取資料型別清單 {#list}

您可以分別向`/global/datatypes`或`/tenant/datatypes`發出GET要求，列出`global`或`tenant`容器下的所有資料型別。

>[!NOTE]
>
>列出資源時，結構描述登入將結果集限製為300個專案。 為了傳回超過此限制的資源，您必須使用分頁引數。 也建議您使用其他查詢引數來篩選結果並減少傳回的資源數量。 如需詳細資訊，請參閱附錄檔案中有關[查詢引數](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 您要擷取資料型別的容器： `global` (針對Adobe建立的資料型別)或`tenant` （針對貴組織擁有的資料型別）。 |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 如需可用引數的清單，請參閱[附錄檔案](./appendix.md#query)。 |

{style="table-layout:auto"}

**要求**

下列要求會使用`orderby`查詢引數，依資料型別的`title`屬性排序資料型別，從`tenant`容器擷取資料型別清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標頭。 下列`Accept`標題可用於列出資料型別：

| `Accept`標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON資料型別，包括原始`$ref`和`allOf`。 （上限： 300） |

{style="table-layout:auto"}

**回應**

上述要求使用了`application/vnd.adobe.xed-id+json` `Accept`標頭，因此回應只包含每個資料型別的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標頭(`application/vnd.adobe.xed+json`)會傳回每種資料型別的所有屬性。 根據您在回應中需要的資訊，選取適當的`Accept`標頭。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## 查詢資料型別 {#lookup}

您可以在GET請求的路徑中包含資料型別的ID，以查詢特定的資料型別。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取之資料型別的容器： `global`用於Adobe建立的資料型別，或`tenant`用於您的組織擁有的資料型別。 |
| `{DATA_TYPE_ID}` | 您要查閱之資料型別的`meta:altId`或URL編碼`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會依照路徑中提供的`meta:altId`值擷取資料型別。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標頭。 所有查詢請求都要求在`Accept`標頭中包含`version`。 下列`Accept`標頭可供使用：

| `Accept`標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`和`allOf`已解決，有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 含有`$ref`和`allOf`的原始，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref`和`allOf`已解決，無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | 已解決`$ref`和`allOf`，包含描述元。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回資料型別的詳細資料。 傳回的欄位取決於請求中傳送的`Accept`標頭。 嘗試使用不同的`Accept`標頭來比較回應，並決定哪個標頭最適合您的使用案例。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立資料型別 {#create}

您可以發出POST要求，在`tenant`容器下定義自訂資料型別。

**API格式**

```http
POST /tenant/datatypes
```

**要求**

與欄位群組不同，定義資料型別不需要`meta:extends`或`meta:intendedToExtend`欄位，也不需要巢狀化欄位以避免衝突。

在定義資料型別本身的欄位結構時，您可以使用基本型別（例如`string`或`object`），也可以透過`$ref`屬性參考其他現有的資料型別。 請參閱[在API](../tutorials/custom-fields-api.md)中定義自訂XDM欄位的指南，以取得不同XDM欄位型別的預期格式的詳細指引。

下列要求會建立具有子屬性`yearBuilt`、`propertyType`和`location`的「屬性建構」物件資料型別：

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**回應**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立資料型別之詳細資料的承載，包括`$id`、`meta:altId`和`version`。 這三個值是唯讀值，並由[!DNL Schema Registry]指派。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

執行[列出租使用者容器中所有資料型別](#list)的GET要求現在會包含屬性詳細資料資料資料型別，或者您可以[使用URL編碼的`$id` URI執行查詢(GET)要求](#lookup)以直接檢視新的資料型別。

## 更新資料型別 {#put}

您可以透過PUT作業取代整個資料型別，基本上就是重新寫入資源。 透過PUT要求更新資料型別時，本文必須包含在POST要求中[建立新資料型別](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新資料型別的一部分而不是完全取代它，請參閱[更新資料型別的一部分](#patch)一節。

**API格式**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATA_TYPE_ID}` | 您要重新寫入之資料型別的`meta:altId`或URL編碼`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會重新寫入現有的資料型別，新增新的`floorSize`欄位。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**回應**

成功的回應會傳回已更新資料型別的詳細資料。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 更新資料型別的一部分 {#patch}

您可以使用PATCH請求來更新資料型別的一部分。 [!DNL Schema Registry]支援所有標準JSON修補程式操作，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果您想要以新值取代整個資源，而非更新個別欄位，請參閱[使用PUT作業取代資料型別](#put)一節。

**API格式**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{DATA_TYPE_ID}` | URL編碼的`$id` URI或您要更新的資料型別的`meta:altId`。 |

{style="table-layout:auto"}

**要求**

下列範例要求會更新現有資料型別的`description`，並新增新的`floorSize`欄位。

請求內文採用陣列形式，每個列出的物件代表個別欄位的特定變更。 每個物件都包含要執行的作業(`op`)、應在哪個欄位上執行該作業(`path`)，以及該作業中應包含哪些資訊(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**回應**

回應顯示兩個作業都已成功執行。 `description`已更新，且`floorSize`已新增至`definitions`下。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type": "object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 刪除資料型別 {#delete}

有時可能需要從結構描述登入中移除資料型別。 若要這麼做，請使用路徑中提供的資料型別ID執行DELETE請求。

**API格式**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATA_TYPE_ID}` | URL編碼的`$id` URI或您要刪除之資料型別的`meta:altId`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試對資料型別進行[查詢(GET)請求](#lookup)，以確認刪除。 您需要在要求中加入`Accept`標頭，但應該會收到HTTP狀態404 （找不到），因為資料型別已從結構描述登入中移除。
