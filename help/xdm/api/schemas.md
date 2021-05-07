---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；模式註冊；模式註冊；模式；模式；模式；模式；模式；模式；建立
solution: Experience Platform
title: 方案API端點
description: 架構註冊表API中的/schemas端點可讓您以程式設計方式管理體驗應用程式中的XDM架構。
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 2%

---

# 方案端點

架構可視為您要收錄至Adobe Experience Platform之資料的藍圖。 每個模式由類和零個或多個模式欄位組組成。 [!DNL Schema Registry] API中的`/schemas`端點可讓您以程式設計方式管理體驗應用程式中的架構。

## 快速入門

本指南中使用的API端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 檢索方案清單{#list}

您可以分別向`/global/schemas`或`/tenant/schemas`發出GET請求，以列出`global`或`tenant`容器下的所有方案。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 還建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 如需詳細資訊，請參閱附錄檔案中有關[查詢參數](./appendix.md#query)的章節。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之結構的容器：`global`代表Adobe建立的結構，或`tenant`代表您組織擁有的結構。 |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 有關可用參數的清單，請參見[附錄文檔](./appendix.md#query)。 |

**要求**

以下請求從`tenant`容器中檢索方案清單，使用`orderby`查詢參數按其`title`屬性對結果進行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 以下`Accept`標題可用於列出方案：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，並包含原始的`$ref`和`allOf`。 (限制：300) |

**回應**

上述請求使用`application/vnd.adobe.xed-id+json` `Accept`標題，因此回應僅包含每個架構的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標題(`application/vnd.adobe.xed+json`)會傳回每個架構的所有屬性。 根據您在回應中需要的資訊，選擇適當的`Accept`標題。

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

## 查找架構{#lookup}

您可以透過在路徑中提出包含架構ID的GET請求，來尋找特定的架構。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之結構的容器：`global`代表Adobe建立的架構，或`tenant`代表您組織擁有的架構。 |
| `{SCHEMA_ID}` | 要查找的架構的`meta:altId`或URL編碼`$id`。 |

**要求**

以下請求檢索路徑中由其`meta:altId`值指定的架構。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 所有查閱請求都要求`version`包含在`Accept`標題中。 以下`Accept`標題可用：

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw含`$ref`和`allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 而且 `allOf` 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw含`$ref`和`allOf`，無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 並解 `allOf` 決，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 並解 `allOf` 決了包含的描述符。 |

**回應**

成功的響應返回方案的詳細資訊。 傳回的欄位取決於請求中傳送的`Accept`標題。 嘗試不同的`Accept`標題，以比較回應並判斷哪個標題最適合您的使用案例。

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
          "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/fieldgroups/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
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

## 建立方案{#create}

架構構成過程從分配類開始。 該類定義資料的關鍵行為方面（記錄或時間序列），以及描述將接收的資料所需的最小欄位。

>[!NOTE]
>
>以下範例呼叫只是如何在API中建立架構的基準範例，其中類別的構成需求最低，而無欄位群組。 有關如何在API中建立架構的完整步驟，包括如何使用欄位組和資料類型分配欄位，請參見[架構建立教程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**要求**

請求必須包含`allOf`屬性，該屬性引用類的`$id`。 此屬性定義了方案將實施的「基本類」。 在此範例中，基本類別是先前建立的「屬性資訊」類別。

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
| `allOf` | 對象的陣列，每個對象引用模式實施的欄位的類或欄位組。 每個對象都包含一個屬性(`$ref`)，其值代表新模式將實施的類或欄位組的`$id`。 必須提供一個類，並且包含零個或多個附加欄位組。 在上例中，`allOf`陣列中的單個對象是方案的類。 |

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立模式詳細資訊的裝載，包括`$id`、`meta:altId`和`version`。 這些值是只讀的，由[!DNL Schema Registry]指定。

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

執行[清單租用戶容器中所有結構](#list)的GET請求時，現在會包含新結構。 您可以使用URL編碼的`$id` URI來執行[查閱(GET)請求](#lookup)，以直接檢視新架構。

要向架構添加其他欄位，可以執行[PATCH操作](#patch)，以將欄位組添加到架構的`allOf`和`meta:extends`陣列。

## 更新架構{#put}

您可以通過PUT操作來替換整個方案，實際上是重寫資源。 通過PUT請求更新方案時，主體必須包括[在POST請求中建立新方案](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新架構的一部分而不是完全替換它，請參見[中有關更新架構的一部分的章節。](#patch)

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要重寫的架構的`meta:altId`或URL編碼`$id`。 |

**要求**

下列請求會取代現有結構，變更其`title`、`description`和`allOf`屬性。

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

## 更新方案{#patch}的一部分

您可以使用PATCH請求來更新方案的一部分。 [!DNL Schema Registry]支援所有標準JSON修補程式作業，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替換整個資源，而不是更新單個欄位，請參閱[中的「使用PUT操作替換方案」部分](#put)。

最常見的PATCH操作之一是將先前定義的欄位組添加到模式，如下例所示。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要更新的架構的URL編碼`$id` URI或`meta:altId`。 |

**要求**

下面的示例請求通過將欄位組的`$id`值添加到`meta:extends`和`allOf`陣列中，將新欄位組添加到方案中。

請求主體採用陣列的形式，每個列出的對象代表對單個欄位的特定更改。 每個對象包括要執行的操作(`op`)，該操作應在哪個欄位(`path`)上執行，以及該操作應包括哪些資訊(`value`)。

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
          "value":  "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**回應**

響應顯示兩個操作均成功執行。 欄位組`$id`已添加到`meta:extends`陣列中，而欄位組`$id`的引用(`$ref`)現在顯示在`allOf`陣列中。

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
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

## 啟用用於即時客戶概要檔案{#union}的方案

為了使架構參與[即時客戶概要檔案](../../profile/home.md)，您必須向架構的`meta:immutableTags`陣列添加`union`標籤。 您可以透過對相關結構提出PATCH要求來完成此作業。

>[!IMPORTANT]
>
>不可變標籤是要設定但從不移除的標籤。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要啟用的方案的URL編碼`$id` URI或`meta:altId`。 |

**要求**

下面的示例請求將`meta:immutableTags`陣列添加到現有模式，為該陣列提供一個`union`的單字串值，以便在配置式中使用。

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

成功的響應返回更新模式的詳細資訊，顯示`meta:immutableTags`陣列已添加。

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
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

您現在可以查看此架構類的union，以確認已表示該架構的欄位。 有關詳細資訊，請參見[聯合端點指南](./unions.md)。

## 刪除方案{#delete}

有時可能需要從架構註冊表中刪除架構。 這是透過使用路徑中提供的架構ID執行DELETE要求來完成的。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要刪除的架構的URL編碼`$id` URI或`meta:altId`。 |

**要求**

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

您可以嘗試對結構進行查閱(GET)請求，以確認刪除。 您需要在請求中包含`Accept`標題，但應接收HTTP狀態404（找不到），因為架構已從架構註冊表中移除。
