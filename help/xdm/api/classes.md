---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；類註冊表；模式註冊表；類；類；類；類；類；建立
solution: Experience Platform
title: 類API終結點
description: 通過架構註冊表API中的/classes終結點，可以以寫程式方式管理體驗應用程式中的XDM類。
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 1%

---

# 類終結點

所有體驗資料模型(XDM)架構必須基於類。 類確定基於該類的所有方案必須包含的公共屬性的基本結構，以及哪些方案欄位組有資格在這些方案中使用。 此外，架構的類確定架構將包含的資料的行為方面，其中有兩種類型：

* **[!UICONTROL 記錄]**:提供有關主題屬性的資訊。 主題可以是組織或個人。
* **[!UICONTROL 時間序列]**:提供記錄主題直接或間接執行操作時系統的快照。

>[!NOTE]
>
>有關資料行為對架構組成影響的詳細資訊，請參閱 [架構組合基礎](../schema/composition.md)。

的 `/classes` 端點 [!DNL Schema Registry] API允許您以寫程式方式管理體驗應用程式中的類。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索類清單 {#list}

可以在 `global` 或 `tenant` 容器：向 `/global/classes` 或 `/tenant/classes`的下界。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 要返回超出此限制的資源，必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少返回的資源數。 請參閱 [查詢參數](./appendix.md#query) 的子菜單。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 要從以下位置檢索類的容器： `global` 用於Adobe建立的類或 `tenant` 為您組織擁有的類。 |
| `{QUERY_PARAMS}` | 用於篩選結果的可選查詢參數。 查看 [附錄文檔](./appendix.md#query) 的子菜單。 |

{style="table-layout:auto"}

**要求**

以下請求從 `tenant` 容器，使用 `orderby` 查詢參數，按類排序 `title` 屬性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

響應格式取決於 `Accept` 請求中發送的標頭。 以下 `Accept` 標題可用於清單類：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標頭。 (限制：300) |
| `application/vnd.adobe.xed+json` | 為每個資源返回完整的JSON類，原始 `$ref` 和 `allOf` 包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

上述請求使用 `application/vnd.adobe.xed-id+json` `Accept` 標頭，因此響應僅包括 `title`。 `$id`。 `meta:altId`, `version` 每個類的屬性。 使用其他 `Accept` 標題(H)`application/vnd.adobe.xed+json`)返回每個類的所有屬性。 選擇相應的 `Accept` 標題，具體取決於您在回應中需要的資訊。

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

通過將類的ID包括在GET請求的路徑中，可以查找特定類。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 包含要檢索的類的容器： `global` 為Adobe建立的類或 `tenant` 你所在組織的課。 |
| `{CLASS_ID}` | 的 `meta:altId` 或URL編碼 `$id` 你想查的班級。 |

{style="table-layout:auto"}

**要求**

以下請求通過 `meta:altId` 路徑中提供的值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

成功的響應返回類的詳細資訊。 返回的欄位取決於 `Accept` 請求中發送的標頭。 不同實驗 `Accept` 標題：比較響應並確定哪個標題最適合您的使用案例。

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

可在 `tenant` 容器，方法是發出POST請求。

>[!IMPORTANT]
>
>在基於您定義的自定義類合成架構時，將無法使用標準欄位組。 每個欄位組定義它們與之相容的類 `meta:intendedToExtend` 屬性。 一旦開始定義與新類相容的欄位組(使用 `$id` 你新班的 `meta:intendedToExtend` 欄位組)中，每次定義實現定義的類的方案時，您都可以重用這些欄位組。 請參閱 [建立欄位組](./field-groups.md#create) 和 [建立架構](./schemas.md#create) 的子菜單。
>
>如果您計畫在即時客戶概要檔案中使用基於自定義類的方案，還必須記住，聯合方案僅基於共用同一類的方案構建。 如果希望在聯合中為其他類包括自定義類架構，例如 [!UICONTROL XDM個人配置檔案] 或 [!UICONTROL XDM體驗事件]，必須與使用該類的其他架構建立關係。 請參閱上的教程 [在API中建立兩個架構之間的關係](../tutorials/relationship-api.md) 的子菜單。

**API格式**

```http
POST /tenant/classes
```

**要求**

建立(POST)類的請求必須包括 `allOf` 包含屬性 `$ref` 值之一： `https://ns.adobe.com/xdm/data/record` 或 `https://ns.adobe.com/xdm/data/time-series`。 這些值表示類所基於的行為（分別是記錄或時間序列）。 有關記錄資料和時間序列資料之間差異的詳細資訊，請參閱中有關行為類型的一節 [架構組合基礎](../schema/composition.md)。

在定義類時，還可以在類定義中包括欄位組或自定義欄位。 這將導致添加的欄位組和欄位包含在實現類的所有方案中。 下面的示例請求定義一個名為&quot;Property&quot;的類，該類捕獲有關公司擁有和運營的不同屬性的資訊。 它包括 `propertyId` 在每次使用類時包含的欄位。

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
| `_{TENANT_ID}` | 的 `TENANT_ID` 組織的命名空間。 您的組織建立的所有資源都必須包括此屬性，以避免與 [!DNL Schema Registry]。 |
| `allOf` | 要由新類繼承其屬性的資源清單。 其中 `$ref` 陣列中的對象定義類的行為。 在此示例中，類繼承「record」行為。 |

{style="table-layout:auto"}

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立類的詳細資訊的負載，包括 `$id`。 `meta:altId`, `version`。 這三個值是只讀的，由 [!DNL Schema Registry]。

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

執行GET請求 [列出所有類](#list) 的 `tenant` 容器現在將包括Property類。 您也可以 [執行查找(GET)請求](#lookup) 使用URL編碼 `$id` 的子菜單。

## 更新類 {#put}

您可以通過PUT操作替換整個類，實際上就是重新寫入資源。 通過PUT請求更新類時，正文必須包括在 [建立新類](#create) POST。

>[!NOTE]
>
>如果只想更新類的一部分，而不想完全替換它，請參見上的 [更新類的一部分](#patch)。

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 的 `meta:altId` 或URL編碼 `$id` 你想重寫的課。 |

{style="table-layout:auto"}

**要求**

以下請求重寫現有類，並更改其 `description` 和 `title` 其中一塊田地。

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

成功的響應將返回更新的類的詳細資訊。

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

您可以使用PATCH請求更新類的一部分。 的 [!DNL Schema Registry] 支援所有標準JSON修補程式操作，包括 `add`。 `remove`, `replace`。 有關JSON修補程式的詳細資訊，請參見 [API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱上的部分 [使用PUT操作替換類](#put)。

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` URI或 `meta:altId` 類的。 |

{style="table-layout:auto"}

**要求**

下面的示例請求更新 `description` 現有課程的 `title` 其中一塊田地。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象都包括要執行的操作(`op`)，應對(執行的操作`path`)，以及該操作中應包含哪些資訊(`value`)。

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

該響應顯示已成功執行兩個操作。 的 `description` 已更新，以及 `title` 的 `propertyId` 的子菜單。

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

有時可能需要從架構註冊表中刪除類。 這是通過使用路徑中提供的類ID執行DELETE請求來完成的。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` URI或 `meta:altId` 刪除的類。 |

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

成功的響應返回HTTP狀態204（無內容）和空白正文。

您可以通過嘗試 [查找(GET)請求](#lookup) 為班級。 您需要包括 `Accept` 請求中的標頭，但應接收HTTP狀態404（未找到），因為類已從架構註冊表中刪除。
