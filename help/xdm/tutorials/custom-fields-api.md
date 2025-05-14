---
title: 在結構描述登入API中定義XDM欄位
description: 瞭解如何在Schema Registry API中建立自訂Experience Data Model (XDM)資源時定義不同的欄位。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6c6104a6aa0a80c886f4f02486a7645eb95da781
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# 在結構描述登入API中定義XDM欄位

所有Experience Data Model (XDM)欄位都是使用套用至其欄位型別的標準[JSON結構描述](https://json-schema.org/)限制來定義，以及針對Adobe Experience Platform強制執行的欄位名稱的其他限制。 結構描述登入API可讓您透過使用格式和選用限制來定義結構描述中的自訂欄位。 XDM欄位型別由欄位層級屬性`meta:xdmType`公開。

>[!NOTE]
>
>`meta:xdmType`是系統產生的值，因此使用API時，您不需要將此屬性新增到欄位的JSON中（除了在[建立自訂對應型別](#custom-maps)時）。 最佳實務是將JSON結構描述型別（例如`string`和`integer`）搭配適當的最小/最大條件約束，如下表所示。

本指南會概述定義不同欄位型別的適當格式，包括那些具有選擇性屬性的欄位型別。 有關選擇性屬性和型別特定關鍵字的詳細資訊，請參閱[JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/type.html)。

若要開始，請尋找所需的欄位型別，並使用提供的範常式式碼來建置您的API要求，以便[建立欄位群組](../api/field-groups.md#create)或[建立資料型別](../api/data-types.md#create)。

## [!UICONTROL 字串] {#string}

[!UICONTROL 字串]欄位由`type: string`表示。

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

您可選擇透過下列其他屬性，限制可為字串輸入哪些型別的值：

* `pattern`：要限制的Regex模式。
* `minLength`：字串的最小長度。 字串預設會接收最小值`1`。
* `maxLength`：字串的長度上限。

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

[!UICONTROL URI]欄位由`type: string`表示，其中`format`屬性設定為`uri`。 不接受其他任何屬性。

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 列舉] {#enum}

[!UICONTROL 列舉]欄位必須使用`type: string`，列舉值本身則在`enum`陣列下提供：

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

您可以選擇為`meta:enum`屬性下的每個值提供面向客戶的標籤，每個標籤都與`enum`下的對應值連線。

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
>`meta:enum`值&#x200B;**不會**&#x200B;自行宣告列舉或驅動任何資料驗證。 在大多數情況下，`meta:enum`下提供的字串也會在`enum`下提供，以確保資料受到限制。 但是，在某些情況下，提供`meta:enum`時沒有對應的`enum`陣列。 如需詳細資訊，請參閱有關[定義建議值](../tutorials/suggested-values.md)的教學課程。

您可以選擇提供`default`屬性，以指出若未提供值，欄位將會使用的預設`enum`值。

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
>如果未提供`default`值，且列舉欄位設定為`required`，則擷取時，遺失此欄位可接受值的任何記錄都將無法驗證。

## [!UICONTROL 數字] {#number}

數字欄位由`type: number`表示，沒有其他必要屬性。

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number`型別用於任何數值型別，可以是整數或浮點數，而[`integer`型別](#integer)則專門用於整數數字。 如需每種型別使用案例的詳細資訊，請參閱數值型別[&#128279;](https://json-schema.org/understanding-json-schema/reference/numeric.html)的JSON結構描述檔案。

## [!UICONTROL 整數] {#integer}

[!UICONTROL 整數]欄位由`type: integer`表示，沒有其他必要欄位。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>雖然`integer`型別是專門參照整數型別，但[`number`型別](#number)用於任何數值型別，可以是整數或浮點數。 如需每種型別使用案例的詳細資訊，請參閱數值型別[&#128279;](https://json-schema.org/understanding-json-schema/reference/numeric.html)的JSON結構描述檔案。

您可以將`minimum`和`maximum`屬性新增至定義，選擇性地限制整數的範圍。 結構描述產生器UI支援的其他數位型別只有`integer`個具有特定`minimum`和`maximum`限制條件的型別，例如[[!UICONTROL Long]](#long)、[[!UICONTROL Short]](#short)和[[!UICONTROL Byte]](#byte)。

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

與透過結構描述產生器UI建立的[!UICONTROL Long]欄位等同的是[`integer`型別欄位](#integer)，具有特定`minimum`和`maximum`值（分別為`-9007199254740992`和`9007199254740992`）。

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL 短整數] {#short}

與透過結構描述產生器UI建立的[!UICONTROL Short]欄位等同的是[`integer`型別欄位](#integer)，具有特定`minimum`和`maximum`值（分別為`-32768`和`32767`）。

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32767
}
```

## [!UICONTROL 位元組] {#byte}

與透過結構描述產生器UI建立的[!UICONTROL 位元組]欄位相當的是[`integer`型別欄位](#integer)，具有特定的`minimum`和`maximum`值（分別為`-128`和`127`）。

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 127
}
```

## [!UICONTROL 布林值] {#boolean}

[!UICONTROL 布林值]欄位由`type: boolean`表示。

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

您可以選擇提供當擷取期間未提供明確值時，欄位將使用的`default`值。

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
>如果未提供`default`值，且布林欄位設定為`required`，則擷取時，任何遺失此欄位可接受值的記錄都將無法驗證。

## [!UICONTROL 日期] {#date}

[!UICONTROL 日期]欄位由`type: string`和`format: date`表示。 您也可選擇提供`examples`陣列，以便在您想要為手動輸入資料的使用者顯示範例日期字串時運用。

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

[!UICONTROL 日期時間]欄位由`type: string`和`format: date-time`表示。 您也可以選擇提供`examples`陣列，以便在您要顯示手動輸入資料之使用者的範例日期時間字串時運用。

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

[!UICONTROL 陣列]欄位由`type: array`和`items`物件表示，該物件定義陣列將接受的專案結構描述。

您可以使用基本型別（例如字串陣列）來定義陣列專案：

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

您也可以透過`$ref`屬性參照資料型別的`$id`，根據現有的資料型別定義陣列專案。 下列是[!UICONTROL 付款專案]物件的陣列：

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

[!UICONTROL 物件]欄位由`type: object`和定義結構描述欄位子屬性的`properties`物件表示。

在`properties`下定義的每個子欄位都可以使用任何基本值`type`來定義，或是透過指向相關資料型別`$id`的`$ref`屬性來參考現有的資料型別：

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

您也可以透過參考資料型別來定義整個物件，前提是相關資料型別本身定義為`type: object`：

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 地圖] {#map}

對應欄位基本上是[`object`型別的欄位](#object)，其索引鍵集不受限制。 如同物件，對應有`type`值`object`，但其`meta:xdmType`已明確設定為`map`。

對應&#x200B;**不得**&#x200B;定義任何屬性。 它&#x200B;**必須**&#x200B;定義單一`additionalProperties`結構描述以說明對應中包含的值型別（每個對應只能包含單一資料型別）。 `type`值必須是`string`或`integer`。

例如，具有字串型別值的對應欄位會定義如下：

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

如需建立自訂對應欄位的詳細資訊，請參閱下節。

### 建立自訂地圖型別 {#custom-maps}

為了在XDM中有效支援「類似對應」資料，物件可能會被設為`map`的`meta:xdmType`註釋，以明確表示物件應像金鑰集未受限制一樣受到管理。 擷取至對應欄位的資料必須使用字串鍵，而且只能使用字串或整數值（由`additionalProperties.type`決定）。

XDM對於此儲存提示的使用會設定下列限制：

* 對應型別必須屬於型別`object`。
* 對應型別不得有已定義的屬性（換言之，它們會定義「空白」物件）。
* 對應型別必須包含`additionalProperties.type`欄位，描述可能放置在對應中的值： `string`或`integer`。

請確定您只在絕對必要時才使用對應型別欄位，因為這些欄位具有下列效能缺陷：

* 來自[Adobe Experience Platform查詢服務](../../query-service/home.md)的回應時間，1億筆記錄會從3秒降低到10秒。
* 地圖必須少於16個索引鍵，否則可能會進一步降低。

Experience Platform使用者介面在擷取對應型別欄位索引鍵的方式上也有限制。 雖然物件型別欄位可以展開，但地圖會顯示為單一欄位。

## 後續步驟

本指南說明如何在API中定義不同的欄位型別。 如需如何格式化XDM欄位型別的詳細資訊，請參閱[XDM欄位型別限制](../schema/field-constraints.md)的指南。
