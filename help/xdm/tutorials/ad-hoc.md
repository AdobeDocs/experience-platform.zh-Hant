---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構登錄；結構註冊表；臨機；臨機；臨機；臨機；教學課程；教學課程；建立；結構；結構
solution: Experience Platform
title: 建立臨機結構
description: 在特定情況下，您可能需要建立Experience Data Model(XDM)結構，其中欄位的命名空間僅限單一資料集使用。 這稱為「臨機」結構。 臨機結構用於各種資料擷取工作流程中，以供Experience Platform使用，包括擷取CSV檔案和建立特定類型的來源連線。
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 2%

---

# 建立隨選結構

在特定情況下，可能需要建立 [!DNL Experience Data Model] (XDM)結構，其欄位的名稱僅限單一資料集使用。 這稱為「臨機」結構。 臨機結構用於的各種資料擷取工作流程 [!DNL Experience Platform]，包括擷取CSV檔案和建立特定類型的來源連線。

本檔案提供使用 [結構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 其目的是與其他 [!DNL Experience Platform] 需要在工作流程中建立臨機結構的教學課程。 這些檔案都提供如何為其特定使用案例正確配置臨時架構的詳細資訊。

## 快速入門

本教學課程需要深入了解 [!DNL Experience Data Model] (XDM)系統。 開始本教學課程之前，請先檢閱下列XDM檔案：

- [XDM系統概觀](../home.md):XDM及其實作的概觀，於 [!DNL Experience Platform].
- [結構構成基本概念](../schema/composition.md):概述XDM結構的基本元件。

開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 以取得您需要知道的重要資訊，以便成功對 [!DNL Schema Registry] API。 這包括 `{TENANT_ID}`、「容器」的概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。

## 建立臨機類別

XDM架構的資料行為由其基礎類別決定。 建立臨機架構的第一步，是根據 `adhoc` 行為。 若要這麼做，請向 `/tenant/classes` 端點。

**API格式**

```http
POST /tenant/classes
```

**要求**

下列請求會建立新的XDM類別，由裝載中提供的屬性設定。 提供 `$ref` 屬性設定為 `https://ns.adobe.com/xdm/data/adhoc` 在 `allOf` 陣列，此類會繼承 `adhoc` 行為。 請求也會定義 `_adhoc` 對象，包含類的自定義欄位。

>[!NOTE]
>
>下定義的自訂欄位 `_adhoc` 視臨機架構的使用案例而異。 請根據使用案例，針對必要的自訂欄位，參閱適當教學課程中的特定工作流程。

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
| `$ref` | 新類的資料行為。 對於臨機類，此值必須設定為 `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | 包含類別自訂欄位的物件，以欄位名稱和資料類型的索引鍵值組表示。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新類別的詳細資訊，取代 `properties._adhoc` 對象的名稱，該GUID是系統生成的類的唯讀標識符。 此 `meta:datasetNamespace` 屬性也會自動產生，並包含在回應中。

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
| `$id` | 作為只讀、系統生成的新Ad-Hoc類唯一標識符的URI。 此值將用於建立臨機架構的下一個步驟。 |

{style="table-layout:auto"}

## 建立隨選結構

建立隨選類別後，您就可以透過向發出POST要求，以建立實作該類別的新結構 `/tenant/schemas` 端點。

**API格式**

```http
POST /tenant/schemas
```

**要求**

下列請求會建立新結構，並提供參考(`$ref`) `$id` 的值。

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

成功的回應會傳回新建立架構的詳細資訊，包括其系統產生的唯讀 `$id`.

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

## 檢視完整的臨機結構

>[!NOTE]
>
>此步驟為選填。如果您不想檢查臨機結構的欄位結構，可跳至 [後續步驟](#next-steps) 一節。

建立隨選結構後，您可以進行查詢(GET)請求，以展開形式檢視結構。 請在GET要求中使用適當的Accept標題來完成，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 要存取的臨機結構。 |

{style="table-layout:auto"}

**要求**

以下請求使用Accept標題 `application/vnd.adobe.xed-full+json; version=1`，會傳回結構的展開形式。 請注意，從 [!DNL Schema Registry]，要求的「接受」標題必須包含相關資源的主要版本。

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

成功的回應會傳回架構的詳細資訊，包括下方巢狀的所有欄位 `properties`.

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

依照本教學課程，您已成功建立新的臨機結構。 如果您是作為其他教學課程的一部分帶到本檔案中，現在可以使用 `$id` 來依照指示完成工作流程。

如需使用的詳細資訊 [!DNL Schema Registry] API，請參閱 [開發人員指南](../api/getting-started.md).
