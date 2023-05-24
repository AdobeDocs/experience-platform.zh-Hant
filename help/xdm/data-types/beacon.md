---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；信標；交互詳細資訊；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 信標資料類型
description: 本文檔概述了XDM Individual Profile類。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# [!UICONTROL 信標] 資料類型

[!UICONTROL 信標] 是標準XDM資料類型，它描述當移動設備在範圍內時向移動應用程式傳送身份資訊的無線設備。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconMajor` | 雙倍 | 主要值標識和區分1和65,535之間的組和無符號整數值。 |
| `beaconMinor` | 雙倍 | 次要值標識和區分介於1和65,535之間的單個和無符號整數值。 |
| `proximity` | 字串 | 估計到信標的距離。 查看 [附錄](#proximity) 以獲取接受的值和定義。 |
| `proximityUUID` | 字串 | 鄰近UUID（通用唯一標識符）是一種特殊類型的標識符，用於將網路中的信標與控制範圍外的網路中的所有其它信標區分開來。 鄰近UUID被配置成信標，被傳輸到範圍內的移動設備以標識組織的信標。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 附錄

以下部分包含有關 [!UICONTROL 信標] 資料類型。

## 接受的鄰近度值 {#proximity}

下表概述了 `proximity` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `immediate` | 幾公分之內。 |
| `near` | 不到10米。 |
| `far` | 大於10米。 |
| `unknown` | 由於信號微弱，無法確定距離。 |
