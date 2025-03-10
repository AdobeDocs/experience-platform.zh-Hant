---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；網頁互動；資料型別；資料型別；
solution: Experience Platform
title: 網路互動資料型別
description: 瞭解網路互動Experience Data Model (XDM)資料型別。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---

# [!UICONTROL 網頁互動]資料型別

[!UICONTROL 網頁互動]是標準的Experience Data Model (XDM)資料型別，描述初次頁面載入完成後發生在網頁上的互動資訊。 它可用來記錄豐富網頁應用程式(例如單頁網頁應用程式(SPA))中的互動，而不會觸發新的頁面載入。

![網頁互動影像](../images/data-types/web-interaction.PNG){width=500}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 量值]](./measure.md) | 追蹤網頁連結點選的測量。 |
| `URL` | 字串 | 用於此網路互動的實際連結或 URL。 |
| `name` | 字串 | 用於此網頁連結的規範名稱。 這用於分類目的。 |
| `type` | 字串 | 連結型別。 此屬性必須等於下列其中一個列舉值： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
