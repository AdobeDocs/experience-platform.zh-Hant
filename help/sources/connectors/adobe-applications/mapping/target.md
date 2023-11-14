---
solution: Experience Platform
title: 將Adobe Target事件資料對應至XDM
description: 瞭解如何將Adobe Target事件欄位對應到體驗資料模型(XDM)結構描述，以便在Adobe Experience Platform使用。
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 目標對應欄位對應

下表概述Experience Data Model (XDM) Experience Event結構描述的欄位，以及對應到Adobe Target中的對應欄位。 此外，也提供部分對應的其他附註。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| XDM ExperienceEvent欄位 | Target要求欄位 | 附註 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一請求識別碼 |
| **`dataSource`** | | 設定為所有使用者端的「1」。 |
| `dataSource._id` | 系統產生的值，無法與要求一併傳入。 | 此資料來源的唯一ID。 這將由個人或建立資料來源的系統來提供。 |
| `dataSource.code` | 系統產生的值，無法與要求一併傳入。 | 完整@id的捷徑。 至少可以使用其中一個程式碼或@id。 有時候，此程式碼稱為資料來源整合程式碼。 |
| `dataSource.tags` | 系統產生的值，無法與要求一併傳入。 | 標籤可用來指出應用程式應如何使用這些別名來解譯指定資料來源所代表的別名。<br><br>範例：<br><ul><li>`isAVID`：代表Analytics訪客ID的資料來源。</li><li>`isCRSKey`：代表應在CRS中作為索引鍵使用的別名的資料來源。</li></ul>標籤會在建立資料來源時設定，但也會在參照特定資料來源時納入管道訊息中。 |
| **`timestamp`** | 事件時間戳記 |
| **`channel`** | `context.channel` | 僅適用於檢視傳遞。 選項包括「網頁」和「行動裝置」，預設值為「網頁」。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。 |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 根據請求的IP位址解析的行動電信業者名稱。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （若為V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （若為V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 適用於客戶定義環境（例如開發、qa或生產環境）的Target內部對應。 |
| `experience.target.supplementalDataID` | 用於將Target事件與Analytics事件拼接的識別碼 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 訪客已符合資格的活動清單（陣列） |
| `experience.target.activities[i].activityID` | 訪客符合資格的任何指定活動的ID |
| `experience.target.activities[i].version` | 訪客符合資格的任何特定活動的版本 |
| `experience.target.activities[i].activityEvents` | 包含使用者透過此事件點選的活動事件的詳細資料。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 下列屬性之一 `deviceAtlas` （或NULL）： <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 隨機UUID （必要） |
| `placeContext.geo.city` | 根據請求的IP位址解析的城市名稱。 |
| `placeContext.geo.countryCode` | 根據請求的IP位址解析的國家代碼。 |
| `placeContext.geo.dmaId` | 已根據請求的IP位址解析指定的市場區碼。 |
| `placeContext.geo.postalCode` | 根據請求的IP位址解析的郵遞區號。 |
| `placeContext.geo.stateProvince` | 根據請求的IP位址解析的州或省。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | 只有在請求中存在訂單詳細資料時才會設定。 |
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
