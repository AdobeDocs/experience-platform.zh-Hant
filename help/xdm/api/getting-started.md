---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構註冊表；結構註冊表；
solution: Experience Platform
title: 架構註冊表API快速入門
description: 本檔案介紹您在嘗試呼叫結構註冊表API前，需要了解的核心概念。
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---

# 開始使用 [!DNL Schema Registry] API

此 [!DNL Schema Registry] API可讓您建立和管理各種Experience Data Model(XDM)資源。 本檔案簡介您在嘗試呼叫 [!DNL Schema Registry] API。

## 先決條件

若要使用開發人員指南，您必須妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../schema/composition.md):了解XDM結構的基本建置組塊。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

XDM使用JSON結構描述格式來說明和驗證擷取的客戶體驗資料結構。 因此，強烈建議您檢閱 [官方JSON結構檔案](https://json-schema.org/) 來更好地理解這個基礎技術。

## 讀取範例API呼叫

此 [!DNL Schema Registry] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

## 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Schema Registry]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱檔案](../../sandboxes/home.md).

對的所有查閱(GET)請求 [!DNL Schema Registry] 需要 `Accept` 標題，其值會決定API傳回的資訊格式。 請參閱 [接受標題](#accept) 一節以取得詳細資訊。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 知道您的TENANT_ID {#know-your-tenant_id}

在API指南中，您會看到的參考 `TENANT_ID`. 此ID可確保您建立的資源與IMS組織中的資源命名正確，且完整無缺。 如果您不知道您的ID，則可執行下列GET請求來存取：

**API格式**

```http
GET /stats
```

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回貴組織使用 [!DNL Schema Registry]. 這包括 `tenantId` 屬性，其值為 `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## 了解 `CONTAINER_ID` {#container}

呼叫 [!DNL Schema Registry] API需要使用 `CONTAINER_ID`. 有兩個容器可對其進行API呼叫：the `global` 容器和 `tenant` 容器。

### 全域容器

此 `global` 容器保留所有標準Adobe, [!DNL Experience Platform] 合作夥伴提供的類、架構欄位組、資料類型和架構。 您只能對 `global` 容器。

使用 `global` 容器看起來如下所示：

```http
GET /global/classes
```

### 租用戶容器

不要與你的獨特 `TENANT_ID`, `tenant` 容器包含由IMS組織定義的所有類別、欄位群組、資料類型、結構和描述元。 這是每個組織專屬的值，表示其他IMS組織無法看到或管理這些值。 您可以對您在 `tenant` 容器。

使用 `tenant` 容器看起來如下所示：

```http
POST /tenant/fieldgroups
```

在 `tenant` 容器，則會儲存至 [!DNL Schema Registry] 並指派 `$id` 包含 `TENANT_ID`. 此 `$id` 會在整個API中使用來參考特定資源。 範例 `$id` 值會提供於下一節。

## 資源標識 {#resource-identification}

XDM資源的識別方式為 `$id` 屬性，如下列範例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為了使URI更便於REST使用，架構還在名為的屬性中具有URI的點記號編碼 `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

呼叫 [!DNL Schema Registry] API將支援URL編碼 `$id` URI或 `meta:altId` （點記號格式）。 最佳作法是使用URL編碼 `$id` 對API發出REST呼叫時的URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標題 {#accept}

在 [!DNL Schema Registry] API, an `Accept` 需要標題，才能判斷API傳回的資料格式。 查詢特定資源時，也必須在 `Accept` 頁首。

下表列出相容的 `Accept` 標題值，包括版本號碼，以及使用API時傳回內容的說明。

| Accept | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回完整JSON結構清單（含原始結構） `$ref` 和 `allOf` 已包含。 這可用來傳回完整資源的清單。 |
| `application/vnd.adobe.xed+json; version=1` | 原始XDM，搭配 `$ref` 和 `allOf`. 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始XDM，搭配 `$ref` 和 `allOf`. 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 包括描述符。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 和 `allOf` 已解析，有標題和說明。 已棄用的欄位以 `meta:status` 屬性 `deprecated`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>平台目前僅支援每個架構的一個主要版本(`1`)。 因此， `version` 必須一律 `1` 執行查詢請求時，以傳回結構的最新次要版本。 如需架構版本設定的詳細資訊，請參閱下方小節。

### 架構版本設定 {#versioning}

參考結構版本 `Accept` 方案註冊表API中的標題，以及 `schemaRef.contentType` 屬性。

目前，Platform僅支援單一主要版本(`1`)。 根據 [模式演化規則](../schema/composition.md#evolution)，架構的每次更新都必須是非破壞性的，這表示架構的新次要版本(`1.2`, `1.3`等) 始終向後相容於以前的次要版本。 因此，在指定 `version=1`，架構註冊表一律會傳回 **最新** 主要版本 `1` ，表示不會傳回舊的次要版本。

>[!NOTE]
>
>只有在資料集參考結構且下列其中一種情況成立後，才會強制執行結構演變的非破壞性需求：
>
>* 資料已內嵌至資料集。
>* 資料集已啟用，可在「即時客戶設定檔」中使用（即使未擷取任何資料亦然）。
>
>如果結構尚未與符合上述其中一個條件的資料集建立關聯，則可對其進行任何變更。 然而，在所有情況下， `version` 元件仍在 `1`.

## XDM欄位限制和最佳實務

架構的欄位會列在其中 `properties` 物件。 每個欄位本身就是一個物件，包含要說明和限制欄位可包含之資料的屬性。 請參閱 [定義API中的自訂欄位](../tutorials/custom-fields-api.md) 適用於最常使用的資料類型的程式碼範例和選用限制。

下列範例欄位說明格式正確的XDM欄位，並提供以下命名限制和最佳實務的詳細資訊。 定義包含類似屬性的其他資源時，也可套用這些實務。

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* 欄位對象的名稱可能包含英數字元、破折號或底線字元，但 **不能** 從底線開始。
   * **正確：** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **錯誤：** `_fieldName`
* 欄位物件名稱偏好使用camelCase。 範例：`fieldName`
* 欄位應包含 `title`，在標題案例中撰寫。 範例：`Field Name`
* 欄位需要 `type`.
   * 定義某些類型可能需要 `format`.
   * 若需要特定格式的資料， `examples` 可新增為陣列。
   * 也可使用註冊表中的任何資料類型來定義欄位類型。 請參閱 [建立資料類型](./data-types.md#create) （位於「資料類型」端點指南中）以取得詳細資訊。
* 此 `description` 說明欄位和有關欄位資料的相關資訊。 它應以完整的句子寫成，語言清楚，讓任何存取架構的人都能了解欄位的意圖。

## 後續步驟

若要開始使用進行呼叫 [!DNL Schema Registry] API，請選取任一可用的端點指南。
