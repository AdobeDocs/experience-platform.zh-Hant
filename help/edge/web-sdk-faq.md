---
title: Adobe Experience PlatformWeb SDK常見問題
description: 獲取有關Adobe Experience PlatformWeb SDK的常見問題的答案。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# 常見問答

本指南提供了有關Adobe Experience PlatformWeb SDK的常見問題的答案。

## 什麼是Adobe Experience PlatformWeb SDK?

Adobe Experience PlatformWeb SDK是客戶端JavaScript庫，它允許Adobe Experience Cloud客戶與Experience Cloud中的各種服務進行交互。

它以解決方案不可知的方式(XDM)將資料發送到Adobe Experience Platform邊緣網路，然後將資料映射到解決方案特定的格式和目標，並即時發送。

**詳細資訊**
[Adobe Summit演示](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience PlatformWeb SDK與以前的解決方案有何不同？

### Adobe Experience PlatformSDK之前

目前，您必鬚根據每個解決方案部署不同的JavaScript庫。

* 每個解決方案都有其自己的JavaScript庫、模式和域。
* 這些圖書館都不是為了彼此合作而建的。
* 跨解決方案和Adobe Experience Platform使用案例要求這些不同的庫相互依賴，從而導致部署摩擦。

儘管平台中的標籤使部署和管理這些庫變得盡可能容易，但仍存在以下問題：

* 庫大小(頁面上的Adobe代碼過多)
* 效能（站點載入時間過長）
* 針對單個使用案例的多個調用
* 在個性化調用之前等待ECID返回（導致延遲）
* 斷開的資料收集（什麼是平均資料？）
* 解決方案(A4T)之間的模式混淆
* 其他很多不太理想的事情

此外，目前沒有直接將資料發送到Adobe Experience Platform的JavaScript庫。

### 使用Adobe Experience PlatformWeb SDK

新的Web SDK將以下解決方案的資料發送到單個目標(Adobe Experience Platform邊緣網路)，並解決上述最常見的解決方案使用情形。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 訪客 ID
* Adobe Experience Platform

其他解決方案將在今年晚些時候出台。

Adobe Experience PlatformWeb SDK還可以直接將資料發送到Adobe Experience Platform。 此資料在XDM中，並映射到伺服器端解決方案架構。

## 此新Web SDK的價值是什麼？

**效能：** Web SDK比使用所有當前Adobe庫的容量小，並提供了顯著更快的頁面載入。

**簡潔性：** XDM、Web SDK、標籤、體驗邊緣、Adobe Experience Cloud解決方案和Adobe Experience Platform的結合，可建立一個易於理解且易於跟蹤的資料收集故事。

* **XDM:** 用於將資料發送到Adobe的解決方案不可知架構。 不再為躲避者或箱子添加標籤。
* **Adobe Experience PlatformWeb SDK:** 使得向Adobe Experience Platform邊緣網路發送和接收資料變得容易。
* **標籤：** 簡化站點上Web SDK（和任何其他JavaScript標籤）的部署和配置。
* **體驗邊緣：** 輕鬆將資料以所需格式路由到Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：** 實現其價值主張。

**控制項：** 因為所有資料都使用一個連接的資料流，所以您可以邏輯上跟蹤並控制資料在訪問應用程式和從應用程式訪問資料的每一毫秒中的外觀。

**現代且為未來做好準備：** Web SDK及其與體驗邊緣網路的連接使Adobe能夠大大現代化Adobe處理資料收集、個性化、同意和第三方Cookie的未來的方式。 (它啟用由Adobe管理的第一方域。)

**價值實現時間：** Adobe已經努力（並將繼續），以盡可能輕鬆地通過標籤部署Web SDK並將客戶端資料映射到XDM。 完成該工作後，所有其他Adobe解決方案和Adobe Experience Platform服務都可以開啟或關閉伺服器端。 例如，如果您正在將此功能用於Adobe Analytics，並且要開啟目標或Experience Platform，則只需在Datastream配置上翻轉，並點亮這些使用情形。

## 什麼是合金？

Alloy是Adobe Experience PlatformWeb SDK的代碼名。 它在SDK的原始碼和檔案名中使用，但Adobe Experience PlatformWeb SDK是正式名稱。

## 客戶是否需要購買Adobe Experience Platform [!DNL Web SDK]?

不可以。 任何Adobe數字型驗客戶都可以免費使用Adobe Experience PlatformWeb SDK。 希望使用 [!DNL Web SDK] 需要配置在資料收集UI或Experience PlatformUI中建立架構、資料集、標識命名空間和資料流的權限。

有關配置這些權限的詳細資訊，請參閱我們的文檔 [資料收集權限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en)。

## 誰應使用Web SDK?

Adobe Experience PlatformWeb SDK已開發給以下人員：

* Adobe Experience Platform用戶
   * 如果您需要直接從設備向Adobe Experience Platform發送資料，則正式建議使用此方法。
   * Adobe知道，如果客戶已經擁有了Adobe Analytics，則使用Adobe Analytics連接器會更快，但這不是資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客戶應從新的Web SDK開始，而不應使用舊版庫。
   * 希望獲得盡可能最佳化實施的現有客戶應使用新的Web SDK。


## 如何獲得使用Adobe Experience PlatformWeb SDK的權限？

Web SDK目前可供一般公眾使用，可用於向Adobe Experience Cloud產品發送資料。 向第三方解決方案發送資料的能力將在不久的將來出現。 SDK不收費，由Adobe免費托管。 如果需要，您可以免費下載並將其托管在您自己的伺服器上。 平台Web SDK需要訪問Datastream配置和Adobe Experience PlatformXDM架構構建器，以便Adobe的伺服器正確處理來自SDK的入站資料。 如果您想獲得訪問權限，請與Adobe帳戶團隊聯繫以啟動請求流程。

## Web SDK當前支援哪些使用案例？

Web SDK正在快速發展。 正在處理更多使用案例。 您可以找到 [此處當前支援的使用案例清單。](https://github.com/adobe/alloy/projects/5)

## 當前客戶是否必須重新標籤其站點？

視情況而定。Adobe Experience PlatformWeb SDK可以部署為兩種不同的樣式。 將來的遷移文檔將提供更多詳細資訊。

* **只是另一個標籤：** 如果站點已標籤瞭解決方案，並且您無法重新標籤，但是您希望將資料發送到Adobe Experience Platform邊緣網路以便Experience Platform使用案例或即將發生的事件轉發功能（請參閱下面），則可以添加 `alloy.js` 標籤到站點，在該站點中，它的作用是「僅僅是另一個標籤」。

* **唯一標籤：** 如果要將Web SDK用於Experience Cloud解決方案，則必須將其用於 _全部_ 那頁的解決方案。 例如，如果您的站點已為Adobe Analytics添加標籤，並且您希望將其用於目標，則您需要將其用於兩者，以及將來的任何其他站點。

換句話說，如果您決定將Adobe Experience PlatformWeb SDK用於非解決方案使用情形，則可以使用 `alloy.js` 繼續，好像這是新的解決方案。 如果要將其用於Adobe Analytics、目標或Audience Manager，或用於應用程式使用情形，則可能必須刪除頁面上的任何舊代碼。

## 當我開始使用Alloy時，是否可以遷移ECID，以便我的網站訪問者不會開始以新訪問者的身份出現？

是，Adobe Experience PlatformWeb SDK提供了身份遷移功能。 按照中的ID遷移說明 [平台Web SDK標識文檔](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 的子菜單。

## Web SDK與標籤有何不同？

* **Experience Platform中的標籤** 管理設備代碼。 使用它們可以更輕鬆地部署代碼。 他們自由而強大。

* **Adobe Experience PlatformWeb SDK** 是新代碼的正式名稱，該代碼將由標籤部署以用於Adobe使用案例。 它也是自由而強大的。

* **`alloy.js`** 是Adobe Experience PlatformWeb SDK代碼的檔案名。

## 是否必須使用標籤來部署Web SDK?

不可以。 您可以下載 `alloy.js` 自己歸檔。

但是：

* Adobe Experience PlatformWeb SDK需要一種稱為資料流ID的東西，以便邊緣網路能夠識別流並確定如何處理資料。 此ID是在Experience Platform中建立的。 這並不意味著您必須使用UI來建立屬性或部署JavaScript代碼，但是您確實需要使用標籤來建立配置ID。

* 標籤不僅是最好的可用標籤和SDK管理器，它使部署非常容易 `alloy.js` 將資料映射到XDM模式。 如果您決定不使用標籤，則必須管理部署 `alloy.js`、執行事件處理，並在發送資料之前將其映射到XDM。 這是 _多_ 比使用標籤更困難。

* 建議您使用標籤來部署 `alloy.js`即使它是你唯一用的標籤。

## 什麼是事件轉發？

如果您使用我們的SDK並將XDM發送到體驗邊緣，這些新功能事件轉發允許您安裝新的伺服器端擴展並將資料映射到任何位置，並從我們的邊緣網路發送到任何位置。 將其視為「資料收集即服務」。 這項服務將付費，並作為Adobe Experience Platform的一部分打包。

## 什麼是CNAME或第一方域，它為什麼重要？

有關CNAME的詳細資訊，請參閱 [Adobe文檔](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience PlatformWeb SDK是否使用cookie? 如果是，它會使用什麼Cookie?

是的，目前Web SDK使用的Cookie介於一到七個之間，具體取決於您的實現。 以下是Web SDK中可能看到的Cookie清單及其使用方式：

| **名稱** | **最大時間** | **友好時代** | **說明** |
|---|---|---|---|
| **kndct_orgid標識** | 34128000 | 395 天 | 標識cookie儲存ECID以及與ECID相關的其他資訊。 |
| **kndctr_orgid_concens_check** | 7200 | 2 小時 | 此cookie儲存用戶對網站的同意偏好。 |
| **kndctr_orgid_connection** | 15552000 | 180 天 | 此基於會話的cookie指示伺服器查找同意首選項伺服器端。 |
| **kndctr_orgid_cluster** | 1800 | 30 分鐘 | 此Cookie儲存正在為當前用戶的請求提供服務的體驗邊緣區域。 該區域用在URL路徑中，以便「體驗邊緣」可將請求路由到正確的區域。 此cookie的生存期為30分鐘，因此如果用戶使用不同的IP地址連接，則可以將請求路由到最近的區域。 |
| **mbox** | 63072000 | 2 年 | 當目標遷移設定設定為true時，將顯示此cookie。 這將允許目標 [郵箱cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 由Web SDK設定。 |
| **mboxEdgeCluster** | 1800 | 30 分鐘 | 當目標遷移設定設定為true時，將顯示此cookie。 此Cookie允許Web SDK將正確的邊緣群集與at.js通信，以便當用戶在站點中導航時，目標配置檔案可以保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 僅當啟用Adobe Experience PlatformWeb SDK上的ID遷移時，才會顯示此cookie。 此Cookie在轉換到Web SDK時有所幫助，而站點的某些部分仍在使用visitor.js。 查看 [idMigrationEnabled文檔](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) 來查看有關此設定的詳細資訊。 |

使用Web SDK時，邊緣網路會設定上面的一個或多個Cookie。 邊緣網路將所有Cookie `secure` 和 `sameSite="none"` 屬性。

如果您的網站上當前同時有安全和非安全部分，這可能會干擾用戶標識。 當用戶從站點的安全部分導航到非安全部分時，邊緣網路生成新 `ECID` 我的請求。

## Adobe Experience PlatformWeb SDK支援哪些瀏覽器？

Adobe Experience PlatformWeb SDK設計為在最新版本的GoogleChrome、Safari、火狐、Internet Explorer 11和MicrosoftEdge Crr中以最佳方式工作。 在較舊版本的瀏覽器上使用某些功能時可能會遇到問題。

## 從哪裡可以獲取有關Adobe Experience PlatformWeb SDK的更多資訊？

* [文件](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant)
* [原始碼](https://github.com/adobe/alloy)
