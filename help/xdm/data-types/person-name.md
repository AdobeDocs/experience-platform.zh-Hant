---
keywords: Experience Platform；首頁；熱門主題；結構描述；XDM；欄位；結構描述；結構描述；fullName；xdm：fullName；人員名稱；名稱；資料型別；資料型別；
solution: Experience Platform
title: 個人名稱資料型別
description: 瞭解人員名稱XDM資料型別。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# [!UICONTROL 個人名稱]資料型別

[!UICONTROL 人員名稱]是描述人員完整名稱的標準XDM資料型別。 由於不同語言和文化的名稱結構慣例差異極大，因此名稱應一律使用此資料型別建立模型。

此外，資料型別提供許多可選屬性，可用於只需要使用全名片段的狀況，例如建立正式或非正式的問候語。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 屬性 | 說明 |
| --- | --- |
| `courtesyTitle` | 個人職稱、敬語或稱呼語的縮寫（例如`Mr.`、`Miss.`或`Dr.`）。 |
| `firstName` | 在姓名的語言中最常被接受的書寫順序的第一個姓名區段。 |
| `fullName` | 以姓名的語言中最常被接受的書寫順序所表示的個人全名。 |
| `lastName` | 在姓名的語言中最常被接受的書寫順序的最後一個姓名區段。 |
| `middleName` | 名字與姓氏之間的中間名、備用名稱或附加名稱。 |
| `suffix` | 接在個人名稱后的一組字母，以提供其他資訊（例如`Jr.`、`Sr.`、`M.D.`、`PhD`、`I`、`II`、`III`等）。 |

{style="table-layout:auto"}

有關個人名稱資料型別的更多詳細資訊，請參閱公共XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
