---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；地理；資料型別；資料型別；
solution: Experience Platform
title: 地理資料型別
description: 瞭解地理XDM資料型別。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 34%

---

# [!UICONTROL 地理]資料型別

[!UICONTROL 地理]是標準的XDM資料型別，可描述觀察事件的地理區域。

![](../images/data-types/geo.png){width=400}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理座標]](./geo-coordinates.md) | 說明地點的地理座標。 |
| `_id` | 字串 | 系統產生的唯一座標ID。 |
| `city` | 字串 | 城市的名稱。 |
| `countryCode` | 字串 | 國家/地區的雙字元<a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a>代碼。 |
| `dmaID` | 整數 | Nielsen 媒體研究指定的市場區域。 |
| `msaID` | 整數 | 進行觀察的美國大都會統計區域。 |
| `postalCode` | 字串 | 地點的郵遞區號。無法提供所有國家/地區的郵遞區號。在部分國家/地區，這僅包含部分的郵遞區號。 |
| `stateProvince` | 字串 | 觀察的州或省的部分。 格式遵循[ISO 3166-2 （國家/地區和次分割）](https://www.unece.org/cefact/locode/subdivisions.html)標準。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
