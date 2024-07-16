---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；裝置；資料型別；資料型別；
solution: Experience Platform
title: 裝置資料型別
description: 瞭解裝置XDM資料型別。
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 18%

---

# [!UICONTROL 裝置]資料型別

[!UICONTROL 裝置]是描述已識別裝置的標準XDM資料型別。 裝置是可跨工作階段追蹤的應用程式或瀏覽器例項，通常可透過Cookie追蹤。

<img src="../images/data-types/device.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `colorDepth` | 整數 | 顯示器能表現的顏色數量。 |
| `manufacturer` | 字串 | 擁有裝置的設計和建立的組織名稱。 |
| `model` | 字串 | 裝置的型號名稱。這是裝置的通用、可讀取或行銷名稱。 例如，「iPhone 6S」是行動電話的一種特定型號。 |
| `modelNumber` | 字串 | 製造商為此裝置指定的唯一型號編號。型號不是版本，而是識別特定型號設定的唯一識別碼。 |
| `screenHeight` | 整數 | 裝置的活動顯示 (以預設方向) 的垂直像素數。 |
| `screenOrientation` | 字串 | 目前的熒幕方向。 接受的值包括`portrait`和`landscape`。 |
| `screenWidth` | 字串 | 裝置的活動顯示 (以預設方向) 的水平像素數。 |
| `type` | 字串 | 被追蹤的裝置型別。 接受的值包括： <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 字串 | 裝置的識別碼。 這可能是來自DeviceAtlas或其他服務的識別碼，用於識別正在使用的硬體。 |
| `typeIDService` | 字串 | 用於識別裝置型別的服務的名稱空間。 如需接受值的詳細資訊，請參閱[附錄](#typeIDService)。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 附錄

下列區段包含有關[!UICONTROL 裝置]資料型別的額外資訊。

## typeIDService接受的值 {#typeIDService}

下表概述`typeIDService`的接受值及其相關意義：

| 值 | 說明 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | 已使用DeviceAtlas識別裝置。 |
| `https://ns.adobe.com/xdm/external/adobecampaign` | 已使用Adobe Campaign識別裝置。 |
