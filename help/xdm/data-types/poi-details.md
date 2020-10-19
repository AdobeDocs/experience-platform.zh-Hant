---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;poi details;point of interest;point of interest details;datatype;data-type;data type;
solution: Experience Platform
title: 興趣點詳細資料資料類型
topic: overview
description: 本檔案提供興趣點詳細資訊XDM資料類型的概觀。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 4%

---


# [!UICONTROL 興趣點詳細資料] ，資料類型

[!UICONTROL 興趣點詳細資訊] ，是一種標準的XDM資料類型，可說明觀察到事件的地理相關資料。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 信標]](./beacon.md) | 說明POI互動中作用中的信標詳細資訊。 |
| `geoInteractionDetails` | [[!UICONTROL 地理互動詳細資訊]](./geo-interaction-details.md) | 說明POI互動作用中的地理詳細資料。 |
| `category` | 字串 | 由POI定義管理員為組織POI而分配的常規類別。 |
| `distanceToPOICenter` | 雙倍 | 預計距離POI中心的距離（以米為單位）。 |
| `locatingType` | 字串 | 用於確定位置的機構。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字串 | 給POI的名稱。 |
| `poiID` | 字串 | POI的唯一識別碼。 |
| `type` | 字串 | POI的一般類型，使用由POI定義的管理員選擇的類型模式。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)