---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；地理；資料類型；資料類型；
solution: Experience Platform
title: 地理資料類型
description: 本文檔概述了Geo XDM資料類型。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# [!UICONTROL 吉奧] 資料類型

[!UICONTROL 吉奧] 是標準XDM資料類型，它描述了觀察事件的地理區域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理坐標]](./geo-coordinates.md) | 描述某個位置的地理坐標。 |
| `_id` | 字串 | 坐標系的唯一系統生成ID。 |
| `city` | 字串 | 城市名稱。 |
| `countryCode` | 字串 | 兩個字元 <a href="https://datahub.io/core/country-list">ISO 3166-1α-2</a> 國家代碼。 |
| `dmaID` | 整數 | 尼爾森媒體研究指定了市場區域。 |
| `msaID` | 整數 | 觀察發生地的美國的都市統計區。 |
| `postalCode` | 字串 | 地點的郵遞區號。 並非所有國家都有郵遞區號。 在一些國家，這隻包含部分郵遞區號。 |
| `stateProvince` | 字串 | 觀察的省或州部分。 格式跟在 [ISO 3166-2（國家和地區）](https://www.unece.org/cefact/locode/subdivisions.html) 標準。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
