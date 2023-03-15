---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；poi;poi詳細資訊；地標；地標詳細資訊；資料類型；資料類型；
solution: Experience Platform
title: 興趣點詳細資料資料類型
description: 本檔案概述興趣點詳細資料XDM資料類型。
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 3%

---

# [!UICONTROL 興趣點詳細資訊] 資料類型

[!UICONTROL 興趣點詳細資訊] 是標準的XDM資料類型，可說明觀察到事件的地理相關資料。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 信標]](./beacon.md) | 說明POI互動中作用中的信標詳細資訊。 |
| `geoInteractionDetails` | [[!UICONTROL 地理互動詳細資料]](./geo-interaction-details.md) | 說明POI互動中作用中的地理詳細資訊。 |
| `category` | 字串 | 由POI定義的管理員為組織POI而指派的一般類別。 |
| `distanceToPOICenter` | 雙倍 | 與POI中心的估計距離（以公尺為單位）。 |
| `locatingType` | 字串 | 用於確定位置的機制。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字串 | POI的名稱。 |
| `poiID` | 字串 | POI的唯一識別碼。 |
| `type` | 字串 | POI的一般類型，使用POI定義管理員選取的類型結構。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
