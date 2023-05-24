---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；架構；地理；坐標；資料類型；資料類型；
solution: Experience Platform
title: 地理坐標資料類型
description: 本文檔概述了Geo Coordinates XDM資料類型。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 地理坐標] 資料類型

[!UICONTROL 地理坐標] 是一個標準的XDM資料類型，它描述了某個位置的地理坐標。 此資料類型基於上記錄的公共規範 [架構.org](https://schema.org/GeoCoordinates)。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.description` | 字串 | 坐標標識的說明。 |
| `_schema.elevation` | 雙倍 | 定義的坐標的特定高度。 值必須與 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 以米為單位測量。 |
| `_schema.latitude` | 雙倍 | 地理點的帶符號垂直坐標。 |
| `_schema.longitude` | 雙倍 | 地理點的帶符號水準坐標。 |
| `_id` | 字串 | 坐標系的唯一系統生成ID。 |
