---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；模式註冊；模式註冊；相容性；相容性模式；相容性模式；欄位類型；欄位類型；
solution: Experience Platform
title: 方案註冊表API指南附錄
description: 本文檔提供與使用方案註冊表API有關的補充資訊。
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: dcfdc9c479e8a77296f7cb0bf9f5bb36e9261b75
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 方案註冊表API指南附錄

本檔案提供與使用[!DNL Schema Registry] API相關的補充資訊。

## 使用查詢參數 {#query}

[!DNL Schema Registry]支援在列出資源時，使用查詢參數來篩選結果至頁面。

>[!NOTE]
>
>組合多個查詢參數時，必須以&amp;符號(`&`)分隔。

### 分頁 {#paging}

最常用於分頁的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `start` | 指定列出的結果的開始位置。 此值可從清單回應的`_page.next`屬性中取得，並用於存取下一頁結果。 如果`_page.next`值為null，則沒有其他頁面可用。 |
| `limit` | 限制傳回的資源數。 範例：`limit=5`將會傳回5個資源的清單。 |
| `orderby` | 依特定屬性排序結果。 範例：`orderby=title`將依標題以升序排序結果(A-Z)。 在參數值(`orderby=-title`)之前新增`-`，將依標題以遞減順序(Z-A)排序項目。 |

### 篩選 {#filtering}

您可以使用`property`參數來篩選結果，此參數可用來針對擷取的資源內的指定JSON屬性套用特定運算子。 支援的運算子包括：

| 運算元 | 說明 | 範例 |
| --- | --- | --- |
| `==` | 依屬性是否等於提供的值來篩選。 | `property=title==test` |
| `!=` | 依屬性是否不等於提供的值來篩選。 | `property=title!=test` |
| `<` | 依屬性是否小於提供的值來篩選。 | `property=version<5` |
| `>` | 依屬性是否大於提供的值來篩選。 | `property=version>5` |
| `<=` | 依屬性是否小於或等於提供的值來篩選。 | `property=version<=5` |
| `>=` | 依屬性大於或等於提供的值來篩選。 | `property=version>=5` |
| `~` | 依屬性是否與提供的規則運算式相符來篩選。 | `property=title~test$` |
| (None) | 僅聲明屬性名稱僅返回存在屬性的條目。 | `property=title` |

>[!TIP]
>
>您可以使用`property`參數，按照其相容類來過濾模式欄位組。 例如，`property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`僅返回與[!DNL XDM Individual Profile]類相容的欄位組。

## 相容模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是公開記載的規格，由Adobe所推動，以改善數位體驗的互用性、表現性和強大性。Adobe在GitHub](https://github.com/adobe/xdm/)上的[開放原始碼專案中維護原始碼和正式的XDM定義。 這些定義是以XDM標準記法撰寫，使用JSON-LD（連結資料的JavaScript物件記法）和JSON結構描述作為定義XDM結構描述的語法。

在公共儲存庫中查看正式的XDM定義時，您可以看到標準XDM與您在Adobe Experience Platform看到的不同。 您在[!DNL Experience Platform]中看到的內容稱為相容模式，它提供了標準XDM與在[!DNL Platform]中使用方式之間的簡單映射。

### 相容性模式的運作方式

相容性模式可讓XDM JSON-LD模型變更標準XDM中的值，並維持相同的語義，以便與現有的資料基礎架構搭配運作。 它使用巢狀JSON結構，以樹狀格式顯示結構。

在標準XDM和相容性模式之間，您會注意到的主要區別是刪除欄位名稱的&quot;xdm:&quot;前置詞。

以下是並排比較，顯示標準XDM和相容性模式中與生日相關的欄位（已移除「說明」屬性）。 請注意，「相容性模式」欄位在「meta:xdmField」和「meta:xdmType」屬性中包含對XDM欄位及其資料類型的參考。

<table>
  <th>標準XDM</th>
  <th>相容模式</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate":{
              「標題」:"出生日期",
              「類型」:"字串",
              「格式」:「日期」,
          },
          "xdm:phirthDayAndMonth":{
              「標題」:"出生日期",
              「類型」:"字串",
              「模式」:"[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:parthYear":{
              「標題」:"出生年"
              「類型」:"integer",
              「最小」:1,
              「最大值」:郵編：32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "birthDate":{
              「標題」:"出生日期",
              「類型」:"字串",
              「格式」:「日期」,
              "meta:xdmField":"xdm:birthDate",
              "meta:xdmType":"日期"
          },
          "brithDayAndMonth":{
              「標題」:"出生日期",
              「類型」:"字串",
              「模式」:"[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField":"xdm:phortyDayAndMonth",
              "meta:xdmType":"字串"
          },
          "pristorYear":{
              「標題」:"出生年"
              「類型」:"integer",
              「最小」:1,
              「最大值」:32767,
              "meta:xdmField":"xdm:parthYear",
              "meta:xdmType":"short"
        }
      </pre>
  </td>
  </tr>
</table>

### 為什麼需要相容模式？

Adobe Experience Platform的設計是與多種解決方案和服務搭配使用，每種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊特性）。 為了克服這些限制，開發了相容模式。

大多數[!DNL Experience Platform]服務（包括[!DNL Catalog]、[!DNL Data Lake]和[!DNL Real-time Customer Profile]）都使用[!DNL Compatibility Mode]代替標準XDM。 [!DNL Schema Registry] API也使用[!DNL Compatibility Mode]，本文中的範例都使用[!DNL Compatibility Mode]顯示。

值得知道的是，標準XDM與[!DNL Experience Platform]中操作方式之間發生了映射，但不應影響您對[!DNL Platform]服務的使用。

開放原始碼專案可供您使用，但是在透過[!DNL Schema Registry]與資源互動時，本檔案中的API範例提供您應瞭解和遵循的最佳實務。
