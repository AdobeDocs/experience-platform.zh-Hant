---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;Schemas；信標；交互詳細資訊；datatype；資料類型；
solution: Experience Platform
title: 地理互動詳細資料資料類型
topic-legacy: overview
description: 本檔案提供地理互動詳細資訊XDM資料類型的概觀。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 2%

---

# [!UICONTROL Geo interaction details] 資料類型

[!UICONTROL Geo interaction details] 是標準的XDM資料類型，它描述了地理定義區域中包含的當前狀態。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | 說明所互動區域的地理形狀。 此欄位可描述方塊、圓或多邊形。 |
| `deviceGeoAccuracy` | 雙倍 | 地質測量裝置或機構的精度，以米計測量。 |
| `distanceToCenter` | 雙倍 | 若是地理圈，則距地理中心的距離，以米為單位。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
