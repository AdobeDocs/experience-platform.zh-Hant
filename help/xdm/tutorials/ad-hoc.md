---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構登錄；結構註冊表；臨機；臨機；臨機；臨機；教學課程；教學課程；建立；結構；結構
solution: Experience Platform
title: 建立臨機結構
description: 在特定情況下，您可能需要建立Experience Data Model(XDM)結構，其中欄位的命名空間僅限單一資料集使用。 這稱為「臨機」結構。 臨機結構用於各種資料擷取工作流程中，以供Experience Platform使用，包括擷取CSV檔案和建立特定類型的來源連線。
topic-legacy: tutorial
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 3%

---

# 建立隨選結構

在特定情況下，您可能需要建立[!DNL Experience Data Model](XDM)架構，其中的欄位命名空間僅限單一資料集使用。 這稱為「臨機」結構。 [!DNL Experience Platform]的各種資料擷取工作流程中會使用臨機結構，包括擷取CSV檔案和建立特定類型的來源連線。

本檔案提供使用[Schema Registry API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)建立臨機架構的一般步驟。 它旨在與其他需要建立隨選架構作為其工作流程一部分的[!DNL Experience Platform]教學課程搭配使用。 這些檔案都提供如何為其特定使用案例正確配置臨時架構的詳細資訊。

## 快速入門

本教學課程需要妥善了解[!DNL Experience Data Model](XDM)系統。 開始本教學課程之前，請先檢閱下列XDM檔案：

- [XDM系統概觀](../home.md):概略概述XDM及其實作於中 [!DNL Experience Platform]。
- [結構構成基本概念](../schema/composition.md):概述XDM結構的基本元件。

開始本教學課程之前，請檢閱[開發人員指南](../api/getting-started.md)，以取得您需要了解的重要資訊，以便成功呼叫[!DNL Schema Registry] API。 這包括您的`{TENANT_ID}`、「容器」的概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。

## 建立臨機類別

XDM架構的資料行為由其基礎類別決定。 建立臨機架構的第一步是根據`adhoc`行為建立類。 這是透過向`/tenant/classes`端點提出POST要求來完成。

**API格式**

```http
POST /tenant/classes
```

**要求**

下列請求會建立新的XDM類別，由裝載中提供的屬性設定。 通過在`allOf`陣列中提供設定為`https://ns.adobe.com/xdm/data/adhoc`的`$ref`屬性，該類繼承`adhoc`行為。 請求還定義了`_adhoc`對象，該對象包含類的自定義欄位。

>[!NOTE]
>
>`_adhoc`下定義的自訂欄位會依臨機架構的使用案例而有所不同。 請根據使用案例，針對必要的自訂欄位，參閱適當教學課程中的特定工作流程。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `$ref` | 新類的資料行為。 對於臨機類，此值必須設定為`https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含類別自訂欄位的物件，以欄位名稱和資料類型的索引鍵值組表示。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回新類的詳細資訊，將`properties._adhoc`對象的名稱替換為系統生成的只讀類唯一標識符GUID。 也會自動產生`meta:datasetNamespace`屬性並包含在回應中。

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
    "imsOrg": "{IMS_ORG}",
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

{style=&quot;table-layout:auto&quot;}

## 建立隨選結構

建立臨機類後，可通過向`/tenant/schemas`端點發出POST請求來建立實施該類的新架構。

**API格式**

```http
POST /tenant/schemas
```

**要求**

下列請求會建立新結構，為先前建立之臨機類別的裝載中的`$id`提供參考(`$ref`)。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的響應返回新建架構的詳細資訊，包括其系統生成的只讀`$id`。

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
    "imsOrg": "{IMS_ORG}",
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
>此步驟為選填。如果您不想檢查臨機架構的欄位結構，可跳到本教學課程結尾的[下一步](#next-steps)區段。

建立隨選結構後，您可以進行查詢(GET)請求，以展開形式檢視結構。 請在GET要求中使用適當的Accept標題來完成，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要訪問的臨機架構的URL編碼的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求使用Accept標頭`application/vnd.adobe.xed-full+json; version=1`，其返回架構的擴展形式。 請注意，從[!DNL Schema Registry]擷取特定資源時，請求的Accept標題必須包含相關資源的主要版本。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回架構的詳細資訊，包括`properties`下嵌套的所有欄位。

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
    "imsOrg": "{IMS_ORG}",
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

依照本教學課程，您已成功建立新的臨機結構。 如果您是作為其他教學課程的一部分帶到本檔案，您現在可以使用臨機架構的`$id`依照指示完成工作流程。

有關使用[!DNL Schema Registry] API的詳細資訊，請參閱[開發人員指南](../api/getting-started.md)。
