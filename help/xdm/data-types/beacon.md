---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: 信標資料類型
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---


# [!UICONTROL 信標] 資料類型

[!UICONTROL Beacon] 是標準的XDM資料類型，可說明當行動裝置在範圍內時，將身分資訊傳送至行動應用程式的無線裝置。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconMajor` | 雙倍 | 主要值可識別和區分1到65,535之間的組和無號整數值。 |
| `beaconMinor` | 雙倍 | 次要值可識別並區分1和65,535之間的個別和無號整數值。 |
| `proximity` | 字串 | 估計的信標距離。 請參閱附 [錄](#proximity) ，瞭解接受的值和定義。 |
| `proximityUUID` | 字串 | 鄰近UUID（通用唯一標識符）是一種特殊類型的標識符，用於將網路中的信標與您控制之外的網路中的所有其他信標區分開來。 鄰近UUID被配置成信標，被傳輸到範圍內的移動設備以標識組織的信標。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 附錄

以下章節包含有關信標資料類 [!UICONTROL 型的其] 他資訊。

## 接受的鄰近值 {#proximity}

下表概述接受的值及其 `proximity` 相關意義：

| 值 | 說明 |
| --- | --- |
| `immediate` | 幾公分內。 |
| `near` | 距離酒店不到10米。 |
| `far` | 距離酒店超過10米。 |
| `unknown` | 由於信號微弱，距離無法確定。 |