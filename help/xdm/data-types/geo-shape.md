---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；地理；地理形狀；資料類型；資料類型；
solution: Experience Platform
title: 地理形狀資料類型
description: 本檔案概述「地理形狀」XDM資料類型。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL 地理形狀] 資料類型

[!UICONTROL 地理形狀] 是描述地理區域形狀的標準XDM資料類型。 此資料類型基於上記錄的公共規範 [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.box` | 陣列 [[!UICONTROL 地理座標]](./geo-coordinates.md) | 描述由兩個坐標組成的矩形所圍成的地理區域。 第一坐標是矩形的下角，第二坐標是上角。 |
| `_schema.circle` | 陣列 [[!UICONTROL 地理座標]](./geo-coordinates.md) | 描述以地理坐標為中心的特定半徑的圓形區域。 |
| `_schema.polygon` | [[!UICONTROL 地理圈]](./geo-circle.md) | 四個或更多座標的系列，其中第一個和最後一個坐標相同。 |
| `_schema.description` | 字串 | 形狀定義的說明。 |
| `_schema.elevation` | 雙倍 | 形狀的特定或最小高度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，以公尺為單位測量。 結合 `ceiling`，此屬性可用來表示位置的三維邊界方框。 |
| `_id` | 字串 | 形狀的唯一、系統生成的標識符。 |
| `ceiling` | 雙倍 | 形狀的最大高度。 此屬性僅在與 `elevation`. 值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，以公尺為單位測量。 結合 `elevation`，此屬性可用來表示位置的三維邊界方框。 |
