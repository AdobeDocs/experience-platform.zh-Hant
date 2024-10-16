---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；欄位群組；欄位群組；欄位群組；資料型別；資料型別；資料型別；結構描述設計；資料型別；資料型別；資料型別；結構描述；結構描述；結構描述設計；結構描述設計；對應；對應；
solution: Experience Platform
title: XDM欄位型別限制
description: Experience Data Model (XDM)中欄位型別限制的參考，包括它們可以對應的其他序列化格式，以及如何在API中定義您自己的欄位型別。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: eb1cf204e95591082b27dc97cd3c709a23b20b08
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# XDM欄位型別限制

在Experience Data Model (XDM)結構描述中，欄位的型別會限制欄位可包含哪種資料。 本檔案提供每種核心欄位型別的概觀，包括可對應的其他序列化格式，以及如何在API中定義自己的欄位型別，以強制實施不同的限制。

## 快速入門

使用本指南之前，請先檢閱結構描述組合的[基本知識](./composition.md)，以瞭解XDM結構描述、類別和結構描述欄位群組的簡介。

如果您打算在API中定義自己的欄位型別，強烈建議您從[Schema Registry開發人員指南](../api/getting-started.md)開始，瞭解如何建立欄位群組和資料型別，以包含您的自訂欄位。 如果您使用Experience PlatformUI建立結構描述，請參閱[在UI中定義欄位的指南](../ui/fields/overview.md)，以瞭解如何在自訂欄位群組和資料型別中定義的欄位上實作限制。

## 基底結構和範例 {#basic-types}

XDM是以JSON結構描述為基礎建立，因此XDM欄位在定義其型別時繼承類似的語法。 瞭解不同的欄位型別在JSON結構描述中的呈現方式，有助於指出每種型別的基本限制。 自訂欄位名稱不區分大小寫，且在結構描述的相同層級上必須有不同的名稱。

>[!NOTE]
>
>請參閱[API基礎指南](../../landing/api-fundamentals.md#json-schema)，以取得有關JSON結構描述和Platform API中其他基礎技術的詳細資訊。

下表概述每個XDM型別在JSON結構描述中的呈現方式，以及與型別相容的範例值：

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM型別</th>
      <th>JSON結構描述</th>
      <th>範例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[！UICONTROL字串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL編號]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：9007199254740991，
  "minimum"： -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL整數]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：2147483648，
  "minimum"： -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：32768，
  "minimum"： -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL位元組]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：128，
  "minimum"： -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "string"，
  "format"： "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL日期時間]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "string"，
  "format"： "date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式字串都必須符合ISO 8601標準（[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節）。*

## 將XDM型別對應到其他格式

以下各節說明每個XDM型別如何對應至其他常見的序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Surospike和Protobuf 2](#mongo)

>[!NOTE]
>
>在下表列出的標準XDM型別中，[!UICONTROL 對應]型別也包括在內。 當資料以對應到特定值的索引鍵來表示，或索引鍵無法合理地包含在靜態結構描述中且必須被視為資料值時，標準結構描述會使用對應。
>
>許多標準XDM元件都使用對應型別，您也可以[定義自訂對應欄位](../tutorials/custom-fields-api.md#custom-maps) （如果需要）。 下表包含對應型別，其用意是協助您決定如何將現有資料對應至XDM （如果目前儲存在下列任何格式中）。

### Parquet、Spark SQL和Java {#parquet}

| XDM型別 | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | 型別： `BYTE_ARRAY`<br>註解： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 數字] | 類型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 長] | 類型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整數] | 型別： `INT32`<br>註解： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 短整數] | 型別： `INT32`<br>註解： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 位元組] | 型別： `INT32`<br>註解： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 日期] | 型別： `INT32`<br>註解： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL 日期時間] | 型別： `INT64`<br>註解： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布林值] | 類型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地圖] | `MAP` — 註解的群組<br><br>（`<key-type>`必須為`STRING`） | `MapType`<br><br>（`keyType`必須為`StringType`） | `java.util.Map` |

{style="table-layout:auto"}

### Scala、.NET和CosmosDB {#scala}

| XDM型別 | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | `String` | `System.String` | `String` |
| [!UICONTROL 數字] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 長] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 整數] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 短整數] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 位元組] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 日期] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 日期時間] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 布林值] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 地圖] | `Map` | （不適用） | `object` |

{style="table-layout:auto"}

### MongoDB、Surospike和Protobuf 2 {#mongo}

| XDM型別 | MongoDB | 尖峰 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL 字串] | `string` | `String` | `string` |
| [!UICONTROL 數字] | `double` | `Double` | `double` |
| [!UICONTROL 長] | `long` | `Integer` | `int64` |
| [!UICONTROL 整數] | `int` | `Integer` | `int32` |
| [!UICONTROL 短整數] | `int` | `Integer` | `int32` |
| [!UICONTROL 位元組] | `int` | `Integer` | `int32` |
| [!UICONTROL 日期] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 日期時間] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 布林值] | `bool` | `Integer`<br>（0/1二進位） | `bool` |
| [!UICONTROL 地圖] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## 在API中定義XDM欄位型別 {#define-fields}

Schema Registry API可讓您透過使用格式和選用限制來定義自訂欄位。 如需詳細資訊，請參閱[在結構描述登入API](../tutorials/custom-fields-api.md)中定義自訂欄位的指南。
