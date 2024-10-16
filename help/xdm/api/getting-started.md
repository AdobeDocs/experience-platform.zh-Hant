---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；Schema登入；
solution: Experience Platform
title: 開始使用結構描述登入API
description: 本檔案會介紹您在嘗試呼叫Schema Registry API之前需要瞭解的核心概念。
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: eb1cf204e95591082b27dc97cd3c709a23b20b08
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 5%

---

# 開始使用[!DNL Schema Registry] API

[!DNL Schema Registry] API可讓您建立和管理各種Experience Data Model (XDM)資源。 本檔案提供嘗試呼叫[!DNL Schema Registry] API之前需要瞭解的核心概念簡介。

## 先決條件

使用開發人員指南需要深入瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../schema/composition.md)：瞭解XDM結構描述的基本建置區塊。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

XDM使用JSON結構描述格式來說明及驗證所擷取客戶體驗資料的結構。 因此，強烈建議您檢閱[官方JSON結構描述檔案](https://json-schema.org/)，以更加瞭解此基礎技術。

## 讀取範例 API 呼叫

[!DNL Schema Registry] API檔案提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

## 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Schema Registry]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱檔案](../../sandboxes/home.md)。

對[!DNL Schema Registry]的所有查詢(GET)請求都需要額外的`Accept`標頭，其值會決定API傳回的資訊格式。 如需詳細資訊，請參閱下方的[接受標頭](#accept)區段。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* `Content-Type: application/json`

## 知道您的TENANT_ID {#know-your-tenant_id}

在整個API指南中，您將會看到`TENANT_ID`的參考。 此ID可用來確保您建立的資源能正確進行名稱空間，並包含在您的組織內。 如果您不知道您的ID，可以透過執行以下GET請求來存取它：

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

成功的回應會傳回有關貴組織使用[!DNL Schema Registry]的資訊。 這包含`tenantId`屬性，其值是您的`TENANT_ID`。

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

## 瞭解`CONTAINER_ID` {#container}

呼叫[!DNL Schema Registry] API需要使用`CONTAINER_ID`。 有兩個可對其進行API呼叫的容器： `global`容器和`tenant`容器。

### 全域容器

`global`容器儲存所有標準Adobe和[!DNL Experience Platform]合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 您只能對`global`容器執行清單和查詢(GET)請求。

使用`global`容器的呼叫範例如下所示：

```http
GET /global/classes
```

### 租使用者容器

`tenant`容器包含所有由組織定義的類別、欄位群組、資料型別、結構描述和描述項，切勿與您的唯一`TENANT_ID`混淆。 這些對於每個組織都是獨一無二的，這表示其他組織看不到或無法管理這些值。 您可以針對您在`tenant`容器中建立的資源，執行所有CRUD作業(GET、POST、PUT、PATCH、DELETE)。

使用`tenant`容器的呼叫範例如下所示：

```http
POST /tenant/fieldgroups
```

當您在`tenant`容器中建立類別、欄位群組、結構描述或資料型別時，它會儲存到[!DNL Schema Registry]並指派包含您的`TENANT_ID`的`$id` URI。 此`$id`在整個API中使用來參考特定資源。 下一節提供`$id`值的範例。

## 資源識別 {#resource-identification}

XDM資源以URI形式的`$id`屬性來識別，例如以下範例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

若要讓URI更適合REST，結構描述在稱為`meta:altId`的屬性中也會有URI的點標籤法編碼：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

對[!DNL Schema Registry] API的呼叫將支援URL編碼的`$id` URI或`meta:altId` （點標籤法格式）。 最佳實務是在對API進行REST呼叫時使用URL編碼的`$id` URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept標題 {#accept}

在[!DNL Schema Registry] API中執行清單和查詢(GET)作業時，需要`Accept`標頭來決定API傳回的資料格式。 查詢特定資源時，`Accept`標頭中也必須包含版本號碼。

下表列出相容的`Accept`標頭值，包括版本號碼的值，以及使用API時傳回的描述。

| 接受 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 只傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回包含原始`$ref`和`allOf`的完整JSON結構描述清單。 這可用來傳回完整資源的清單。 |
| `application/vnd.adobe.xed+json; version=1` | 含有`$ref`和`allOf`的原始XDM。 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | 已解決`$ref`屬性和`allOf`。 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 含有`$ref`和`allOf`的原始XDM。 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | 已解決`$ref`屬性和`allOf`。 無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | 已解決`$ref`屬性和`allOf`。 包含描述項。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref`和`allOf`已解決，有標題和說明。 已棄用的欄位以`deprecated`的`meta:status`屬性表示。 |

{style="table-layout:auto"}

>[!NOTE]
>
>平台目前僅支援每個結構描述(`1`)的一個主要版本。 因此，在執行查詢要求時，`version`的值必須一律為`1`，才能傳回結構描述的最新次要版本。 請參閱以下小節，以取得架構版本設定的詳細資訊。

### 方案版本設定 {#versioning}

結構描述版本由結構描述登入API中的`Accept`標頭以及下游平台服務API裝載中的`schemaRef.contentType`屬性參考。

目前，Platform僅支援每個結構描述的單一主要版本(`1`)。 根據結構描述演化](../schema/composition.md#evolution)的[規則，結構描述的每次更新都必須是非破壞性的，這表示結構描述的新次要版本（`1.2`、`1.3`等） 始終與先前的次要版本回溯相容。 因此，在指定`version=1`時，結構描述登入一律會傳回結構描述的&#x200B;**latest**&#x200B;主要版本`1`，這表示不會傳回先前的次要版本。

>[!NOTE]
>
>只有在資料集參考結構描述且下列其中一個情況為真時，才會強制執行結構描述演化的非破壞性需求：
>
>* 資料已內嵌到資料集中。
>* 此資料集已啟用用於即時客戶個人檔案（即使未擷取任何資料）。
>
>如果結構描述尚未與符合上述其中一項條件的資料集建立關聯，則可以對資料集進行任何變更。 但是，在所有情況下，`version`元件仍保持在`1`。

## XDM欄位限制和最佳實務

結構描述的欄位列在它的`properties`物件中。 每個欄位本身都是物件，包含可描述和限制欄位可包含之資料的屬性。 請參閱[在API](../tutorials/custom-fields-api.md)中定義自訂欄位的指南，以取得程式碼範例和最常用資料型別的選擇性限制。

以下範例欄位說明正確格式化的XDM欄位，並提供以下有關命名限制和最佳實務的更多詳細資訊。 定義包含類似屬性的其他資源時，也可以套用這些實務。

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

* 欄位物件的名稱可能包含英數、破折號或底線字元，但&#x200B;**不能**&#x200B;以底線開頭。
   * **正確：** `fieldName`，`field_name2`，`Field-Name`，`field-name_3`
   * **不正確：** `_fieldName`
* 欄位名稱不區分大小寫，且結構描述中的相同層級必須有不同的名稱。
* 欄位物件的名稱偏好使用camelCase。 範例：`fieldName`
* 欄位應包含以字首大寫寫寫的`title`。 範例：`Field Name`
* 欄位需要`type`。
   * 定義某些型別可能需要選擇性的`format`。
   * 在需要特定格式化的資料時，可以將`examples`新增為陣列。
   * 也可以使用登入中的任何資料型別來定義欄位型別。 如需詳細資訊，請參閱資料型別端點指南中有關[建立資料型別](./data-types.md#create)的章節。
* `description`說明欄位和欄位資料的相關資訊。 應以完整的句子撰寫並加上清晰的語言，讓存取結構描述的任何人都能瞭解此欄位的意圖。

## 後續步驟

若要開始使用[!DNL Schema Registry] API進行呼叫，請選取其中一個可用的端點指南。
