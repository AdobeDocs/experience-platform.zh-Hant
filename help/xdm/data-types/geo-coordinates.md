---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；地理；座標；資料型別；資料型別；
solution: Experience Platform
title: 地理座標資料型別
description: 瞭解地理座標XDM資料型別。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---

# [!UICONTROL 地理座標]資料型別

[!UICONTROL 地理座標]是描述某個地點地理座標的標準XDM資料型別。 此資料型別是以[schema.org](https://schema.org/GeoCoordinates)上記錄的公用規格為基礎。

![](../images/data-types/geo-coordinates.png){width=400}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.description` | 字串 | 座標識別內容的說明。 |
| `_schema.elevation` | 雙精度 | 已定義座標的特定上升量。 值必須符合[WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)基準，並以公尺測量。 |
| `_schema.latitude` | 雙精度 | 地理點的已簽署垂直座標。 |
| `_schema.longitude` | 雙精度 | 地理點的已簽署水平座標。 |
| `_id` | 字串 | 系統產生的唯一座標ID。 |
