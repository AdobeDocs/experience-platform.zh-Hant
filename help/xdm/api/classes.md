---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: 建立類
description: 方案註冊表API中的/classes端點允許您以寫程式方式管理體驗應用程式中的XDM類。
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---


# 類端點

所有體驗資料模型(XDM)結構必須以類別為基礎。 類確定基於該類的所有方案必須包含的公共屬性的基本結構，以及哪些混合適用於這些方案。 此外，架構的類確定了架構將包含的資料的行為方面，其中有兩種類型：

* **[!UICONTROL 記錄]**:提供主題屬性的相關資訊。 主題可以是組織或個人。
* **[!UICONTROL 時間系列]**:提供記錄主體直接或間接採取操作時系統的快照。

>[!NOTE]
>
>有關資料行為如何影響架構構成的詳細資訊類，請參閱架構構 [成的基本資訊](../schema/composition.md)。

API中 `/classes` 的端點可讓您以程式設計方式 [!DNL Schema Registry] 管理體驗應用程式中的類別。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)。 在繼續之前，請先閱讀快速入門手冊 [](./getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 檢索類清單 {#list}

您可以分別向或發出 `global` GET請 `tenant` 求，以列出或容器下 `/global/classes` 的所有類 `/tenant/classes`別。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 如需詳細資訊，請 [參閱附錄檔案](./appendix.md#query) 中查詢參數一節。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 要從以下位置檢索類的容器： `global` 適用於Adobe建立的類別或 `tenant` 您組織擁有的類別。 |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 如需可用 [參數的清單](./appendix.md#query) ，請參閱附錄檔案。 |

**請求**

以下請求從容器中檢索類的列 `tenant` 表，使用查 `orderby` 詢參數按類的屬性對類進行排序 `title` 。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於在請求 `Accept` 中傳送的標題。 列出類 `Accept` 別時可使用以下標題：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，其中包含 `$ref` 原始 `allOf` 資源。 (限制：300) |

**回應**

上述請求使用標 `application/vnd.adobe.xed-id+json` 題，因此回應僅包 `Accept` 含每個類別的 `title`、 `$id``meta:altId`和 `version` 屬性。 使用其他 `Accept` 標題(`application/vnd.adobe.xed+json`)會傳回每個類別的所有屬性。 根據您在回 `Accept` 應中需要的資訊，選擇適當的標題。

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

## 查找類 {#lookup}

您可以在GET請求的路徑中加入類別的ID，以尋找特定類別。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之類別的容器： `global` Adobe建立的類別或您 `tenant` 組織擁有的類別。 |
| `{CLASS_ID}` | 您 `meta:altId` 要尋找的類 `$id` 別的或URL編碼。 |

**請求**

下列請求會依路徑中提供的 `meta:altId` 值擷取類別。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於在請求 `Accept` 中傳送的標題。 所有查閱請求都 `version` 必須包含在標 `Accept` 題中。 The following `Accept` headers are available:

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw含 `$ref` 和 `allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 而且 `allOf` 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw含 `$ref` 和 `allOf`，無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 並解 `allOf` 決，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和已解 `allOf` 析的包含描述符。 |

**回應**

成功的響應返回類的詳細資訊。 傳回的欄位取決於請求 `Accept` 中傳送的標題。 嘗試不同 `Accept` 的標題以比較回應，並判斷哪個標題最適合您的使用案例。

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

## 建立類 {#create}

您可以透過提出POST請求，在容 `tenant` 器下定義自訂類別。

>[!IMPORTANT]
>
>根據您定義的自訂類合成架構時，將無法使用標準混音。 每個mixin都定義其屬性中相容的類 `meta:intendedToExtend` 別。 一旦開始定義與新類相容的混音(使用混音的欄位中的 `$id``meta:intendedToExtend` 新類)，您每次定義實現所定義類的方案時，都可以重複使用這些混音。 如需詳細資訊，請 [參閱各自端點](./mixins.md#create)[指南中有關建立混合和建立結構的章節](./schemas.md#create) 。
>
>如果您打算在即時客戶配置檔案中使用基於自定義類的方案，請務必記住，聯合方案僅基於共用同一類的方案構建。 如果要將自定義類模式包括在聯合中，以用於 [!UICONTROL XDM Individual Profile] 或 [!UICONTROL XDM ExperienceEvent]，則必須與使用該類的其他模式建立關係。 如需詳細資訊， [請參閱API中關於建立兩個結構描述之間關係的教學課程](../tutorials/relationship-api.md) 。

**API格式**

```http
POST /tenant/classes
```

**請求**

建立(POST)類別的請求必須包含包含 `allOf` 兩個值之 `$ref` 一的屬性： `https://ns.adobe.com/xdm/data/record` 或 `https://ns.adobe.com/xdm/data/time-series`者。 這些值代表類別所依據的行為（分別是記錄或時間序列）。 有關記錄資料和時間序列資料之間差異的詳細資訊，請參閱架構構成基礎中有關行 [為類型的部分](../schema/composition.md)。

在定義類時，您也可以在類定義中包含混合或自訂欄位。 這會導致新增的混音和欄位包含在實施類別的所有結構中。 下列範例請求定義名為&quot;Property&quot;的類別，可擷取公司擁有和經營之不同屬性的相關資訊。 它包含 `propertyId` 每次使用類時要包含的欄位。

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
| `_{TENANT_ID}` | 組織 `TENANT_ID` 的命名空間。 您的組織建立的所有資源都必須包含此屬性，以避免與中的其他資源發生衝突 [!DNL Schema Registry]。 |
| `allOf` | 要由新類繼承其屬性的資源清單。 陣列中的 `$ref` 一個對象定義類的行為。 在此示例中，類繼承了「記錄」行為。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立）和包含新建立類別詳細資訊的裝載，包括 `$id`、 `meta:altId`和 `version`。 這三個值是唯讀的，由指定 [!DNL Schema Registry]。

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

執行GET請求以列 [出容器中的所有類](#list)`tenant` 目前將包含屬性類。 您也可以 [使用URL編碼的](#lookup) ，執行查閱(GET) `$id` 請求，以直接檢視新類別。

## 更新類 {#put}

您可以通過PUT操作替換整個類，實際上重寫資源。 通過PUT請求更新類時，主體必須包含在POST請求中建立新類 [時所需的所有欄位](#create) 。

>[!NOTE]
>
>如果只想更新部分類，而不是完全替換類，請參見有關更 [新部分類的部分](#patch)。

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 要 `meta:altId` 重寫的類 `$id` 的或URL編碼類。 |

**請求**

下列請求會重寫現有類，並變更其 `description` 中一 `title` 個欄位的類別。

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

## 更新類別的一部分 {#patch}

您可以使用PATCH請求更新類的一部分。 支援 [!DNL Schema Registry] 所有標準JSON修補程式作業， `add`包括 `remove`、和 `replace`。 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱有關使用PUT [操作替換類的部分](#put)。

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼的 `$id` URI或 `meta:altId` 您要更新的類別。 |

**請求**

以下範例請求會更 `description` 新現有類別及其其 `title` 中一個欄位的範例。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象包括要執行的操作(`op`)，該操作應在哪個欄位上執行(`path`)，以及該操作應包括哪些資訊(`value`)。

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

響應顯示兩個操作均成功執行。 已 `description` 更新，以及字 `title` 段的 `propertyId` 名稱。

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

## 刪除類 {#delete}

有時可能需要從架構註冊表中刪除類。 這是透過使用路徑中提供的類別ID來執行DELETE請求來完成的。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` 的URI `meta:altId` 或您要刪除的類別。 |

**請求**

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

您可以嘗試類別的查閱( [GET)請求](#lookup) ，以確認刪除。 您需要在請求中加 `Accept` 入標題，但應會收到HTTP狀態404（找不到），因為類別已從架構註冊表中移除。