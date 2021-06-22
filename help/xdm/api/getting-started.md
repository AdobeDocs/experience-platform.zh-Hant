---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構註冊表；結構註冊表；
solution: Experience Platform
title: 架構註冊表API快速入門
description: 本檔案介紹您在嘗試呼叫結構註冊表API前，需要了解的核心概念。
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 0%

---

# [!DNL Schema Registry] API快速入門

[!DNL Schema Registry] API可讓您建立和管理各種Experience Data Model(XDM)資源。 本檔案介紹您在嘗試呼叫[!DNL Schema Registry] API之前需要了解的核心概念。

## 先決條件

若要使用開發人員指南，您必須妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../schema/composition.md):了解XDM結構的基本建置組塊。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

XDM使用JSON結構描述格式來說明和驗證擷取的客戶體驗資料結構。 因此，強烈建議您檢閱[官方JSON結構描述檔案](https://json-schema.org/)，以深入了解此基礎技術。

## 讀取範例API呼叫

[!DNL Schema Registry] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的區段。

## 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Schema Registry]的資源，都會隔離至特定虛擬沙箱。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱檔案](../../sandboxes/home.md)。

對[!DNL Schema Registry]的所有查詢(GET)請求都需要額外的`Accept`標題，其值會決定API傳回的資訊格式。 如需詳細資訊，請參閱下方的[接受標題](#accept)一節。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 知道您的TENANT_ID {#know-your-tenant_id}

在API指南中，您會看到`TENANT_ID`的參考。 此ID可確保您建立的資源與IMS組織中的資源命名正確，且完整無缺。 如果您不知道您的ID，則可執行下列GET請求來存取：

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

成功的回應會傳回貴組織使用[!DNL Schema Registry]的相關資訊。 這包括`tenantId`屬性，其值為`TENANT_ID`。

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

## 了解`CONTAINER_ID` {#container}

呼叫[!DNL Schema Registry] API需要使用`CONTAINER_ID`。 有兩個容器可對其進行API呼叫：`global`容器和`tenant`容器。

### 全域容器

`global`容器包含所有標準Adobe和[!DNL Experience Platform]合作夥伴提供的類、架構欄位組、資料類型和架構。 您只能對`global`容器執行清單和查詢(GET)請求。

使用`global`容器的呼叫範例如下所示：

```http
GET /global/classes
```

### 租用戶容器

`tenant`容器不要與您的唯一`TENANT_ID`混淆，它包含由IMS組織定義的所有類、欄位群組、資料類型、結構和描述元。 這是每個組織專屬的值，表示其他IMS組織無法看到或管理這些值。 您可以對您在`tenant`容器中建立的資源執行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。

使用`tenant`容器的呼叫範例如下所示：

```http
POST /tenant/fieldgroups
```

在`tenant`容器中建立類、欄位組、架構或資料類型時，該類型將保存到[!DNL Schema Registry]，並分配一個`$id` URI，其中包含您的`TENANT_ID`。 此`$id`會在整個API中用來參考特定資源。 下一節將提供`$id`值的範例。

## 資源標識{#resource-identification}

XDM資源以URI形式以`$id`屬性來識別，如以下範例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為了使URI更便於REST使用，架構還在名為`meta:altId`的屬性中具有URI的點記號編碼：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

對[!DNL Schema Registry] API的呼叫將支援URL編碼的`$id` URI或`meta:altId`（點記號格式）。 最佳實務是對API進行REST呼叫時，使用URL編碼的`$id` URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標題 {#accept}

在[!DNL Schema Registry] API中執行清單和查閱(GET)操作時，需要`Accept`標題來判斷API傳回的資料格式。 查找特定資源時，`Accept`標題中也必須包含版本號。

下表列出相容的`Accept`標題值，包括具有版本號碼的值，以及使用API時傳回內容的說明。

| Accept | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回完整JSON結構的清單，其中包含原始的`$ref`和`allOf`。 這可用來傳回完整資源的清單。 |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始XDM。 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和已 `allOf` 解析。有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 具有`$ref`和`allOf`的原始XDM。 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 屬性和已 `allOf` 解析。無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 屬性和已 `allOf` 解析。包括描述符。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>平台目前僅支援每個架構(`1`)一個主要版本。 因此，執行查詢請求時，`version`的值必須一律為`1`，才能傳回架構的最新次要版本。 如需架構版本設定的詳細資訊，請參閱下方小節。

### 架構版本設定 {#versioning}

架構版本由架構註冊表API中的`Accept`標題和下游Platform服務API裝載中的`schemaRef.contentType`屬性參照。

目前，Platform僅支援每個架構的單一主要版本(`1`)。 根據架構演化的[規則](../schema/composition.md#evolution)，架構的每次更新都必須是非破壞性的，這表示架構的新次要版本（`1.2`、`1.3`等） 始終向後相容於以前的次要版本。 因此，指定`version=1`時，架構註冊表始終返回架構的&#x200B;**最新**&#x200B;主版本`1` ，這表示不返回以前的次版本。

>[!NOTE]
>
>只有在資料集參考結構且下列其中一種情況成立後，才會強制執行結構演變的非破壞性需求：
>
>* 資料已內嵌至資料集。
>* 資料集已啟用，可在「即時客戶設定檔」中使用（即使未擷取任何資料亦然）。

>
>
如果結構尚未與符合上述其中一個條件的資料集建立關聯，則可對其進行任何變更。 但是，在所有情況下，`version`元件仍保持在`1`。

## XDM欄位限制和最佳實務

架構的欄位列在其`properties`物件中。 每個欄位本身就是一個物件，包含要說明和限制欄位可包含之資料的屬性。

有關在API中定義欄位類型的詳細資訊，請參閱本指南的[欄位限制指南](../schema/field-constraints.md)，包括最常使用資料類型的程式碼範例和選用限制。

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

* 欄位對象的名稱可能包含英數字元、破折號或下划線字元，但&#x200B;**不能**&#x200B;以下划線開頭。
   * **正確：** `fieldName`,  `field_name2`,  `Field-Name`,  `field-name_3`
   * **錯誤：** `_fieldName`
* 欄位物件名稱偏好使用camelCase。 範例：`fieldName`
* 欄位應包含`title`，寫在標題案例中。 範例：`Field Name`
* 欄位需要`type`。
   * 定義某些類型可能需要選用`format`。
   * 若需要特定的資料格式，`examples`可以新增為陣列。
   * 也可使用註冊表中的任何資料類型來定義欄位類型。 如需詳細資訊，請參閱資料類型端點指南中關於[建立資料類型](./data-types.md#create)的一節。
* `description`說明欄位和有關欄位資料的相關資訊。 它應以完整的句子寫成，語言清楚，讓任何存取架構的人都能了解欄位的意圖。

請參閱[欄位限制](../schema/field-constraints.md)的相關檔案，以取得如何在API中定義不同欄位類型的詳細資訊。

## 後續步驟

若要開始使用[!DNL Schema Registry] API進行呼叫，請選取可用的端點指南之一。
