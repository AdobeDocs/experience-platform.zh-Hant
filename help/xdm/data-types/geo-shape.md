---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;geo;geo;shape;datatype；資料類型；
solution: Experience Platform
title: 地理形狀資料類型
topic-legacy: overview
description: 本檔案提供地理形狀XDM資料類型的概觀。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 2%

---

# [!UICONTROL Geo Shape] 資料類型

[!UICONTROL Geo Shape] 是描述地理區域形狀的標準XDM資料類型。此資料類型基於[schema.org](https://schema.org/GeoShape)上記載的公共規範。

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.box` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md)陣列 | 描述由兩個坐標構成的矩形所包圍的地理區域。 第一坐標是矩形的下角，第二坐標是上角。 |
| `_schema.circle` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md)陣列 | 描述圓形區域，其特定半徑位於地理坐標上。 |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | 一系列四個或多個坐標，其中第一個和最後一個坐標相同。 |
| `_schema.description` | 字串 | 描述形狀的定義。 |
| `_schema.elevation` | 雙倍 | 形狀的特定或最小高度。 此值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基準，以米為單位測量。 與`ceiling`結合使用，此屬性可用於表示位置的三維邊界框。 |
| `_id` | 字串 | 形狀的唯一、系統產生的識別碼。 |
| `ceiling` | 雙倍 | 形狀的最大高度。 此屬性僅在與`elevation`結合使用時有效。 該值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基準，並以米為單位測量。 與`elevation`結合使用，此屬性可用於表示位置的三維邊界框。 |
