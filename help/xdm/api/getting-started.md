---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: 架構註冊表API快速入門
description: 本文檔介紹了在嘗試調用方案註冊表API之前需要知道的核心概念。
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Getting started with the [!DNL Schema Registry] API

API [!DNL Schema Registry] 可讓您建立和管理各種Experience Data Model(XDM)資源。 本檔案提供您在嘗試呼叫 [!DNL Schema Registry] API之前，需要瞭解的核心概念。

## 必要條件

使用開發人員指南需要瞭解Adobe Experience Platform的下列元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../schema/composition.md):瞭解XDM架構的基本建置區塊。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

XDM使用JSON結構描述格式來說明並驗證所擷取客戶體驗資料的結構。 因此，強烈建議您檢閱官方的JSON [結構描述檔案](https://json-schema.org/) ，以進一步瞭解此基礎技術。

## 讀取範例API呼叫

API文 [!DNL Schema Registry] 件提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

## 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Schema Registry]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資 [!DNL Platform]訊，請參閱沙 [盒檔案](../../sandboxes/home.md)。

對的所有查閱(GET)請 [!DNL Schema Registry] 求都需要額 `Accept` 外的標題，其值會決定API傳回的資訊格式。 如需詳細 [資訊，請參閱下方](#accept) 「接受標題」一節。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 瞭解您的TENANT_ID {#know-your-tenant_id}

在API指南中，您會看到參考 `TENANT_ID`。 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 如果您不知道您的ID，可以執行下列GET要求來存取它：

**API格式**

```http
GET /stats
```

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您組織使用的相關資訊 [!DNL Schema Registry]。 這包括 `tenantId` 屬性，其值為您的 `TENANT_ID`。

```JSON
{
  "imsOrg":"{IMS_ORG}",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

對 [!DNL Schema Registry] API的呼叫需要使用 `CONTAINER_ID`。 有兩個容器可對其進行API呼叫：容器 `global` 和容 `tenant` 器。

### 全域容器

容器 `global` 包含所有標準Adobe及合作夥伴 [!DNL Experience Platform] 提供的類別、混合、資料類型和結構。 您只能對容器執行清單和查閱(GET) `global` 請求。

使用容器的呼叫范 `global` 例如下：

```http
GET /global/classes
```

### 租用戶容器

不要與您的獨特性混淆 `TENANT_ID`，容器 `tenant` 包含由IMS組織定義的所有類別、混合、資料類型、方案和描述符。 這是每個組織所獨有的，也就是說，其他IMS組織無法看到或管理。 您可以對容器中建立的資源執行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。 `tenant`

使用容器的呼叫范 `tenant` 例如下：

```http
POST /tenant/mixins
```

當您在容器中建立類別、mixin、結構或資料類 `tenant` 型時，會將其儲存至並指 [!DNL Schema Registry] 派 `$id` 包含您的URI `TENANT_ID`。 這 `$id` 會在整個API中用來參考特定資源。 值的范 `$id` 例會在下一節中提供。

## 資源識別 {#resource-identification}

XDM資源以URI形 `$id` 式的屬性來標識，如以下示例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為了使URI更適合REST，架構在名為 `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

呼叫 [!DNL Schema Registry] API將支援URL編碼的 `$id` URI `meta:altId` 或（點符號格式）。 最佳實務是在對API進行REST呼叫時， `$id` 使用URL編碼的URI，例如：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標題 {#accept}

在 [!DNL Schema Registry] API中執行清單和查閱(GET)作業時，需要 `Accept` 標題來判斷API傳回之資料的格式。 查找特定資源時，標題中還必須包含版本號 `Accept` 碼。

下表列出相容的 `Accept` 標題值，包括版本編號的值，以及使用API時傳回內容的說明。

| 接受 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回包含原始和內含的完整JSON結 `$ref` 構 `allOf` 清單。 這可用來傳回完整資源清單。 |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw XDM `$ref` with和 `allOf`. 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 屬性和已解 `allOf` 決。 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw XDM `$ref` with和 `allOf`. 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 屬性和已解 `allOf` 決。 無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 屬性和已解 `allOf` 決。 包括描述符。 |

>[!NOTE]
>
>如果僅提供主版本（如1、2、3），則註冊表將返回最新的次版本(如.1、.2、.3)。

## XDM現場限制和最佳做法

方案的欄位列在其對象中 `properties` 。 每個欄位本身都是物件，包含屬性以說明並限制欄位可包含的資料。

如需在API中定義欄位類型的詳細資訊，請參閱本指南的附 [錄](appendix.md) ，包括程式碼範例和常用資料類型的選用限制。

以下示例欄位說明了格式正確的XDM欄位，下面提供了有關命名約束和最佳做法的詳細資訊。 在定義包含類似屬性的其他資源時，也可套用這些做法。

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

* 欄位物件的名稱可能包含英數字元、破折號或底線字元，但 **不得以底線** 開頭。
   * **正確：**`fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **錯誤：** `_fieldName`
* camelCase是欄位對象名稱的首選參數。 範例: `fieldName`
* 欄位應包含在「 `title`標題大小寫」中寫入的。 範例: `Field Name`
* 欄位需要 `type`。
   * 定義某些類型可能需要選擇 `format`。
   * 當需要特定格式化資料時， `examples` 可新增為陣列。
   * 也可以使用註冊表中的任何資料類型定義欄位類型。 如需詳細資訊，請 [參閱資料類型端點指南](./data-types.md#create) 中有關建立資料類型的章節。
* 說明 `description` 了有關現場資料的現場和相關資訊。 它應以完整的句子編寫，使用清楚的語言，讓任何存取架構的人都能瞭解欄位的意圖。

如需如何在API中定 [義不同欄位類型的詳細資訊](../schema/field-constraints.md) ，請參閱欄位限制檔案。

## 後續步驟

若要開始使用 [!DNL Schema Registry] API進行呼叫，請選取其中一個可用的端點指南。
