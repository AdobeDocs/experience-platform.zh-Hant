---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；信標；交互詳細資訊；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 地理交互詳細資訊資料類型
description: 本文檔概述了Geo Interaction Details XDM資料類型。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---

# [!UICONTROL 地理交互詳細資訊] 資料類型

[!UICONTROL 地理交互詳細資訊] 是一個標準XDM資料類型，它描述地理上定義的區域中包含的當前狀態。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形狀]](./geo-shape.md) | 描述與之交互的區域的地理形狀。 此欄位可以描述框、圓或多邊形。 |
| `deviceGeoAccuracy` | 雙倍 | 地球測量裝置或機構的精度，以米計量。 |
| `distanceToCenter` | 雙倍 | 在地球圈中，到地球中心的距離以米計。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
