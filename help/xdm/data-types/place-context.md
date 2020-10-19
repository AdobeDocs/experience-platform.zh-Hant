---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: 置入上下文資料類型
topic: overview
description: 本文檔概述「置入上下文XDM」資料類型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---


# [!UICONTROL 置入上下文] ，資料類型

[!UICONTROL 置入上下文] (Place context)是一種標準的XDM資料類型，用於描述觀察到的事件的位置，包括興趣點資訊和地理坐標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點互動]](./poi-interaction.md) | 說明興趣點(POI)互動的詳細資訊。 |
| `activePOIs` | 興趣點 [[!UICONTROL 詳細資訊陣列]](./poi-details.md) | 說明造成事件的POI。 |
| `geo` | [[!UICONTROL 地理]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | DateTime | 以 [RFC 3339格式表示的時間戳](https://tools.ietf.org/html/rfc3339) ，用於指示本地時間和指定的時區偏移。 格式模式 `yyyy-MM-dd'T'HH:mm:ssXXX` 為(例如 `2001-07-04T12:08:56-07:00`)。 |
| `localTimezoneOffset` | 整數 | 當前本地時區與UTC的值偏移(以分鐘為單 `localTime` 位)。 這應包括目前的DST偏移（如果適用）。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)