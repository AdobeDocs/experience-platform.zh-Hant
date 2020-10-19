---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;datatype;data-type;data type;
solution: Experience Platform
title: 地理資料類型
topic: overview
description: 本檔案提供Geo XDM資料類型的概觀。
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---


# [!UICONTROL 地理資料] 類型

[!UICONTROL Geo] 是標準的XDM資料類型，可說明觀察到事件的地理區域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理坐標]](./geo-coordinates.md) | 說明地理座標。 |
| `_id` | 字串 | 坐標系的唯一系統生成ID。 |
| `city` | 字串 | 城市名稱。 |
| `countryCode` | 字串 | 國家／地區 <a href="https://datahub.io/core/country-list">的雙字元ISO 3166-1 alpha-2</a> 程式碼。 |
| `dmaID` | 整數 | 尼爾森媒體研究指定了市場區域。 |
| `msaID` | 整數 | 觀察發生地的美國都市統計區。 |
| `postalCode` | 字串 | 位置的郵遞區號。 郵遞區號並非所有國家／地區皆可使用。 在某些國家，這只會包含部分郵遞區號。 |
| `stateProvince` | 字串 | 觀察的州或省部分。 格式遵循 [ISO 3166-2（國家／地區和細分）標準](http://www.unece.org/cefact/locode/subdivisions.html) 。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)