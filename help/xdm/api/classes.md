---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；類別註冊表；結構註冊表；類別；類別；類別；類別；類別；建立
solution: Experience Platform
title: 類API端點
description: Schema Registry API中的/classes端點可讓您以程式設計方式管理體驗應用程式中的XDM類別。
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 3%

---

# 類端點

所有Experience Data Model(XDM)結構都必須以類別為基礎。 類決定了基於該類的所有架構必須包含的公共屬性的基本結構，以及哪些架構欄位組有資格在這些架構中使用。 此外，架構的類別會決定架構將包含之資料的行為方面，其中有兩種類型：

* **[!UICONTROL 記錄]**:提供主題屬性的相關資訊。 主題可以是組織或個人。
* **[!UICONTROL 時間序列]**:提供記錄主體直接或間接執行操作時系統的快照。

>[!NOTE]
>
>有關資料行為如何影響架構構成的詳細資訊，請參閱 [綱要構成基本知識](../schema/composition.md).

此 `/classes` 端點 [!DNL Schema Registry] API可讓您以程式設計方式管理體驗應用程式中的類別。

## 快速入門

本指南中使用的端點屬於 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 檢索類清單 {#list}

您可以列出 `global` 或 `tenant` 容器，方法是向 `/global/classes` 或 `/tenant/classes`，分別為。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 請參閱 [查詢參數](./appendix.md#query) ，以取得詳細資訊。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 要從中檢索類的容器： `global` Adobe建立的類或 `tenant` 適用於貴組織擁有的類別。 |
| `{QUERY_PARAMS}` | 可選的查詢參數，以依據篩選結果。 請參閱 [附錄檔案](./appendix.md#query) 以取得可用參數的清單。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會從 `tenant` 容器，使用 `orderby` 查詢參數，按類的順序排序 `title` 屬性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於 `Accept` 請求中傳送的標題。 以下 `Accept` 標題可用於清單類：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別（原始） `$ref` 和 `allOf` 已包含。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**回應**

上述請求使用 `application/vnd.adobe.xed-id+json` `Accept` 標題，因此回應僅包含 `title`, `$id`, `meta:altId`，和 `version` 屬性。 使用 `Accept` 標題(`application/vnd.adobe.xed+json`)會傳回每個類別的所有屬性。 選取適當的 `Accept` 標題，視您在回應中需要的資訊而定。

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

您可以在GET請求的路徑中加入類別的ID，以查找特定類別。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 容納要檢索的類的容器： `global` 針對Adobe建立的類或 `tenant` 為貴組織擁有的類。 |
| `{CLASS_ID}` | 此 `meta:altId` 或URL編碼 `$id` 你想查的班級。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會依其擷取類別 `meta:altId` 值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於 `Accept` 請求中傳送的標題。 所有查詢請求都需要 `version` 包含在 `Accept` 頁首。 以下 `Accept` 標題可供使用：

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 原始格式 `$ref` 和 `allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 和 `allOf` 已解析，有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始格式 `$ref` 和 `allOf`，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 和 `allOf` 已解析，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 和 `allOf` 已解析，包含描述符。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回類別的詳細資訊。 傳回的欄位取決於 `Accept` 請求中傳送的標題。 使用不同 `Accept` 標題來比較回應，並判斷哪個標題最適合您的使用案例。

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

## 建立類 {#create}

您可以在 `tenant` 容器，方法是提出POST請求。

>[!IMPORTANT]
>
>根據定義的自定義類合成架構時，將無法使用標準欄位組。 每個欄位組定義它們在其中相容的類 `meta:intendedToExtend` 屬性。 開始定義與新類相容的欄位組後(使用 `$id` 新課的 `meta:intendedToExtend` 欄位群組)，則每次定義實施您所定義類別的架構時，您都可以重複使用這些欄位群組。 請參閱 [建立欄位群組](./field-groups.md#create) 和 [建立綱要](./schemas.md#create) 以取得詳細資訊。
>
>如果您打算在即時客戶設定檔中使用以自訂類別為基礎的結構，也請務必留意，聯合結構僅根據共用相同類別的結構而建構。 如果要在聯合中包含其他類(如 [!UICONTROL XDM個別設定檔] 或 [!UICONTROL XDM ExperienceEvent]，您必須與採用該類別的其他架構建立關係。 請參閱 [在API中建立兩個架構的關係](../tutorials/relationship-api.md) 以取得更多資訊。

**API格式**

```http
POST /tenant/classes
```

**要求**

建立(POST)類的請求必須包含 `allOf` 包含 `$ref` 至兩個值之一： `https://ns.adobe.com/xdm/data/record` 或 `https://ns.adobe.com/xdm/data/time-series`. 這些值表示類所基於的行為（分別記錄或時間序列）。 如需記錄資料與時間序列資料之間差異的詳細資訊，請參閱 [綱要構成基本知識](../schema/composition.md).

在定義類時，還可以在類定義中包含欄位組或自定義欄位。 這會導致新增的欄位群組和欄位包含在實施類別的所有結構中。 下列範例要求會定義「屬性」類別，以擷取關於公司擁有和運作之不同屬性的資訊。 其中包含 `propertyId` 欄位，每次使用類時都要包含。

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
| `_{TENANT_ID}` | 此 `TENANT_ID` 組織的命名空間。 您的組織建立的所有資源都必須包含此屬性，以避免與 [!DNL Schema Registry]. |
| `allOf` | 要由新類繼承其屬性的資源清單。 其中 `$ref` 陣列內的對象定義類的行為。 在此示例中，類繼承「記錄」行為。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態201（已建立），並傳回包含新建立類別詳細資訊的裝載，包括 `$id`, `meta:altId`，和 `version`. 這三個值是唯讀的，並由 [!DNL Schema Registry].

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

執行GET請求 [列出所有類](#list) 在 `tenant` 容器現在會包含「屬性」類別。 您也可以 [執行查閱(GET)請求](#lookup) 使用URL編碼 `$id` 以直接查看新類。

## 更新類 {#put}

您可以通過PUT操作替換整個類，實際上重新寫入資源。 透過PUT請求更新類別時，內文必須包含當 [建立新類](#create) 在POST請求中。

>[!NOTE]
>
>如果您只想更新類的一部分，而不想完全替換它，請參閱 [更新類的一部分](#patch).

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 此 `meta:altId` 或URL編碼 `$id` 你想重寫的課。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求會重寫現有類，並更改其 `description` 和 `title` 其中一個領域。

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

成功的回應會傳回更新類別的詳細資訊。

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

## 更新類的一部分 {#patch}

您可以使用PATCH請求來更新類的一部分。 此 [!DNL Schema Registry] 支援所有標準JSON修補程式操作，包括 `add`, `remove`，和 `replace`. 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>如果您想要以新值取代整個資源，而非更新個別欄位，請參閱 [使用PUT操作替換類](#put).

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` URI或 `meta:altId` 要更新的類。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下範例要求會更新 `description` 現有類別的 `title` 其中一個領域。

要求內文採用陣列的形式，每個列出的物件代表個別欄位的特定變更。 每個對象都包括要執行的操作(`op`)，應在(`path`)，以及該操作應包含哪些資訊(`value`)。

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

響應顯示兩個操作均已成功執行。 此 `description` 已更新，連同 `title` 的 `propertyId` 欄位。

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

## 刪除類 {#delete}

有時可能需要從架構註冊表中刪除類。 若要這麼做，請使用路徑中提供的類別ID執行DELETE要求。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` URI或 `meta:altId` 刪除的類。 |

{style=&quot;table-layout:auto&quot;}

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

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

您可以嘗試 [查閱(GET)請求](#lookup) 為班級。 您需要包含 `Accept` 標題，但應會收到HTTP狀態404（找不到），因為類別已從架構註冊表中移除。
