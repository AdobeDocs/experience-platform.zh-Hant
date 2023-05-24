---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；完整名稱；xdm:fullName；人名；名稱；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 人員姓名資料類型
description: 此文檔概述了人員姓名XDM資料類型。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# [!UICONTROL 人員姓名] 資料類型

[!UICONTROL 人員姓名] 是描述人員全名的標準XDM資料類型。 由於不同語言和文化對名稱結構的約定差異很大，因此名稱應始終使用此資料類型建模。

此外，資料類型提供了許多可選屬性，這些屬性可用於僅使用全名片段的情況，例如建立正式問候語或非正式問候語。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 屬性 | 說明 |
| --- | --- |
| `courtesyTitle` | 人員標題、榮譽或稱呼(如 `Mr.`。 `Miss.`或 `Dr.`)。 |
| `firstName` | 該名稱的首段以書寫順序排列，最常以名稱的語言接受。 |
| `fullName` | 該人的全稱，按最常用名稱語言接受的書寫順序排列。 |
| `lastName` | 該名稱的最後一段是書寫順序，最常用的名稱語言。 |
| `middleName` | 名和姓氏之間提供的中間名、備用名或附加名。 |
| `suffix` | 在人員姓名後提供的一組信件以提供附加資訊(如 `Jr.`。 `Sr.`。 `M.D.`。 `PhD`。 `I`。 `II`。 `III`等)。 |

{style="table-layout:auto"}

有關人員姓名資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
