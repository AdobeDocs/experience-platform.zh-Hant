---
title: 在架構註冊表API中定義XDM欄位
description: 瞭解如何在架構註冊表API中建立自定義體驗資料模型(XDM)資源時定義不同的欄位。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 在架構註冊表API中定義XDM欄位

所有體驗資料模型(XDM)欄位都使用標準 [JSON架構](https://json-schema.org/) 適用於其欄位類型的約束，以及Adobe Experience Platform強制實施的欄位名稱的附加約束。 使用方案註冊表API，您可以通過使用格式和可選約束來定義方案中的自定義欄位。 XDM欄位類型由欄位級屬性公開， `meta:xdmType`。

>[!NOTE]
>
>`meta:xdmType` 是系統生成的值，因此使用API時不需要將此屬性添加到欄位的JSON(除非 [建立自定義映射類型](#custom-maps))。 最佳做法是使用JSON架構類型(如 `string` 和 `integer`)，具有下表中定義的相應最小/最大約束。

本指南概述了定義不同欄位類型（包括具有可選屬性的欄位類型）的適當格式。 有關可選屬性和類型特定關鍵字的詳細資訊，請通過 [JSON架構文檔](https://json-schema.org/understanding-json-schema/reference/type.html)。

要開始，請查找所需的欄位類型，並使用提供的示例代碼生成API請求 [建立欄位組](../api/field-groups.md#create) 或 [建立資料類型](../api/data-types.md#create)。

## [!UICONTROL 字串] {#string}

[!UICONTROL 字串] 欄位由 `type: string`。

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

可以通過以下附加屬性來根據需要約束可以為字串輸入哪些類型的值：

* `pattern`:要約束的規則運算式模式。
* `minLength`:字串的最小長度。
* `maxLength`:字串的最大長度。

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] 欄位由 `type: string` 帶 `format` 屬性設定為 `uri`。 不接受其他屬性。

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 枚舉] {#enum}

[!UICONTROL 枚舉] 必須使用 `type: string`，在 `enum` 陣列：

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

您可以選擇在以下位置為每個值提供面向客戶的標籤 `meta:enum` 屬性，每個標籤在下面的相應值 `enum`。

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  }
}
```

>[!NOTE]
>
>的 `meta:enum` 值 **不** 聲明枚舉或自行驅動任何資料驗證。 在大多數情況下， `meta:enum` 也提供 `enum` 確保資料受到約束。 但是，有些使用情況 `meta:enum` 沒有相應的 `enum` 陣列。 請參閱上的教程 [定義建議值](../tutorials/suggested-values.md) 的子菜單。

您可以選擇提供 `default` 屬性，以指示預設值 `enum` 欄位在未提供值時使用的值。

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  },
  "default": "value1"
}
```

>[!IMPORTANT]
>
>否 `default` 提供值，並將枚舉欄位設定為 `required`，任何缺少此欄位的接受值的記錄在接收時將無法驗證。

## [!UICONTROL 數字] {#number}

數字欄位由 `type: number` 沒有其他必需的屬性。

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` 類型用於任何數字類型（整數或浮點數），而 [`integer` 類型](#integer) 具體用於積分數。 請參閱 [數字類型上的JSON架構文檔](https://json-schema.org/understanding-json-schema/reference/numeric.html) 的子菜單。

## [!UICONTROL 整數] {#integer}

[!UICONTROL 整數] 欄位由 `type: integer` 沒有其他必填欄位。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>同時 `integer` 類型具體是指整數， [`number` 類型](#number) 用於任何數字類型（整數或浮點數）。 請參閱 [數字類型上的JSON架構文檔](https://json-schema.org/understanding-json-schema/reference/numeric.html) 的子菜單。

可以通過添加 `minimum` 和 `maximum` 屬性。 架構生成器UI支援的其他幾種數值類型 `integer` 特定類型 `minimum` 和 `maximum` 約束，例如 [[!UICONTROL 龍]](#long)。 [[!UICONTROL 短]](#short), [[!UICONTROL 位元組]](#byte)。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL 龍] {#long}

等價於 [!UICONTROL 龍] 通過架構生成器UI建立的欄位是 [`integer` 類型欄位](#integer) 具體 `minimum` 和 `maximum` 值(`-9007199254740992` 和 `9007199254740992`)。

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL 短] {#short}

等價於 [!UICONTROL 短] 通過架構生成器UI建立的欄位是 [`integer` 類型欄位](#integer) 具體 `minimum` 和 `maximum` 值(`-32768` 和 `32768`)。

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL 位元組] {#byte}

等價於 [!UICONTROL 位元組] 通過架構生成器UI建立的欄位是 [`integer` 類型欄位](#integer) 具體 `minimum` 和 `maximum` 值(`-128` 和 `128`)。

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL 布林值] {#boolean}

[!UICONTROL 布爾型] 欄位由 `type: boolean`。

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

您可以選擇提供 `default` 在接收期間未提供顯式值時欄位將使用的值。

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>否 `default` 值，布爾欄位設定為 `required`，任何缺少此欄位的接受值的記錄在接收時將無法驗證。

## [!UICONTROL 日期] {#date}

[!UICONTROL 日期] 欄位由 `type: string` 和 `format: date`。 您還可以選擇提供 `examples` 在您希望為手動輸入資料的用戶顯示示例日期字串時，可使用。

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL 日期時間] {#date-time}

[!UICONTROL 日期時間] 欄位由 `type: string` 和 `format: date-time`。 您還可以選擇提供 `examples` 在希望為手動輸入資料的用戶顯示示例日期時間字串時，可使用此選項。

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL 陣列] {#array}

[!UICONTROL 陣列] 欄位由 `type: array` 和 `items` 定義陣列將接受的項的架構的對象。

可以使用基元類型定義陣列項，如字串陣列：

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

您還可以參考 `$id` 資料類型 `$ref` 屬性。 以下是 [!UICONTROL 付款項] 對象：

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL 物件] {#object}

[!UICONTROL 對象] 欄位由 `type: object` 和 `properties` 定義架構欄位子屬性的對象。

定義的每個子欄位 `properties` 可以使用任何基元定義 `type` 或通過 `$ref` 指向 `$id` 類型：

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

也可以通過引用資料類型來定義整個對象，前提是所討論的資料類型本身定義為 `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 地圖] {#map}

映射欄位本質上是 [`object` — 類型欄位](#object) 不受約束的鍵集。 與對象一樣，地圖 `type` 值 `object`但是 `meta:xdmType` 已顯式設定為 `map`。

地圖 **不能** 定義任何屬性。 它 **必須** 定義單個 `additionalProperties` 模式，用於描述映射中包含的值的類型（每個映射只能包含單個資料類型）。 的 `type` 值必須為 `string` 或 `integer`。

例如，將定義一個具有字串類型值的映射欄位，如下所示：

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

有關建立自定義映射欄位的進一步詳細資訊，請參閱下節。

### 建立自定義映射類型 {#custom-maps}

為了在XDM中有效地支援「類地圖」資料，可以使用 `meta:xdmType` 設定為 `map` 以明確管理對象時，應將鍵集視為不受約束。 被攝入到映射欄位中的資料必須使用字串鍵，並且只使用字串或整數值(由 `additionalProperties.type`)。

XDM對此儲存提示的使用設定了以下限制：

* 映射類型MUST為類型 `object`。
* 映射類型不能定義屬性（換句話說，它們定義「空」對象）。
* 映射類型必須包括 `additionalProperties.type` 欄位，該欄位描述可能放置在映射中的值 `string` 或 `integer`。

確保在完全必要時僅使用映射類型欄位，因為這些欄位具有以下效能缺陷：

* 響應時間 [Adobe Experience Platform查詢服務](../../query-service/home.md) 從3秒到10秒就有1億條記錄。
* 地圖必須少於16個鍵，否則可能會進一步退化。

平台用戶介面在如何提取映射類型欄位的鍵方面也有局限性。 對象類型欄位可以展開，但映射將顯示為單個欄位。

## 後續步驟

本指南介紹如何在API中定義不同的欄位類型。 有關如何格式化XDM欄位類型的詳細資訊，請參見上的指南 [XDM欄位類型約束](../schema/field-constraints.md)。
