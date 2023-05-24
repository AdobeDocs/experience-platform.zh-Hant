---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；架構；地理；圓；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 地理圓資料類型
description: 本文檔概述了Geo Circle XDM資料類型。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 地理圓] 資料類型

[!UICONTROL 地理圓] 是一種標準XDM資料類型，它描述圓形地理區域，給定以特定坐標集為中心的特定半徑。 此資料類型基於上記錄的公共規範 [架構.org](https://schema.org/GeoCircle)。

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理坐標]](./geo-coordinates.md) | 描述圓心的地理坐標。 |
| `_schema.description` | 字串 | 圓包含的內容的說明。 |
| `_schema.radius` | 雙倍 | 圓半徑的長度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 以米為單位測量。 |
| `_id` | 字串 | 為圓生成的唯一系統ID。 |
