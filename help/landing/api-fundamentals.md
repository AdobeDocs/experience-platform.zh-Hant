---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Experience PlatformAPI基礎
description: 本文檔簡要概述了與Experience PlatformAPI相關的一些底層技術和語法。
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Experience PlatformAPI基礎

Adobe Experience PlatformAPI採用了一些基礎技術和語法，對於有效管理基於JSON的API來說，這些技術和語法非常重要 [!DNL Platform] 資源。 本文檔簡要概述了這些技術，並提供了指向外部文檔的連結以瞭解更多資訊。

## JSON指針 {#json-pointer}

JSON指針是標準字串語法([RFC 6901](https://tools.ietf.org/html/rfc6901))，用於標識JSON文檔中的特定值。 JSON指針是由 `/` 字元，這些字元指定對象鍵或陣列索引，標籤可以是字串或數字。 JSON指針字串用於許多PATCH操作 [!DNL Platform] API，如本文檔後面所述。 有關JSON指針的詳細資訊，請參閱 [JSON指針概述文檔](https://rapidjson.org/md_doc_pointer.html)。

### 示例JSON架構對象

以下JSON表示一個簡化的XDM架構，其欄位可以使用JSON指針字串引用。 請注意，已使用自定義架構欄位組添加的所有欄位(如 `loyaltyLevel`)在 `_{TENANT_ID}` 對象，而已使用核心欄位組添加的欄位(如 `fullName`)不是。

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

### 基於架構對象的JSON指針示例

| JSON指針 | 解析為 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (返回對 `fullName` 欄位，由核心欄位組提供)。 |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (返回對 `loyaltyLevel` 欄位，由自定義欄位組提供)。 |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>處理 `xdm:sourceProperty` 和 `xdm:destinationProperty` 屬性 [!DNL Experience Data Model] (XDM)描述符，任何 `properties` 鍵 **排除** 從JSON指針字串中。 查看 [!DNL Schema Registry] API開發人員指南子指南 [描述符](../xdm/api/descriptors.md) 的子菜單。

## JSON修補程式 {#json-patch}

有許多PATCH操作 [!DNL Platform] 接受JSON修補程式對象的請求負載的API。 JSON修補程式是標準化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))，用於描述對JSON文檔的更改。 它允許您定義對JSON的部分更新，而無需在請求正文中發送整個文檔。

### 示例JSON修補程式對象

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修補程式操作的類型。 雖然JSON修補程式支援多種不同的操作類型，但並非所有PATCH操作 [!DNL Platform] API與每種操作類型相容。 可用的操作類型有：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON結構的部分，使用 [JSON指針](#json-pointer) 符號。

取決於中指示的操作類型 `op`,JSON修補程式對象可能需要其他屬性。 有關不同JSON修補程式操作及其所需語法的詳細資訊，請參閱 [JSON修補程式文檔](https://datatracker.ietf.org/doc/html/rfc6902)。

## JSON架構 {#json-schema}

JSON架構是用於描述和驗證JSON資料結構的格式。 [體驗資料模型(XDM)](../xdm/home.md) 利用JSON架構功能對所接收客戶體驗資料的結構和格式強制實施約束。 有關JSON架構的詳細資訊，請參閱 [正式檔案](https://json-schema.org/)。

## 後續步驟

本文檔介紹了管理基於JSON的資源時涉及的一些技術和語法 [!DNL Experience Platform]。 請參閱 [入門指南](api-guide.md) 瞭解有關使用平台API（包括最佳實踐）的更多資訊。 有關常見問題的回答，請參閱 [平台故障排除指南](troubleshooting.md)。
