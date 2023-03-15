---
keywords: Experience Platform；首頁；熱門主題；目標對應；目標對應
solution: Experience Platform
title: 將Adobe Target事件資料對應至XDM
description: 了解如何將Adobe Target事件欄位對應至Experience Data Model(XDM)結構，以便在Adobe Experience Platform中使用。
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 目標映射欄位映射

Adobe Experience Platform可讓您透過Target來源連接器內嵌Adobe Target資料。 使用連接器時，來自Target欄位的所有資料都必須對應至 [Experience Data Model(XDM)](../../../../xdm/home.md) 與XDM ExperienceEvent類別相關聯的欄位。

下表概述體驗事件結構的欄位(*XDM ExperienceEvent欄位*)和對應的Target欄位，應該對應到(*Target請求欄位*)。 也提供一些對應的其他附註。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| XDM ExperienceEvent欄位 | Target請求欄位 | 附註 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一請求識別碼 |
| **`dataSource`** |  | 針對所有用戶端設為「1」。 |
| `dataSource._id` | 無法與要求一併傳入的系統產生值。 | 此資料來源的唯一ID。 這將由建立資料來源的個人或系統提供。 |
| `dataSource.code` | 無法與要求一併傳入的系統產生值。 | 快速鍵到完整@id。 可以使用代碼或@id中的至少一個。 有時，此程式碼稱為資料來源整合程式碼。 |
| `dataSource.tags` | 無法與要求一併傳入的系統產生值。 | 標籤用於指示應用程式如何使用給定資料源表示的別名。<br><br>範例：<br><ul><li>`isAVID`:代表Analytics訪客ID的資料來源。</li><li>`isCRSKey`:代表應作為CRS中索引鍵之別名的資料來源。</li></ul>標籤會在建立資料來源時設定，但在參考指定資料來源時，標籤也會包含在管道訊息中。 |
| **`timestamp`** | 事件時間戳記 |
| **`channel`** | `context.channel` | 僅適用於檢視傳送。 選項為「web」和「mobile」，預設值為「web」。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Experience CloudID(ECID)也稱為MCID，會繼續用於命名空間。 |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 根據請求的IP位址解析行動電信業者名稱。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （若為V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （若為V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 適用於客戶定義環境（例如開發、qa或prod）的Target內部對應。 |
| `experience.target.supplementalDataID` | 用來將Target事件與Analytics事件結合的識別碼 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 訪客符合資格的活動清單（陣列） |
| `experience.target.activities[i].activityID` | 訪客符合資格的任何指定活動的ID |
| `experience.target.activities[i].version` | 訪客符合資格的任何指定活動的版本 |
| `experience.target.activities[i].activityEvents` | 包含使用者因此事件而點擊的活動事件詳細資料。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 下列屬性之一： `deviceAtlas` （或NULL）: <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 隨機UUID（必要） |
| `placeContext.geo.city` | 根據請求的IP位址解析的城市名稱。 |
| `placeContext.geo.countryCode` | 根據請求的IP位址解析的國家/地區代碼。 |
| `placeContext.geo.dmaId` | 根據請求的IP位址解析的指定市場區域代碼。 |
| `placeContext.geo.postalCode` | 根據請求的IP位址解析的郵遞區號。 |
| `placeContext.geo.stateProvince` | 根據請求的IP位址解決的州或省。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 只有在請求中有訂單詳細資料時才設定。 |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
