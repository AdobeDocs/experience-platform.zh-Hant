---
keywords: Experience Platform；主題；熱門主題；模式；模式；欄位組；欄位組；欄位組；欄位組；資料類型；資料類型；資料類型；資料類型；資料類型；資料類型；資料類型；資料類型；資料類型；模式；模式；模式；圖表；映射；
solution: Experience Platform
title: XDM欄位類型約束
description: 體驗資料模型(XDM)中欄位類型約束的引用，包括可以映射到的其它序列化格式以及如何在API中定義自己的欄位類型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 4%

---

# XDM欄位類型約束

在經驗資料模型(XDM)架構中，欄位的類型約束欄位可以包含的資料類型。 本文檔概述了每個核心欄位類型，包括可映射到的其他序列化格式以及如何在API中定義自己的欄位類型以強制實施不同的約束。

## 快速入門

使用本指南之前，請查看 [架構組合基礎](./composition.md) 介紹XDM架構、類和架構欄位組。

如果您計畫在API中定義自己的欄位類型，強烈建議您從 [架構註冊表開發人員指南](../api/getting-started.md) 瞭解如何建立域組和資料類型以在中包括自定義域。 如果使用Experience PlatformUI建立方案，請參閱上的指南 [定義UI中的欄位](../ui/fields/overview.md) 瞭解如何對自定義欄位組和資料類型中定義的欄位實施約束。

## 基本結構和示例 {#basic-types}

XDM構建在JSON架構之上，因此XDM欄位在定義其類型時繼承了類似的語法。 瞭解JSON架構中不同欄位類型的表示方式有助於指明每種類型的基本約束。

>[!NOTE]
>
>查看 [API基礎指南](../../landing/api-fundamentals.md#json-schema) 有關平台API中JSON架構和其他基礎技術的詳細資訊。

下表概述了如何在JSON架構中表示每個XDM類型，以及與該類型一致的示例值：

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM類型</th>
      <th>JSON架構</th>
      <th>範例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL字串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"（類型）:"字串"</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"（類型）:"數字"</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL長]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer","maximum":9007199254740991，「最低」：-9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL整數]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer","maximum":2147483648，「最低」：-2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL短]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer","maximum":32768，「最低」：-32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL位元組]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer","maximum":128，「最低」：-128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"string","format":"日期" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL日期時間]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"string","format":"日期時間" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL布爾]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"（類型）:"字串"</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式字串必須符合ISO 8601標準([RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6))。*

## 將XDM類型映射到其他格式

以下各節介紹了每種XDM類型如何映射到其他常用序列化格式：

* [Parke、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、塞式機和Protobuf 2](#mongo)

>[!NOTE]
>
>在下表中列出的標準XDM類型中， [!UICONTROL 地圖] 類型。 當資料被表示為映射到某些值的鍵時，或當鍵不能合理地包括在靜態方案中且必須被視為資料值時，映射在標準方案中使用。
>
>許多標準XDM元件使用映射類型，您還可以 [定義自定義映射欄位](../tutorials/custom-fields-api.md#custom-maps) 按鈕。 映射類型包含在下表中，旨在幫助您確定如果現有資料當前以下面列出的任何格式儲存，如何將其映射到XDM。

### Parke、Spark SQL和Java {#parquet}

| XDM類型 | 鑲木 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | 類型： `BYTE_ARRAY`<br>注釋： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 雙倍] | 類型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 龍] | 類型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整數] | 類型： `INT32`<br>注釋： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 短] | 類型： `INT32`<br>注釋： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 位元組] | 類型： `INT32`<br>注釋： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 日期] | 類型： `INT32`<br>注釋： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL 日期時間] | 類型： `INT64`<br>注釋： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布林值] | 類型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地圖] | `MAP` — 注釋組<br><br>(`<key-type>` 必須 `STRING`) | `MapType`<br><br>(`keyType` 必須 `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala、.NET和CosmosDB {#scala}

| XDM類型 | 斯卡拉 | .NET | 宇宙資料庫 |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | `String` | `System.String` | `String` |
| [!UICONTROL 雙倍] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 龍] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 整數] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 短] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 位元組] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 日期] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 日期時間] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 布林值] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 地圖] | `Map` | (不適用) | `object` |

{style="table-layout:auto"}

### MongoDB、塞式機和Protobuf 2 {#mongo}

| XDM類型 | 蒙戈DB | 塞式火箭 | 原武夫2 |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | `string` | `String` | `string` |
| [!UICONTROL 雙倍] | `double` | `Double` | `double` |
| [!UICONTROL 龍] | `long` | `Integer` | `int64` |
| [!UICONTROL 整數] | `int` | `Integer` | `int32` |
| [!UICONTROL 短] | `int` | `Integer` | `int32` |
| [!UICONTROL 位元組] | `int` | `Integer` | `int32` |
| [!UICONTROL 日期] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 日期時間] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 布林值] | `bool` | `Integer`<br>（0/1二進位） | `bool` |
| [!UICONTROL 地圖] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## 在API中定義XDM欄位類型 {#define-fields}

「方案註冊表API」允許您通過使用格式和可選約束來定義自定義欄位。 請參閱上的指南 [定義架構註冊表API中的自定義欄位](../tutorials/custom-fields-api.md) 的子菜單。
