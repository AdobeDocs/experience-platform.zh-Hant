---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;Schemas；信標；交互詳細資訊；datatype；資料類型；
solution: Experience Platform
title: 信標資料類型
topic-legacy: overview
description: 本文檔概述了XDM Individual Profile類。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# [!UICONTROL Beacon] 資料類型

[!UICONTROL Beacon] 是標準的XDM資料類型，可說明當行動裝置在範圍內時，可將身分資訊傳送至行動應用程式的無線裝置。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconMajor` | 雙倍 | 主要值可識別和區分1到65,535之間的組和無號整數值。 |
| `beaconMinor` | 雙倍 | 次要值可識別並區分1和65,535之間的個別和無號整數值。 |
| `proximity` | 字串 | 估計的信標距離。 有關接受的值和定義，請參見[附錄](#proximity)。 |
| `proximityUUID` | 字串 | 鄰近UUID（通用唯一標識符）是一種特殊類型的標識符，用於將網路中的信標與您控制之外的網路中的所有其他信標區分開來。 鄰近UUID被配置成信標，被傳輸到範圍內的移動設備以標識組織的信標。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 附錄

以下部分包含有關[!UICONTROL Beacon]資料類型的其他資訊。

## 接受的proximity {#proximity}值

下表概述`proximity`的接受值及其相關含義：

| 值 | 說明 |
| --- | --- |
| `immediate` | 幾公分內。 |
| `near` | 距離酒店不到10米。 |
| `far` | 距離酒店超過10米。 |
| `unknown` | 由於信號微弱，距離無法確定。 |
