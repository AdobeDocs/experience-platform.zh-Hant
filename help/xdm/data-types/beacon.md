---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；信標；互動詳細資訊；資料類型；資料類型；
solution: Experience Platform
title: 信標資料類型
topic-legacy: overview
description: 本檔案概述XDM個別設定檔類別。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

#  信標資料類型

 Beaconis是標準的XDM資料類型，可說明當行動裝置在範圍內時，將身分資訊傳送給行動應用程式的無線裝置。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconMajor` | 雙倍 | 主要值可識別和區分1和65,535之間的組和無符號整數值。 |
| `beaconMinor` | 雙倍 | 小值可識別並區分介於1和65,535之間的個別和無號整數值。 |
| `proximity` | 字串 | 估計的信標距離。 有關接受的值和定義，請參閱[附錄](#proximity)。 |
| `proximityUUID` | 字串 | 鄰近地區UUID（通用唯一標識符）是一種特殊類型的標識符，用於區分網路中的信標與您控制之外的網路中的所有其他信標。 鄰近UUID設定為信標，以傳輸至範圍內的行動裝置，以識別組織的信標。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 附錄

下節包含有關[!UICONTROL Beacon]資料類型的其他資訊。

## 接近度的接受值 {#proximity}

下表概述`proximity`的接受值及其相關含義：

| 值 | 說明 |
| --- | --- |
| `immediate` | 幾公分以內。 |
| `near` | 距離酒店不到10米。 |
| `far` | 距離酒店10米。 |
| `unknown` | 由於信號微弱，無法確定距離。 |
