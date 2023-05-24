---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；架構；地理；地理形狀；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 地理形狀資料類型
description: 本文檔概述了Geo Shape XDM資料類型。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL 地理形狀] 資料類型

[!UICONTROL 地理形狀] 是描述地理區域形狀的標準XDM資料類型。 此資料類型基於上記錄的公共規範 [架構.org](https://schema.org/GeoShape)。

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.box` | 陣列 [[!UICONTROL 地理坐標]](./geo-coordinates.md) | 描述由兩個坐標組成的矩形所圍成的地理區域。 第一坐標是矩形的下角，第二坐標是上角。 |
| `_schema.circle` | 陣列 [[!UICONTROL 地理坐標]](./geo-coordinates.md) | 描述具有以地理坐標為中心的特定半徑的圓形區域。 |
| `_schema.polygon` | [[!UICONTROL 地理圓]](./geo-circle.md) | 四個或四個以上坐標的系列，其中第一和最終坐標相同。 |
| `_schema.description` | 字串 | 形狀定義的說明。 |
| `_schema.elevation` | 雙倍 | 形狀的特定高度或最小高度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 以米為單位測量。 與 `ceiling`，此屬性可用於表示位置的三維定界框。 |
| `_id` | 字串 | 形狀的唯一、系統生成的標識符。 |
| `ceiling` | 雙倍 | 形狀的最大高度。 僅當與 `elevation`。 該值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 以米為單位測量。 與 `elevation`，此屬性可用於表示位置的三維定界框。 |
