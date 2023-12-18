---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；地理；圓形；資料型別；資料型別；
solution: Experience Platform
title: 地理圓圈資料型別
description: 瞭解地理圈XDM資料型別。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---

# [!UICONTROL 地理圓形] 資料型別

[!UICONTROL 地理圓形] 是標準的XDM資料型別，可說明圓形地理區域，以一組特定座標為中心的特定半徑。 此資料型別以記錄的公開規格為基礎 [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理座標]](./geo-coordinates.md) | 描述圓心的地理座標。 |
| `_schema.description` | 字串 | 圓圈包含內容的說明。 |
| `_schema.radius` | 雙倍 | 圓半徑的長度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，並以公尺測量。 |
| `_id` | 字串 | 系統產生的圓形唯一ID。 |
