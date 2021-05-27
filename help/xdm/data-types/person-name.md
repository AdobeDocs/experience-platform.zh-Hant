---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；完整名稱；xdm:fullName；人員名稱；資料類型；資料類型；
solution: Experience Platform
title: 人員名稱資料類型
topic-legacy: overview
description: 本檔案概述人員名稱XDM資料類型。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# [!UICONTROL 人員] 名稱資料類型

[!UICONTROL 人] 員名稱是標準XDM資料類型，可說明人員的完整名稱。由於名稱結構的慣例在不同語言和文化之間差異很大，因此應始終使用此資料類型來建模名稱。

此外，資料類型還提供了一些可選屬性，可用於僅使用全名片段的情況，例如建立正式問候語或非正式問候語。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 屬性 | 說明 |
| --- | --- |
| `courtesyTitle` | 人員標題、榮譽或稱呼的縮寫（例如`Mr.`、`Miss.`或`Dr.`）。 |
| `firstName` | 以書寫順序排列的名稱的第一段，最常以名稱的語言接受。 |
| `fullName` | 人的全名，以最常用的文字書寫順序。 |
| `lastName` | 以書寫順序排列的名稱的最後一段，最常以名稱的語言接受。 |
| `middleName` | 名字和姓氏之間提供的中間、替代或其他名稱。 |
| `suffix` | 在人名後提供的一組字母，用於提供其他資訊（如`Jr.`、`Sr.`、`M.D.`、`PhD`、`I`、`II`、`III`等）。 |

{style=&quot;table-layout:auto&quot;}

如需人員名稱資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)
