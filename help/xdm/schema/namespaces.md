---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；xdm；體驗資料模型；名稱空間；名稱空間；相容模式；xed；
solution: Experience Platform
title: Experience Data Model (XDM)中的名稱空間
description: 瞭解Experience Data Model (XDM)中的名稱空間如何讓您擴充結構描述，並在不同結構描述元件彙整時防止欄位衝突。
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Experience Data Model (XDM)中的名稱空間

>[!IMPORTANT]
>
>在XDM中，名稱空間（此頁面主題）是用來區分結構描述中的欄位。 這與Identity Service中的身分名稱空間概念不同，該概念會使用名稱空間來區分身分值。 如需詳細資訊，請參閱身分識別服務](../../identity-service/features/namespaces.md)中[名稱空間的檔案。

體驗資料模型(XDM)結構描述中的所有欄位都有關聯的名稱空間。 這些名稱空間可讓您擴充結構描述，並在不同結構描述元件彙整時防止欄位衝突。 本檔案概述XDM中的名稱空間，以及這些名稱空間在[結構描述登入API](../api/overview.md)中的表示方式。

名稱空間可讓您在一個名稱空間中定義欄位，以表示不同名稱空間中相同欄位的意義。 實際上，欄位的名稱空間會指出建立欄位的人員(例如標準XDM (Adobe)、廠商或您的組織)。

例如，假設某個XDM結構描述使用[[!UICONTROL 個人聯絡詳細資訊]欄位群組](../field-groups/profile/demographic-details.md)，而該群組的標準`mobilePhone`欄位存在於`xdm`名稱空間中。 在相同結構描述中，您也可以在不同的名稱空間（您的[租使用者識別碼](../api/getting-started.md#know-your-tenant_id)）下建立個別的`mobilePhone`欄位。 這兩個欄位可以共存，但具有不同的基本含義或限制。

## 名稱空間語法

以下章節示範如何以XDM語法指派名稱空間。

### 標準XDM {#standard}

標準XDM語法可讓您深入瞭解名稱空間在結構描述中的呈現方式(包括[它們在Adobe Experience Platform](#compatibility)中的轉譯方式)。

標準XDM使用[JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts)語法將名稱空間指派給欄位。 此名稱空間採用URI的形式（例如`xdm`名稱空間的`https://ns.adobe.com/xdm`），或是在結構描述的`@context`屬性中設定的速記首碼。

以下是標準XDM語法中產品的結構描述範例。 除了`@id` （由JSON-LD規格定義的唯一識別碼）之外，`properties`下的每個欄位都會以名稱空間開頭，並以欄位名稱結尾。 如果使用在`@context`下定義的速記首碼，則名稱空間和欄位名稱會以冒號(`:`)分隔。 如果不使用首碼，則名稱空間和欄位名稱會以斜線(`/`)分隔。

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
| `@context` | 一個物件，定義可以使用的速記首碼，而不是`properties`下的完整名稱空間URI。 |
| `@id` | [JSON-LD規格](https://www.w3.org/TR/json-ld11/#node-identifiers)所定義的記錄唯一識別碼。 |
| `xdm:sku` | 使用速記首碼表示名稱空間的欄位範例。 在此案例中，`xdm`是名稱空間(`https://ns.adobe.com/xdm`)，`sku`是欄位名稱。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整名稱空間URI的欄位範例。 在此案例中，`https://ns.adobe.com/xdm/channels`是名稱空間，`application`是欄位名稱。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 廠商資源提供的欄位會使用其專屬的名稱空間。 在此範例中，`https://ns.adobe.com/vendorA/product`是廠商名稱空間，`stockNumber`是欄位名稱。 |
| `tenantId:internalSku` | 貴組織定義的欄位會使用您的唯一租使用者ID作為其名稱空間。 在此範例中，`tenantId`是租使用者名稱空間(`https://ns.adobe.com/tenantId`)，`internalSku`是欄位名稱。 |

{style="table-layout:auto"}

### 相容性模式 {#compatibility}

在Adobe Experience Platform中，XDM結構描述是以[相容性模式](../api/appendix.md#compatibility)語法表示，不會使用JSON-LD語法來表示名稱空間。 Platform會將名稱空間轉換為父欄位（以底線開頭），並將欄位巢狀在其下。

例如，標準XDM `repo:createdDate`已轉換為`_repo.createdDate`，並會顯示在相容性模式的下列結構下：

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

使用`xdm`名稱空間的欄位會顯示為`properties`下的根欄位，並捨棄以[標準XDM語法](#standard)顯示的`xdm:`首碼。 例如，`xdm:sku`只列為`sku`。

以下JSON代表如何將以上所示的標準XDM語法範例轉譯為相容性模式。

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

本指南概述XDM名稱空間及其在JSON中的呈現方式。 如需有關如何使用API設定XDM結構描述的詳細資訊，請參閱[結構描述登入API指南](../api/overview.md)。
