---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Experience PlatformAPI基礎知識
description: 本檔案簡要概述與Experience PlatformAPI相關的一些基礎技術和語法。
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Experience PlatformAPI基礎知識

Adobe Experience Platform API採用數種須了解的基礎技術和語法，以有效管理JSON型 [!DNL Platform] 資源。 本檔案提供這些技術的簡短概述，以及外部檔案的連結以取得詳細資訊。

## JSON指標 {#json-pointer}

JSON指標是標準化的字串語法([RFC 6901](https://tools.ietf.org/html/rfc6901))，以識別JSON檔案中的特定值。 JSON指標是以 `/` 字元，可指定物件索引或陣列索引，代號可以是字串或數字。 JSON指標字串用於的許多PATCH操作 [!DNL Platform] API，如本檔案稍後所述。 如需JSON指標的詳細資訊，請參閱 [JSON指標概觀檔案](https://rapidjson.org/md_doc_pointer.html).

### 範例JSON結構描述物件

下列JSON代表簡化的XDM結構，其欄位可使用JSON指標字串參照。 請注意，使用自訂結構欄位群組新增的所有欄位(例如 `loyaltyLevel`)的命名空間位於 `_{TENANT_ID}` 物件，而使用核心欄位群組新增的欄位(例如 `fullName`)則否。

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

### 基於結構描述物件的JSON指標範例

| JSON指標 | 解析至 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (傳回對 `fullName` 欄位，由核心欄位群組提供。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (傳回對 `loyaltyLevel` 欄位，由自訂欄位群組提供。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>當處理 `xdm:sourceProperty` 和 `xdm:destinationProperty` 屬性 [!DNL Experience Data Model] (XDM)描述元，任何 `properties` 鍵必須 **已排除** 從JSON指標字串。 請參閱 [!DNL Schema Registry] 上的API開發人員指南子指南 [描述符](../xdm/api/descriptors.md) 以取得更多資訊。

## JSON修補程式 {#json-patch}

有許多PATCH操作 [!DNL Platform] 接受JSON修補程式物件作為要求裝載的API。 JSON修補程式是標準化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))，以說明JSON檔案的變更。 它可讓您定義JSON的部分更新，而不需在要求內文中傳送整個檔案。

### 範例JSON修補程式物件

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修補程式操作的類型。 雖然JSON修補程式支援數種不同的作業類型，但並非所有PATCH作業均位於 [!DNL Platform] API與每種作業類型相容。 可用的操作類型包括：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON結構部分，請使用 [JSON指標](#json-pointer) 標籤法。

視 `op`，則JSON Patch物件可能需要其他屬性。 如需不同JSON修補程式作業及其必要語法的詳細資訊，請參閱 [JSON修補程式檔案](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON結構 {#json-schema}

JSON結構描述是用來說明和驗證JSON資料結構的格式。 [Experience Data Model(XDM)](../xdm/home.md) 運用JSON結構功能，對擷取的客戶體驗資料的結構和格式強制執行限制。 如需JSON結構的詳細資訊，請參閱 [官方檔案](https://json-schema.org/).

## 後續步驟

本檔案介紹管理JSON型資源(適用於 [!DNL Experience Platform]. 請參閱 [快速入門手冊](api-guide.md) 如需使用Platform API的詳細資訊，包括最佳實務。 如需常見問題的解答，請參閱 [平台疑難排解指南](troubleshooting.md).
