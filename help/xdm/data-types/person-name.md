---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;fullName;xdm:fullName;person name;name;datatype；資料類型；
solution: Experience Platform
title: 人員姓名資料類型
topic-legacy: overview
description: 本文檔概述了人員名稱XDM資料類型。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# [!UICONTROL Person name] 資料類型

[!UICONTROL Person name] 是一種標準的XDM資料類型，它描述了人員的全名。由於不同語言和文化中名稱結構的慣例差異很大，因此名稱應始終使用此資料類型建模。

此外，資料類型還提供一些可選屬性，這些屬性可用於只需要使用完整名稱片段（例如建立正式或非正式問候語）的情況。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 屬性 | 說明 |
| --- | --- |
| `courtesyTitle` | 人員職稱、榮譽稱號或問候語的縮寫（例如`Mr.`、`Miss.`或`Dr.`）。 |
| `firstName` | 名稱的第一段，其書寫順序最常用的名稱語言。 |
| `fullName` | 人員的全名，以最常用的文字順序排列。 |
| `lastName` | 名稱的最後一段，其書寫順序最常用的名稱語言。 |
| `middleName` | 名字和姓氏之間提供的中間名、替代名或其他名稱。 |
| `suffix` | 一組字母在人名後提供，以提供其他資訊（例如`Jr.`、`Sr.`、`M.D.`、`PhD`、`I`、`II`、`III`等）。 |

有關人員名稱資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)
