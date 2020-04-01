---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立臨機結構
topic: tutorials
translation-type: tm+mt
source-git-commit: 956d1e5b4a994c9ea52d818f3dd6d3ff88cb16b6

---


# 建立臨機結構

在特定情況下，可能需要建立Experience Data Model(XDM)架構，其中欄位的名稱僅限單一資料集使用。 這稱為「臨機」架構。 臨機結構描述用於Experience Platform的各種資料擷取工作流程，包括擷取CSV檔案並建立特定類型的來源連線。

本檔案提供使用架構註冊表API建立臨機架構的一 [般步驟](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 它可與其他需要在工作流程中建立臨機架構的Experience Platform教學課程搭配使用。 這些文檔中的每個文檔都提供了有關如何為特定使用案例正確配置臨時架構的詳細資訊。

## 快速入門

本教學課程需要對體驗資料模型(XDM)系統有良好的認識。 開始本教學課程之前，請先閱讀下列XDM檔案：

- [XDM系統概述](../home.md):XDM及其在Experience Platform中的實作概觀。
- [架構構成基礎](../schema/composition.md):概述XDM架構的基本元件。

在開始本教學課程之前，請先閱讀開 [發人員指南](../api/getting-started.md) ，以取得成功呼叫架構註冊表API所需的重要資訊。 這包括您 `{TENANT_ID}`的「容器」概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。

## 建立臨機類別

XDM模式的資料行為由其基礎類確定。 建立臨機架構的第一步是根據行為建立類 `adhoc` 別。 這是通過向端點發出POST請求來完 `/tenant/classes` 成的。

**API格式**

```http
POST /tenant/classes
```

**請求**

下列請求會建立新的XDM類別，由裝載中提供的屬性設定。 通過在數 `$ref` 組中提供 `https://ns.adobe.com/xdm/data/adhoc` 設定為的 `allOf` 屬性，此類繼承行為 `adhoc` 。 此請求還定義 `_adhoc` 了一個對象，該對象包含類的自定義欄位。

>[!NOTE] 在下定義的自訂欄 `_adhoc` 位會依臨機架構的使用案例而有所不同。 請參考適當教學課程中的特定工作流程，以根據使用案例，針對必要的自訂欄位。

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
| `$ref` | 新類的資料行為。 對於臨機類，此值必須設定為 `https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含類自定義欄位的對象，表示為欄位名和資料類型的鍵值對。 |

**回應**

成功的響應返回新類的詳細資訊，用 `properties._adhoc` GUID替換對象的名稱，該GUID是系統生成的唯讀類唯一標識符。 屬性 `meta:datasetNamespace` 也會自動產生，並包含在回應中。

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
| `$id` | 作為唯讀系統生成新臨機類唯一標識符的URI。 此值用於建立臨機結構的下一個步驟。 |

## 建立臨機結構

建立臨機類別後，您就可以建立新的架構，透過對端點提出POST請求來實作該類 `/tenant/schemas` 別。

**API格式**

```http
POST /tenant/schemas
```

**請求**

下列請求會建立新的架構，提供(`$ref`)先前建 `$id` 立之臨機類別在其裝載中的參考。

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

成功的響應返回新建立的架構的詳細資訊，包括其系統生成的只讀模式 `$id`。

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

## 檢視完整的臨機架構

>[!NOTE] 此步驟為可選步驟。 如果您不想檢查臨機架構的欄位結構，可跳至本教學課程結 [束時的](#next-steps) 「後續步驟」一節。

在建立臨機結構描述後，您就可以進行查詢(GET)請求，以擴充的形式檢視結構描述。 在GET請求中使用適當的「接受」標題即可完成，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 您要存取的 `$id` 臨機 `meta:altId` 結構的URL編碼URI或URI。 |

**請求**

以下請求使用「接受」標 `application/vnd.adobe.xed-full+json; version=1`題，該標題會傳回架構的擴充形式。 請注意，從方案註冊表檢索特定資源時，請求的「接受」標題必須包含相關資源的主要版本。

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

成功的響應返回方案的詳細資訊，包括下嵌套的所有欄位 `properties`。

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

## 下一步 {#next-steps}

遵循本教學課程，您已成功建立新的臨機結構。 如果您是作為另一個教學課程的一部分來到本檔案，您現在可以使用臨機 `$id` 架構依照指示完成工作流程。

有關使用架構註冊表API的詳細資訊，請參閱開發人員 [指南](../api/getting-started.md)。