---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；模式註冊；欄位組；欄位組；建立
solution: Experience Platform
title: 欄位群組API端點
description: 架構註冊表API中的/fieldgroups端點允許您以寫程式方式管理體驗應用程式中的XDM架構欄位組。
topic: 開發人員指南
translation-type: tm+mt
source-git-commit: b25c545e86c8ffd6b5832893152aef597feaf71f
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 2%

---


# 方案欄位組端點

架構欄位組是可重複使用的元件，它定義了表示特定概念的一個或多個欄位，如個人、郵件地址或Web瀏覽器環境。 欄位組將作為實現相容類的架構的一部分包括，具體取決於它們所代表的資料（記錄或時間序列）的行為。 [!DNL Schema Registry] API中的`/fieldgroups`端點可讓您以程式設計方式管理體驗應用程式中的欄位群組。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 檢索欄位組{#list}清單

您可以分別向`/global/fieldgroups`或`/tenant/fieldgroups`發出GET請求，以列出`global`或`tenant`容器下的所有欄位群組。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 如需詳細資訊，請參閱附錄檔案中有關[查詢參數](./appendix.md#query)的章節。

**API格式**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 您要擷取欄位群組的容器：`global`代表Adobe建立的欄位群組，或`tenant`代表您組織擁有的欄位群組。 |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 有關可用參數的清單，請參見[附錄文檔](./appendix.md#query)。 |

**要求**

下列請求會從`tenant`容器中擷取欄位群組清單，使用`orderby`查詢參數，依其`title`屬性來排序欄位群組。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 下列`Accept`標題可用於列出欄位群組：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON欄位群組，並包含原始的`$ref`和`allOf`。 (限制：300) |

**回應**

上述請求使用`application/vnd.adobe.xed-id+json` `Accept`標題，因此回應僅包含每個欄位群組的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標題(`application/vnd.adobe.xed+json`)會傳回每個欄位群組的所有屬性。 根據您在回應中需要的資訊，選擇適當的`Accept`標題。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.fieldgroups.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.fieldgroups.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.fieldgroups.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.fieldgroups.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## 查找欄位組{#lookup}

您可以在請求的路徑中加入欄位群組的ID，以尋找特定欄位群組。

**API格式**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之欄位群組的容器：`global`代表Adobe建立的欄位群組，或`tenant`代表您組織擁有的欄位群組。 |
| `{FIELD_GROUP_ID}` | 您要尋找之欄位群組的`meta:altId`或URL編碼`$id`。 |

**要求**

以下請求通過路徑中提供的`meta:altId`值檢索欄位組。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 所有查閱請求都要求`version`包含在`Accept`標題中。 以下`Accept`標題可用：

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw含`$ref`和`allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 而且 `allOf` 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw含`$ref`和`allOf`，無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 並解 `allOf` 決，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 並解 `allOf` 決了包含的描述符。 |

**回應**

成功的回應會傳回欄位群組的詳細資料。 傳回的欄位取決於請求中傳送的`Accept`標題。 嘗試不同的`Accept`標題，以比較回應並判斷哪個標題最適合您的使用案例。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
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

## 建立欄位組{#create}

您可以透過提出POST請求，在`tenant`容器下定義自訂欄位群組。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

定義新欄位組時，它必須包含`meta:intendedToExtend`屬性，列出與欄位組相容的類的`$id`。 在此示例中，欄位組與先前定義的`Property`類相容。 自訂欄位必須巢狀內嵌在`_{TENANT_ID}`下（如範例所示），以避免與類別和其他欄位群組提供的類似欄位產生衝突。

>[!NOTE]
>
>有關如何定義要包括在欄位組中的不同欄位類型的詳細資訊，請參閱[欄位約束指南](../schema/field-constraints.md#define-fields)。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
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
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**回應**

成功的回應會傳回HTTP狀態201（已建立）和包含新建立欄位群組詳細資料的裝載，包括`$id`、`meta:altId`和`version`。 這些值是只讀的，由[!DNL Schema Registry]指定。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
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
  "imsOrg": "{IMS_ORG}",
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

執行[清單租用戶容器中所有欄位群組](#list)的GET請求，現在會包含「屬性詳細資料」欄位群組，或者您可以[使用URL編碼的`$id` URI，執行查閱(GET)請求](#lookup)，以直接檢視新欄位群組。

## 更新欄位組{#put}

您可以通過PUT操作替換整個欄位組，實際上重寫資源。 當通過PUT請求更新欄位組時，主體必須包括[在POST請求中建立新欄位組](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新部分欄位組而不是完全替換欄位組，請參閱[中有關更新部分欄位組的章節](#patch)。

**API格式**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 要重寫的欄位組的`meta:altId`或URL編碼`$id`。 |

**要求**

下列請求會重寫現有欄位群組，並新增新的`propertyCountry`欄位。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
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
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**回應**

成功的回應會傳回更新欄位群組的詳細資料。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
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
  "imsOrg": "{IMS_ORG}",
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

## 更新欄位組{#patch}的一部分

您可以使用PATCH請求來更新欄位群組的一部分。 [!DNL Schema Registry]支援所有標準JSON修補程式作業，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱[中的「使用PUT操作替換欄位組」部分。](#put)

**API格式**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 要更新的欄位組的URL編碼`$id` URI或`meta:altId`。 |

**要求**

以下範例請求會更新現有欄位群組的`description`，並新增新的`propertyCity`欄位。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象包括要執行的操作(`op`)，該操作應在哪個欄位(`path`)上執行，以及該操作應包括哪些資訊(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**回應**

響應顯示兩個操作均成功執行。 `description`已更新，`propertyCountry`已在`definitions`下添加。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
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
  "imsOrg": "{IMS_ORG}",
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

## 刪除欄位組{#delete}

有時可能需要從架構註冊表中刪除欄位組。 這是透過使用路徑中提供的欄位群組ID執行DELETE要求來完成。

**API格式**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 要刪除的欄位組的URL編碼`$id` URI或`meta:altId`。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。

您可以嘗試對欄位群組執行[查閱(GET)請求](#lookup)以確認刪除。 您需要在請求中包含`Accept`標題，但應接收HTTP狀態404（找不到），因為欄位群組已從架構註冊表中移除。