---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；架構註冊；架構註冊；架構註冊；架構；架構；架構；架構；建立
solution: Experience Platform
title: 架構API終結點
description: 通過架構註冊表API中的/schemas終結點，可以以寫程式方式管理體驗應用程式中的XDM架構。
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 2%

---

# 架構終結點

可以將模式視為您希望輸入到Adobe Experience Platform的資料的藍圖。 每個架構由類和零個或多個架構欄位組組成。 的 `/schemas` 端點 [!DNL Schema Registry] API允許您以寫程式方式管理體驗應用程式中的架構。

## 快速入門

本指南中使用的API終結點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索方案清單 {#list}

您可以在 `global` 或 `tenant` 容器：向 `/global/schemas` 或 `/tenant/schemas`的下界。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 要返回超出此限制的資源，必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少返回的資源數。 請參閱 [查詢參數](./appendix.md#query) 的子菜單。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 儲存要檢索的架構的容器： `global` 用於Adobe建立的架構或 `tenant` 為組織擁有的架構。 |
| `{QUERY_PARAMS}` | 用於篩選結果的可選查詢參數。 查看 [附錄文檔](./appendix.md#query) 的子菜單。 |

{style="table-layout:auto"}

**要求**

以下請求從 `tenant` 容器，使用 `orderby` 查詢參數，按結果排序 `title` 屬性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

響應格式取決於 `Accept` 請求中發送的標頭。 以下 `Accept` 標題可用於清單架構：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標頭。 (限制：300) |
| `application/vnd.adobe.xed+json` | 為每個資源返回完整的JSON架構（原始） `$ref` 和 `allOf` 包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

上述請求使用 `application/vnd.adobe.xed-id+json` `Accept` 標頭，因此響應僅包括 `title`。 `$id`。 `meta:altId`, `version` 每個架構的屬性。 使用其他 `Accept` 標題(H)`application/vnd.adobe.xed+json`)返回每個架構的所有屬性。 選擇相應的 `Accept` 標題，具體取決於您在回應中需要的資訊。

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

可以通過發出GET請求來查找特定架構，該請求在路徑中包括該架構的ID。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 儲存要檢索的架構的容器： `global` Adobe建立的架構或 `tenant` 組織擁有的架構。 |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL編碼 `$id` 要查找的架構。 |

{style="table-layout:auto"}

**要求**

以下請求檢索其指定的架構 `meta:altId` 值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 和 `allOf` 已解析，有標題和說明。 不建議使用的欄位 `meta:status` 屬性 `deprecated`。 |

{style="table-layout:auto"}

**回應**

成功的響應返回架構的詳細資訊。 返回的欄位取決於 `Accept` 請求中發送的標頭。 不同實驗 `Accept` 標題：比較響應並確定哪個標題最適合您的使用案例。

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
  "imsOrg": "{ORG_ID}",
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

## 建立方案 {#create}

架構合成過程從分配類開始。 該類定義資料（記錄或時間序列）的關鍵行為方面以及描述將要接收的資料所需的最小欄位。

>[!NOTE]
>
>下面的示例調用只是有關如何在API中建立架構的基準示例，該架構具有類的最小合成要求且沒有欄位組。 有關如何在API中建立架構的完整步驟，包括如何使用欄位組和資料類型分配欄位，請參見 [架構建立教程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**要求**

請求必須包括 `allOf` 引用的屬性 `$id` 班級的。 此屬性定義架構將實現的「基類」。 在本示例中，基類是以前建立的「屬性資訊」類。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `allOf` | 對象陣列，每個對象引用其模式實現的欄位的類或欄位組。 每個對象都包含一個屬性(`$ref`)，其值表示 `$id` 新架構將實現的類或欄位組。 必須提供一個類，並且包含零個或多個附加欄位組。 在上例中， `allOf` array是架構的類。 |

{style="table-layout:auto"}

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立架構的詳細資訊的負載，包括 `$id`。 `meta:altId`, `version`。 這些值是只讀的，由 [!DNL Schema Registry]。

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
    "imsOrg": "{ORG_ID}",
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

執行GET請求 [列出所有架構](#list) 現在，租戶容器中將包含新架構。 您可以執行 [查找(GET)請求](#lookup) 使用URL編碼 `$id` URI，用於直接查看新架構。

要向架構添加其他欄位，可以執行 [PATCH操作](#patch) 將欄位組添加到架構 `allOf` 和 `meta:extends` 陣列。

## 更新架構 {#put}

您可以通過PUT操作替換整個架構，實際上就是重寫資源。 通過PUT請求更新架構時，主體必須包括在 [建立新架構](#create) POST。

>[!NOTE]
>
>如果只想更新部分架構而不是完全替換它，請參見上的 [更新模式的一部分](#patch)。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL編碼 `$id` 要重寫的架構。 |

{style="table-layout:auto"}

**要求**

以下請求替換現有架構，並更改其 `title`。 `description`, `allOf` 屬性。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

可以使用PATCH請求更新方案的一部分。 的 [!DNL Schema Registry] 支援所有標準JSON修補程式操作，包括 `add`。 `remove`, `replace`。 有關JSON修補程式的詳細資訊，請參見 [API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱上的部分 [使用PUT操作替換模式](#put)。

最常見的PATCH操作之一涉及將先前定義的欄位組添加到架構中，如下例所示。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 要更新的架構。 |

{style="table-layout:auto"}

**要求**

下面的示例請求通過添加該欄位組的 `$id` 值 `meta:extends` 和 `allOf` 陣列。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象都包括要執行的操作(`op`)，應對(執行的操作`path`)，以及該操作中應包含哪些資訊(`value`)。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

該響應顯示已成功執行兩個操作。 欄位組 `$id` 已添加到 `meta:extends` 陣列和引用(`$ref`)到欄位組 `$id` 的 `allOf` 陣列。

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
    "imsOrg": "{ORG_ID}",
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

## 啟用用於即時客戶配置檔案的方案 {#union}

為了讓架構參與 [即時客戶配置檔案](../../profile/home.md)，必須添加 `union` 標籤到架構 `meta:immutableTags` 陣列。 可以通過對有關的架構發出PATCH請求來完成此操作。

>[!IMPORTANT]
>
>不可變標籤是要設定但從未刪除的標籤。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 的子菜單。 |

{style="table-layout:auto"}

**要求**

下面的示例請求將 `meta:immutableTags` 陣列到現有架構，為陣列提供 `union` 啟用它以在配置檔案中使用。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的響應將返回更新的架構的詳細資訊，顯示 `meta:immutableTags` 已添加陣列。

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
    "imsOrg": "{ORG_ID}",
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

現在，您可以查看此架構類的聯合，以確認已表示該架構的欄位。 查看 [聯合端點指南](./unions.md) 的子菜單。

## 刪除架構 {#delete}

有時可能需要從架構註冊表中刪除架構。 這是通過執行DELETE請求來完成的，該請求的模式ID在路徑中提供。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 的子菜單。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態204（無內容）和空白正文。

您可以通過嘗試對架構進行查找(GET)請求來確認刪除。 您需要包括 `Accept` 請求中的標頭，但應接收HTTP狀態404（未找到），因為該架構已從架構註冊表中刪除。
