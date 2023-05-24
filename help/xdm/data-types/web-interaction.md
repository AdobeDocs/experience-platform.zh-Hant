---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；Schemas;Web交互；datatype;datatype；資料類型；
solution: Experience Platform
title: Web交互資料類型
description: 本文檔概述了Web交互體驗資料模型(XDM)資料類型。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# [!UICONTROL Web交互] 資料類型

[!UICONTROL Web交互] 是標準的體驗資料模型(XDM)資料類型，它描述了在完成初始頁面載入後發生在網頁上的交互的資訊。 它用於記錄富Web應用程式中不觸發新頁面載入(如單頁Web應用(SPA))的交互。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 度量]](./measure.md) | 跟蹤Web連結點擊的測量。 |
| `URL` | 字串 | 用於此Web交互的實際連結或URL。 |
| `name` | 字串 | 用於此Web連結的規範名稱。 這用於分類。 |
| `type` | 字串 | 連結類型。 此屬性必須等於以下枚舉值之一： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
