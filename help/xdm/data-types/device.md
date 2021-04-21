---
keywords: Experience Platform;home；常用主題；模式；模式；XDM;fields；模式；設備；資料類型；資料類型；
solution: Experience Platform
title: 裝置資料類型
topic-legacy: overview
description: 本文檔概述了Device XDM資料類型。
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 4%

---

# [!UICONTROL Device] 資料類型

[!UICONTROL Device] 是描述已識別設備的標準XDM資料類型。裝置是應用程式或瀏覽器例項，可跨作業追蹤，通常由Cookie追蹤。

<img src="../images/data-types/device.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `colorDepth` | 整數 | 顯示器能夠表示的顏色數。 |
| `manufacturer` | 字串 | 擁有設計和建立裝置的組織名稱。 |
| `model` | 字串 | 設備的型號名稱。 這是裝置的通用、可讀或行銷名稱。 例如，「iPhone 6S」是行動電話的特定機型。 |
| `modelNumber` | 字串 | 製造商為此設備指定的唯一型號。 型號不是版本，而是標識特定型號配置的唯一標識符。 |
| `screenHeight` | 整數 | 預設方向的裝置作用中顯示的垂直像素數。 |
| `screenOrientation` | 字串 | 目前的畫面方向。 接受的值包括`portrait`和`landscape`。 |
| `screenWidth` | 字串 | 預設方向中裝置作用中顯示的水準像素數。 |
| `type` | 字串 | 所追蹤的裝置類型。 接受的值包括： <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 字串 | 裝置的識別碼。 這可以是DeviceAtlas的識別碼，或是識別所使用硬體的其他服務。 |
| `typeIDService` | 字串 | 用於標識設備類型的服務的名稱空間。 有關接受值的詳細資訊，請參見[附錄](#typeIDService)。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 附錄

以下部分包含有關[!UICONTROL Device]資料類型的其他資訊。

## typeIDService {#typeIDService}的接受值

下表概述`typeIDService`的接受值及其相關含義：

| 值 | 說明 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | 已使用DeviceAtlas識別裝置。 |
| `https://ns.adobe.com/xdm/external/adobecampaign` | 已使用Adobe Campaign識別此裝置。 |
