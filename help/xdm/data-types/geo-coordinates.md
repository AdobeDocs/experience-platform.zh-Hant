---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；地理；座標；資料類型；資料類型；
solution: Experience Platform
title: 地理座標資料類型
description: 本檔案概述「地理座標」XDM資料類型。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 地理座標] 資料類型

[!UICONTROL 地理座標] 是描述地理座標的標準XDM資料類型。 此資料類型基於上記錄的公共規範 [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.description` | 字串 | 座標識別的說明。 |
| `_schema.elevation` | 雙倍 | 定義的坐標的特定高度。 值必須符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，以公尺為單位測量。 |
| `_schema.latitude` | 雙倍 | 地理點的有符號垂直坐標。 |
| `_schema.longitude` | 雙倍 | 地理點的標籤水準坐標。 |
| `_id` | 字串 | 座標的唯一、系統產生的ID。 |
