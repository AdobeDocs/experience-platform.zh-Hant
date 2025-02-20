---
title: 棄用API中的XDM欄位
description: 瞭解如何淘汰結構描述登入API中的Experience Data Model (XDM)欄位。
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---

# 棄用API中的XDM欄位

在Experience Data Model (XDM)中，您可以使用[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)來取代結構描述或自訂資源中的欄位。 棄用欄位會使其在下游UI (例如[!UICONTROL 設定檔]工作區和Customer Journey Analytics)中隱藏，但這是不中斷的變更，不會對現有資料流程造成負面影響。

本文介紹如何為不同的XDM資源棄用欄位。 如需在Experience Platform使用者介面中使用「結構描述編輯器」來取代XDM欄位的步驟，請參閱有關[取代UI](./field-deprecation-ui.md)中的XDM欄位的教學課程。

## 快速入門

本教學課程需要呼叫Schema Registry API。 請檢閱[開發人員指南](../api/getting-started.md)，以取得進行這些API呼叫所需瞭解的重要資訊。 這包括您的`{TENANT_ID}`、「容器」的概念以及發出要求所需的標頭（特別注意`Accept`標頭及其可能的值）。

## 棄用自訂欄位 {#custom}

若要棄用自訂類別、欄位群組或資料型別中的欄位，請透過PUT或PATCH要求更新自訂資源，並將屬性`meta:status: deprecated`新增到相關欄位。

>[!NOTE]
>
>如需更新XDM中自訂資源的一般資訊，請參閱下列檔案：
>
>* [更新類別](../api/classes.md#patch)
>* [更新欄位群組](../api/field-groups.md#patch)
>* [更新資料型別](../api/data-types.md#patch)

以下範例API呼叫會淘汰自訂資料型別中的欄位。

**API格式**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**要求**

下列要求會針對描述不動產屬性的資料型別，取代`expansionArea`欄位。

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

成功的回應會傳回自訂資源的更新詳細資料，且已棄用的欄位包含`meta:status`值`deprecated`。 以下範例回應已截斷空格。

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

## 棄用結構描述中的標準欄位 {#standard}

標準類別、欄位群組和資料型別中的欄位無法直接棄用。 反之，您可以在採用這些標準資源的個別結構描述中，使用描述項來取代標準資源。

### 建立欄位取代描述項 {#create-descriptor}

若要為您要棄用的結構描述欄位建立描述項，請對`/tenant/descriptors`端點發出POST要求。

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
| `@type` | 描述項的型別。 對於欄位取代描述項，此值必須設定為`xdm:descriptorDeprecated`。 |
| `xdm:sourceSchema` | 您要套用描述項之結構描述的URI `$id`。 |
| `xdm:sourceVersion` | 您要套用描述項的結構描述版本。 應該設定為`1`。 |
| `xdm:sourceProperty` | 在要套用描述項的結構描述中，屬性的路徑。 如果您想要將描述項套用至多個屬性，可以陣列形式提供路徑清單（例如，`["/firstName", "/lastName"]`）。 |

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

### 驗證已棄用的欄位 {#verify-deprecation}

在套用描述項後，您可以在使用適當的`Accept`標頭時查詢相關結構描述，以驗證欄位是否已過時。

>[!NOTE]
>
>目前不支援在列出結構描述時顯示已棄用的欄位。

**API格式**

```http
GET /tenant/schemas
```

**要求**

若要在API回應中包含已棄用欄位的相關資訊，您必須將`Accept`標題設定為`application/vnd.adobe.xed-deprecatefield+json; version=1`。

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

成功的回應會傳回結構描述的詳細資料，已棄用的欄位包含`meta:status`值`deprecated`。 以下範例回應已截斷空格。

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

本檔案說明如何使用結構描述登入API來棄用XDM欄位。 如需設定自訂資源欄位的詳細資訊，請參閱[在API中定義XDM欄位的指南](./custom-fields-api.md)。 如需有關管理描述元的詳細資訊，請參閱[描述元端點指南](../api/descriptors.md)。
