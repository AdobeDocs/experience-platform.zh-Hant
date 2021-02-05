---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；模式；信標；交互詳細資訊；資料類型；資料類型；
solution: Experience Platform
title: 地理互動詳細資料資料類型
topic: overview
description: 本檔案提供地理互動詳細資訊XDM資料類型的概觀。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# [!UICONTROL 地理互動詳細] 資料類型

[!UICONTROL 地理互] 動詳細說明標準XDM資料類型，可說明地理定義區域中目前包含狀態。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形狀]](./geo-shape.md) | 說明所互動區域的地理形狀。 此欄位可描述方塊、圓或多邊形。 |
| `deviceGeoAccuracy` | 雙倍 | 地質測量裝置或機構的精度，以米計測量。 |
| `distanceToCenter` | 雙倍 | 若是地理圈，則距地理中心的距離，以米為單位。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
