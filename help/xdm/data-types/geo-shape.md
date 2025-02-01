---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；地理；地理形狀；資料型別；資料型別；資料型別；
solution: Experience Platform
title: 地理形狀資料型別
description: 瞭解地理形狀XDM資料型別。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# [!UICONTROL 地理形狀]資料型別

[!UICONTROL 地理形狀]是描述地理區域形狀的標準XDM資料型別。 此資料型別是以[schema.org](https://schema.org/GeoShape)上記錄的公用規格為基礎。

![](../images/data-types/geo-shape.png){width=500}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.box` | [[!UICONTROL 地理座標陣列]](./geo-coordinates.md) | 描述由兩個座標形成的矩形所圍住的地理區域。 第一個座標是矩形的下角，第二個座標是上角。 |
| `_schema.circle` | [[!UICONTROL 地理座標陣列]](./geo-coordinates.md) | 描述以地理座標為中心的特定半徑圓形區域。 |
| `_schema.polygon` | [[!UICONTROL 地理圈]](./geo-circle.md) | 一系列四個或更多座標，其中第一個和最後一個座標完全相同。 |
| `_schema.description` | 字串 | 定義何種形狀的說明。 |
| `_schema.elevation` | 雙精度 | 形狀的特定或最小上升量。 此值符合[WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)基準，並以公尺測量。 此屬性與`ceiling`結合使用，可用來表示位置的三維邊界方框。 |
| `_id` | 字串 | 形狀的系統產生的唯一識別碼。 |
| `ceiling` | 雙精度 | 形狀的最大上升量。 此屬性只有在與`elevation`結合使用時才有效。 值符合[WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)基準，並以公尺測量。 此屬性與`elevation`結合使用，可用來表示位置的三維邊界方框。 |
