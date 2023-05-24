---
keywords: Experience Platform；主題；熱門主題；api;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；資料類型註冊表；模式註冊表；資料類型；資料類型；資料類型；資料類型；建立
solution: Experience Platform
title: 資料類型API終結點
description: 通過架構註冊表API中的/datatypes終結點，您可以以寫程式方式管理體驗應用程式中的XDM資料類型。
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 342da62b83d0d804b31744a580bcd3e38412ea51
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 2%

---

# 資料類型終結點

資料類型在類或方案欄位組中以與基本文本欄位相同的方式用作參考型別欄位，主要區別在於資料類型可以定義多個子欄位。 雖然與允許一致使用多欄位結構的欄位組類似，但資料類型更靈活，因為它們可以包含在架構結構中的任何位置，而欄位組只能在根級別添加。 的 `/datatypes` 端點 [!DNL Schema Registry] API允許您以寫程式方式管理體驗應用程式中的資料類型。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索資料類型清單 {#list}

您可以在 `global` 或 `tenant` 容器：向 `/global/datatypes` 或 `/tenant/datatypes`的下界。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 要返回超出此限制的資源，必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少返回的資源數。 請參閱 [查詢參數](./appendix.md#query) 的子菜單。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 要從以下位置檢索資料類型的容器： `global` 用於Adobe建立的資料類型或 `tenant` 用於您組織擁有的資料類型。 |
| `{QUERY_PARAMS}` | 用於篩選結果的可選查詢參數。 查看 [附錄文檔](./appendix.md#query) 的子菜單。 |

{style="table-layout:auto"}

**要求**

以下請求從 `tenant` 容器，使用 `orderby` 查詢參數，按資料類型排序 `title` 屬性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

響應格式取決於 `Accept` 請求中發送的標頭。 以下 `Accept` 標題可用於列出資料類型：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標頭。 (限制：300) |
| `application/vnd.adobe.xed+json` | 為每個資源返回完整的JSON資料類型（原始） `$ref` 和 `allOf` 包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

上述請求使用 `application/vnd.adobe.xed-id+json` `Accept` 標頭，因此響應僅包括 `title`。 `$id`。 `meta:altId`, `version` 每個資料類型的屬性。 使用其他 `Accept` 標題(H)`application/vnd.adobe.xed+json`)返回每個資料類型的所有屬性。 選擇相應的 `Accept` 標題，具體取決於您在回應中需要的資訊。

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

## 查找資料類型 {#lookup}

通過在GET請求的路徑中包含資料類型的ID，可以查找特定資料類型。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 儲存要檢索的資料類型的容器： `global` Adobe建立的資料類型或 `tenant` 屬於您組織的資料類型。 |
| `{DATA_TYPE_ID}` | 的 `meta:altId` 或URL編碼 `$id` 的子目錄。 |

{style="table-layout:auto"}

**要求**

以下請求通過其檢索資料類型 `meta:altId` 路徑中提供的值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

響應格式取決於 `Accept` 請求中發送的標頭。 所有查找請求都需要 `version` 包括在 `Accept` 標題。 以下 `Accept` 標題可用：

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 原始 `$ref` 和 `allOf`，包含標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 和 `allOf` 已解析，有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始 `$ref` 和 `allOf`，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 和 `allOf` 已解析，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 和 `allOf` 已解析，包含描述符。 |

{style="table-layout:auto"}

**回應**

成功的響應返回資料類型的詳細資訊。 返回的欄位取決於 `Accept` 請求中發送的標頭。 不同實驗 `Accept` 標題：比較響應並確定哪個標題最適合您的使用案例。

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

## 建立資料類型 {#create}

可在 `tenant` 容器，方法是發出POST請求。

**API格式**

```http
POST /tenant/datatypes
```

**要求**

與欄位組不同，定義資料類型不需要 `meta:extends` 或 `meta:intendedToExtend` 欄位，也不需要嵌套欄位以避免衝突。

在定義資料類型本身的欄位結構時，可以使用基元類型(如 `string` 或 `object`)，或者可以引用其他現有資料類型 `$ref` 屬性。 請參閱上的指南 [在API中定義自定義XDM欄位](../tutorials/custom-fields-api.md) 有關不同XDM欄位類型的預期格式的詳細指導。

以下請求建立具有子屬性的「屬性構造」對象資料類型 `yearBuilt`。 `propertyType`, `location`:

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

成功的響應返回HTTP狀態201（已建立）和包含新建立資料類型的詳細資訊的負載，包括 `$id`。 `meta:altId`, `version`。 這三個值是只讀的，由 [!DNL Schema Registry]。

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

執行GET請求 [列出所有資料類型](#list) 現在，租戶容器中將包含「屬性詳細資訊」資料類型，或者 [執行查找(GET)請求](#lookup) 使用URL編碼 `$id` URI，用於直接查看新資料類型。

## 更新資料類型 {#put}

您可以通過PUT操作替換整個資料類型，實際上就是重新寫入資源。 通過PUT請求更新資料類型時，正文必須包括在以下情況下所需的所有欄位 [建立新資料類型](#create) POST。

>[!NOTE]
>
>如果只想更新部分資料類型，而不想完全替換它，請參見上的部分 [更新資料類型的一部分](#patch)。

**API格式**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATA_TYPE_ID}` | 的 `meta:altId` 或URL編碼 `$id` 類型。 |

{style="table-layout:auto"}

**要求**

以下請求重寫現有資料類型，並添加新資料 `floorSize` 的子菜單。

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

成功的響應將返回更新資料類型的詳細資訊。

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

## 更新資料類型的一部分 {#patch}

您可以使用PATCH請求更新資料類型的一部分。 的 [!DNL Schema Registry] 支援所有標準JSON修補程式操作，包括 `add`。 `remove`, `replace`。 有關JSON修補程式的詳細資訊，請參見 [API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱上的部分 [使用PUT操作替換資料類型](#put)。

**API格式**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{DATA_TYPE_ID}` | URL編碼 `$id` URI或 `meta:altId` 類型。 |

{style="table-layout:auto"}

**要求**

下面的示例請求更新 `description` 添加一個 `floorSize` 的子菜單。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象都包括要執行的操作(`op`)，應對(執行的操作`path`)，以及該操作中應包含哪些資訊(`value`)。

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

該響應顯示已成功執行兩個操作。 的 `description` 已更新， `floorSize` 已添加到 `definitions`。

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

## 刪除資料類型 {#delete}

有時可能需要從架構註冊表中刪除資料類型。 這是通過執行DELETE請求，該請求具有路徑中提供的資料類型ID。

**API格式**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATA_TYPE_ID}` | URL編碼 `$id` URI或 `meta:altId` 類型。 |

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

成功的響應返回HTTP狀態204（無內容）和空白正文。

您可以通過嘗試 [查找(GET)請求](#lookup) 到資料類型。 您需要包括 `Accept` 請求中的標頭，但應接收HTTP狀態404（未找到），因為已從架構註冊表中刪除了資料類型。
