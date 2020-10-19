---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: 地理形狀資料類型
topic: overview
description: 本檔案提供地理形狀XDM資料類型的概觀。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# [!UICONTROL 地理形狀] 資料類型

[!UICONTROL Geo Shape] （地理形狀）是標準的XDM資料類型，可描述地理區域的形狀。 此資料類型基於 [schema.org上記錄的公用規範](https://schema.org/GeoShape)。

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.box` | 地理座 [[!UICONTROL 標陣列]](./geo-coordinates.md) | 描述由兩個坐標構成的矩形所包圍的地理區域。 第一坐標是矩形的下角，第二坐標是上角。 |
| `_schema.circle` | 地理座 [[!UICONTROL 標陣列]](./geo-coordinates.md) | 描述圓形區域，其特定半徑位於地理坐標上。 |
| `_schema.polygon` | [[!UICONTROL 地域社交圈]](./geo-circle.md) | 一系列四個或多個坐標，其中第一個和最後一個坐標相同。 |
| `_schema.description` | 字串 | 描述形狀的定義。 |
| `_schema.elevation` | 雙倍 | 形狀的特定或最小高度。 此值符合 [WGS84基準](http://gisgeography.com/wgs84-world-geodetic-system/) ，以米為單位測量。 與組合使 `ceiling`用時，此屬性可用於表示位置的三維邊界框。 |
| `_id` | 字串 | 形狀的唯一、系統產生的識別碼。 |
| `ceiling` | 雙倍 | 形狀的最大高度。 此屬性僅在與搭配使用時有效 `elevation`。 該值符合 [WGS84基準](http://gisgeography.com/wgs84-world-geodetic-system/) ，並以米為單位測量。 與組合使 `elevation`用時，此屬性可用於表示位置的三維邊界框。 |
