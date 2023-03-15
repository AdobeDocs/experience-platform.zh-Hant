---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；Web交互；資料類型；資料類型；
solution: Experience Platform
title: Web交互資料類型
description: 本檔案概略介紹Web互動Experience Data Model(XDM)資料類型。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# [!UICONTROL 網路互動] 資料類型

[!UICONTROL 網路互動] 是標準的Experience Data Model(XDM)資料類型，可說明初次頁面載入完成後網頁上發生的互動相關資訊。 其用途是記錄不會觸發新頁面載入(例如單頁網頁應用程式(SPA))的豐富網頁應用程式互動。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 測量]](./measure.md) | 追蹤網站連結點按的測量。 |
| `URL` | 字串 | 用於此Web交互的實際連結或URL。 |
| `name` | 字串 | 用於此Web連結的規範名稱。 這會用於分類用途。 |
| `type` | 字串 | 連結類型。 此屬性必須等於下列列舉值之一： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
