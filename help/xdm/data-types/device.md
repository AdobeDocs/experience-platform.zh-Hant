---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;device;datatype;data-type;data type;
solution: Experience Platform
title: 裝置資料類型
topic: overview
description: 本文檔概述了Device XDM資料類型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 4%

---


# [!UICONTROL 裝置] 資料類型

[!UICONTROL Device] （設備）是一種標準的XDM資料類型，用於描述已識別的設備。 裝置是應用程式或瀏覽器例項，可跨作業追蹤，通常由Cookie追蹤。

<img src="../images/data-types/device.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `colorDepth` | 整數 | 顯示器能夠表示的顏色數。 |
| `manufacturer` | 字串 | 擁有設計和建立裝置的組織名稱。 |
| `model` | 字串 | 設備的型號名稱。 這是裝置的通用、可讀或行銷名稱。 例如，「iPhone 6S」是行動電話的特定機型。 |
| `modelNumber` | 字串 | 製造商為此設備指定的唯一型號。 型號不是版本，而是標識特定型號配置的唯一標識符。 |
| `screenHeight` | 整數 | 預設方向的裝置作用中顯示的垂直像素數。 |
| `screenOrientation` | 字串 | 目前的畫面方向。 接受的值包 `portrait` 括和 `landscape`。 |
| `screenWidth` | 字串 | 預設方向中裝置作用中顯示的水準像素數。 |
| `type` | 字串 | 所追蹤的裝置類型。 接受的值包括： <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 字串 | 裝置的識別碼。 這可以是DeviceAtlas的識別碼，或是識別所使用硬體的其他服務。 |
| `typeIDService` | 字串 | 用於標識設備類型的服務的名稱空間。 如需已接 [受值的詳細資訊](#typeIDService) ，請參閱附錄。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 附錄

下節包含有關「設備」資料類 [!UICONTROL 型的其] 他資訊。

## typeIDService的接受值 {#typeIDService}

下表概述接受的值及其 `typeIDService` 相關意義：

| 值 | 說明 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | 已使用DeviceAtlas識別裝置。 |
| `https://ns.adobe.com/xdm/external/adobecampaign` | 裝置已使用Adobe Campaign加以識別。 |