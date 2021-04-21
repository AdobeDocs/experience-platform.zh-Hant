---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;geo;datatype；資料類型；
solution: Experience Platform
title: 地理資料類型
topic-legacy: overview
description: 本檔案提供Geo XDM資料類型的概觀。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 4%

---

# [!UICONTROL Geo] 資料類型

[!UICONTROL Geo] 是標準的XDM資料類型，可描述觀察到事件的地理區域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | 說明地理座標。 |
| `_id` | 字串 | 坐標系的唯一系統生成ID。 |
| `city` | 字串 | 城市名稱。 |
| `countryCode` | 字串 | 國家／地區的雙字元<a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a>程式碼。 |
| `dmaID` | 整數 | 尼爾森媒體研究指定了市場區域。 |
| `msaID` | 整數 | 觀察發生地的美國都市統計區。 |
| `postalCode` | 字串 | 位置的郵遞區號。 郵遞區號並非所有國家／地區皆可使用。 在某些國家，這只會包含部分郵遞區號。 |
| `stateProvince` | 字串 | 觀察的州或省部分。 格式遵循[ISO 3166-2（國家／地區和細分）](http://www.unece.org/cefact/locode/subdivisions.html)標準。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)
