---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；地理；社交圈；資料類型；資料類型；
solution: Experience Platform
title: 地理圈資料類型
description: 本檔案概述「地理圈XDM」資料類型。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 地理圈] 資料類型

[!UICONTROL 地理圈] 是描述圓形地理區域的標準XDM資料類型，假設特定半徑以特定座標集為中心。 此資料類型基於上記錄的公共規範 [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理座標]](./geo-coordinates.md) | 說明圓心的地理座標。 |
| `_schema.description` | 字串 | 關於社交圈包含內容的說明。 |
| `_schema.radius` | 雙倍 | 圓半徑的長度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，以公尺為單位測量。 |
| `_id` | 字串 | 圓圈的唯一、系統產生的ID。 |
