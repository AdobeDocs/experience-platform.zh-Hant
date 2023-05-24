---
keywords: Experience Platform；首頁；熱門主題；目標映射；目標映射
solution: Experience Platform
title: 將Adobe Target事件資料映射到XDM
description: 瞭解如何將Adobe Target事件欄位映射到在Adobe Experience Platform使用的體驗資料模型(XDM)架構。
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 目標映射欄位映射

Adobe Experience Platform允許您通過目標源連接器接收Adobe Target資料。 使用連接器時，必須將「目標」欄位中的所有資料映射到 [體驗資料模型(XDM)](../../../../xdm/home.md) 與XDM ExperienceEvent類關聯的欄位。

下表概述了體驗事件架構的欄位(*XDM ExperienceEvent欄位*)和應映射到的相應目標欄位(*目標請求欄位*)。 還提供了一些映射的附加說明。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| XDM ExperienceEvent欄位 | 目標請求欄位 | 附註 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一請求標識符 |
| **`dataSource`** |  | 已配置為「1」，用於所有客戶端。 |
| `dataSource._id` | 無法與請求一起傳遞的系統生成的值。 | 此資料源的唯一ID。 這將由建立資料源的個人或系統提供。 |
| `dataSource.code` | 無法與請求一起傳遞的系統生成的值。 | 到完整的快捷方式@id。 可以使用代碼或@id中的至少一個。 有時，此代碼稱為資料源整合代碼。 |
| `dataSource.tags` | 無法與請求一起傳遞的系統生成的值。 | 標籤用於指示應用程式如何使用給定資料源表示的別名。<br><br>範例：<br><ul><li>`isAVID`:表示分析訪問者ID的資料源。</li><li>`isCRSKey`:表示應用作CRS中鍵的別名的資料源。</li></ul>建立資料源時設定標籤，但引用給定資料源時，這些標籤也包含在管道消息中。 |
| **`timestamp`** | 事件時間戳 |
| **`channel`** | `context.channel` | 僅適用於視圖交付。 選項為&quot;web&quot;和&quot;mobile&quot;，預設值為&quot;web&quot;。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Experience CloudID(ECID)也稱為MCID，繼續用於命名空間。 |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 根據請求的IP地址解析移動運營商名稱。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （如果採用V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （如果採用V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 客戶定義環境（如dev、qa或prod）的目標內部映射。 |
| `experience.target.supplementalDataID` | 用於將目標事件與分析事件組合的標識符 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 訪問者有資格進行的活動清單（陣列） |
| `experience.target.activities[i].activityID` | 訪問者符合的任何給定活動的ID |
| `experience.target.activities[i].version` | 訪問者有資格進行的任何給定活動的版本 |
| `experience.target.activities[i].activityEvents` | 包括用戶在此事件中擊中的活動事件的詳細資訊。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 以下屬性之一 `deviceAtlas` （或NULL）: <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 隨機UUID（必需） |
| `placeContext.geo.city` | 根據請求的IP地址解析城市名稱。 |
| `placeContext.geo.countryCode` | 基於請求的IP地址解析的國家/地區代碼。 |
| `placeContext.geo.dmaId` | 根據請求的IP地址解析的指定市場區域代碼。 |
| `placeContext.geo.postalCode` | 根據請求的IP地址解析的郵遞區號。 |
| `placeContext.geo.stateProvince` | 根據請求的IP地址解決的省/市/自治區。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 僅當請求中存在訂單詳細資訊時才設定。 |
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
