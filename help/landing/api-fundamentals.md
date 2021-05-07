---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Experience PlatformAPI基礎
topic-legacy: getting started
description: 本文檔簡要概述了與Experience PlatformAPI相關的一些基礎技術和語法。
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Experience PlatformAPI基礎

Adobe Experience PlatformAPI採用數種重要的基礎技術和語法，以有效管理以JSON為基礎的[!DNL Platform]資源。 本檔案提供這些技術的簡要概述，以及外部檔案的連結，以取得更多資訊。

## JSON指標{#json-pointer}

JSON指標是用於識別JSON檔案內特定值的標準字串語法([RFC 6901](https://tools.ietf.org/html/rfc6901))。 JSON指標是由`/`字元分隔的Token字串，可指定物件索引或陣列索引，Token可以是字串或數字。 JSON指針字串用於[!DNL Platform] API的許多PATCH作業，如本文稍後所述。 如需JSON指標的詳細資訊，請參閱[JSON指標概觀檔案](https://rapidjson.org/md_doc_pointer.html)。

### 範例JSON結構描述物件

下列JSON代表簡化的XDM結構描述，其欄位可使用JSON指針字串加以參考。 請注意，使用自訂架構欄位群組新增的所有欄位（例如`loyaltyLevel`）都是在`_{TENANT_ID}`物件下命名，而使用核心欄位群組新增的欄位（例如`fullName`）則不是。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### 基於架構物件的JSON指針範例

| JSON指標 | 解析為 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | （傳回核心欄位群組所提供之`fullName`欄位的參考）。 |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | （傳回自訂欄位群組所提供之`loyaltyLevel`欄位的參考）。 |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>處理[!DNL Experience Data Model](XDM)描述符的`xdm:sourceProperty`和`xdm:destinationProperty`屬性時，任何`properties`鍵都必須從JSON指針字串中排除&#x200B;****。 有關詳細資訊，請參閱[描述符](../xdm/api/descriptors.md)上的[!DNL Schema Registry] API開發人員指南子指南。

## JSON修補程式{#json-patch}

[!DNL Platform] API有許多PATCH作業，可接受JSON修補物件的要求負載。 JSON修補程式是用於描述JSON檔案變更的標準格式([RFC 6902](https://tools.ietf.org/html/rfc6902))。 它可讓您定義JSON的部分更新，而不需在請求內文中傳送整個檔案。

### 範例JSON修補程式物件

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修補程式操作的類型。雖然JSON修補程式支援數種不同的作業類型，但[!DNL Platform] API中的所有PATCH作業並非都與每種作業類型相容。 可用的操作類型包括：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON結構部分，使用 [JSON Pointernotation](#json-pointer) 識別。

根據`op`中指出的作業類型，JSON Patch物件可能需要其他屬性。 有關不同JSON修補程式作業及其必要語法的詳細資訊，請參閱[JSON修補程式檔案](http://jsonpatch.com/)。

## JSON結構描述{#json-schema}

JSON結構描述是用於說明和驗證JSON資料結構的格式。 [體驗資料模型(XDM)運](../xdm/home.md) 用JSON結構描述功能，對所擷取的客戶體驗資料的結構和格式實施限制。如需JSON結構描述的詳細資訊，請參閱[官方檔案](https://json-schema.org/)。

## 後續步驟

本檔案介紹了管理[!DNL Experience Platform] JSON型資源時涉及的一些技術和語法。 請參閱[快速入門手冊](api-guide.md)以取得有關使用平台API的詳細資訊，包括最佳實務。 有關常見問題的解答，請參閱[平台疑難排解指南](troubleshooting.md)。
