---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；位置內容；placeContext；資料類型；資料類型；
solution: Experience Platform
title: 放置上下文資料類型
description: 本檔案概述「放置內容XDM」資料類型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 4%

---

# [!UICONTROL 放置內容] 資料類型

[!UICONTROL 放置內容] 是標準的XDM資料類型，可說明觀察到事件的位置，包括地標資訊和地理座標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點互動]](./poi-interaction.md) | 說明地標(POI)互動的詳細資訊。 |
| `activePOIs` | 陣列 [[!UICONTROL 興趣點詳細資訊]](./poi-details.md) | 說明造成事件的POI。 |
| `geo` | [[!UICONTROL 地理]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | DateTime | 時間戳記，位於 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式，表示使用時區偏移的本地時間。 格式模式為 `yyyy-MM-dd'T'HH:mm:ssXXX` (例如， `2001-07-04T12:08:56-07:00`)。 |
| `localTimezoneOffset` | 整數 | 當前本地時區偏移（以分鐘為單位），離 `localTime` 值。 這應包括目前的DST偏移（如果適用）。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
