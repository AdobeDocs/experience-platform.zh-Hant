---
keywords: Experience Platform；首頁；熱門主題；方案；方案；欄位組；欄位組；欄位組；資料類型；資料類型；資料類型；方案設計；資料類型；資料類型；資料類型；資料類型；資料類型；資料類型；方案；方案；方案；方案；方案；方案；方案；方案；方案；映射；
solution: Experience Platform
title: XDM欄位類型限制
description: Experience Data Model(XDM)中欄位類型限制的參考，包括可對應的其他序列化格式，以及如何在API中定義您自己的欄位類型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 4%

---

# XDM欄位類型限制

在Experience Data Model(XDM)結構中，欄位的類型會限制欄位可包含的資料類型。 本檔案概略介紹每個核心欄位類型，包括可對應的其他序列化格式，以及如何在API中定義您自己的欄位類型，以強制執行不同的限制。

## 快速入門

使用本指南之前，請先檢閱 [綱要構成基本知識](./composition.md) XDM結構、類別和結構欄位群組的簡介。

如果您打算在API中定義自己的欄位類型，強烈建議您從 [Schema Registry開發人員指南](../api/getting-started.md) 了解如何建立欄位群組和資料類型，以在中納入自訂欄位。 如果您是使用Experience PlatformUI來建立結構，請參閱 [定義UI中的欄位](../ui/fields/overview.md) 了解如何對您在自訂欄位群組和資料類型中定義的欄位實施限制。

## 基礎結構與範例 {#basic-types}

XDM是以JSON結構描述為基礎而建置，因此XDM欄位在定義其類型時會繼承類似的語法。 了解JSON結構描述中不同欄位類型的呈現方式，有助於指出每種類型的基本限制。

>[!NOTE]
>
>請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-schema) 如需Platform API中JSON結構描述和其他基礎技術的詳細資訊。

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
{ "type":"integer", "maximum":9007199254740991，「最低」：-9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL整數]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer", "maximum":2147483648，「最低」：-2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL簡稱]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer", "maximum":32768，「最低」：-32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL位元組]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer", "maximum":128，「最低」：-128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"string", "format":"date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"string", "format":"date-time" }</pre>
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

**所有日期格式字串都必須符合ISO 8601標準([RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6))。*

## 將XDM類型對應至其他格式

以下各節說明各種XDM類型如何對應至其他常見序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Aerospike和Protobuf 2](#mongo)

>[!NOTE]
>
>在下表所列的標準XDM類型中， [!UICONTROL 地圖] 也包含類型。 當資料以對應至特定值的索引鍵來表示，或當索引鍵無法合理納入靜態架構且必須視為資料值時，標準架構中會使用地圖。
>
>許多標準XDM元件都使用對應類型，您也可以 [定義自訂地圖欄位](../tutorials/custom-fields-api.md#custom-maps) 如果需要。 如果現有資料目前是以下列任何格式儲存，下表中包含的對應類型可協助您判斷如何將現有資料對應至XDM。

### Parquet、Spark SQL和Java {#parquet}

| XDM類型 | 鑲木 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | 類型： `BYTE_ARRAY`<br>注釋： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 雙倍] | 類型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 長] | 類型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整數] | 類型： `INT32`<br>注釋： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 簡短] | 類型： `INT32`<br>注釋： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 位元組] | 類型： `INT32`<br>注釋： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 日期] | 類型： `INT32`<br>注釋： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 類型： `INT64`<br>注釋： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布林值] | 類型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地圖] | `MAP` — 注釋組<br><br>(`<key-type>` 必須 `STRING`) | `MapType`<br><br>(`keyType` 必須 `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

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

{style="table-layout:auto"}

## 在API中定義XDM欄位類型 {#define-fields}

Schema Registry API可讓您透過使用格式和選用限制來定義自訂欄位。 請參閱 [定義結構註冊表API中的自訂欄位](../tutorials/custom-fields-api.md) 以取得更多資訊。
