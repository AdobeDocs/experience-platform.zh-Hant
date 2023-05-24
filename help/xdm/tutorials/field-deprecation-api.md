---
title: 棄用API中的XDM欄位
description: 瞭解如何棄用架構註冊表API中的「體驗資料模型」(XDM)欄位。
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 2%

---

# 棄用API中的XDM欄位

在體驗資料模型(XDM)中，可以使用 [架構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。 棄用某個欄位會使其隱藏在下游UI中，如 [!UICONTROL 配置檔案] 工作區和Customer Journey Analytics，但是，它不會發生中斷更改，不會對現有資料流產生負面影響。

本文檔介紹如何為不同的XDM資源棄用欄位。 有關使用Experience Platform用戶介面中的架構編輯器來棄用XDM欄位的步驟，請參見上的教程 [棄用UI中的XDM欄位](./field-deprecation-ui.md)。

## 快速入門

本教程要求調用架構註冊表API。 請查看 [開發者指南](../api/getting-started.md) 獲取進行這些API調用所需的重要資訊。 這包括您 `{TENANT_ID}`、&quot;容器&quot;的概念以及提出請求所需的標題(特別注意 `Accept` 標題及其可能值)。

## 棄用自定義欄位 {#custom}

要棄用自定義類、欄位組或資料類型中的欄位，請通過PUT或PATCH請求更新自定義資源，並添加屬性 `meta:status: deprecated` 去那個領域。

>[!NOTE]
>
>有關在XDM中更新自定義資源的一般資訊，請參閱以下文檔：
>
>* [更新類](../api/classes.md#patch)
>* [更新欄位組](../api/field-groups.md#patch)
>* [更新資料類型](../api/data-types.md#patch)


下面的示例API調用使自定義資料類型中的欄位失效。

**API格式**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**要求**

以下請求棄用 `expansionArea` 用於描述不動產屬性的資料類型的欄位。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**回應**

成功的響應將返回自定義資源的更新詳細資訊，其中不建議使用的欄位包含 `meta:status` 值 `deprecated`。 下面的示例響應已被截斷為空間。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
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
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
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

## 棄用架構中的標準欄位 {#standard}

不能直接棄用標準類、欄位組和資料類型中的欄位。 相反，您可以通過使用描述符來取消它們在使用這些標準資源的各個方案中的使用。

### 建立欄位棄用描述符 {#create-descriptor}

要為要棄用的架構欄位建立POST符，請向 `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 描述符的類型。 對於欄位棄用描述符，必須將此值設定為 `xdm:descriptorDeprecated`。 |
| `xdm:sourceSchema` | URI `$id` 將描述符應用到的架構。 |
| `xdm:sourceVersion` | 要將描述符應用到的架構的版本。 應設定為 `1`。 |
| `xdm:sourceProperty` | 將描述符應用到的架構中的屬性的路徑。 如果要將描述符應用於多個屬性，可以以陣列的形式提供路徑清單(例如， `["/firstName", "/lastName"]`)。 |

**回應**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### 驗證已棄用欄位 {#verify-deprecation}

在應用描述符後，您可以使用相應的方法查找有關的架構，以驗證是否已棄用該欄位 `Accept` 標題。

>[!NOTE]
>
>當列出架構時顯示不建議使用的欄位。

**API格式**

```http
GET /tenant/schemas
```

**要求**

要在API響應中包括有關已過時欄位的資訊，必須設定 `Accept` 標題 `application/vnd.adobe.xed-deprecatefield+json; version=1`。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**回應**

成功的響應將返回架構的詳細資訊，其中不建議使用的欄位包含 `meta:status` 值 `deprecated`。 下面的示例響應已被截斷為空間。

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## 後續步驟

本文檔介紹了如何使用架構註冊表API棄用XDM欄位。 有關為自定義資源配置欄位的詳細資訊，請參見上的指南 [定義API中的XDM欄位](./custom-fields-api.md)。 有關管理描述符的詳細資訊，請參見 [描述符端點指南](../api/descriptors.md)。
