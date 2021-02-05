---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas;place context;placeContext;datatype；資料類型；
solution: Experience Platform
title: 置入上下文資料類型
topic: overview
description: 本文檔概述「置入上下文XDM」資料類型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---


# [!UICONTROL 置入] contextdata類型

[!UICONTROL 放] 置內容是標準的XDM資料類型，可描述觀察到的事件位置，包括興趣點資訊和地理座標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點互動]](./poi-interaction.md) | 說明興趣點(POI)互動的詳細資訊。 |
| `activePOIs` | [[!UICONTROL 興趣點詳細資料的陣列]](./poi-details.md) | 說明造成事件的POI。 |
| `geo` | [[!UICONTROL 地理]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | DateTime | [RFC 3339](https://tools.ietf.org/html/rfc3339)格式的時間戳，指示使用指定時區偏移的本地時間。 格式模式為`yyyy-MM-dd'T'HH:mm:ssXXX`（例如`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整數 | 當前本地時區距離`localTime`值的UTC偏移（以分鐘為單位）。 這應包括目前的DST偏移（如果適用）。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)