---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: 地理坐標資料類型
topic: overview
description: 本檔案概述「地理座標XDM」資料類型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---


# [!UICONTROL 地理坐標] 資料類型

[!UICONTROL 地理座標] (Geo Coordinates)是一種標準的XDM資料類型，可描述地理座標。 此資料類型基於 [schema.org上記錄的公用規範](https://schema.org/GeoCoordinates)。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.description` | 字串 | 坐標標識的說明。 |
| `_schema.elevation` | 雙倍 | 定義坐標的特定高度。 該值必須符合 [WGS84基準](http://gisgeography.com/wgs84-world-geodetic-system/) ，並以米為單位測量。 |
| `_schema.latitude` | 雙倍 | 地理點的符號垂直坐標。 |
| `_schema.longitude` | 雙倍 | 地理點的有符號水準座標。 |
| `_id` | 字串 | 坐標系的唯一系統生成ID。 |
