---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；信標；互動詳細資訊；資料類型；資料類型；
solution: Experience Platform
title: 地域互動詳細資料資料類型
topic-legacy: overview
description: 本檔案概述「地理互動詳細資料」XDM資料類型。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 4%

---

# [!UICONTROL 地理互動詳] 細資料類型

[!UICONTROL 地理互] 動詳細說明標準XDM資料類型，說明地理定義區域中包含的目前狀態。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形狀]](./geo-shape.md) | 說明要互動之區域的地理形狀。 此欄位可以描述框、圓或多邊形。 |
| `deviceGeoAccuracy` | 雙倍 | 地球測量裝置或機構的準確度，以公尺為單位測量。 |
| `distanceToCenter` | 雙倍 | 以公尺為單位的地理圈與地理中心的距離。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
