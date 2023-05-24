---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；方案；位置上下文；placeContext;datatype；資料類型；
solution: Experience Platform
title: 放置上下文資料類型
description: 此文檔概述了「置入上下文XDM」資料類型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 4%

---

# [!UICONTROL 放置上下文] 資料類型

[!UICONTROL 放置上下文] 是一種標準的XDM資料類型，它描述觀察到的事件的位置，包括興趣點資訊和地理坐標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點交互]](./poi-interaction.md) | 描述有關興趣點(POI)交互的詳細資訊。 |
| `activePOIs` | 陣列 [[!UICONTROL 興趣點詳細資訊]](./poi-details.md) | 描述導致事件的POI。 |
| `geo` | [[!UICONTROL 地理]](./geo.md) | 描述提供體驗的地理位置。 |
| `localTime` | 日期時間 | 時間戳 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式，指示使用指定時區偏移的本地時間。 格式圖案為 `yyyy-MM-dd'T'HH:mm:ssXXX` (例如， `2001-07-04T12:08:56-07:00`)。 |
| `localTimezoneOffset` | 整數 | 當前本地時區偏移（以分鐘為單位） `localTime` 值。 這應包括當前DST偏移（如果適用）。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
