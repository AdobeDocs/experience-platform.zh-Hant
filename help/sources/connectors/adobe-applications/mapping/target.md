---
keywords: Experience Platform；首頁；熱門主題；目標映射；目標映射
solution: Experience Platform
title: 將Adobe Target事件資料映射到XDM
topic-legacy: overview
description: 瞭解如何將Adobe Target事件欄位對應至Experience Data Model(XDM)架構，以便用於Adobe Experience Platform。
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# 目標映射欄位映射

Adobe Experience Platform允許您通過Target源連接器接收Adobe Target資料。 使用連接器時，來自Target欄位的所有資料都必須映射至與XDM ExperienceEvent類別相關聯的[Experience Data Model(XDM)](../../../../xdm/home.md)欄位。

下表概述「體驗事件」架構的欄位（*XDM ExperienceEvent欄位*），以及對應的「目標」欄位（*「目標請求」欄位*）。 另外，也提供一些映射的附加說明。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| XDM ExperienceEvent欄位 | 目標請求欄位 | 附註 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一的請求識別碼 |
| **`dataSource`** |  | 已配置為「1」（所有客戶端）。 |
| `dataSource._id` | 無法隨請求傳遞的系統產生值。 | 此資料來源的唯一ID。 這將由建立資料源的個人或系統提供。 |
| `dataSource.code` | 無法隨請求傳遞的系統產生值。 | 通往完整@id的捷徑。 您至少可以使用其中一個程式碼或@id。 有時，此程式碼稱為資料來源整合程式碼。 |
| `dataSource.tags` | 無法隨請求傳遞的系統產生值。 | 標籤用於指示應用程式如何使用給定資料源表示的別名。<br><br>範例:<br><ul><li>`isAVID`:代表Analytics訪客ID的資料來源。</li><li>`isCRSKey`:表示應當用作CRS中鍵的別名的資料源。</li></ul>標籤是在建立資料源時設定的，但在引用給定資料源時，標籤也包括在管線消息中。 |
| **`timestamp`** | 事件時間戳記 |
| **`channel`** | `context.channel` | 僅適用於檢視傳送。 選項為「web」和「mobile」，預設值為「web」。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 行動電信業者名稱已根據要求的IP位址解析。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （若為V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （若為V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 客戶定義環境（例如開發、qa或prod）的Target內部對應。 |
| `experience.target.supplementalDataID` | 用於將Target事件與Analytics事件結合的識別碼 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 訪客符合的活動清單（陣列） |
| `experience.target.activities[i].activityID` | 訪客符合的任何指定活動的ID |
| `experience.target.activities[i].version` | 訪客符合的任何特定活動版本 |
| `experience.target.activities[i].activityEvents` | 包含使用者在此事件中點擊的活動事件的詳細資料。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | `deviceAtlas`（或NULL）的以下屬性之一： <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 隨機UUID（必要） |
| `placeContext.geo.city` | 根據請求的IP位址解決城市名稱。 |
| `placeContext.geo.countryCode` | 根據請求的IP位址解決國家／地區代碼。 |
| `placeContext.geo.dmaId` | 指定的市場區域代碼已根據要求的IP位址解決。 |
| `placeContext.geo.postalCode` | 郵遞區號已根據請求的IP位址解決。 |
| `placeContext.geo.stateProvince` | 根據請求的IP位址解決州或省。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 只有在請求中出現訂單詳細資訊時才設定。 |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style=&quot;table-layout:auto&quot;}
