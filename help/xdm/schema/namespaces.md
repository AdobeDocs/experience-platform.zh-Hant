---
keywords: Experience Platform;home；熱門主題；模式；模式；xdm;experience資料模型；namespace;namespaces；相容模式；固定；
solution: Experience Platform
title: 體驗資料模型(XDM)中的名稱空間調整
topic-legacy: overviews
description: 瞭解Experience Data Model(XDM)中的名稱空間調整如何讓您在將不同的架構元件整合在一起時，擴充架構並防止欄位衝突。
source-git-commit: b4c4f8f7e428d27f389bff5591a03925b6afa6d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# 體驗資料模型(XDM)中的名稱空間調整

Experience Data Model(XDM)架構中的所有欄位都有關聯的命名空間。 這些名稱空間可讓您擴充架構，並防止不同架構元件匯整在一起時發生欄位衝突。 本檔案提供了
XDM以及它們在[方案註冊表API](../api/overview.md)中的表示方式。

名稱空間允許您將一個名稱空間中的欄位定義為不同名稱空間中相同欄位的含義。 實際上，欄位的名稱空間會指出欄位的建立者(例如標準XDM(Adobe)、廠商或您的組織)。

例如，考慮使用[[!UICONTROL 個人聯繫人詳細資訊]欄位組](../field-groups/profile/demographic-details.md)的XDM模式，該欄位具有存在於`xdm`命名空間中的標準`mobilePhone`欄位。 在相同的架構中，您也可以在不同名稱空間（您的[租用戶ID](../api/getting-started.md#know-your-tenant_id)）下，自由建立個別的`mobilePhone`欄位。 這兩個欄位可以共存，同時具有不同的基本含義或約束。

## 命名空間語法

以下各節將演示如何以XDM語法指定命名空間。

### 標準XDM {#standard}

標準XDM語法可深入瞭解名稱空間在架構中的呈現方式(包括[如何在Adobe Experience Platform](#compatibility)中翻譯名稱空間)。

標準XDM使用[JSON-LD](https://json-ld.org/)語法，將名稱空間指派給欄位。 此命名空間以URI（例如`xdm`名稱空間的`https://ns.adobe.com/xdm`）形式出現，或以架構的`@context`屬性中配置的速記前置詞形式出現。

以下是標準XDM語法中產品的範例架構。 除`@id`（由JSON-LD規格定義的唯一識別碼）外，`properties`下方的每個欄位都以命名空間開頭，並以欄位名稱結尾。 如果使用在`@context`下定義的速記前置詞，則命名空間和欄位名將以冒號(`:`)分隔。 如果不使用前置詞，則命名空間和欄位名將用斜線(`/`)分隔。

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `@context` | 一個對象，用於定義可以使用的速記前置詞，而不是`properties`下的完整名稱空間URI。 |
| `@id` | 由[JSON-LD規格](https://json-ld.org/spec/latest/json-ld/#node-identifiers)定義的記錄唯一識別碼。 |
| `xdm:sku` | 使用速記前置詞表示命名空間的欄位示例。 在本例中，`xdm`是名稱空間(`https://ns.adobe.com/xdm`)，而`sku`是欄位名稱。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整名稱空間URI的欄位範例。 在本例中，`https://ns.adobe.com/xdm/channels`是namespace，而`application`是欄位名稱。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 由供應商資源提供的欄位使用它們自己的唯一名稱空間。 在此示例中，`https://ns.adobe.com/vendorA/product`是供應商名稱空間，而`stockNumber`是欄位名稱。 |
| `tenantId:internalSku` | 您組織定義的欄位會使用您唯一的租用戶ID做為其命名空間。 在此範例中，`tenantId`是租用戶名稱空間(`https://ns.adobe.com/tenantId`)，而`internalSku`是欄位名稱。 |

{style=&quot;table-layout:auto&quot;}

### 相容模式 {#compatibility}

在Adobe Experience Platform,XDM結構描述以[相容性模式](../api/appendix.md#compatibility)語法表示，該語法不使用JSON-LD語法表示命名空間。 Platform會將命名空間轉換為父欄位（從底線開始），並巢狀內嵌其下的欄位。

例如，標準XDM `repo:createdDate`將轉換為`_repo.createdDate`，並會出現在相容模式的以下結構中：

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

使用`xdm`名稱空間的欄位會顯示為`properties`下方的根欄位，並放入[標準XDM語法](#standard)中會出現的`xdm:`首碼。 例如，`xdm:sku`只會改為列為`sku`。

下列JSON代表如何將上述標準XDM語法範例轉譯為相容模式。

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## 後續步驟

本指南提供XDM名稱空間的概觀，以及它們在JSON中的呈現方式。 有關如何使用API配置XDM架構的詳細資訊，請參見[架構註冊表API指南](../api/overview.md)。
