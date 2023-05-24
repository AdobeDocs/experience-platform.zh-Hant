---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；模式；方案；poi;poi詳細資訊；興趣點；資料類型；資料類型；
solution: Experience Platform
title: 興趣點詳細資訊資料類型
description: 此文檔概述了興趣點詳細資訊XDM資料類型。
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 3%

---

# [!UICONTROL 興趣點詳細資訊] 資料類型

[!UICONTROL 興趣點詳細資訊] 是一個標準XDM資料類型，它描述了在其中觀察到事件的地理相關資料。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 信標]](./beacon.md) | 描述POI交互活動的信標詳細資訊。 |
| `geoInteractionDetails` | [[!UICONTROL 地理交互詳細資訊]](./geo-interaction-details.md) | 描述POI交互活動的地理詳細資訊。 |
| `category` | 字串 | 由POI定義管理員為組織POI而分配的一般類別。 |
| `distanceToPOICenter` | 雙倍 | POI中心的估計距離（以米計）。 |
| `locatingType` | 字串 | 用於確定位置的機構。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字串 | 給POI的名字。 |
| `poiID` | 字串 | POI的唯一標識符。 |
| `type` | 字串 | 使用POI定義管理員選擇的鍵入架構的POI的一般類型。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
