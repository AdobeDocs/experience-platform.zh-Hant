---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；信標；互動詳細資訊；資料型別；資料型別；
solution: Experience Platform
title: 地理互動詳細資料資料型別
description: 瞭解地理互動細節XDM資料型別。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 13%

---

# [!UICONTROL 地理互動詳細資料]資料型別

[!UICONTROL 地理互動詳細資料]是標準的XDM資料型別，說明地理定義區域中目前的包含狀態。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形狀]](./geo-shape.md) | 說明互動區域的地理形狀。 此欄位可描述方塊、圓形或多邊形。 |
| `deviceGeoAccuracy` | 雙精度 | 地理測量裝置或機制的精確性 (以公尺衡量)。 |
| `distanceToCenter` | 雙精度 | 有地理圓圈的情況下和地理中心的距離（以公尺測量）。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
