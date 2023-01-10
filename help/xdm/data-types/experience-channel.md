---
keywords: Experience Platform；首頁；熱門主題；方案；方案； XDM；欄位；方案；方案；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: 體驗管道資料類型
description: 本檔案概述Experience Channel Experience Data Model(XDM)資料類型。
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# [!UICONTROL 體驗管道] 資料類型

[!UICONTROL 體驗管道] 是描述體驗管道的標準Experience Data Model(XDM)資料類型。 體驗管道代表如何使用數位體驗的方法或路徑。

有多個體驗管道，每個管道對內容的傳遞方式、觀察客戶互動的方式以及收集資料的方式都有不同的限制。 在通道內，體驗可以傳遞至特定位置。 管道中存在的位置和類型因管道而異。

![](../images/data-types/experience-channel.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | 字串 | 可唯一識別管道的ID。 每個特定體驗管道會定義常數 `@id`. |
| `_type` | 字串 | 為具有類似屬性的管道提供粗略分類標籤。 |
| `contentTypes` | 字串陣列 | 此管道可傳送的內容類型。 |
| `locationTypes` | 字串陣列 | 此頻道包含且可傳送內容的位置類型（虛擬位置）。 |
| `mediaAction` | 字串 | 說明體驗事件媒體動作（若適用）。 |
| `mediaType` | 字串 | 說明媒體類型是付費、擁有還是獲得。 |
| `metricTypes` | 字串陣列 | 可在此管道收集的量度。 |
| `mode` | 字串 | 體驗在此管道中的傳遞方式。 |
| `typeAtSource` | 字串 | 管道的自訂名稱。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
