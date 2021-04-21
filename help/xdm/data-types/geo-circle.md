---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;geo;circle;datatype；資料類型；
solution: Experience Platform
title: 地域社交圈資料類型
topic-legacy: overview
description: 本檔案提供地理圈XDM資料類型的概觀。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# [!UICONTROL Geo Circle] 資料類型

[!UICONTROL Geo Circle] 是標準的XDM資料類型，它描述圓形地理區域，給定以特定坐標集為中心的特定半徑。此資料類型基於[schema.org](http://schema.org/GeoCircle)上記載的公共規範。

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | 說明圓心的地理座標。 |
| `_schema.description` | 字串 | 社交圈包含的說明。 |
| `_schema.radius` | 雙倍 | 圓半徑的長度。 此值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基準，以米為單位測量。 |
| `_id` | 字串 | 社交圈的唯一、系統產生的ID。 |
