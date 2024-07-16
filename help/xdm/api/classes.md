---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；類別登入；Schema登入；類別；類別；類別；類別；建立
solution: Experience Platform
title: 類別API端點
description: Schema Registry API中的/classes端點可讓您以程式設計方式管理體驗應用程式中的XDM類別。
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 1%

---

# 類別端點

所有Experience Data Model (XDM)結構描述都必須根據類別。 類別決定以該類別為基礎的所有結構描述都必須包含的通用屬性的基底結構，以及哪些結構描述欄位群組適合用於這些結構描述。 此外，結構描述的類別會決定結構描述將包含之資料的行為方面，其中有兩種型別：

* **[!UICONTROL 記錄]**：提供有關主旨屬性的資訊。 主旨可以是組織或個人。
* **[!UICONTROL 時間序列]**：提供記錄主體直接或間接執行動作時的系統快照。

>[!NOTE]
>
>如需資料行為如何影響結構描述構成的詳細資訊，請參閱結構描述構成的[基本概念](../schema/composition.md)。

[!DNL Schema Registry] API中的`/classes`端點可讓您以程式設計方式管理體驗應用程式中的類別。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取類別清單 {#list}

您可以分別向`/global/classes`或`/tenant/classes`發出GET要求，列出`global`或`tenant`容器下的所有類別。

>[!NOTE]
>
>列出資源時，結構描述登入將結果集限製為300個專案。 為了傳回超過此限制的資源，您必須使用分頁引數。 也建議您使用其他查詢引數來篩選結果並減少傳回的資源數量。 如需詳細資訊，請參閱附錄檔案中有關[查詢引數](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 您要擷取類別的容器： `global` (針對Adobe建立的類別)或`tenant` （針對貴組織擁有的類別）。 |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 如需可用引數的清單，請參閱[附錄檔案](./appendix.md#query)。 |

{style="table-layout:auto"}

**要求**

下列要求從`tenant`容器擷取類別清單，使用`orderby`查詢引數依類別的`title`屬性排序類別。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標頭。 下列`Accept`標頭可用於列出類別：

| `Accept`標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，包含原始`$ref`和`allOf`。 （上限： 300） |

{style="table-layout:auto"}

**回應**

上述要求使用了`application/vnd.adobe.xed-id+json` `Accept`標頭，因此回應只包含每個類別的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標頭(`application/vnd.adobe.xed+json`)會傳回每個類別的所有屬性。 根據您在回應中需要的資訊，選取適當的`Accept`標頭。

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

## 查詢類別 {#lookup}

您可以在GET請求的路徑中包含類別ID來查詢特定類別。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取類別的容器： `global`用於Adobe建立的類別，或`tenant`用於貴組織擁有的類別。 |
| `{CLASS_ID}` | 您要查閱之類別的`meta:altId`或URL編碼的`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會依照路徑中提供的`meta:altId`值擷取類別。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

成功的回應會傳回類別的詳細資料。 傳回的欄位取決於請求中傳送的`Accept`標頭。 嘗試使用不同的`Accept`標頭來比較回應，並決定哪個標頭最適合您的使用案例。

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
  "imsOrg":"{ORG_ID}",
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

## 建立類別 {#create}

您可以發出POST要求，在`tenant`容器下定義自訂類別。

>[!IMPORTANT]
>
>根據您定義的自訂類別構成結構描述時，您將無法使用標準欄位群組。 每個欄位群組都會定義在其`meta:intendedToExtend`屬性中相容的類別。 一旦您開始定義與新類別相容的欄位群組（透過使用欄位群組`meta:intendedToExtend`欄位中新類別的`$id`），每次定義實作您定義之類別的結構描述時，您都可以重複使用這些欄位群組。 如需詳細資訊，請參閱[建立欄位群組](./field-groups.md#create)和[在各自的端點指南中建立結構描述](./schemas.md#create)的相關章節。
>
>如果您打算根據即時客戶設定檔中的自訂類別來使用結構描述，請務必記住，聯合結構描述僅根據共用相同類別的結構描述來建構。 如果您想在另一個類別（例如[!UICONTROL XDM Individual Profile]或[!UICONTROL XDM ExperienceEvent]）的聯合中包含自訂類別結構描述，您必須與使用該類別的其他結構描述建立關係。 如需詳細資訊，請參閱有關[在API](../tutorials/relationship-api.md)中建立兩個結構描述之間關係的教學課程。

**API格式**

```http
POST /tenant/classes
```

**要求**

建立(POST)類別的要求必須包含`allOf`屬性，該屬性包含`$ref`到兩個值之一： `https://ns.adobe.com/xdm/data/record`或`https://ns.adobe.com/xdm/data/time-series`。 這些值代表類別所依據的行為（分別是記錄或時間序列）。 如需記錄資料與時間序列資料之間差異的詳細資訊，請參閱結構描述組合[基本概念中的行為型別區段](../schema/composition.md)。

定義類別時，您也可以在類別定義中包含欄位群組或自訂欄位。 這會使新增的欄位群組和欄位包含在實作類別的所有結構描述中。 以下範例請求會定義一個名為「Property」的類別，用於擷取公司擁有和經營的不同屬性的相關資訊。 它包含每次使用類別時要包含的`propertyId`欄位。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | 您組織的`TENANT_ID`名稱空間。 貴組織建立的所有資源都必須包含此屬性，以避免與[!DNL Schema Registry]中的其他資源發生衝突。 |
| `allOf` | 新類別要繼承其屬性的資源清單。 陣列中的`$ref`物件之一定義了類別的行為。 在此範例中，類別會繼承「記錄」行為。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立類別之詳細資訊的承載，包括`$id`、`meta:altId`和`version`。 這三個值是唯讀值，並由[!DNL Schema Registry]指派。

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
  "imsOrg": "{ORG_ID}",
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

執行GET要求至[列出`tenant`容器中的所有類別](#list)現在將包含Property類別。 您也可以[使用URL編碼的`$id`執行查詢(GET)要求](#lookup)，以直接檢視新類別。

## 更新類別 {#put}

您可以透過PUT作業取代整個類別，基本上就是重新寫入資源。 透過PUT要求更新類別時，本文必須包含在POST要求中[建立新類別](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新類別的一部分而不是完全取代它，請參閱[更新類別的一部分](#patch)一節。

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 您要重新寫入之類別的`meta:altId`或URL編碼的`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會重新寫入現有類別，變更其`description`及其其中一個欄位的`title`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  "imsOrg": "{ORG_ID}",
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

## 更新類別的一部分 {#patch}

您可以使用PATCH請求來更新類別的一部分。 [!DNL Schema Registry]支援所有標準JSON修補程式操作，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果您想要以新值取代整個資源，而不是更新個別欄位，請參閱[使用PUT作業取代類別](#put)一節。

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼的`$id` URI或您要更新的類別的`meta:altId`。 |

{style="table-layout:auto"}

**要求**

下列範例要求會更新現有類別的`description`及其其中一個欄位的`title`。

請求內文採用陣列形式，每個列出的物件代表個別欄位的特定變更。 每個物件都包含要執行的作業(`op`)、應在哪個欄位上執行該作業(`path`)，以及該作業中應包含哪些資訊(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**回應**

回應顯示兩個作業都已成功執行。 已更新`description`以及`propertyId`欄位的`title`。

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
  "imsOrg": "{ORG_ID}",
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

## 刪除類別 {#delete}

有時可能需要從結構描述登入中移除類別。 若要這麼做，請使用路徑中提供的類別ID執行DELETE要求。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼的`$id` URI或您要刪除之類別的`meta:altId`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試該類別的[查詢(GET)要求](#lookup)以確認刪除。 您需要在要求中包含`Accept`標頭，但應該會收到HTTP狀態404 （找不到），因為類別已從結構描述登入中移除。
