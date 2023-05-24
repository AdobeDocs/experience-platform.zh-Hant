---
keywords: Experience Platform；主題；流行主題；架構；模式；xdm；經驗資料模型；命名空間；相容模式；混合；
solution: Experience Platform
title: 體驗資料模型(XDM)中的命名空間
description: 瞭解體驗資料模型(XDM)中的命名空間如何允許擴展架構並防止在將不同架構元件組合在一起時發生欄位衝突。
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 體驗資料模型(XDM)中的命名空間

體驗資料模型(XDM)架構中的所有欄位都具有關聯的命名空間。 這些命名空間允許擴展您的架構，並防止在將不同的架構元件合併在一起時發生欄位衝突。 本文檔概述了XDM中的命名空間及其在中的表示方式 [架構註冊表API](../api/overview.md)。

命名空間允許您將一個命名空間中的欄位定義為不同於另一個命名空間中同一欄位的含義。 在實踐中，欄位的命名空間指示誰建立了該欄位(如標準XDM(Adobe)、供應商或您的組織)。

例如，請考慮使用 [[!UICONTROL 個人聯繫人詳細資訊] 欄位組](../field-groups/profile/demographic-details.md)，它有標準 `mobilePhone` 欄位 `xdm` 命名空間。 在同一架構中，您也可以自由建立 `mobilePhone` 欄位 [租戶ID](../api/getting-started.md#know-your-tenant_id))。 這兩個欄位可以共存，同時具有不同的底蘊或約束。

## 命名空間語法

以下各節演示了如何以XDM語法分配命名空間。

### 標準XDM {#standard}

標準XDM語法提供了對命名空間在架構中的表示方式(包括 [如何在Adobe Experience Platform翻譯](#compatibility))。

標準XDM使用 [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) 語法，將命名空間分配給欄位。 此命名空間以URI的形式(如 `https://ns.adobe.com/xdm` 為 `xdm` 名稱空間)，或作為在 `@context` 架構的屬性。

以下是標準XDM語法中產品的示例架構。 除非 `@id` （JSON-LD規範定義的唯一標識符）, `properties` 以命名空間開頭，以欄位名結尾。 如果使用在 `@context`，命名空間和欄位名用冒號(`:`)。 如果未使用前置詞，則命名空間和欄位名用斜槓(`/`)。

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
| `@context` | 定義可以使用的速記前置詞（而不是位於以下位置的完整命名空間URI）的對象 `properties`。 |
| `@id` | 由 [JSON-LD規範](https://www.w3.org/TR/json-ld11/#node-identifiers)。 |
| `xdm:sku` | 使用速記前置詞來表示命名空間的欄位示例。 在這個例子中， `xdm` 是命名空間(`https://ns.adobe.com/xdm`)和 `sku` 是欄位名。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整命名空間URI的欄位的示例。 在這個例子中， `https://ns.adobe.com/xdm/channels` 是命名空間， `application` 是欄位名。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 供應商資源提供的欄位使用其自己的唯一命名空間。 在本例中， `https://ns.adobe.com/vendorA/product` 是供應商命名空間， `stockNumber` 是欄位名。 |
| `tenantId:internalSku` | 由您的組織定義的欄位使用您唯一的租戶ID作為其命名空間。 在本例中， `tenantId` 是租戶命名空間(`https://ns.adobe.com/tenantId`)和 `internalSku` 是欄位名。 |

{style="table-layout:auto"}

### 相容模式 {#compatibility}

在Adobe Experience Platform, XDM架構在 [相容模式](../api/appendix.md#compatibility) 語法，它不使用JSON-LD語法來表示命名空間。 相反，Platform會將命名空間轉換為父欄位（以下划線開頭），並將欄位嵌套在其下。

例如，標準XDM `repo:createdDate` 轉換為 `_repo.createdDate` 並將出現在「相容性模式」中的以下結構下：

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

使用 `xdm` 命名空間顯示為根欄位 `properties` 然後 `xdm:` 將出現在 [標準XDM語法](#standard)。 比如說， `xdm:sku` 僅列為 `sku` 的雙曲餘切值。

以下JSON表示如何將上面顯示的標準XDM語法示例轉換為相容模式。

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

本指南概述了XDM命名空間及其在JSON中的表示方式。 有關如何使用API配置XDM架構的詳細資訊，請參見 [架構註冊API指南](../api/overview.md)。
