---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；位置內容；placeContext；資料型別；資料型別；
solution: Experience Platform
title: 地標內容資料型別
description: 瞭解地點內容XDM資料型別。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL 放置內容]資料型別

[!UICONTROL 放置內容]是標準的XDM資料型別，可描述觀察到的事件位置，包括興趣點資訊和地理座標。

![](../images/data-types/place-context.png){width=500}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點互動]](./poi-interaction.md) | 說明興趣點(POI)互動的詳細資訊。 |
| `activePOIs` | [[!UICONTROL 興趣點詳細資訊的陣列]](./poi-details.md) | 說明造成事件的POI。 |
| `geo` | [[!UICONTROL 地理]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | 日期時間 | 以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式表示的時間戳記，表示使用具有指定時區位移的當地時間。 格式化模式為`yyyy-MM-dd'T'HH:mm:ssXXX` （例如，`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整數 | `localTime`值的目前當地時區與UTC的偏移量（分鐘）。 這應該包括目前的DST位移（如果適用）。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
