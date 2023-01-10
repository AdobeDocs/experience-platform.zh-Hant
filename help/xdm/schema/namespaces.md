---
keywords: Experience Platform；首頁；熱門主題；結構；結構；xdm；體驗資料模型；命名空間；命名空間；相容性模式；修正；
solution: Experience Platform
title: Experience Data Model(XDM)中的命名空間調整
description: 了解Experience Data Model(XDM)中的名稱調整功能可如何協助您擴充結構，並防止不同結構元件匯整在一起時發生欄位衝突。
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Experience Data Model(XDM)中的命名空間調整

Experience Data Model(XDM)結構中的所有欄位都有相關聯的命名空間。 這些命名空間可讓您擴充結構並防止欄位衝突，因為不同的結構元件會結合在一起。 本檔案概略說明XDM中的命名空間，以及在 [結構註冊表API](../api/overview.md).

命名空間調整可讓您將一個命名空間中的欄位定義為不同命名空間中相同欄位的不同之處。 實際上，欄位的命名空間會指出欄位的建立者(例如標準XDM(Adobe)、廠商或您的組織)。

例如，假設使用 [[!UICONTROL 個人聯繫人詳細資訊] 欄位群組](../field-groups/profile/demographic-details.md)，此標準 `mobilePhone` 欄位中存在 `xdm` 命名空間。 在相同的架構中，您也可以自由建立個別 `mobilePhone` 欄位(您的 [租用戶ID](../api/getting-started.md#know-your-tenant_id))。 這兩個欄位可以共存，同時具有不同的基本含義或限制。

## 命名步調語法

以下各節說明如何以XDM語法指派命名空間。

### 標準XDM {#standard}

標準XDM語法可讓您深入了解命名空間在結構中的表示方式(包括 [如何在Adobe Experience Platform翻譯](#compatibility))。

標準XDM使用 [JSON-LD](https://json-ld.org/) 將命名空間指派給欄位的語法。 此命名空間以URI(如 `https://ns.adobe.com/xdm` 針對 `xdm` 命名空間)，或作為在 `@context` 結構的屬性。

以下是標準XDM語法中產品的範例結構。 除 `@id` （由JSON-LD規格定義的唯一識別碼）, `properties` 以命名空間開頭，並以欄位名稱結尾。 若使用 `@context`，命名空間和欄位名稱會以冒號(`:`)。 如果不使用首碼，則命名空間和欄位名稱會以斜線(`/`)。

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
| `@context` | 定義可使用的速記前置詞，而不是下面的完整命名空間URI的對象 `properties`. |
| `@id` | 記錄的唯一標識符，由 [JSON-LD規格](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | 使用速記首碼表示命名空間的欄位範例。 在這種情況下， `xdm` 是命名空間(`https://ns.adobe.com/xdm`)和 `sku` 是欄位名稱。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整命名空間URI的欄位範例。 在這種情況下， `https://ns.adobe.com/xdm/channels` 是命名空間，和 `application` 是欄位名稱。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 供應商資源提供的欄位使用其獨特的命名空間。 在此範例中， `https://ns.adobe.com/vendorA/product` 是供應商命名空間， `stockNumber` 是欄位名稱。 |
| `tenantId:internalSku` | 貴組織定義的欄位會使用您的唯一租用戶ID做為其命名空間。 在此範例中， `tenantId` 是租用戶命名空間(`https://ns.adobe.com/tenantId`)和 `internalSku` 是欄位名稱。 |

{style=&quot;table-layout:auto&quot;}

### 相容性模式 {#compatibility}

在Adobe Experience Platform中，XDM結構以 [相容性模式](../api/appendix.md#compatibility) 語法，此語法不使用JSON-LD語法來表示命名空間。 相反地，Platform會將命名空間轉換為父欄位（以底線開頭），並巢狀內嵌其下的欄位。

例如，標準XDM `repo:createdDate` 轉換為 `_repo.createdDate` 和會出現在相容模式的以下結構下：

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

使用 `xdm` 命名空間在 `properties` 然後 `xdm:` 前置詞會出現在 [標準XDM語法](#standard). 例如， `xdm:sku` 僅列為 `sku` 。

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

本指南概述XDM命名空間，以及它們在JSON中的表示方式。 如需如何使用API設定XDM結構的詳細資訊，請參閱 [Schema Registry API指南](../api/overview.md).
