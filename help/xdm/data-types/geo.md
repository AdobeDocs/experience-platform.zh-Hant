---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；地理；資料類型；資料類型；
solution: Experience Platform
title: 地理資料類型
description: 本檔案概述Geo XDM資料類型。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# [!UICONTROL 地理] 資料類型

[!UICONTROL 地理] 是標準XDM資料類型，可說明觀察到事件的地理區域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理座標]](./geo-coordinates.md) | 說明地理座標。 |
| `_id` | 字串 | 座標的唯一、系統產生的ID。 |
| `city` | 字串 | 城市的名字。 |
| `countryCode` | 字串 | 兩個字元 <a href="https://datahub.io/core/country-list">ISO 3166-1alpha-2</a> 國家/地區的代碼。 |
| `dmaID` | 整數 | Nielsen媒體研究指定的市場區域。 |
| `msaID` | 整數 | 觀察發生地的美國大都市統計區。 |
| `postalCode` | 字串 | 位置的郵遞區號。 郵遞區號不適用於所有國家/地區。 在某些國家/地區，這只會包含部分郵遞區號。 |
| `stateProvince` | 字串 | 觀察的州或省部分。 格式會遵循 [ISO 3166-2（國家/地區和細分）](https://www.unece.org/cefact/locode/subdivisions.html) 標準。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
