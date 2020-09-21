---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: 架構註冊開發人員附錄
description: 本文檔提供與使用方案註冊表API有關的補充資訊。
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 附錄

本檔案提供與使用 [!DNL Schema Registry] API相關的補充資訊。

## 相容模式

[!DNL Experience Data Model] (XDM)是公開記載的規格，由Adobe推動，以改善數位體驗的互用性、表現力和力量。 Adobe在GitHub上的開放原始碼專案中維護原始碼 [和正式的XDM定義](https://github.com/adobe/xdm/)。 這些定義是以XDM標準記法撰寫，使用JSON-LD（連結資料的JavaScript物件記法）和JSON結構描述作為定義XDM結構描述的語法。

在公共資料庫中查看正式的XDM定義時，您可以看到標準XDM與您在Adobe Experience Platform中看到的不同。 您在中看到的 [!DNL Experience Platform] 內容稱為相容性模式，它提供了標準XDM和其使用方式之間的簡單映射 [!DNL Platform]。

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
        { "xdm:borthDate":{ "title":「出生日期」、「類型」:"string", "format":"date", }, "xdm:birthDayAndMonth":{ "title":「出生日期」、「類型」:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", }, "xdm:borthYear":{ "title":「出生年」、「類型」:"integer", "minimum":1, "maximum":32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "borthDate":{ "title":「出生日期」、「類型」:"string", "format":"date"、"meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":「出生日期」、「類型」:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", "meta:xdmField":"xdm:birthDayAndMonth", "meta:xdmType":"string" }, "borthYear":{ "title":「出生年」、「類型」:"integer", "minimum":1, "maximum":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 為什麼需要相容模式？

Adobe Experience Platform可搭配多種解決方案和服務運作，每種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊特徵）。 為了克服這些限制，開發了相容模式。

大部 [!DNL Experience Platform] 分服務 [!DNL Catalog]，包括 [!DNL Data Lake]、使用和 [!DNL Real-time Customer Profile] 取代 [!DNL Compatibility Mode] 標準XDM。 此 [!DNL Schema Registry] API也使用 [!DNL Compatibility Mode]，而本文中的範例都使用 [!DNL Compatibility Mode]。

值得知道的是，標準XDM和其操作方式之間會進行映射 [!DNL Experience Platform]，但不應影響您的服務使 [!DNL Platform] 用。

開放原始碼專案可供您使用，但是在透過與資源互動時 [!DNL Schema Registry]，本檔案中的API範例提供您應瞭解和遵循的最佳實務。