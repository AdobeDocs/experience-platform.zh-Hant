---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；模式註冊；
solution: Experience Platform
title: 架構註冊表API快速入門
description: 本文檔介紹了在嘗試調用方案註冊表API之前需要知道的核心概念。
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# [!DNL Schema Registry] API快速入門

[!DNL Schema Registry] API可讓您建立和管理各種Experience Data Model(XDM)資源。 本檔案提供您在嘗試呼叫[!DNL Schema Registry] API之前，需要瞭解的核心概念的簡介。

## 先決條件

使用開發人員指南需要對下列Adobe Experience Platform元件有良好的認識：

* [[!DNL Experience Data Model (XDM) System]](../home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../schema/composition.md):瞭解XDM架構的基本建置區塊。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

XDM使用JSON結構描述格式來說明並驗證所擷取客戶體驗資料的結構。 因此，強烈建議您檢閱[官方JSON結構描述檔案](https://json-schema.org/)，以進一步瞭解此基礎技術。

## 讀取範例API呼叫

[!DNL Schema Registry] API檔案提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Schema Registry]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒檔案](../../sandboxes/home.md)。

所有對[!DNL Schema Registry]的查閱(GET)請求都需要額外的`Accept`標題，其值會決定API傳回的資訊格式。 如需詳細資訊，請參閱下方的[接受標題](#accept)一節。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 瞭解您的TENANT_ID {#know-your-tenant_id}

在API指南中，您會看到`TENANT_ID`的參考。 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 如果您不知道您的ID，可以執行下列GET要求來存取它：

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回有關您組織使用[!DNL Schema Registry]的資訊。 這包括`tenantId`屬性，其值為`TENANT_ID`。

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "fieldgroups": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "fieldgroups",
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
      "meta:resourceType": "fieldgroups",
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

## 瞭解`CONTAINER_ID` {#container}

對[!DNL Schema Registry] API的呼叫需要使用`CONTAINER_ID`。 有兩個容器可對其進行API呼叫：`global`容器和`tenant`容器。

### 全域容器

`global`容器包含所有標準Adobe和[!DNL Experience Platform]合作夥伴提供的類、方案欄位組、資料類型和方案。 您只能對`global`容器執行清單和查閱(GET)請求。

使用`global`容器的呼叫範例如下：

```http
GET /global/classes
```

### 租用戶容器

不要與您的唯一`TENANT_ID`混淆，`tenant`容器包含由IMS組織定義的所有類、欄位組、資料類型、方案和描述符。 這是每個組織所獨有的，也就是說，其他IMS組織無法看到或管理。 您可以對在`tenant`容器中建立的資源執行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。

使用`tenant`容器的呼叫範例如下：

```http
POST /tenant/fieldgroups
```

在`tenant`容器中建立類、欄位組、方案或資料類型時，它將保存到[!DNL Schema Registry]，並分配一個包含`TENANT_ID`的`$id` URI。 此`$id`用於整個API中以參考特定資源。 `$id`值的範例將在下一節中提供。

## 資源標識{#resource-identification}

XDM資源以URI形式使用`$id`屬性進行標識，例如：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為了使URI更適合REST，架構在名為`meta:altId`的屬性中也具有URI的點標籤編碼：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

對[!DNL Schema Registry] API的呼叫將支援URL編碼的`$id` URI或`meta:altId`（點符號格式）。 最佳實務是在對API進行REST呼叫時使用URL編碼的`$id` URI，如下：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標題{#accept}

在[!DNL Schema Registry] API中執行清單和查閱(GET)作業時，需要`Accept`標題來判斷API傳回的資料格式。 查找特定資源時，`Accept`標題中還必須包含版本號。

下表列出相容的`Accept`標題值，包括具有版本號碼的值，以及使用API時傳回內容的說明。

| Accept | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回包含原始`$ref`和`allOf`的完整JSON結構描述清單。 這可用來傳回完整資源清單。 |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始XDM。 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性並 `allOf` 解析。有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 具有`$ref`和`allOf`的原始XDM。 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 屬性並 `allOf` 解析。無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 屬性並 `allOf` 解析。包括描述符。 |

>[!NOTE]
>
>平台目前僅支援每個架構(`1`)的一個主要版本。 因此，在執行查找請求時，`version`的值必須始終為`1`，以返回方案的最新次要版本。 有關方案版本化的詳細資訊，請參閱以下子部分。

### 方案版本控制{#versioning}

架構版本由架構註冊表API的`Accept`標題和下游平台服務API負載的`schemaRef.contentType`屬性中的標題引用。

目前，平台僅支援每個架構的單一主要版本(`1`)。 根據[模式演化規則](../schema/composition.md#evolution)，對模式的每次更新都必須是非破壞性的，這表示模式的新次要版本（`1.2`、`1.3`等） 始終向後相容以前的次要版本。 因此，在指定`version=1`時，架構註冊表始終返回架構的&#x200B;**最新**&#x200B;主版本`1` ，這表示不返回以前的次版本。

>[!NOTE]
>
>只有在資料集引用了模式且以下情況之一成立後，才會強制執行模式演化的非破壞性要求：
>
>* 資料已收錄至資料集。
>* 資料集已啟用，可用於即時客戶個人檔案（即使未收錄任何資料）。

>
>
如果模式尚未與符合上述條件之一的資料集建立關聯，則可對其進行任何變更。 但是，在所有情況下，`version`元件仍保持在`1`。

## XDM現場限制和最佳做法

方案的欄位列在其`properties`對象中。 每個欄位本身都是物件，包含屬性以說明並限制欄位可包含的資料。

有關在API中定義欄位類型的詳細資訊，請參閱本指南的[欄位約束指南](../schema/field-constraints.md)，包括代碼示例和最常用資料類型的可選約束。

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

* 欄位物件的名稱可能包含英數字元、破折號或底線字元，但&#x200B;**不得**&#x200B;以底線開頭。
   * **正確：** `fieldName`、 `field_name2`、 `Field-Name`、  `field-name_3`
   * **錯誤：** `_fieldName`
* camelCase是欄位對象名稱的首選參數。 範例：`fieldName`
* 欄位應包含`title`，寫在「標題大小寫」中。 範例：`Field Name`
* 欄位需要`type`。
   * 定義某些類型可能需要選擇`format`。
   * 如果需要特定的資料格式，可以將`examples`添加為陣列。
   * 也可以使用註冊表中的任何資料類型定義欄位類型。 如需詳細資訊，請參閱資料類型端點指南中有關建立資料類型[的章節。](./data-types.md#create)
* `description`說明欄位和有關欄位資料的相關資訊。 它應以完整的句子編寫，使用清楚的語言，讓任何存取架構的人都能瞭解欄位的意圖。

如需如何定義API中不同欄位類型的詳細資訊，請參閱[欄位限制](../schema/field-constraints.md)上的檔案。

## 後續步驟

若要開始使用[!DNL Schema Registry] API進行呼叫，請選取其中一個可用的端點指南。
