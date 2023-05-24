---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；經驗資料模型；經驗資料模型；資料模型；資料模型；模式註冊；模式註冊；
solution: Experience Platform
title: 架構註冊表API入門
description: 本文檔介紹了在嘗試調用架構註冊表API之前需要瞭解的核心概念。
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# 入門 [!DNL Schema Registry] API

的 [!DNL Schema Registry] API允許您建立和管理各種體驗資料模型(XDM)資源。 本文檔介紹了在嘗試呼叫至 [!DNL Schema Registry] API。

## 先決條件

使用開發人員指南需要瞭解Adobe Experience Platform的以下元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../schema/composition.md):瞭解XDM架構的基本構建塊。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

XDM使用JSON架構格式來描述和驗證所接收客戶體驗資料的結構。 因此，強烈建議您 [正式JSON架構文檔](https://json-schema.org/) 來更好地理解這個基礎技術。

## 讀取示例API調用

的 [!DNL Schema Registry] API文檔提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

## 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Schema Registry]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒文檔](../../sandboxes/home.md)。

所有查找(GET)請求 [!DNL Schema Registry] 需要 `Accept` 標頭，其值確定API返回的資訊格式。 查看 [接受標題](#accept) 的子菜單。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* `Content-Type: application/json`

## 瞭解您的TENANT_ID {#know-your-tenant_id}

在整個API指南中，您將看到對 `TENANT_ID`。 此ID用於確保您建立的資源與組織中的資源同名，並且包含在組織中。 如果您不知道您的ID，可以通過執行以下GET請求來訪問它：

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

成功的響應將返回有關您的組織使用 [!DNL Schema Registry]。 這包括 `tenantId` 屬性，其值是 `TENANT_ID`。

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

## 瞭解 `CONTAINER_ID` {#container}

呼叫 [!DNL Schema Registry] API需要使用 `CONTAINER_ID`。 有兩個容器可對其進行API調用：這樣 `global` 容器和 `tenant` 容器。

### 全局容器

的 `global` 容器容納所有標準Adobe [!DNL Experience Platform] 合作夥伴提供的類、模式欄位組、資料類型和模式。 您只能對 `global` 容器。

使用 `global` 容器如下所示：

```http
GET /global/classes
```

### 租戶容器

別被你的獨特 `TENANT_ID`，也請參見Wiki頁。 `tenant` 容器包含由組織定義的所有類、欄位組、資料類型、方案和描述符。 這是每個組織所獨有的，這意味著它們不可見，也不可由其他組織管理。 您可以對在中建立的資源執行所有CRUD操作(GET、POST、PUT、PATCH、DELETE) `tenant` 容器。

使用 `tenant` 容器如下所示：

```http
POST /tenant/fieldgroups
```

在中建立類、欄位組、方案或資料類型時 `tenant` 容器，保存到 [!DNL Schema Registry] 並分配 `$id` 包含您的 `TENANT_ID`。 此 `$id` 在整個API中使用以引用特定資源。 示例 `$id` 值在下一節中提供。

## 資源標識 {#resource-identification}

XDM資源用 `$id` 屬性，如以下示例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為使URI更易於REST，架構還在名為 `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

呼叫 [!DNL Schema Registry] API將支援URL編碼 `$id` URI或 `meta:altId` （點標籤格式）。 最佳做法是使用URL編碼 `$id` 對API進行REST調用時的URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標題 {#accept}

在中執行清單和查找(GET)操作時 [!DNL Schema Registry] API, `Accept` 需要標頭來確定API返回的資料的格式。 查找特定資源時，還必須在 `Accept` 標題。

下表列出了相容 `Accept` 標題值，包括具有版本號的值，以及API在使用時返回的內容的說明。

| Accept | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅返回ID清單。 這是列出資源時最常用的方法。 |
| `application/vnd.adobe.xed+json` | 返回具有原始的完整JSON架構的清單 `$ref` 和 `allOf` 包含。 這用於返回完整資源清單。 |
| `application/vnd.adobe.xed+json; version=1` | 原始XDM `$ref` 和 `allOf`。 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始XDM `$ref` 和 `allOf`。 沒有標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 沒有標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 包括描述符。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 和 `allOf` 已解析，有標題和說明。 不建議使用的欄位 `meta:status` 屬性 `deprecated`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>平台當前僅支援每個架構的一個主版本(`1`)。 因此， `version` 必須始終 `1` 執行查找請求以返回架構的最新次版本時。 有關方案版本化的詳細資訊，請參閱下面的子節。

### 架構版本控制 {#versioning}

架構版本由 `Accept` 架構註冊表API中和中的標頭 `schemaRef.contentType` 下游平台服務API負載中的屬性。

目前，平台僅支援單個主版本(`1`)。 根據 [模式演化規則](../schema/composition.md#evolution)，對架構的每個更新都必須是非破壞性的，這意味著架構的新次版本(`1.2`。 `1.3`等) 始終向後相容以前的次版本。 因此，當指定 `version=1`，架構註冊表始終返回 **最新** 主要版本 `1` 架構，表示不返回以前的次版本。

>[!NOTE]
>
>只有在模式被資料集引用且以下情況之一為真後，才強制執行模式演化的非破壞性要求：
>
>* 資料已被攝取到資料集中。
>* 資料集已啟用，可用於即時客戶配置檔案（即使沒有接收資料）。
>
>如果模式尚未與滿足上述條件之一的資料集關聯，則可以對其進行任何更改。 然而，在所有情況下 `version` 元件仍保留 `1`。

## XDM現場限制和最佳做法

架構的欄位列在其中 `properties` 的雙曲餘切值。 每個欄位本身都是一個對象，包含用於描述和約束欄位可包含的資料的屬性。 請參閱上的指南 [定義API中的自定義欄位](../tutorials/custom-fields-api.md) 代碼示例和最常用資料類型的可選約束。

下面的示例欄位說明了格式正確的XDM欄位，下面提供了有關命名約束和最佳做法的進一步詳細資訊。 在定義包含相似屬性的其他資源時，也可應用這些做法。

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

* 欄位對象的名稱可能包含字母數字、短划線或下划線字元，但 **不能** 以下划線開頭。
   * **正確：** `fieldName`。 `field_name2`。 `Field-Name`。 `field-name_3`
   * **錯誤：** `_fieldName`
* camelCase是欄位對象名稱的首選項。 範例：`fieldName`
* 該欄位應包括 `title`，寫在標題中。 範例：`Field Name`
* 該欄位需要 `type`。
   * 定義某些類型可能需要可選 `format`。
   * 如果需要特定格式化的資料， `examples` 可以添加為陣列。
   * 也可以使用註冊表中的任何資料類型定義欄位類型。 請參閱 [建立資料類型](./data-types.md#create) 的子菜單。
* 的 `description` 說明了欄位和有關欄位資料的相關資訊。 它應該用完整的句子寫成，並使用清晰的語言，以便任何訪問架構的人都能理解該欄位的意圖。

## 後續步驟

使用 [!DNL Schema Registry] API，選擇可用的終結點指南之一。
