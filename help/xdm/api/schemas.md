---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 建立架構
description: 架構註冊表API中的/schemas端點可讓您以程式設計方式管理體驗應用程式中的XDM架構。
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 2%

---


# 方案端點

架構可視為您要匯入Adobe Experience Platform之資料的藍圖。 每個模式由類和零個或多個混合組成。 API中 `/schemas` 的端點可讓您以程式設計方式 [!DNL Schema Registry] 管理體驗應用程式中的架構。

## 快速入門

本指南中使用的API端點是 [[!DNL Schema Registry] API的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 在繼續之前，請先閱讀快速入門手冊 [](./getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 檢索方案清單 {#list}

您可以分別對或發出GET `global` 請求， `tenant` 以列出或容器下 `/global/schemas` 的所有方案 `/tenant/schemas`。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 如需詳細資訊，請 [參閱附錄檔案](./appendix.md#query) 中查詢參數一節。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之結構的容器： `global` 適用於Adobe建立的結構描述 `tenant` 或您組織擁有的結構描述。 |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 如需可用 [參數的清單](./appendix.md#query) ，請參閱附錄檔案。 |

**請求**

以下請求從容器中檢索方案列 `tenant` 表，使用查 `orderby` 詢參數按結果屬性對結果進行 `title` 排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於在請求 `Accept` 中傳送的標題。 列出方 `Accept` 案時，可使用以下標題：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，其中包含 `$ref` 原始 `allOf` 資源。 (限制：300) |

**回應**

上述請求使用標 `application/vnd.adobe.xed-id+json` 題，因此回應僅包 `Accept` 含每個方案的 `title`、 `$id``meta:altId`和 `version` 屬性。 使用其他標 `Accept` 題(`application/vnd.adobe.xed+json`)會傳回每個架構的所有屬性。 根據您在回 `Accept` 應中需要的資訊，選擇適當的標題。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## 查找架構 {#lookup}

您可以通過發出GET請求來查找特定方案，該請求在路徑中包括方案的ID。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之結構的容器： `global` 適用於Adobe建立的架構或 `tenant` 您組織擁有的架構。 |
| `{SCHEMA_ID}` | 您 `meta:altId` 要尋找之 `$id` 結構的或URL編碼。 |

**請求**

以下請求檢索路徑中由其值指 `meta:altId` 定的方案。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

成功的響應返回方案的詳細資訊。 傳回的欄位取決於請求 `Accept` 中傳送的標題。 嘗試不同 `Accept` 的標題以比較回應，並判斷哪個標題最適合您的使用案例。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立架構 {#create}

架構構成過程從分配類開始。 該類定義資料的關鍵行為方面（記錄或時間序列），以及描述將接收的資料所需的最小欄位。

>[!NOTE]
>
>以下範例呼叫僅是如何在API中建立架構的基準範例，其中類別的構圖需求最低，而無混音。 如需如何在API中建立架構的完整步驟，包括如何使用混合和資料類型指派欄位，請參閱架構建 [立教學課程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**請求**

請求必須包含 `allOf` 引用類的 `$id` 屬性。 此屬性定義了方案將實施的「基本類」。 在此範例中，基本類別是先前建立的「屬性資訊」類別。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `allOf` | 對象陣列，每個對象引用模式實現其欄位的類或混合。 每個對象都包含一個屬性(`$ref`)，其值表示將實 `$id` 現的類或新模式中混合的類。 必須提供一個類別，並附加零個或多個混音。 在上例中，陣列中的單 `allOf` 個對象是方案的類。 |

**回應**

成功的回應會傳回HTTP狀態201（已建立）和包含新建架構詳細資訊的裝載，包括 `$id`、 `meta:altId`和 `version`。 這些值是唯讀的，由指定 [!DNL Schema Registry]。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

執行GET請求以列 [出租用戶容器中](#list) ，現在會包含新的結構。 您可以使 [用URL編碼的](#lookup) URI來執行查 `$id` 閱(GET)請求，以直接檢視新結構。

要向架構添加其他欄位，可以執行 [PATCH操作](#patch) ，以向架構和陣列添加混 `allOf` 合 `meta:extends` 集。

## 更新架構 {#put}

您可以通過PUT操作替換整個模式，實際上重寫資源。 通過PUT請求更新方案時，主體必須包含在POST請求中建立新方案 [時所需的所有欄位](#create) 。

>[!NOTE]
>
>如果您只想更新架構的一部分，而不是完全替換它，請參見有關更 [新架構部分的部分](#patch)。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 您 `meta:altId` 要重寫之 `$id` 結構的或URL編碼。 |

**請求**

下列請求會取代現有的架構，並變更其 `title`、 `description`和 `allOf` 屬性。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**回應**

成功的響應返回更新的架構的詳細資訊。

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 更新架構的一部分 {#patch}

您可以使用PATCH請求來更新方案的一部分。 支援 [!DNL Schema Registry] 所有標準JSON修補程式作業， `add`包括 `remove`、和 `replace`。 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參見有關使用PUT [操作替換方案的部分](#put)。

最常見的PATCH操作之一是將先前定義的混合添加到模式，如下例所示。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的 `$id` URI或 `meta:altId` 您要更新的架構。 |

**請求**

下面的示例請求通過將mixin的值添加到陣列和陣列中，將 `$id` 新的混 `meta:extends` 合添加到 `allOf` 架構。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象包括要執行的操作(`op`)，該操作應在哪個欄位上執行(`path`)，以及該操作應包括哪些資訊(`value`)。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**回應**

響應顯示兩個操作均成功執行。 混頻已 `$id` 經添加到陣列 `meta:extends` 中，而混頻的參考(`$ref`)現在出現 `$id` 在陣列中 `allOf` 。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 啟用結構以用於即時客戶描述檔 {#union}

為了讓結構參與 [即時客戶配置檔案](../../profile/home.md)，必須向結構 `union` 的陣列添加標 `meta:immutableTags` 記。 您可以通過對相關方案發出PATCH請求來完成此操作。

>[!IMPORTANT]
>
>不可變標籤是要設定但從不移除的標籤。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的 `$id` URI或 `meta:altId` 您要啟用的架構。 |

**請求**

下面的示例請求將數 `meta:immutableTags` 組添加到現有模式，為陣列提供單個字串值，以 `union` 便在配置檔案中使用。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**回應**

成功的響應返回更新模式的詳細資訊，顯示 `meta:immutableTags` 陣列已添加。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

您現在可以查看此架構類的union，以確認已表示該架構的欄位。 See the [unions endpoint guide](./unions.md) for more information.

## 刪除架構 {#delete}

有時可能需要從架構註冊表中刪除架構。 這是透過使用路徑中提供的架構ID執行DELETE請求來完成的。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的 `$id` URI或 `meta:altId` 您要刪除之架構的URI。 |

**請求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。

您可以嘗試對結構進行查閱(GET)請求，以確認刪除。 您需要在請求中加 `Accept` 入標題，但應會收到HTTP狀態404（找不到），因為架構已從架構註冊表中移除。