---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；設備；資料類型；資料類型；
solution: Experience Platform
title: 設備資料類型
description: 本文檔概述了Device XDM資料類型。
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 4%

---

# [!UICONTROL 設備] 資料類型

[!UICONTROL 設備] 是描述已識別設備的標準XDM資料類型。 設備是可跨會話跟蹤的應用程式或瀏覽器實例，通常由cookie跟蹤。

<img src="../images/data-types/device.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `colorDepth` | 整數 | 顯示器能夠表示的顏色數。 |
| `manufacturer` | 字串 | 負責設計和建立設備的組織的名稱。 |
| `model` | 字串 | 設備的型號名稱。 這是設備的常用、可讀或營銷名稱。 例如，&quot;iPhone6S&quot;是一款特定的手機。 |
| `modelNumber` | 字串 | 製造商為此設備指定的唯一型號編號。 型號不是版本，而是標識特定型號配置的唯一標識符。 |
| `screenHeight` | 整數 | 設備的活動顯示在預設方向上的垂直像素數。 |
| `screenOrientation` | 字串 | 當前螢幕方向。 接受的值包括 `portrait` 和 `landscape`。 |
| `screenWidth` | 字串 | 設備活動顯示在預設方向的水準像素數。 |
| `type` | 字串 | 正在跟蹤的設備類型。 接受的值包括： <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 字串 | 設備的標識符。 這可能是DeviceAtlas或標識正在使用的硬體的其他服務的標識符。 |
| `typeIDService` | 字串 | 用於標識設備類型的服務的命名空間。 查看 [附錄](#typeIDService) 中。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 附錄

以下部分包含有關 [!UICONTROL 設備] 資料類型。

## 類型IDService的接受值 {#typeIDService}

下表概述了 `typeIDService` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | 已使用DeviceAtlas識別設備。 |
| `https://ns.adobe.com/xdm/external/adobecampaign` | 已使用Adobe Campaign識別設備。 |
