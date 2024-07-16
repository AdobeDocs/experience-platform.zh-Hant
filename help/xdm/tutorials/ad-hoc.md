---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；Schema登入；ad-hoc；ad-hoc；Ad-hoc；Ad-hoc；教學課程；教學課程；建立；結構描述；結構描述
solution: Experience Platform
title: 建立臨時結構描述
description: 在特定情況下，可能需要建立體驗資料模型(XDM)結構描述，其欄位需由單一資料集命名以供使用。 這稱為「臨機」結構描述。 臨機結構用於各種資料擷取工作流程中以進行Experience Platform，包括擷取CSV檔案和建立特定型別的來源連線。
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# 建立臨時結構描述

在特定情況下，可能需要建立[!DNL Experience Data Model] (XDM)結構描述，其欄位必須由單一資料集命名以供使用。 這稱為「臨機」結構描述。 特定結構描述用於[!DNL Experience Platform]的各種資料擷取工作流程，包括擷取CSV檔案和建立特定型別的來源連線。

本檔案提供使用[結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)建立臨機結構描述的一般步驟。 此教學課程旨在搭配其他[!DNL Experience Platform]教學課程使用，這些教學課程需要建立隨選結構描述作為其工作流程的一部分。 其中每個檔案都提供了有關如何為其特定使用案例正確配置臨時方案的詳細資訊。

## 快速入門

此教學課程需要實際瞭解[!DNL Experience Data Model] (XDM)系統。 開始進行本教學課程之前，請先檢閱下列XDM檔案：

- [XDM系統總覽](../home.md)： [!DNL Experience Platform]中XDM及其實作的高層級總覽。
- [結構描述組合的基本概念](../schema/composition.md)： XDM結構描述的基本元件概觀。

開始進行此教學課程之前，請檢閱[開發人員指南](../api/getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫[!DNL Schema Registry] API。 這包括您的`{TENANT_ID}`、「容器」的概念，以及發出要求所需的標頭（特別注意Accept標頭及其可能的值）。

## 建立臨時類別

XDM結構描述的資料行為取決於其基礎類別。 建立臨時結構描述的第一步是根據`adhoc`行為建立類別。 這是透過向`/tenant/classes`端點發出POST要求來完成。

**API格式**

```http
POST /tenant/classes
```

**要求**

以下請求會建立新的XDM類別，由承載中提供的屬性設定。 透過提供`allOf`陣列中設定為`https://ns.adobe.com/xdm/data/adhoc`的`$ref`屬性，此類別會繼承`adhoc`行為。 此要求也定義了`_adhoc`物件，其中包含類別的自訂欄位。

>[!NOTE]
>
>在`_adhoc`下定義的自訂欄位會依臨機操作結構描述的使用案例而有所不同。 如需根據使用案例的必要自訂欄位，請參閱相關教學課程中的特定工作流程。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `$ref` | 新類別的資料行為。 若為臨機類別，此值必須設為`https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含類別自訂欄位的物件，以欄位名稱和資料型別的索引鍵值配對表示。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新類別的詳細資料，將`properties._adhoc`物件的名稱取代為系統產生的類別唯讀唯一識別碼GUID。 `meta:datasetNamespace`屬性也會自動產生並包含在回應中。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `$id` | 作為唯讀、系統為新的ad-hoc類別產生的唯一識別碼的URI。 此值用於建立臨機模式的下一個步驟。 |

{style="table-layout:auto"}

## 建立臨時結構描述

一旦建立臨機類別後，您就可以對`/tenant/schemas`端點發出POST要求，建立實作該類別的新結構描述。

**API格式**

```http
POST /tenant/schemas
```

**要求**

下列要求會建立新的結構描述，提供其承載中先前建立之臨機類別的`$id`的參考(`$ref`)。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**回應**

成功的回應會傳回新建立之結構描述的詳細資料，包括其系統產生的唯讀`$id`。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## 檢視完整的臨時結構描述

>[!NOTE]
>
>此步驟為選填。如果您不想檢查臨機操作結構描述的欄位結構，您可以跳至本教學課程結尾的[後續步驟](#next-steps)區段。

建立臨時結構描述後，您可以提出查詢(GET)請求，以檢視其展開形式的結構描述。 若要這麼做，請在GET請求中使用適當的Accept標頭，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的`$id` URI或您要存取的臨時結構描述的`meta:altId`。 |

{style="table-layout:auto"}

**要求**

下列要求使用Accept標頭`application/vnd.adobe.xed-full+json; version=1`，這會傳回結構描述的展開形式。 請注意，從[!DNL Schema Registry]擷取特定資源時，請求的Accept標頭必須包含相關資源的主要版本。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回結構描述的詳細資料，包括`properties`下巢狀的所有欄位。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功建立新的臨時結構描述。 如果您是作為其他教學課程的一部分而閱讀本檔案，您現在可以使用臨機結構描述的`$id`依照指示完成工作流程。

如需使用[!DNL Schema Registry] API的詳細資訊，請參閱[開發人員指南](../api/getting-started.md)。
