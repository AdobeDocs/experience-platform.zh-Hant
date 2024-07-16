---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；信標；互動詳細資訊；資料型別；資料型別；
solution: Experience Platform
title: 信標資料型別
description: 瞭解XDM個別設定檔類別。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 17%

---

# [!UICONTROL 信標]資料型別

[!UICONTROL 信標]是標準的XDM資料型別，說明在行動裝置進入範圍內時，無線裝置會與行動應用程式通訊身分資訊。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `beaconMajor` | 雙精度 | 主要值會識別和區分 1 和 65,535 之間的群組值與不帶正負號的整數。 |
| `beaconMinor` | 雙精度 | 次要值會識別和區分 1 和 65,535 之間的個別值與不帶正負號的整數。 |
| `proximity` | 字串 | 和信標的預估距離。 如需接受的值和定義，請參閱[附錄](#proximity)。 |
| `proximityUUID` | 字串 | 鄰近UUID （通用唯一識別碼）是一種特殊型別的識別碼，可用來將您網路中的信標與非您控制之網路中的所有其他信標區分開來。 近似程度UUID會設定至信標中，以傳輸到範圍內的行動裝置來識別組織的信標。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 附錄

下列區段包含有關[!UICONTROL 信標]資料型別的額外資訊。

## 近似程度接受的值 {#proximity}

下表概述`proximity`的接受值及其相關意義：

| 值 | 說明 |
| --- | --- |
| `immediate` | 幾公分以內。 |
| `near` | 距離不到10米。 |
| `far` | 10米以外。 |
| `unknown` | 無法確認距離，可能是因為訊號弱。 |
