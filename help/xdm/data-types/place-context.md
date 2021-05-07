---
keywords: Experience Platform;home；常用主題；模式；模式；XDM;fields;schemas;Schemas;place context;placeContext;datatype；資料類型；
solution: Experience Platform
title: 置入上下文資料類型
topic-legacy: overview
description: 本文檔概述「置入上下文XDM」資料類型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 4%

---

# [!UICONTROL Place context] 資料類型

[!UICONTROL Place context] 是標準的XDM資料類型，可描述所觀察到事件的位置，包括興趣點資訊和地理座標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | 說明興趣點(POI)互動的詳細資訊。 |
| `activePOIs` | [[!UICONTROL Point of interest details]](./poi-details.md)陣列 | 說明造成事件的POI。 |
| `geo` | [[!UICONTROL Geo]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | DateTime | [RFC 3339](https://tools.ietf.org/html/rfc3339)格式的時間戳，指示使用指定時區偏移的本地時間。 格式模式為`yyyy-MM-dd'T'HH:mm:ssXXX`（例如`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整數 | 當前本地時區距離`localTime`值的UTC偏移（以分鐘為單位）。 這應包括目前的DST偏移（如果適用）。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
