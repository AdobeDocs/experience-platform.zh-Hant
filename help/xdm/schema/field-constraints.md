---
keywords: Experience Platform；首頁；熱門主題；方案；方案；欄位組；欄位組；欄位組；資料類型；資料類型；資料類型；方案設計；資料類型；資料類型；資料類型；資料類型；資料類型；資料類型；方案；方案；方案；方案；方案；方案；方案；方案；方案；映射；
solution: Experience Platform
title: XDM欄位類型限制
topic-legacy: overview
description: Experience Data Model(XDM)中欄位類型限制的參考，包括可對應的其他序列化格式，以及如何在API中定義您自己的欄位類型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 61025ada3a900a5bd7682e3bb7d4f6cd23347231
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 3%

---

# XDM欄位類型限制

在Experience Data Model(XDM)結構中，欄位的類型會限制欄位可包含的資料類型。 本檔案概略介紹每個核心欄位類型，包括可對應的其他序列化格式，以及如何在API中定義您自己的欄位類型，以強制執行不同的限制。

## 快速入門

使用本指南之前，請先檢閱[架構組合基本介紹](./composition.md)，以了解XDM架構、類別和架構欄位群組的簡介。

如果您打算在API中定義自己的欄位類型，強烈建議您從[Schema Registry開發人員指南](../api/getting-started.md)開始，了解如何建立欄位群組和資料類型，將您的自訂欄位納入。 如果您使用Experience PlatformUI來建立結構，請參閱UI](../ui/fields/overview.md)中[定義欄位的指南，了解如何對您在自訂欄位群組和資料類型中定義的欄位實施限制。

## 基礎結構與範例

XDM是以JSON結構描述為基礎而建置，因此XDM欄位在定義其類型時會繼承類似的語法。 了解JSON結構描述中不同欄位類型的呈現方式，有助於指出每種類型的基本限制。

>[!NOTE]
>
>如需Platform API中JSON結構描述和其他基礎技術的詳細資訊，請參閱[ API基礎指南](../../landing/api-fundamentals.md#json-schema)。

下表概述每個XDM類型在JSON結構描述中的表示方式，以及符合類型的範例值：

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM類型</th>
      <th>JSON結構</th>
      <th>範例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL字串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL長]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":9007199254740991,
  「最小」：-9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL整數]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":2147483648,
  「最小」：-2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL簡稱]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":32768,
  「最小」：-32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL位元組]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":128,
  「最小」：-128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"string",
  "format":"date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"string",
  "format":"date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL布林值]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式化字串必須符合ISO 8601標準（[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節）。*

## 將XDM類型對應至其他格式

以下各節說明各種XDM類型如何對應至其他常見序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Aerospike和Protobuf 2](#mongo)

>[!IMPORTANT]
>
>在下表所列的標準XDM類型中，也包含[!UICONTROL Map]類型。 當資料以對應至特定值的索引鍵來表示，或當索引鍵無法合理納入靜態架構且必須視為資料值時，標準架構中會使用地圖。
>
>地圖類型欄位保留供業界和廠商結構使用，因此無法用於您定義的自訂資源。 如果現有資料目前是以下列任何格式儲存，下表中包含的對應類型僅能協助您判斷如何將現有資料對應至XDM。

### Parquet、Spark SQL和Java {#parquet}

| XDM類型 | 鑲木 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | 類型：`BYTE_ARRAY`<br>注釋：`UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 雙倍] | 類型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 長] | 類型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整數] | 類型：`INT32`<br>注釋：`INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 簡短] | 類型：`INT32`<br>注釋：`INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 位元組] | 類型：`INT32`<br>注釋：`INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | 類型：`INT32`<br>注釋：`DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 類型：`INT64`<br>注釋：`TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布林值] | 類型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地圖] | `MAP` — 注釋組<br><br>(`<key-type>` 必須 `STRING`) | `MapType`<br><br>(`keyType` 必須 `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala、.NET和CosmosDB {#scala}

| XDM類型 | 斯卡拉 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | `String` | `System.String` | `String` |
| [!UICONTROL 雙倍] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 長] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 整數] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 簡短] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 位元組] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 日期] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 布林值] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 地圖] | `Map` | (不適用) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB、Aerospike和Protobuf 2 {#mongo}

| XDM類型 | MongoDB | 塞普克 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | `string` | `String` | `string` |
| [!UICONTROL 雙倍] | `double` | `Double` | `double` |
| [!UICONTROL 長] | `long` | `Integer` | `int64` |
| [!UICONTROL 整數] | `int` | `Integer` | `int32` |
| [!UICONTROL 簡短] | `int` | `Integer` | `int32` |
| [!UICONTROL 位元組] | `int` | `Integer` | `int32` |
| [!UICONTROL 日期] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 布林值] | `bool` | `Integer`<br>（0/1二進位） | `bool` |
| [!UICONTROL 地圖] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## 在API {#define-fields}中定義XDM欄位類型

所有XDM欄位都是使用套用至其欄位類型的標準[JSON結構](https://json-schema.org/)限制來定義，而欄位名稱的其他限制則由[!DNL Experience Platform]強制執行。 Schema Registry API可讓您透過使用格式和選用限制來定義其他欄位類型。 XDM欄位類型由欄位層級屬性`meta:xdmType`公開。

>[!NOTE]
>
>`meta:xdmType` 是系統產生的值，因此使用API時，您不需要將此屬性新增至欄位的JSON。最佳作法是使用JSON結構類型（例如`string`和`integer`）搭配下表所定義的適當最小/最大限制。

下表概述了定義不同欄位類型（包括具有可選屬性的類型）的適當格式。 有關可選屬性和類型特定關鍵字的詳細資訊，請參閱[JSON結構檔案](https://json-schema.org/understanding-json-schema/reference/type.html)。

若要開始，請尋找所需的欄位類型，並使用所提供的范常式式碼來建立[建立欄位群組](../api/field-groups.md#create)或[建立資料類型](../api/data-types.md#create)的API請求。

<table style="table-layout:auto">
  <tr>
    <th>XDM類型</th>
    <th>可選屬性</th>
    <th>範例</th>
  </tr>
  <tr>
    <td>[!UICONTROL字串]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
    "type":"string",
    "pattern":"^[A-Z]{2}$",
    "maxLength":2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "format":"uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL枚舉]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>約束的列舉值提供在<code>enum</code>陣列下，而每個值的可選客戶對應標籤可提供在<code>meta:enum</code>下：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "enum":[
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum":{
      "value1":"值1",
      "value2":"值2",
      "value3":"值3"
  },
  "default":"value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL編號]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL長]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  「最小」：-9007199254740992,
  "maximum":9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL整數]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  「最小」：-2147483648,
  "maximum":2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL簡稱]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  「最小」：-32768,
  "maximum":32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL位元組]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  「最小」：-128,
  "maximum":128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL布林值]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"boolean",
  "default":false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL日期]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "format":"date",
  "examples":["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "format":"date-time",
  "examples":["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL陣列]</td>
    <td></td>
    <td>基本標量類型的陣列（如字串）:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"array",
  "items":{
    "type":"string"
  }
}</pre>
      由另一個架構定義的對象陣列：<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"array",
  "items":{
    "$ref":"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL對象]</td>
    <td></td>
    <td>在<code>properties</code>下定義的每個子欄位的<code>type</code>屬性可使用任何標量類型來定義：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "properties":{
    "field1":{
      "type":"string"
    },
    "field2":{
      "type":"number"
    }
  }
}</pre>
      可通過引用資料類型的<code>$id</code>來定義對象類型欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "$ref":"https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL地圖]</td>
    <td></td>
    <td>映射<strong>不得</strong>定義任何屬性。 它<strong>必須</strong>定義單個<code>additionalProperties</code>架構，以說明映射中包含的值類型（每個映射只能包含單一資料類型）。 值可以是任何有效的XDM <code>type</code>屬性，或使用<code>$ref</code>屬性對其他架構的引用。<br/><br/>具有字串類型值的映射欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "type":"string"
  }
}</pre>
    值的字串陣列對應欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "type":"array",
    "items":{
      "type":"string"
    }
  }
}</pre>
    參考其他資料類型的對應欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "$ref":"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
