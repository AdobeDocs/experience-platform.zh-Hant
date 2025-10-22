---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；結構描述；結構描述；結構描述；建立
solution: Experience Platform
title: 結構描述API端點
description: 結構描述登入API中的/schemas端點可讓您以程式設計方式管理體驗應用程式中的XDM結構描述。
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: dc5ac5427e1eeef47434c3974235a1900d29b085
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 3%

---

# 結構描述端點

結構描述可視為您要擷取至Adobe Experience Platform的資料的藍圖。 每個結構描述都由一個類別和零個或多個結構描述欄位群組組成。 `/schemas` API中的[!DNL Schema Registry]端點可讓您以程式設計方式管理體驗應用程式中的結構描述。

## 快速入門

本指南中使用的API端點是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 在繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience Platform API所需必要標題的重要資訊。

## 擷取結構描述清單 {#list}

您可以分別向`global`或`tenant`發出GET要求，列出`/global/schemas`或`/tenant/schemas`容器下的所有結構描述。

>[!NOTE]
>
>列出資源時，結構描述登入將結果集限製為300個專案。 為了傳回超過此限制的資源，您必須使用分頁引數。 也建議您使用其他查詢引數來篩選結果並減少傳回的資源數量。 如需詳細資訊，請參閱附錄檔案中有關[查詢引數](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取之結構描述的容器： `global`用於Adobe建立的結構描述，或`tenant`用於您組織擁有的結構描述。 |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 如需可用引數的清單，請參閱[附錄檔案](./appendix.md#query)。 |

{style="table-layout:auto"}

**要求**

下列要求會使用`tenant`查詢引數，依結果的`orderby`屬性排序結果，從`title`容器擷取結構描述清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標頭。 下列`Accept`標題可用於列出結構描述：

| `Accept`標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，包括原始`$ref`和`allOf`。 （上限： 300） |

{style="table-layout:auto"}

**回應**

上述要求使用了`application/vnd.adobe.xed-id+json` `Accept`標頭，因此回應只包含每個結構描述的`title`、`$id`、`meta:altId`和`version`屬性。 使用其他`Accept`標頭(`application/vnd.adobe.xed+json`)會傳回每個結構描述的所有屬性。 根據您在回應中需要的資訊，選取適當的`Accept`標頭。

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

## 查詢結構描述 {#lookup}

您可以發出GET請求，在路徑中包含結構描述的ID，藉此查詢特定的結構描述。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取之結構描述的容器： `global`用於Adobe建立的結構描述，或`tenant`用於您組織擁有的結構描述。 |
| `{SCHEMA_ID}` | 您要查閱之結構描述的`meta:altId`或URL編碼的`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會擷取由路徑中`meta:altId`值所指定的結構描述。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標頭。 所有查詢請求都要求在`version`標頭中包含`Accept`。 下列`Accept`標頭可供使用：

| `Accept`標題 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`和`allOf`已解決，有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 含有`$ref`和`allOf`的原始，沒有標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref`和`allOf`已解決，無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | 已解決`$ref`和`allOf`，包含描述元。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref`和`allOf`已解決，有標題和說明。 已棄用的欄位以`meta:status`的`deprecated`屬性表示。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回結構的詳細資料。 傳回的欄位取決於請求中傳送的`Accept`標頭。 嘗試使用不同的`Accept`標頭來比較回應，並決定哪個標頭最適合您的使用案例。

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

## 建立結構描述 {#create}

架構構成程式從指派類別開始。 類別會定義資料的主要行為方面（記錄或時間序列），以及描述將擷取之資料所需的最少欄位。

如需有關建立不含類別或欄位群組的結構描述（稱為關聯式結構描述）的指示，請參閱[建立關聯式結構描述](#create-relational-schema)區段。

>[!NOTE]
>
>以下範例呼叫只是如何在API中建立結構描述的基準範例，具有類別的最低構成需求，但沒有欄位群組。 如需有關如何在API中建立結構描述的完整步驟，包括如何使用欄位群組和資料型別指派欄位，請參閱[結構描述建立教學課程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**要求**

要求必須包含參考類別`allOf`的`$id`屬性。 此屬性會定義結構描述將實作的「基底類別」。 在此範例中，基底類別是先前建立的「屬性資訊」類別。

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
| `allOf` | 一個物件陣列，每個物件都參照到結構描述實作其欄位的類別或欄位群組。 每個物件都包含單一屬性(`$ref`)，其值代表新結構描述將實作的類別或欄位群組的`$id`。 必須提供一個類別，具有零個或多個額外的欄位群組。 在上述範例中，`allOf`陣列中的單一物件是結構描述的類別。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立之結構描述詳細資料的承載，包括`$id`、`meta:altId`和`version`。 這些值是唯讀的，並由[!DNL Schema Registry]指派。

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

執行GET要求以[列出租使用者容器中的所有結構描述](#list)現在將包含新的結構描述。 您可以使用URL編碼的[&#x200B; URI執行](#lookup)查詢(GET)要求`$id`，以直接檢視新的結構描述。

若要將其他欄位新增至結構描述，您可以執行[PATCH作業](#patch)，將欄位群組新增至結構描述的`allOf`和`meta:extends`陣列。

## 建立關聯式結構描述 {#create-relational-schema}

>[!AVAILABILITY]
>
>Adobe Journey Optimizer **協調的行銷活動**&#x200B;授權持有人可使用Data Mirror和關聯式結構描述。 視您的授權和功能啟用而定，它們也可作為Customer Journey Analytics使用者的&#x200B;**有限版本**&#x200B;提供。 請聯絡您的Adobe代表以取得存取權。

>[!NOTE]
>
>關聯式結構描述先前在Adobe Experience Platform API檔案的舊版本中稱為模型式結構描述。 功能保持不變 — 只是術語發生了更改，以清楚明瞭。

對`/schemas`端點發出POST要求，以建立關聯式結構描述。 關聯式結構描述儲存結構化的關聯式樣式資料&#x200B;**，但不含**&#x200B;類別或欄位群組。 直接在結構描述上定義欄位，並使用邏輯行為標籤將結構描述識別為關聯式。

>[!IMPORTANT]
>
>若要建立關聯式結構描述，請將`meta:extends`設定為`"https://ns.adobe.com/xdm/data/adhoc-v2"`。 這是&#x200B;**邏輯行為識別碼** （不是實體行為或類別）。 在&#x200B;**中**&#x200B;不`allOf`參考類別或欄位群組，並且&#x200B;**不**&#x200B;在`meta:extends`中包含類別或欄位群組。

請先使用`POST /tenant/schemas`建立結構描述。 然後使用[描述項API (`POST /tenant/descriptors`)](../api/descriptors.md)新增必要的描述項：

- [主索引鍵描述項](../api/descriptors.md#primary-key-descriptor)：主索引鍵欄位必須位於&#x200B;**根層級**&#x200B;且&#x200B;**標示為必要**。
- [版本描述項](../api/descriptors.md#version-descriptor)： **必要** （當主索引鍵存在時）。
- [關聯描述項](../api/descriptors.md#relationship-descriptor)：選擇性，定義聯結；內嵌時未強制使用基數。
- [時間戳記描述項](../api/descriptors.md#timestamp-descriptor)：對於時間序列結構描述，主索引鍵必須是包含時間戳記欄位的&#x200B;**複合**&#x200B;索引鍵。

>[!NOTE]
>
>在UI結構描述編輯器中，版本描述項和時間戳記描述項分別顯示為&quot;[!UICONTROL Version identifier]&quot;和&quot;[!UICONTROL Timestamp identifier]&quot;。

>[!CAUTION]
>
>關聯式結構描述&#x200B;**與聯合結構描述**&#x200B;不相容。 使用關聯式結構描述時，請勿將`union`標籤套用至`meta:immutableTags`。 UI已封鎖此設定，但API目前並未封鎖此設定。 如需聯合結構描述行為的詳細資訊，請參閱[聯合端點指南](./unions.md)。

**API格式**

```http
POST /tenant/schemas
```

**要求**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### 要求內文屬性

| 屬性 | 類型 | 說明 |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | 字串 | 結構描述的顯示名稱。 |
| `description` | 字串 | 結構描述用途的簡短說明。 |
| `type` | 字串 | 關聯式結構描述必須是`"object"`。 |
| `definitions` | 物件 | 包含定義結構描述欄位的根層級物件。 |
| `definitions.<name>.properties` | 物件 | 欄位名稱和資料型別。 |
| `allOf` | 陣列 | 參考根層級物件定義（例如，`#/definitions/marketing_customers`）。 |
| `meta:extends` | 陣列 | 必須包含`"https://ns.adobe.com/xdm/data/adhoc-v2"`，才能將結構描述識別為關聯式。 |
| `meta:behaviorType` | 字串 | 設定為`"record"`。 只有在啟用且適當的情況下才使用`"time-series"`。 |

>[!IMPORTANT]
>
>關聯式綱要的綱要演化遵循與標準綱要相同的加法規則。 您可以使用PATCH請求新增欄位。 只有在未將資料擷取到資料集時，才允許重新命名或移除欄位等變更。

**回應**

成功的要求傳回&#x200B;**HTTP 201 （已建立）**&#x200B;和已建立的結構描述。

>[!NOTE]
>
>關聯式結構描述不會繼承預先內建的欄位（例如id、時間戳記或eventType）。 在結構描述中明確定義所有必填欄位。

**範例回應**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### 回應內文屬性

| 屬性 | 類型 | 說明 |
| ------------------- | ------ | -------------------------- |
| `$id` | 字串 | 已建立綱要的唯一URL。 用於後續API呼叫。 |
| `meta:altId` | 字串 | 結構描述的替代識別碼。 |
| `meta:resourceType` | 字串 | 資源型別（一律為`"schemas"`）。 |
| `version` | 字串 | 建立時指派的結構描述版本。 |
| `title` | 字串 | 結構描述的顯示名稱。 |
| `description` | 字串 | 結構描述用途的簡短說明。 |
| `type` | 字串 | 結構描述型別。 |
| `definitions` | 物件 | 定義架構中所使用的可重複使用物件或欄位群組。 這通常包括主要資料結構，並在`allOf`陣列中參考以定義結構描述根。 |
| `allOf` | 陣列 | 透過參考一或多個定義（例如，`#/definitions/marketing_customers`）來指定結構描述的根物件。 |
| `meta:extends` | 陣列 | 識別關聯式結構描述(`adhoc-v2`)。 |
| `meta:behaviorType` | 字串 | 行為型別（`record`或`time-series`，啟用時）。 |
| `meta:containerId` | 字串 | 儲存結構描述的容器（例如，`tenant`）。 |

若要在關聯式結構描述建立後新增欄位，請發出[PATCH要求](#patch)。 關聯式結構描述不會繼承或自動演化。 只有在未將資料擷取到資料集時，才允許重新命名或刪除欄位等結構變更。 一旦資料存在，則僅支援&#x200B;**加總變更** （例如新增欄位）。

您可以新增根級欄位（在根定義或根`properties`內），但無法移除、重新命名或變更現有欄位的型別。

>[!CAUTION]
>
>使用結構描述初始化資料集後，結構描述演化會受到限制。 請事先謹慎規劃欄位名稱和型別，因為一旦擷取資料，就無法刪除或修改欄位。

## 更新結構 {#put}

您可以透過PUT作業取代整個結構描述，基本上就是重新寫入資源。 透過PUT要求更新結構描述時，本文必須包含在POST要求中[建立新結構描述](#create)時所需的所有欄位。

>[!NOTE]
>
>如果您只想更新部分結構描述，而不是完全取代它，請參閱[更新部分結構描述](#patch)一節。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 您要重新寫入之結構描述的`meta:altId`或URL編碼的`$id`。 |

{style="table-layout:auto"}

**要求**

下列要求會取代現有結構描述，變更其`title`、`description`和`allOf`屬性。

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

成功的回應會傳回已更新結構的詳細資料。

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

## 更新結構描述的一部分 {#patch}

您可以使用PATCH請求更新結構描述的一部分。 [!DNL Schema Registry]支援所有標準JSON修補程式操作，包括`add`、`remove`和`replace`。 如需JSON修補程式的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果您想要以新值取代整個資源，而非更新個別欄位，請參閱[使用PUT作業取代結構描述](#put)一節。

PATCH最常見的操作之一，是將先前定義的欄位群組新增到結構描述，如下列範例所示。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的`$id` URI或您要更新的結構描述`meta:altId`。 |

{style="table-layout:auto"}

**要求**

下列範例要求將新欄位群組新增至結構描述，方法是將該欄位群組的`$id`值新增至`meta:extends`和`allOf`陣列。

請求內文採用陣列形式，每個列出的物件代表個別欄位的特定變更。 每個物件都包含要執行的作業(`op`)、應在哪個欄位上執行該作業(`path`)，以及該作業中應包含哪些資訊(`value`)。

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

回應顯示兩個作業都已成功執行。 欄位群組`$id`已新增至`meta:extends`陣列，而且欄位群組`$ref`的參考(`$id`)現在出現在`allOf`陣列中。

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

## 啟用結構以用於Real-Time Customer Profile {#union}

為了讓結構描述參與[即時客戶設定檔](../../profile/home.md)，您必須將`union`標籤新增至結構描述的`meta:immutableTags`陣列。 您可以向相關結構描述發出PATCH要求來達到此目的。

>[!IMPORTANT]
>
>不可變標籤是打算設定但從未移除的標籤。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的`$id` URI或您要啟用之結構描述的`meta:altId`。 |

{style="table-layout:auto"}

**要求**

下列範例要求將`meta:immutableTags`陣列新增至現有結構描述，給予該陣列單一字串值`union`以啟用它以用於設定檔中。

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

成功的回應會傳回已更新結構描述的詳細資料，顯示`meta:immutableTags`陣列已新增。

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

您現在可以檢視此結構描述類別的聯合，以確認表示結構描述的欄位。 如需詳細資訊，請參閱[聯合端點指南](./unions.md)。

## 刪除結構描述 {#delete}

有時可能需要從結構描述登入中移除結構描述。 若要這麼做，請使用路徑中提供的結構ID執行DELETE要求。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的`$id` URI或您要刪除的結構描述`meta:altId`。 |

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

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試對結構描述進行查詢(GET)以確認刪除。 您需要在要求中加入`Accept`標頭，但應該會收到HTTP狀態404 （找不到），因為結構描述已從結構描述登入中移除。
