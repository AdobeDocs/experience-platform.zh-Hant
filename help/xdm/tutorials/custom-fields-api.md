---
title: 在架構註冊表API中定義XDM欄位
description: 瞭解如何在架構註冊表API中建立自定義體驗資料模型(XDM)資源時定義不同的欄位。
source-git-commit: af4c345819d3e293af4e888c9cabba6bd874583b
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# 在架構註冊表API中定義XDM欄位

所有體驗資料模型(XDM)欄位都使用標準 [JSON架構](https://json-schema.org/) 適用於其欄位類型的約束，以及Adobe Experience Platform強制實施的欄位名稱的附加約束。 使用方案註冊表API，您可以通過使用格式和可選約束來定義方案中的自定義欄位。 XDM欄位類型由欄位級屬性公開， `meta:xdmType`。

>[!NOTE]
>
>`meta:xdmType` 是系統生成的值，因此使用API時不需要將此屬性添加到欄位的JSON(除非 [建立自定義映射類型](#maps))。 最佳做法是使用JSON架構類型(如 `string` 和 `integer`)，具有下表中定義的相應最小/最大約束。

下表概述了用於定義不同欄位類型（包括具有可選屬性的欄位類型）的適當格式。 有關可選屬性和類型特定關鍵字的詳細資訊，請通過 [JSON架構文檔](https://json-schema.org/understanding-json-schema/reference/type.html)。

要開始，請查找所需的欄位類型，並使用提供的示例代碼生成API請求 [建立欄位組](../api/field-groups.md#create) 或 [建立資料類型](../api/data-types.md#create)。

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
"sampleField":{ "type":"string","pattern":"^[A-Z]{2}$","maxLength":2 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string","format":"uri" }</pre>
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
    <td>約束枚舉值提供在 <code>enum</code> 陣列，而每個值的面向客戶的可選標籤可在下面提供 <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string","enum":[ "value1"、"value2"、"value3" ]、"meta:enum:{ "value1":"值1"、"值2":"值2"、"值3":"值3" }, "default":"值1" }</pre>
    <br>請注意 <code>meta:enum</code> 值 <strong>不</strong> 聲明枚舉或自行驅動任何資料驗證。 在大多數情況下， <code>meta:enum</code> 也提供 <code>enum</code> 確保資料受到約束。 但是，有些使用情況 <code>meta:enum</code> 沒有相應的 <code>enum</code> 陣列。 請參閱上的教程 <a href="../tutorials/extend-soft-enum.md">延伸軟圓</a> 的子菜單。
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL編號]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"數字" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL長]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer","minimum":-9007199254740992，「maximum」（最大）:9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL整數]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer","minimum":-2147483648，「maximum」：2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL短]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer","minimum":-32768，「最大值」：32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL位元組]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer","minimum":-128，「最大值」：128 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL布爾]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"boolean","default":false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL日期]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string","format":"date"、"examples":["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string","format":"date-time"、"examples":[" 2004-10-23T12:00:00-06:00"]}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL陣列]</td>
    <td></td>
    <td>基本標量類型（如字串）的陣列：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"array","items":{ "type":"字串" }</pre>
      由另一方案定義的對象陣列：<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"array","items":{ "$ref":"https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL對象]</td>
    <td></td>
    <td>的 <code>type</code> 定義的每個子欄位的屬性 <code>properties</code> 可以使用任何標量類型定義：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object","properties":{ "field1":{ "type":"string" }, "field2":{ "type":"數字" } }</pre>
      通過引用 <code>$id</code> 資料類型：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object", "$ref":"https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL映射]</td>
    <td></td>
    <td>映射類型欄位實質上是具有不受約束的鍵集的對象類型欄位。 與對象一樣，地圖 <code>type</code> 值 <code>object</code>但是 <code>meta:xdmType</code> 已顯式設定為 <code>map</code>。<br><br>地圖 <strong>不能</strong> 定義任何屬性。 它 <strong>必須</strong> 定義單個 <code>additionalProperties</code> 模式，用於描述映射中包含的值的類型（每個映射只能包含單個資料類型）。 的 <code>type</code> 值必須為 <code>string</code> 或 <code>integer</code>。<br/><br/>具有字串類型值的映射欄位：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object"、"meta:xdmType":"map","additionalProperties":{ "type":"字串" }</pre>
    有關在XDM中建立自定義映射類型的詳細資訊，請參閱下節。
    </td>
  </tr>
</table>

## 建立自定義映射類型 {#maps}

為了在XDM中有效地支援「類地圖」資料，可以使用 `meta:xdmType` 設定為 `map` 以明確管理對象時，應將鍵集視為不受約束。 XDM對此儲存提示的使用設定了以下限制：

* 映射類型MUST為類型 `object`
* 映射類型不能定義屬性（換句話說，它們定義「空」對象）
* 映射類型必須包括單個 `additionalProperties` 描述可能放置在映射中的值的架構

確保在完全必要時僅使用映射類型欄位，因為這些欄位具有以下效能缺陷：

* 對於1億條記錄，Adobe Experience Platform查詢服務的響應時間從三秒縮短到十秒
* 地圖必須少於16個鍵，否則可能進一步降級

平台用戶介面在如何提取映射類型欄位的鍵方面也有局限性。 對象類型欄位可以展開，但映射將顯示為單個欄位。

## 後續步驟

本指南介紹如何在API中定義不同的欄位類型。 有關如何格式化XDM欄位類型的詳細資訊，請參見上的指南 [XDM欄位類型約束](../schema/field-constraints.md)。
