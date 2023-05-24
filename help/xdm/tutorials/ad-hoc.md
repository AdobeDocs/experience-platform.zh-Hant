---
keywords: Experience Platform；主題；熱門主題；api;XDM;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；架構註冊；架構註冊；ad-hoc;ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Adhoc；教程；教程；建立；架構；架構
solution: Experience Platform
title: 建立即席架構
description: 在特定情況下，可能需要建立一個體驗資料模型(XDM)架構，該架構包含僅由單個資料集使用而命名的欄位。 這稱為「臨時」架構。 Ad-hoc模式用於各種資料接收工作流以進行Experience Platform，包括接收CSV檔案和建立某些類型的源連接。
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 2%

---

# 建立即席架構

在特定情況下，可能需要 [!DNL Experience Data Model] (XDM)模式，其欄位僅由單個資料集使用。 這稱為「臨時」架構。 在各種資料接收工作流中使用點對點模式 [!DNL Experience Platform]，包括插入CSV檔案和建立某些類型的源連接。

本文檔提供了使用 [架構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 它打算與其他 [!DNL Experience Platform] 要求在工作流中建立臨時架構的教程。 每個文檔都提供了有關如何為特定用例正確配置臨時架構的詳細資訊。

## 快速入門

本教程要求您對 [!DNL Experience Data Model] (XDM)系統。 在開始本教程之前，請查看以下XDM文檔：

- [XDM系統概述](../home.md):XDM及其在XDM中的實施 [!DNL Experience Platform]。
- [架構組合的基礎](../schema/composition.md):XDM架構的基本元件概述。

在開始本教程之前，請複習 [開發者指南](../api/getting-started.md) 獲取您需要瞭解的重要資訊，以便成功撥打 [!DNL Schema Registry] API。 這包括您 `{TENANT_ID}`、「容器」的概念和發出請求所需的標頭（特別要注意「接受」標頭及其可能值）。

## 建立即席類

XDM架構的資料行為由其基礎類決定。 建立即席模式的第一步是根據 `adhoc` 行為。 這是通過向 `/tenant/classes` 端點。

**API格式**

```http
POST /tenant/classes
```

**要求**

以下請求將建立一個新的XDM類，該類由負載中提供的屬性配置。 通過提供 `$ref` 屬性設定為 `https://ns.adobe.com/xdm/data/adhoc` 的 `allOf` 陣列，此類繼承 `adhoc` 行為。 該請求還定義了 `_adhoc` 對象，其中包含類的自定義欄位。

>[!NOTE]
>
>在下定義的自定義欄位 `_adhoc` 視即席模式的使用情況而定。 請參考相應教程中的特定工作流，以瞭解根據使用案例需要的自定義欄位。

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
| `$ref` | 新類的資料行為。 對於即席類，必須將此值設定為 `https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含類的自定義欄位的對象，表示為欄位名和資料類型的鍵值對。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新類的詳細資訊，替換 `properties._adhoc` 對象的名稱，其GUID是類的系統生成的只讀唯一標識符。 的 `meta:datasetNamespace` 屬性也自動生成並包含在響應中。

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
| `$id` | 用作新ad-hoc類的只讀系統生成的唯一標識符的URI。 此值用於建立即席架構的下一步。 |

{style="table-layout:auto"}

## 建立即席架構

建立即席類後，可以通過向POST請求建立實現該類的新架構 `/tenant/schemas` 端點。

**API格式**

```http
POST /tenant/schemas
```

**要求**

以下請求建立新架構，提供引用(`$ref`) `$id` 以前建立的ad-hoc類的負載。

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

## 查看完整即席架構

>[!NOTE]
>
>此步驟為選填。如果不想檢查即席架構的欄位結構，可跳至 [後續步驟](#next-steps) 的下一頁。

建立即席架構後，可以發出查找(GET)請求，以查看其展開形式的架構。 這是通過在GET請求中使用相應的「接受」標頭來完成的，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 訪問的臨時架構。 |

{style="table-layout:auto"}

**要求**

以下請求使用「接受」標題 `application/vnd.adobe.xed-full+json; version=1`，它返回模式的擴展形式。 請注意，在從 [!DNL Schema Registry]，請求的「接受」標頭必須包含有關資源的主版本。

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

成功的響應返回架構的詳細資訊，包括嵌套在 `properties`。

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

按照本教程，您已成功建立了新的即席架構。 如果您作為另一教程的一部分被帶到此文檔，則現在可以使用 `$id` 即席模式，按照指示完成工作流。

有關使用的詳細資訊 [!DNL Schema Registry] API，請參閱 [開發者指南](../api/getting-started.md)。
