---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Experience PlatformAPI基礎知識
description: 本檔案簡要概述Experience Platform API相關的一些基礎技術和語法。
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Experience PlatformAPI基礎知識

Adobe Experience Platform API採用數個重要的基礎技術和語法，以有效管理JSON型[!DNL Platform]資源。 本檔案提供這些技術的簡短概觀，以及外部檔案的連結以取得詳細資訊。

## JSON指標 {#json-pointer}

JSON指標是標準化的字串語法([RFC 6901](https://tools.ietf.org/html/rfc6901))，用於識別JSON檔案內的特定值。 JSON指標是以`/`字元分隔的權杖字串，指定了物件索引鍵或陣列索引，而權杖可以是字串或數字。 [!DNL Platform] API的許多PATCH作業都會使用JSON指標字串，如本檔案稍後所述。 如需JSON指標的詳細資訊，請參閱[JSON指標概觀檔案](https://rapidjson.org/md_doc_pointer.html)。

### 範例JSON結構描述物件

以下JSON代表簡化的XDM結構描述，其欄位可使用JSON指標字串參照。 請注意，所有使用自訂結構描述欄位群組（例如`loyaltyLevel`）新增的欄位，都是在`_{TENANT_ID}`物件底下命名的，而使用核心欄位群組（例如`fullName`）新增的欄位則否。

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

### 根據結構描述物件的JSON指標範例

| JSON指標 | 解析為 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | （傳回核心欄位群組提供的`fullName`欄位參考。） |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | （傳回自訂欄位群組提供的`loyaltyLevel`欄位參考。） |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>處理[!DNL Experience Data Model] (XDM)描述項的`xdm:sourceProperty`和`xdm:destinationProperty`屬性時，任何`properties`索引鍵都必須從JSON指標字串中&#x200B;**排除**。 如需詳細資訊，請參閱[描述元](../xdm/api/descriptors.md)上的[!DNL Schema Registry] API開發人員指南子指南。

## JSON修補程式 {#json-patch}

[!DNL Platform] API有許多接受JSON修補程式物件的PATCH作業，以供其要求裝載使用。 JSON修補程式是標準化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))，用於說明JSON檔案的變更。 它可讓您定義JSON的部分更新，而不需在請求內文中傳送整個檔案。

### 範例JSON修補程式物件

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`：修補操作的型別。 雖然JSON修補程式支援數種不同的作業型別，但並非所有[!DNL Platform] API中的PATCH作業都與每種作業型別相容。 可用的作業型別為：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`：要更新的JSON結構部分，使用[JSON指標](#json-pointer)標籤法識別。

根據`op`中指示的作業型別，JSON修補程式物件可能需要其他屬性。 如需不同JSON修補程式操作及其所需語法的詳細資訊，請參閱[JSON修補程式檔案](https://datatracker.ietf.org/doc/html/rfc6902)。

## JSON結構描述 {#json-schema}

JSON結構描述是一種用於說明和驗證JSON資料結構的格式。 [體驗資料模型(XDM)](../xdm/home.md)運用JSON結構描述功能，對擷取的客戶體驗資料的結構和格式強制執行限制。 如需JSON結構描述的詳細資訊，請參閱[正式檔案](https://json-schema.org/)。

## 後續步驟

本檔案介紹管理[!DNL Experience Platform]之JSON型資源相關的一些技術和語法。 如需使用Platform API （包括最佳實務）的詳細資訊，請參閱[快速入門手冊](api-guide.md)。 如需常見問題的解答，請參閱[平台疑難排解指南](troubleshooting.md)。
