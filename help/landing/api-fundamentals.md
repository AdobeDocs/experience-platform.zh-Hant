---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform API基礎知識
topic: getting started
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---


# Adobe Experience Platform API基礎知識

Adobe Experience Platform API採用數種重要的基礎技術和語法，以有效管理以JSON為基礎的資 [!DNL Platform] 源。 本檔案提供這些技術的簡要概述，以及外部檔案的連結，以取得更多資訊。

## JSON指標 {#json-pointer}

JSON指標是用於識別JSON檔案內特定值的標準字[串語法(RFC 6901](https://tools.ietf.org/html/rfc6901))。 JSON指標是由字元分隔的Token字 `/` 串，可指定物件索引或陣列索引，Token可以是字串或數字。 JSON指針字串用於許多API的PATCH [!DNL Platform] 作業，如本文稍後所述。 如需JSON指標的詳細資訊，請參閱 [JSON指標概觀檔案](https://rapidjson.org/md_doc_pointer.html)。

### 範例JSON結構描述物件

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### 基於架構物件的JSON指針範例

| JSON指標 | 解析為 |
|--- | ---|
| `"/title"` | &quot;忠誠會員詳細資料&quot; |
| `"/definitions/loyalty"` | (返回對象的內 `loyalty` 容) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Note]
>
>
>處理(XDM)描述 `xdm:sourceProperty` 符的 `xdm:destinationProperty` 和屬性時，必 [!DNL Experience Data Model] 須從「JSON指針」字串 `properties` 中排除任 **** 何索引鍵。 如需詳 [!DNL Schema Registry] 細資訊，請參閱描述 [符的](../xdm/api/descriptors.md) API開發人員指南子指南。

## JSON修補程式

API有許多PATCH作業會接 [!DNL Platform] 受JSON修補物件的要求負載。 JSON修補程式是用於描述JSON檔案變更的[標準格式(RFC 6902](https://tools.ietf.org/html/rfc6902))。 它可讓您定義JSON的部分更新，而不需在請求內文中傳送整個檔案。

### 範例JSON修補程式物件

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: 修補程式操作的類型。 雖然JSON修補程式支援數種不同的作業類型，但API中的所有PATCH [!DNL Platform] 作業並非都與每種作業類型相容。 可用的操作類型包括：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: 要更新的JSON結構部分，使用 [JSON指標籤法識別](#json-pointer) 。

JSON修補物件可能需要其 `op`他屬性，視中指示的作業類型而定。 有關不同JSON修補程式作業及其必要語法的詳細資訊，請參閱 [JSON修補程式檔案](http://jsonpatch.com/)。

## JSON結構描述

JSON結構描述是用於說明和驗證JSON資料結構的格式。 [體驗資料模型(XDM)](../xdm/home.md) 運用JSON結構描述功能，對所擷取的客戶體驗資料的結構和格式實施限制。 如需JSON結構描述的詳細資訊，請參閱官方 [檔案](https://json-schema.org/)。

## 後續步驟

本檔案介紹了管理JSON型資源時的一些技術和同步 [!DNL Experience Platform]。 如需使用API的詳細資訊，包括 [!DNL Platform] 最佳實務和常見問題的解答，請參閱平台疑 [難排解指南](troubleshooting.md)。