---
keywords: Experience Platform;home；熱門主題；模式；模式；混合；Mixin;Mixin;Mixins；資料類型；資料類型；資料類型；資料類型；模式設計；資料類型；資料類型；資料類型；資料類型；模式；模式；映射；映射；
solution: Experience Platform
title: XDM欄位類型約束
topic: 概述
description: Experience Data Model(XDM)中欄位類型限制的參考，包括其他可映射至的序列化格式，以及如何在API中定義您自己的欄位類型。
translation-type: tm+mt
source-git-commit: bb5880340ca4c01d0b25c7cb16fd422d3182a89e
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# XDM欄位類型約束

在Experience Data Model(XDM)架構中，欄位的類型會限制欄位可包含的資料類型。 本檔案提供每個核心欄位類型的概觀，包括其他可映射至的序列化格式，以及如何在API中定義您自己的欄位類型，以執行不同的限制。

## 快速入門

在使用本指南之前，請先閱讀[架構構成的基本說明](./composition.md)，以瞭解XDM架構、類和混合的簡介。

如果您打算在API中定義自己的欄位類型，強烈建議您從[方案註冊表開發人員指南](../api/getting-started.md)開始，以瞭解如何建立混合和資料類型以包含您的自訂欄位。 如果您使用Experience PlatformUI來建立結構，請參閱UI](../ui/fields/overview.md)中[定義欄位的指南，瞭解如何對自訂混合和資料類型中定義的欄位實施限制。

## 基本結構與範例

XDM建立在JSON結構描述之上，因此，在定義其類型時，XDM欄位會繼承類似的語法。 瞭解JSON結構描述中不同欄位類型的表示方式，有助於指出每種類型的基本限制。

>[!NOTE]
>
>如需平台API中JSON結構描述和其他基礎技術的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-schema)。

下表概述JSON結構描述中每個XDM類型的表示方式，以及符合該類型的範例值：

<table>
  <thead>
    <tr>
      <th>XDM類型</th>
      <th>JSON結構描述</th>
      <th>範例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONCONTROL字串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"字串"}</pre>
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
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  「類型」:"integer",
  「最大值」:9007199254740991,
  「最小」:-9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONCONTROL整數]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  「類型」:"integer",
  「最大值」:2147483648,
  「最小」:-2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL簡寫]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  「類型」:"integer",
  「最大值」:32768,
  「最小」:-32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONCONTROL位元組]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  「類型」:"integer",
  「最大值」:128,
  「最小」:-128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONCONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  「類型」:"字串",
  「格式」:"日期"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONCONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  「類型」:"字串",
  「格式」:"日期——時間"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONCONTROL布爾值]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"字串"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式化字串都必須符合ISO 8601標準（[RFC 3339, 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節）。*

## 將XDM類型映射到其他格式

以下各節說明每個XDM類型如何對應至其他常用的序列化格式：

* [Parce、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Aerospike和Protobuf 2](#mongo)

>[!IMPORTANT]
>
>在下表中列出的標準XDM類型中，還包括[!UICONTROL Map]類型。 當資料表示為對應至特定值的索引鍵，或當索引鍵無法合理地包含在靜態架構中且必須視為資料值時，標準架構中會使用地圖。
>
>映射類型欄位保留給行業和供應商模式使用，因此不能用於您定義的自定義資源。 映射類型包含在下表中僅用於幫助您確定如何將現有資料映射到XDM（如果當前資料以下列任何格式儲存）。

### Parce、Spark SQL和Java {#parquet}

| XDM類型 | 鑲木 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | 類型：`BYTE_ARRAY`<br>注釋：`UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | 類型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | 類型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | 類型：`INT32`<br>注釋：`INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | 類型：`INT32`<br>注釋：`INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | 類型：`INT32`<br>注釋：`INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | 類型：`INT32`<br>注釋：`DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 類型：`INT64`<br>注釋：`TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | 類型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` 必須 `STRING`) | `MapType`<br><br>(`keyType` 必須 `StringType`) | `java.util.Map` |

### Scala、.NET和CosmosDB {#scala}

| XDM類型 | 斯卡拉 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (不適用) | `object` |

### MongoDB、Aerospike和Protobuf 2 {#mongo}

| XDM類型 | MongoDB | 塞式飛行器 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>（0/1二進位） | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

## 在API {#define-fields}中定義XDM欄位類型

所有XDM欄位都是使用適用於其欄位類型的標準[JSON結構描述](https://json-schema.org/)限制來定義，並加上[!DNL Experience Platform]所強制之欄位名稱的其他限制。 方案註冊表API允許您通過使用格式和可選約束來定義其他欄位類型。 XDM欄位類型由欄位級屬性`meta:xdmType`公開。

>[!NOTE]
>
>`meta:xdmType` 是系統產生的值，因此使用API時，您不需要將此屬性新增至欄位的JSON。最佳實務是使用JSON結構描述類型（例如`string`和`integer`），並依下表所定義的適當最小／最大限制。

下表概述了定義不同欄位類型（包括具有可選屬性的欄位類型）的適當格式。 有關可選屬性和類型特定關鍵字的詳細資訊，請參閱[JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/type.html)。

若要開始，請尋找所需的欄位類型，並使用提供的范常式式碼來建立您的API要求，以建立[混合](../api/mixins.md#create)或[建立資料類型](../api/data-types.md#create)。

<table style="table-layout:auto">
  <tr>
    <th>XDM類型</th>
    <th>可選屬性</th>
    <th>範例</th>
  </tr>
  <tr>
    <td>[!UICONCONTROL字串]</td>
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
    「類型」:"字串",
    「模式」:"^[A-Z]{2}$",
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
  「類型」:"字串",
  「格式」:"uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL枚舉]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>約束枚舉值在<code>enum</code>陣列下提供，而每個值的可選面向客戶的標籤可在<code>meta:enum</code>下提供：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"字串",
  「列舉」:[ ]
      "value1"、
      "value2",
      "value3"
  ] 、
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
    <td>[!UICONCONTROL編號]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"數字"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"integer",
  「最小」:-9007199254740992,
  「最大值」:9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL整數]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"integer",
  「最小」:-2147483648,
  「最大值」:2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL簡寫]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"integer",
  「最小」:-32768,
  「最大值」:郵編：32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL位元組]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"integer",
  「最小」:-128,
  「最大值」:128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL布爾值]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"布林值",
  "default":false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL日期]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"字串",
  「格式」:「日期」,
  「範例」:["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"字串",
  「格式」:「日期時間」、
  「範例」:["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL陣列]</td>
    <td></td>
    <td>基本標量類型的陣列（例如字串）:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"array"、
  「項目」:{
    「類型」:"字串"
  }
}</pre>
      由另一個方案定義的對象陣列：<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"array"、
  「項目」:{
    「$ref」:"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL對象]</td>
    <td></td>
    <td>在<code>properties</code>下定義的每個子欄位的<code>type</code>屬性可以使用任何標量類型來定義：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"object",
  「屬性」:{
    "field1":{
      「類型」:"字串"
    },
    "field2":{
      「類型」:"數字"
    }
  }
}</pre>
      對象類型欄位可通過引用資料類型的<code>$id</code>來定義：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"object",
  「$ref」:"https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONCONTROL映射]</td>
    <td></td>
    <td>映射<strong>不能</strong>定義任何屬性。 它<strong>必須</strong>定義單個<code>additionalProperties</code>模式，以說明映射中包含的值類型（每個映射只能包含單一資料類型）。 值可以是任何有效的XDM <code>type</code>屬性，或是使用<code>$ref</code>屬性對其他模式的引用。<br/><br/>具有字串類型值的映射欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"object",
  "additionalProperties":{
    「類型」:"字串"
  }
}</pre>
    包含陣列字串的值映射欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"object",
  "additionalProperties":{
    「類型」:"array"、
    「項目」:{
      「類型」:"字串"
    }
  }
}</pre>
    引用其他資料類型的映射欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  「類型」:"object",
  "additionalProperties":{
    「$ref」:"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
