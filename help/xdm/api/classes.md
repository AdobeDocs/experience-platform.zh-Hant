---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；類註冊；模式註冊；類；類；類；建立
solution: Experience Platform
title: 類別API端點
description: 方案註冊表API中的/classes端點允許您以寫程式方式管理體驗應用程式中的XDM類。
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 1%

---

# 類端點

所有體驗資料模型(XDM)結構必須以類別為基礎。 類確定基於該類的所有方案必須包含的公共屬性的基本結構，以及哪些方案欄位組有資格在這些方案中使用。 此外，架構的類確定了架構將包含的資料的行為方面，其中有兩種類型：

* **[!UICONTROL Record]**:提供主題屬性的相關資訊。主題可以是組織或個人。
* **[!UICONTROL Time-series]**:提供記錄主體直接或間接採取操作時系統的快照。

>[!NOTE]
>
>有關資料行為如何影響架構構成的詳細資訊類，請參閱[架構構成的基礎](../schema/composition.md)。

[!DNL Schema Registry] API中的`/classes`端點可讓您以程式設計方式管理體驗應用程式中的類別。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 檢索{#list}類清單

您可以分別向`/global/classes`或`/tenant/classes`發出GET請求，以列出`global`或`tenant`容器下的所有類。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 如需詳細資訊，請參閱附錄檔案中有關[查詢參數](./appendix.md#query)的章節。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 要從以下位置檢索類的容器：`global`代表Adobe建立的類別，或`tenant`代表您組織擁有的類別。 |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 有關可用參數的清單，請參見[附錄文檔](./appendix.md#query)。 |

**要求**

以下請求從`tenant`容器中檢索類清單，使用`orderby`查詢參數按其`title`屬性對類進行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 以下`Accept`標題可用於列出類：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，並包含原始的`$ref`和`allOf`。 (限制：300) |

**回應**

上述請求使用`application/vnd.adobe.xed-id+json` `Accept`標題，因此回應僅包含每個類別的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標題(`application/vnd.adobe.xed+json`)會傳回每個類別的所有屬性。 根據您在回應中需要的資訊，選擇適當的`Accept`標題。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## 查找{#lookup}類

您可以在GET請求的路徑中加入類別的ID，以尋找特定類別。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之類別的容器：`global`代表Adobe建立的類別，或`tenant`代表您組織擁有的類別。 |
| `{CLASS_ID}` | 您要尋找之類的`meta:altId`或URL編碼`$id`。 |

**要求**

以下請求通過路徑中提供的`meta:altId`值檢索類。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 所有查閱請求都要求`version`包含在`Accept`標題中。 以下`Accept`標題可用：

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw含`$ref`和`allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 而且 `allOf` 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw含`$ref`和`allOf`，無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 並解 `allOf` 決，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 並解 `allOf` 決了包含的描述符。 |

**回應**

成功的響應返回類的詳細資訊。 傳回的欄位取決於請求中傳送的`Accept`標題。 嘗試不同的`Accept`標題，以比較回應並判斷哪個標題最適合您的使用案例。

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## 建立{#create}類

您可以透過提出POST請求，在`tenant`容器下定義自訂類別。

>[!IMPORTANT]
>
>根據您定義的自定義類合成方案時，將無法使用標準欄位組。 每個欄位組都定義了與其`meta:intendedToExtend`屬性相容的類。 一旦開始定義與新類相容的欄位組（通過使用欄位組`meta:intendedToExtend`欄位中新類的`$id`），您就可以在每次定義實現定義的類的方案時重新使用這些欄位組。 有關詳細資訊，請參閱[建立欄位組](./field-groups.md#create)和[建立方案](./schemas.md#create)各自端點指南中的章節。
>
>如果您打算在即時客戶配置檔案中使用基於自定義類的方案，請務必記住，聯合方案僅基於共用同一類的方案構建。 如果要在聯合中為[!UICONTROL XDM Individual Profile]或[!UICONTROL XDM ExperienceEvent]等其他類包含自定義類模式，則必須與使用該類的其他模式建立關係。 如需詳細資訊，請參閱API](../tutorials/relationship-api.md)中關於建立兩個架構之間關係的[教學課程。

**API格式**

```http
POST /tenant/classes
```

**要求**

建立(POST)類的請求必須包含`allOf`屬性，該屬性包含`$ref`到以下兩個值之一：`https://ns.adobe.com/xdm/data/record`或`https://ns.adobe.com/xdm/data/time-series`。 這些值代表類別所依據的行為（分別是記錄或時間序列）。 有關記錄資料和時間序列資料之間差異的詳細資訊，請參閱[架構構成基礎](../schema/composition.md)中有關行為類型的部分。

定義類時，您也可以在類定義中包括欄位組或自定義欄位。 這會導致新增的欄位群組和欄位包含在實施類別的所有結構中。 下列範例請求定義名為&quot;Property&quot;的類別，可擷取公司擁有和經營之不同屬性的相關資訊。 它包含`propertyId`欄位，每次使用類別時都會包含此欄位。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `_{TENANT_ID}` | 組織的`TENANT_ID`命名空間。 您的組織所建立的所有資源都必須包含此屬性，以避免與[!DNL Schema Registry]中的其他資源發生衝突。 |
| `allOf` | 要由新類繼承其屬性的資源清單。 陣列中的`$ref`對象之一定義了類的行為。 在此示例中，類繼承了「記錄」行為。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立類詳細資訊的裝載，包括`$id`、`meta:altId`和`version`。 這三個值是只讀的，由[!DNL Schema Registry]指定。

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

執行[列出`tenant`容器中所有類](#list)的GET請求，現在將包含屬性類。 您也可以[使用URL編碼的`$id`執行查閱(GET)請求](#lookup)，以直接檢視新類別。

## 更新{#put}類

您可以通過PUT操作替換整個類，實際上重寫資源。 當通過PUT請求更新類時，主體必須包括[在POST請求中建立新類](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新部分類，而不是完全替換類，請參閱[中有關更新部分類](#patch)的部分。

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 要重寫的類的`meta:altId`或URL編碼`$id`。 |

**要求**

以下請求重寫現有類，更改其`description`和其中一個欄位的`title`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**回應**

成功的回應會傳回更新類別的詳細資料。

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## 更新{#patch}類的一部分

您可以使用PATCH請求來更新類別的一部分。 [!DNL Schema Registry]支援所有標準JSON修補程式作業，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱[中的「使用PUT操作替換類」部分。](#put)

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 要更新類的URL編碼`$id` URI或`meta:altId`。 |

**要求**

下面的範例請求會更新現有類別的`description`，以及其中一個欄位的`title`。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象包括要執行的操作(`op`)，該操作應在哪個欄位(`path`)上執行，以及該操作應包括哪些資訊(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**回應**

響應顯示兩個操作均成功執行。 `description`已更新，`propertyId`欄位的`title`也已更新。

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## 刪除{#delete}類

有時可能需要從架構註冊表中刪除類。 這是透過使用路徑中提供的類別ID執行DELETE要求來完成的。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 要刪除的類的URL編碼`$id` URI或`meta:altId`。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。

您可以嘗試對類別執行[查閱(GET)請求](#lookup)以確認刪除。 您需要在請求中包含`Accept`標題，但應接收HTTP狀態404（找不到），因為類已從架構註冊表中刪除。
