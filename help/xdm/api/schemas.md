---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結構註冊表；結構；結構；結構；結構；結構；建立
solution: Experience Platform
title: 結構API端點
description: Schema Registry API中的/schemas端點可讓您以程式設計方式管理體驗應用程式中的XDM結構。
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 4%

---

# 方案端點

架構可視為您要內嵌至Adobe Experience Platform之資料的藍圖。 每個架構由類和零個或多個架構欄位組組成。 [!DNL Schema Registry] API中的`/schemas`端點可讓您以程式設計方式管理體驗應用程式中的結構。

## 快速入門

本指南中使用的API端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭的重要資訊。

## 擷取結構清單 {#list}

您可以分別向`/global/schemas`或`/tenant/schemas`發出GET請求，以列出`global`或`tenant`容器下的所有結構。

>[!NOTE]
>
>列出資源時，方案註冊表將結果集限制為300個項。 若要傳回超過此限制的資源，您必須使用分頁參數。 建議您使用其他查詢參數來篩選結果並減少傳回的資源數。 如需詳細資訊，請參閱附錄檔案中[查詢參數](./appendix.md#query)一節。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之結構的容器：`global`適用於Adobe建立的結構，或`tenant`適用於您組織擁有的結構。 |
| `{QUERY_PARAMS}` | 可選的查詢參數，以依據篩選結果。 有關可用參數的清單，請參見[附錄文檔](./appendix.md#query)。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會使用`orderby`查詢參數，從`tenant`容器中擷取結構清單，以依其`title`屬性排序結果。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於要求中傳送的`Accept`標題。 下列`Accept`標題可用於列出結構：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構，並包含原始的`$ref`和`allOf`。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**回應**

上述請求使用`application/vnd.adobe.xed-id+json` `Accept`標題，因此回應僅包含每個架構的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標題(`application/vnd.adobe.xed+json`)會傳回每個架構的所有屬性。 根據您在回應中需要的資訊，選取適當的`Accept`標題。

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

## 查詢結構 {#lookup}

您可以提出GET要求，將結構的ID納入路徑中，借此查找特定結構。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 存放您要擷取之結構的容器：`global`適用於Adobe建立的架構，或`tenant`適用於您組織擁有的架構。 |
| `{SCHEMA_ID}` | 您要查詢之架構的`meta:altId`或URL編碼的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會擷取路徑中其`meta:altId`值所指定的架構。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於要求中傳送的`Accept`標題。 所有查詢請求都需要在`Accept`標題中包含`version`。 可使用下列`Accept`標題：

| `Accept` 標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始檔案具有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 和 `allOf` 已解析，有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始格式包含`$ref`和`allOf`，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 和 `allOf` 解析，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 和已 `allOf` 解析的描述符。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回架構的詳細資訊。 傳回的欄位取決於請求中傳送的`Accept`標題。 請試驗不同的`Accept`標題，比較回應並判斷哪個標題最適合您的使用案例。

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

## 建立結構 {#create}

架構合成過程從分配類開始。 類別會定義資料（記錄或時間序列）的關鍵行為方面，以及描述將擷取的資料所需的最小欄位。

>[!NOTE]
>
>以下範例呼叫只是如何在API中建立結構的基準範例，其中類別的組成需求最低，且沒有欄位群組。 如需如何在API中建立架構的完整步驟，包括如何使用欄位群組和資料類型指派欄位，請參閱[架構建立教學課程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**要求**

請求必須包含`allOf`屬性，該屬性引用類的`$id`。 此屬性定義架構將實作的「base class」。 在此示例中，基類是以前建立的「屬性資訊」類。

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
| `allOf` | 對象的陣列，每個對象引用模式實現的域的類或欄位組。 每個對象都包含一個屬性(`$ref`)，其值表示新架構將實施的類或欄位組的`$id`。 必須提供一個類，其中包含零個或多個附加欄位組。 在上例中，`allOf`陣列中的單個對象是架構的類。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態201（已建立），以及包含新建立架構詳細資訊的裝載，包括`$id`、`meta:altId`和`version`。 這些值為唯讀值，由[!DNL Schema Registry]指派。

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

執行[清單租用戶容器中所有結構](#list)的GET請求，現在會包含新結構。 您可以使用URL編碼的`$id` URI執行[查詢(GET)請求](#lookup)以直接檢視新架構。

要向架構添加其他欄位，可以執行[PATCH操作](#patch)以向架構的`allOf`和`meta:extends`陣列添加欄位組。

## 更新結構 {#put}

您可以透過PUT操作取代整個架構，實際上是重新寫入資源。 透過PUT請求更新結構時，內文必須包含[在POST請求中建立新結構](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新部分架構，而不是完全替換架構，請參閱[上更新架構](#patch)的一部分的部分。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要重寫的架構的`meta:altId`或URL編碼的`$id`。 |

{style=&quot;table-layout:auto&quot;}

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

成功的回應會傳回更新架構的詳細資訊。

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

## 更新結構的一部分 {#patch}

您可以使用PATCH請求來更新部分結構。 [!DNL Schema Registry]支援所有標準JSON修補程式操作，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果您想用新值取代整個資源，而不是更新個別欄位，請參閱[上的區段，使用PUT操作](#put)取代架構。

最常見的PATCH操作之一是將先前定義的欄位群組新增至架構，如下列範例所示。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要更新的架構的URL編碼的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下範例要求將欄位群組的`$id`值新增至`meta:extends`和`allOf`陣列，以將新欄位群組新增至架構。

要求內文採用陣列的形式，每個列出的物件代表個別欄位的特定變更。 每個對象包括要執行的操作(`op`)，該操作應在哪個欄位(`path`)上執行，以及該操作應包括哪些資訊(`value`)。

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

響應顯示兩個操作均已成功執行。 欄位組`$id`已添加到`meta:extends`陣列中，而欄位組`$id`的引用(`$ref`)現在顯示在`allOf`陣列中。

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

## 啟用結構以用於即時客戶個人檔案 {#union}

若要讓架構參與[即時客戶設定檔](../../profile/home.md)，您必須將`union`標籤新增至架構的`meta:immutableTags`陣列。 您可以對相關結構提出PATCH要求，以達成此目的。

>[!IMPORTANT]
>
>不可變標籤是旨在設定但從不移除的標籤。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要啟用的架構的URL編碼的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下範例要求將`meta:immutableTags`陣列新增至現有架構，為陣列提供單一字串值`union`，以便在設定檔中使用。

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

成功的回應會傳回更新架構的詳細資訊，顯示已新增`meta:immutableTags`陣列。

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

您現在可以檢視此架構類別的聯合，以確認已呈現該架構的欄位。 如需詳細資訊，請參閱[union端點指南](./unions.md)。

## 刪除結構 {#delete}

有時可能需要從架構註冊表中刪除架構。 若要這麼做，請使用路徑中提供的結構ID執行DELETE要求。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 要刪除的架構的URL編碼的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

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

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

您可以嘗試對結構進行查詢(GET)以確認刪除。 您需要在請求中加入`Accept`標題，但應該會收到HTTP狀態404（找不到），因為架構已從架構註冊表中移除。
