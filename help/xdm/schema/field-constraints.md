---
keywords: Experience Platform;home；熱門主題；架構；Schema;Mixin;Mixin;Mixins；資料類型；資料類型；資料類型；資料類型；模式設計；資料類型；資料類型；資料類型；資料類型；資料類型；模式；架構；架構設計；映射；映射；
solution: Experience Platform
title: XDM欄位類型約束
topic: overview
description: XDM欄位類型限制的參考，包括可映射至的其他序列化格式，以及如何在API中定義您自己的欄位類型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 5%

---


# XDM欄位類型約束

您為方案選擇的XDM欄位類型會限制這些欄位可以包含的資料類型。 本檔案提供每個核心欄位類型的概觀，包括其他可映射至的序列化格式，以及如何在API中定義您自己的欄位類型，以執行不同的限制。

## 快速入門

在使用本指南之前，請先閱讀[架構構成的基本說明](./composition.md)，以瞭解XDM架構、類和混合的簡介。

如果您打算定義自己的欄位類型，強烈建議您從[方案註冊表開發人員指南](../api/getting-started.md)開始，以瞭解如何建立混合和資料類型以包含您的自訂欄位。

## 將XDM類型映射到其他格式

下表說明每個XDM類型(`meta:xdmType`)與其他序列化格式之間的映射。

| XDM類型<br>(meta:xdmType) | JSON<br>（JSON結構描述） | Parce<br>（文字／注釋） | [!DNL Spark] SQL | Java | 斯卡拉 | .NET | CosmosDB | MongoDB | 塞式飛行器 | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| 字串 | 類型：字串 | BYTE_ARRAY/UTF8 | StringType | java.lang.String | 字串 | System.String | 字串 | 字串 | 字串 | 字串 |
| 數字 | 類型：數字 | DOUBLE | DoubleType | java.lang.Double | 雙倍 | System.Double | 數字 | 雙倍 | 雙倍 | 雙倍 |
| long | type:integer<br>maximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | 長 | System.Int64 | 數字 | long | 整數 | int64 |
| int | type:integer<br>maximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | 數字 | int | 整數 | int32 |
| 短 | type:integer<br>maximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | 簡短 | System.Int16 | 數字 | int | 整數 | int32 |
| 位元組 | type:integer<br>maximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | 位元組 | System.SByte | 數字 | int | 整數 | int32 |
| 布林值 | 類型：布爾型 | 布林值 | BooleanType | java.lang.Boolean | 布林值 | System.Boolean | 布林值 | bool | 整數 | 整數 | bool |
| 日期 | type:string<br>format:date<br>（RFC 3339，第5.6節） | INT32/日期 | 日期類型 | java.util.Date | java.util.Date | System.DateTime | 字串 | 日期 | 整數<br>(unix millis) | int64<br>(unix millis) |
| 日期——時間 | type:string<br>format:date-time<br>（RFC 3339，第5.6節） | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | 字串 | timestamp | 整數<br>(unix millis) | int64<br>(unix millis) |
| 地圖 | 物件 | MAP注釋組<br><br>&lt;<span>key_type</span>必須是映射值的STRING<br><br><span>value_type</span>類型 | MapType<br><br>&quot;keyType&quot; MUST be StringType<br><br>&quot;valueType&quot;是映射值的類型。 | java.util.Map | 地圖 | — | 物件 | 物件 | 地圖 | map&lt;<span>key_type, value_type</span>> |

## 在API {#define-fields}中定義XDM欄位類型

XDM結構描述是使用[JSON結構描述](https://json-schema.org/)標準和基本欄位類型來定義的，並對[!DNL Experience Platform]所強制的欄位名稱加上其他限制。 [方案註冊表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)允許您通過使用格式和可選約束定義其他欄位類型。 XDM欄位類型由欄位級屬性`meta:xdmType`公開。

>[!NOTE]
>
>`meta:xdmType` 是系統產生的值，因此您不需要將此屬性新增至欄位的JSON。最佳實務是使用JSON結構描述類型（例如字串和整數），並依下表所定義的適當最小／最大限制。

下表概述了使用可選屬性定義標量欄位類型和更具體欄位類型的適當格式。 有關可選屬性和類型特定關鍵字的詳細資訊，請參閱[JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/type.html)。

若要開始，請尋找所需的欄位類型，並使用提供的范常式式碼來建立您的API要求，以建立[混合](../api/mixins.md#create)或[建立資料類型](../api/data-types.md#create)。

<table>
  <tr>
    <th>所需類型<br/>(meta:xdmType)</th>
    <th>JSON<br/>（JSON結構描述）</th>
    <th>程式碼範例</th>
  </tr>
  <tr>
    <td>字串</td>
    <td>類型：string<br/><br/><strong>Optional屬性：</strong><br/>
      <ul>
        <li>模式</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
            「類型」:"字串",
            「模式」:"^[A-Z]{2}$",
            "maxLength":2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>類型：string<br/>format:uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"字串",
          「格式」:"uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType:字串)</td>
    <td>類型：string<br/><br/><strong>Optional屬性：</strong><br/>
      <ul>
        <li>預設</li>
      </ul>
    </td>
    <td>使用「meta:enum」指定面向客戶的選項標籤：
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>數字</td>
    <td>類型：number<br/>minimum:最大值為±2.23×10^308<br/>:±1.80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"數字"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>類型：整數<br/>maximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"integer",
          「最小」:-9007199254740992,
          「最大值」:9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>類型：integer<br/>maximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"integer",
          「最小」:-2147483648,
          「最大值」:2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>短</td>
    <td>類型：integer<br/>maximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"integer",
          「最小」:-32768,
          「最大值」:郵編：32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>位元組</td>
    <td>類型：整數<br/>maximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"integer",
          「最小」:-128,
          「最大值」:128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>布林值</td>
    <td><br/>類型：boolean<br/>{true, false}<br/><br/><strong>可選屬性：</strong><br/>
      <ul>
        <li>預設</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"布林值",
          "default":false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>日期</td>
    <td>類型：string<br/>format:日期</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"字串",
          「格式」:「日期」,
          「範例」:["2004-10-23"]
        }
      </pre>
      由<a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6</a>節定義的日期，其中"full-date" = date-fullyear "-" date-month "-" date-mday(YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>日期——時間</td>
    <td>類型：string<br/>format:日期——時間</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"字串",
          「格式」:「日期時間」、
          「範例」:["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      日期——時間，由<a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6</a>節定義，其中"date-time" =全日期"T"全時：<br/>(YYYY-MM-DD'T'H:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>陣列</td>
    <td>類型：陣列</td>
    <td>items.type可使用任何標量類型定義：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"array"、
          「項目」:{
            「類型」:"字串"
          }
        }
      </pre>
      由另一個方案定義的對象陣列：<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"array"、
          「項目」:{
            「$ref」:"id"
          }
        }
      </pre>
      其中，「id」是參考架構的{id}。
    </td>
  </tr>
  <tr>
    <td>物件</td>
    <td>類型：物件</td>
    <td>屬性。{field}.type可使用任何標量類型來定義：
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
        }
      </pre>
      由引用方案定義的「對象」類型欄位：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"object",
          「$ref」:"id"
        }
      </pre>
      其中，「id」是參考架構的{id}。
    </td>
  </tr>
  <tr>
    <td>地圖</td>
    <td>類型：object<br/><br/><strong>注意：</strong><br/>使用'map'資料類型是專為業界和廠商架構使用而保留，不適用於租用戶定義欄位。 當資料表示為映射至某個值的索引鍵，或當索引鍵無法合理地包含在靜態架構中且必須視為資料值時，標準架構會使用它。</td>
    <td>'map'不能定義任何屬性。 它必須定義單個"[!UICONTROL additionalProperties]"模式，以說明'map'中包含的值類型。 XDM中的'map'只能包含單一資料類型。 值可以是任何有效的XDM模式定義，包括陣列或對象，或作為對其他模式的引用（通過$ref）。<br/><br/>值類型為'string'的映射欄位：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"object",
          "additionalProperties":{
            「類型」:"字串"
          }
        }
      </pre>
    值為字串陣列的映射欄位：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"object",
          "additionalProperties":{
            「類型」:"array"、
            「項目」:{
              「類型」:"字串"
            }
          }
        }
      </pre>
    引用其他方案的映射欄位：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          「類型」:"object",
          "additionalProperties":{
            「$ref」:"id"
          }
        }
      </pre>
      其中，「id」是參考架構的{id}。
    </td>
  </tr>
</table>
