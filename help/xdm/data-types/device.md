---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；裝置；資料類型；資料類型；
solution: Experience Platform
title: 裝置資料類型
description: 本檔案概述Device XDM資料類型。
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 5%

---

# [!UICONTROL 裝置] 資料類型

[!UICONTROL 裝置] 是描述已識別裝置的標準XDM資料類型。 裝置是可跨工作階段追蹤的應用程式或瀏覽器例項，通常由Cookie追蹤。

<img src="../images/data-types/device.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `colorDepth` | 整數 | 顯示可表示的顏色數。 |
| `manufacturer` | 字串 | 擁有設備設計和建立的組織的名稱。 |
| `model` | 字串 | 設備的型號名稱。 這是裝置的常見、人類看得懂的或行銷名稱。 例如，「iPhone 6S」是行動電話的特定型號。 |
| `modelNumber` | 字串 | 製造商為此設備分配的唯一型號指定。 型號不是版本，而是標識特定型號配置的唯一標識符。 |
| `screenHeight` | 整數 | 以預設方向顯示的裝置作用中垂直像素數。 |
| `screenOrientation` | 字串 | 目前的畫面方向。 接受的值包括 `portrait` 和 `landscape`. |
| `screenWidth` | 字串 | 以預設方向顯示的裝置作用中水準像素數。 |
| `type` | 字串 | 要追蹤的裝置類型。 接受的值包括： <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 字串 | 裝置的識別碼。 這可能是DeviceAtlas的識別碼，或是識別正在使用之硬體的其他服務。 |
| `typeIDService` | 字串 | 用於識別裝置類型的服務的命名空間。 請參閱 [附錄](#typeIDService) 以取得接受值的詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 附錄

下節包含 [!UICONTROL 裝置] 資料類型。

## typeIDService接受的值 {#typeIDService}

下表概述 `typeIDService` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | 已使用DeviceAtlas識別裝置。 |
| `https://ns.adobe.com/xdm/external/adobecampaign` | 已使用Adobe Campaign識別裝置。 |
