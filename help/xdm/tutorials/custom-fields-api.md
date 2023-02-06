---
title: 在結構註冊表API中定義XDM欄位
description: 了解如何在Schema Registry API中建立自訂Experience Data Model(XDM)資源時定義不同欄位。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 定義Schema Registry API中的XDM欄位

所有Experience Data Model(XDM)欄位都是使用標準來定義 [JSON結構](https://json-schema.org/) 套用至其欄位類型的限制，以及Adobe Experience Platform所強制之欄位名稱的其他限制。 Schema Registry API可讓您透過使用格式和選用的限制，定義結構中的自訂欄位。 XDM欄位類型由欄位層級屬性公開， `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 是系統產生的值，因此使用API時，您不需要將此屬性新增至欄位的JSON(除外 [建立自訂地圖類型](#custom-maps))。 最佳作法是使用JSON結構類型(例如 `string` 和 `integer`)，且下表定義適當的最小/最大限制。

本指南概述定義不同欄位類型（包括具有可選屬性的類型）的適當格式。 有關可選屬性和類型特定關鍵字的詳細資訊，請參閱 [JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/type.html).

若要開始，請尋找所需的欄位類型，並使用所提供的范常式式碼來建置您的API請求 [建立欄位群組](../api/field-groups.md#create) 或 [建立資料類型](../api/data-types.md#create).

## [!UICONTROL 字串] {#string}

[!UICONTROL 字串] 欄位的指示方式為 `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

您可以透過下列其他屬性，選擇性地限制可為字串輸入的值類型：

* `pattern`:要限制的規則運算式模式。
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

[!UICONTROL URI] 欄位的指示方式為 `type: string` 帶 `format` 屬性設定為 `uri`. 不接受其他屬性。

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 列舉] {#enum}

[!UICONTROL 列舉] 必須使用 `type: string`，且列舉值本身會提供在 `enum` 陣列：

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

您可以選擇為 `meta:enum` 屬性，每個標籤都鍵入到 `enum`.

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
>此 `meta:enum` 值 **not** 聲明枚舉或自行驅動任何資料驗證。 在大多數情況下， `meta:enum` 也提供於 `enum` 以確保資料受到限制。 不過，在某些使用案例中， `meta:enum` 提供時沒有對應 `enum` 陣列。 請參閱 [定義建議值](../tutorials/suggested-values.md) 以取得更多資訊。

您可以選擇提供 `default` 用於指示預設值的屬性 `enum` 若未提供任何值，欄位將使用的值。

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
>若否 `default` 值，且列舉欄位設為 `required`，任何缺少此欄位已接受值的記錄在擷取時將無法驗證。

## [!UICONTROL 數字] {#number}

數字欄位以表示 `type: number` 沒有其他必要屬性。

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` 類型用於任何數值類型（整數或浮點數），但 [`integer` 類型](#integer) 具體用於整數。 請參閱 [數值類型的JSON結構檔案](https://json-schema.org/understanding-json-schema/reference/numeric.html) 以取得每種類型的使用案例詳細資訊。

## [!UICONTROL 整數] {#integer}

[!UICONTROL 整數] 欄位的指示方式為 `type: integer` 沒有其他必填欄位。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>同時 `integer` 類型具體指整數， [`number` 類型](#number) 可用於任何數值類型，包括整數或浮點數。 請參閱 [數值類型的JSON結構檔案](https://json-schema.org/understanding-json-schema/reference/numeric.html) 以取得每種類型的使用案例詳細資訊。

您可以選擇新增以限制整數的範圍 `minimum` 和 `maximum` 屬性。 結構產生器UI支援的數種其他數值類型僅 `integer` 類型 `minimum` 和 `maximum` 限制，例如 [[!UICONTROL 長]](#long), [[!UICONTROL 簡短]](#short)，和 [[!UICONTROL 位元組]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL 長] {#long}

等同於 [!UICONTROL 長] 透過結構產生器UI建立的欄位是 [`integer` 類型欄位](#integer) 特定 `minimum` 和 `maximum` 值(`-9007199254740992` 和 `9007199254740992`，分別)。

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL 簡短] {#short}

等同於 [!UICONTROL 簡短] 透過結構產生器UI建立的欄位是 [`integer` 類型欄位](#integer) 特定 `minimum` 和 `maximum` 值(`-32768` 和 `32768`，分別)。

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

等同於 [!UICONTROL 位元組] 透過結構產生器UI建立的欄位是 [`integer` 類型欄位](#integer) 特定 `minimum` 和 `maximum` 值(`-128` 和 `128`，分別)。

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

[!UICONTROL 布林值] 欄位的指示方式為 `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

您可以選擇提供 `default` 擷取期間未提供明確值時，欄位將使用的值。

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
>若否 `default` 值，且布林欄位設為 `required`，任何缺少此欄位已接受值的記錄在擷取時將無法驗證。

## [!UICONTROL 日期] {#date}

[!UICONTROL 日期] 欄位的指示方式為 `type: string` 和 `format: date`. 您也可以選擇提供 `examples` ，以便針對手動輸入資料的使用者，顯示範例日期字串時使用。

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] 欄位的指示方式為 `type: string` 和 `format: date-time`. 您也可以選擇提供 `examples` ，以便為手動輸入資料的用戶顯示示例日期時間字串。

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

[!UICONTROL 陣列] 欄位的指示方式為 `type: array` 和 `items` 定義陣列將接受的項的架構的對象。

您可以使用基元類型（例如字串的陣列）來定義陣列項目：

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

您也可以參照 `$id` 資料類型 `$ref` 屬性。 以下是 [!UICONTROL 付款項] 對象：

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

[!UICONTROL 物件] 欄位的指示方式為 `type: object` 和 `properties` 定義架構欄位子屬性的物件。

定義於 `properties` 可使用任何基元來定義 `type` 或透過 `$ref` 指向的屬性 `$id` 的值：

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

您也可以參照資料類型來定義整個物件，前提是相關資料類型本身定義為 `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 地圖] {#map}

映射欄位本質上是 [`object`-type欄位](#object) 以及不受約束的鍵集。 與對象一樣，映射具有 `type` 值 `object`但 `meta:xdmType` 明確設定為 `map`.

地圖 **不能** 定義任何屬性。 It **必須** 定義單一 `additionalProperties` 描述映射中包含的值類型的架構（每個映射只能包含單一資料類型）。 此 `type` 值必須為 `string` 或 `integer`.

例如，含有字串類型值的對應欄位定義如下：

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

如需建立自訂對映欄位的詳細資訊，請參閱下方的區段。

### 建立自訂地圖類型 {#custom-maps}

為了在XDM中有效支援「類似地圖」資料，可以使用 `meta:xdmType` 設為 `map` 要清楚說明對象應被管理，就像密鑰集不受約束一樣。 擷取至映射欄位的資料必須使用字串索引鍵，且僅使用字串或整數值(由 `additionalProperties.type`)。

XDM對於此儲存提示的使用設定了下列限制：

* 映射類型必須為類型 `object`.
* 映射類型不得定義屬性（換句話說，它們定義「空」對象）。
* 映射類型必須包括 `additionalProperties.type` 描述可放置在映射中的值的欄位，其中 `string` 或 `integer`.

請確定您只在絕對必要時使用地圖類型欄位，因為這些欄位有下列效能缺點：

* 回應時間從 [Adobe Experience Platform查詢服務](../../query-service/home.md) 1億條記錄會從3秒降到10秒。
* 地圖必須少於16個鍵，否則可能會進一步退化。

Platform使用者介面在擷取地圖類型欄位索引鍵的方式上也有限制。 雖然物件類型欄位可展開，但地圖會改為單一欄位顯示。

## 後續步驟

本指南說明如何在API中定義不同欄位類型。 如需XDM欄位類型的格式化詳細資訊，請參閱 [XDM欄位類型限制](../schema/field-constraints.md).
