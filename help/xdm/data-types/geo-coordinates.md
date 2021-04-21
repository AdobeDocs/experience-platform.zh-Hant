---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;geo;coordinates;datatype；資料類型；
solution: Experience Platform
title: 地理坐標資料類型
topic-legacy: overview
description: 本檔案概述「地理座標XDM」資料類型。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL Geo Coordinates] 資料類型

[!UICONTROL Geo Coordinates] 是一種標準的XDM資料類型，用於描述地理坐標。此資料類型基於[schema.org](https://schema.org/GeoCoordinates)上記載的公共規範。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.description` | 字串 | 坐標標識的說明。 |
| `_schema.elevation` | 雙倍 | 定義坐標的特定高度。 該值必須符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基準，並以米為單位測量。 |
| `_schema.latitude` | 雙倍 | 地理點的符號垂直坐標。 |
| `_schema.longitude` | 雙倍 | 地理點的有符號水準座標。 |
| `_id` | 字串 | 坐標系的唯一系統生成ID。 |
