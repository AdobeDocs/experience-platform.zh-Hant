---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；位置內容；placeContext；資料類型；資料類型；
solution: Experience Platform
title: 放置上下文資料類型
topic-legacy: overview
description: 本檔案概述「放置內容XDM」資料類型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---

# [!UICONTROL 放置] contextdata類型

[!UICONTROL 放] 置內容是標準XDM資料類型，可說明觀察到事件的位置，包括地標資訊和地理座標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點互動]](./poi-interaction.md) | 說明地標(POI)互動的詳細資訊。 |
| `activePOIs` | [[!UICONTROL 地標詳細資料]](./poi-details.md)的陣列 | 說明造成事件的POI。 |
| `geo` | [[!UICONTROL 地理]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | DateTime | [RFC 3339](https://tools.ietf.org/html/rfc3339)格式的時間戳，用於指示與指定時區偏移一起使用的本地時間。 格式化模式為`yyyy-MM-dd'T'HH:mm:ssXXX`（例如`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整數 | `localTime`值的當前本地時區偏移（以分鐘為單位）距離UTC。 這應包括目前的DST偏移（如果適用）。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
