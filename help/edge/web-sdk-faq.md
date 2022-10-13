---
title: Adobe Experience Platform Web SDK常見問題集
description: 取得Adobe Experience Platform Web SDK常見問題的解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 5586c788f4ae5c61b3b94f93b4180fc293d7e179
workflow-type: tm+mt
source-wordcount: '2101'
ht-degree: 2%

---

# 常見問答

本指南提供經常詢問關於Adobe Experience Platform Web SDK問題的回答。

## 什麼是Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。

它會以不受解決方案限制的方式(XDM)傳送資料至Adobe Experience Platform Edge Network，然後由Edge Network將資料對應至解決方案的特定格式和目的地，並即時傳送資料。

**更多資訊**
[Adobe Summit簡報](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK與舊版解決方案有何不同？

### 在Adobe Experience Platform SDK之前

目前，您必鬚根據每個個別解決方案部署不同的JavaScript程式庫。

* 每個解決方案都有其專屬的JavaScript程式庫、結構和網域。
* 這些程式庫都不是建置成可彼此搭配使用。
* 跨解決方案和Adobe Experience Platform使用案例需要這些不同的程式庫保持相依性，造成部署摩擦。

雖然Platform中的標籤可讓部署及管理這些程式庫盡可能輕鬆，但仍有下列問題：

* 程式庫大小(頁面上的Adobe程式碼過多)
* 效能（網站載入太長）
* 單一使用案例的多次呼叫
* 在個人化呼叫前等候ECID傳回（原因延遲）
* 已斷開的資料收集（什麼是evar？）
* 解決方案(A4T)之間的結構混淆
* 其他很多不那麼優的東西

此外，目前沒有可直接將資料傳送至Adobe Experience Platform的JavaScript程式庫。

### 使用Adobe Experience Platform Web SDK

新的Web SDK會將下列解決方案的資料傳送至單一目的地(Adobe Experience Platform邊緣網路)，並針對前述最常見的解決方案使用案例加以解決。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 訪客 ID
* Adobe Experience Platform

今年晚些時候，其他解決方案將陸續出台。

Adobe Experience Platform Web SDK也可以直接將資料傳送至Adobe Experience Platform。 此資料會以XDM格式呈現，且會對應至伺服器端解決方案架構。

## 這個新Web SDK有何價值？

**效能：** Web SDK比使用所有目前的Adobe程式庫都小，且可大幅加快頁面載入速度。

**簡單：** XDM、Web SDK、標籤、Experience Edge、Adobe Experience Cloud解決方案和Adobe Experience Platform的結合，可建立簡單易懂且易於追蹤的資料收集動態。

* **XDM:** 您用來傳送資料至Adobe的解決方案無關型結構。 不再為eVar或mbox進行標籤。
* **Adobe Experience Platform Web SDK:** 可輕鬆將資料傳送至Adobe Experience Platform Edge Network。
* **標籤：** 簡化網站上Web SDK（及任何其他JavaScript標籤）的部署和設定。
* **體驗Edge:** 以所需格式輕鬆將資料路由至Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：** 啟用其價值主張。

**控制：** 因為所有資料都使用一個連接的資料流，所以您可以邏輯上跟蹤並控制資料在到達應用程式和從應用程式到到達資料的每一毫秒的外觀。

**現代化，為未來做好準備：** Web SDK及其與Experience Edge Network的連線，讓Adobe得以大幅導入Adobe處理資料收集、個人化、同意和第三方Cookie未來的方式。 (它會啟用由Adobe管理的第一方網域。)

**值時間：** Adobe已努力（且將持續），透過標籤輕鬆部署Web SDK，並將用戶端資料對應至XDM。 完成該工作後，所有其他Adobe解決方案和Adobe Experience Platform服務都可在伺服器端開啟或關閉。 例如，如果您將此功能用於Adobe Analytics，而且您想要開啟Target或Experience Platform，您只需扳動Datastream設定的切換開關，然後點亮這些使用案例。

## 什麼是Alloy?

Alloy是Adobe Experience Platform Web SDK的程式碼名稱。 這會在SDK的原始碼和檔案名稱中使用，但Adobe Experience Platform Web SDK是官方名稱。

## 客戶是否需要購買Adobe Experience Platform才能使用 [!DNL Web SDK]?

不可以。 任何Adobe數位體驗客戶都可免費使用Adobe Experience Platform Web SDK。 希望使用 [!DNL Web SDK] 需要設定在資料收集UI或Experience PlatformUI中建立結構、資料集、身分命名空間及資料流的適當權限。

如需設定這些權限的詳細資訊，請參閱 [資料收集權限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Web SDK該由誰使用？

Adobe Experience Platform Web SDK已開發給下列人員：

* Adobe Experience Platform使用者
   * 如果您需要直接從裝置將資料傳送至Adobe Experience Platform，這是官方建議的方式。
   * Adobe知道，如果客戶已有Adobe Analytics，則使用Adobe Analytics連接器會更快，但這並非資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶
   * Adobe Analytics、Adobe Audience Manager和Adobe Target的新客戶應從新的Web SDK開始，而不要使用舊版程式庫。
   * 想要盡可能獲得最佳化實作的現有客戶應使用新的Web SDK。


## 如何存取Adobe Experience Platform Web SDK?

Web SDK目前可供一般大眾使用，且可用於傳送資料至Adobe Experience Cloud產品。 將資料傳送至協力廠商解決方案的功能即將推出。 SDK是免費的、由Adobe免費托管，且可以下載，讓您可以視需要免費在自己的伺服器上托管。 Platform Web SDK需要存取Datastream設定和Adobe Experience Platform XDM結構產生器，以便Adobe的伺服器正確處理來自SDK的傳入資料。 若想取得存取權，請聯絡客戶成功經理(CSM)以開始要求程式。

## Web SDK目前支援哪些使用案例？

Web SDK正在快速發展。 正在處理更多使用案例。 您可以找到 [此處目前支援的使用案例清單。](https://github.com/adobe/alloy/projects/5)

## 目前的客戶是否必須重新標籤其網站？

視情況而定。Adobe Experience Platform Web SDK可部署為兩種不同的樣式。 未來的移轉檔案將提供其他詳細資訊。

* **只是另一個標籤：** 如果網站已經經過解決方案的標籤，且您無法重新標籤，但您想要將資料傳送至Adobe Experience Platform Edge Network，以供Experience Platform使用案例或即將推出的事件轉送功能（請參閱下方），您可以新增 `alloy.js` 標籤至網站，其作用就像「其他標籤」。

* **唯一的標籤：** 如果您想要將Web SDK用於Experience Cloud解決方案，則必須將其用於 _all_ 的解決方案。 例如，如果您的網站已經被標籤為Adobe Analytics，而您想要將其用於Target，則您需要同時將其用於Target，以及未來的任何其他項目。

換言之，如果您決定將Adobe Experience Platform Web SDK用於非解決方案的使用案例，您可以使用 `alloy.js` 再繼續，就像是新的解決方案。 如果您想要將其用於Adobe Analytics、Target或Audience Manager，或應用程式使用案例，您可能必須移除頁面上的任何舊版程式碼。

## 我可以在開始使用Alloy時移轉ECID，以免我的網站訪客開始顯示為新訪客嗎？

是的，Adobe Experience Platform Web SDK提供身分移轉功能。 請依照 [Platform Web SDK身分檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 以取得更多詳細資訊。

## Web SDK與標籤有何不同？

* **Experience Platform** 管理裝置程式碼。 使用它們可更輕鬆部署程式碼。 它們是自由而強大的。

* **Adobe Experience Platform Web SDK** 是新程式碼的官方名稱，由Adobe使用案例的標籤所部署。 它也是自由而強大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK程式碼的檔案名稱。

## 我是否必須使用標籤來部署Web SDK?

不可以。 您可以下載 `alloy.js` 自己歸檔。

不過：

* Adobe Experience Platform Web SDK需要資料流ID，這樣邊緣網路就能識別資料流，並決定該如何處理資料。 此ID是在Experience Platform內建立。 這並不表示您必須使用UI來建立屬性或部署JavaScript程式碼，但您確實需要使用標籤來建立設定ID。

* 標籤不僅是最佳的可用標籤和SDK管理員，還可讓您輕鬆部署 `alloy.js` 並將資料對應至XDM結構。 如果您決定不使用標籤，則必須管理部署 `alloy.js`、執行事件，以及在傳送資料前將資料對應至XDM。 這是 _mod_ 比使用標籤更難的程式。

* 建議您使用標籤來部署 `alloy.js`，即使這是您唯一使用的標籤。

## 什麼是事件轉送？

如果您使用SDK並將XDM傳送至Experience Edge，這些新功能事件轉送可讓您安裝新的伺服器端擴充功能，並將資料對應至任何位置，並從我們的邊緣網路傳送至任何位置。 將其視為「資料收集即服務」。 這項服務需支付成本，並隨Adobe Experience Platform提供整合功能。

## 什麼是CNAME或第一方網域？為什麼這很重要？

如需CNAME的詳細資訊，請參閱 [Adobe檔案](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK是否使用Cookie? 如果是，它會使用哪些Cookie?

是的，根據您的實作，目前Web SDK使用的Cookie介於1到7個之間。 以下是您在Web SDK中可能看到的Cookie清單及其使用方式：

| **名稱** | **maxAge** | **友善年齡** | **說明** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 身分Cookie會儲存ECID，以及與ECID相關的其他資訊。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小時 | 此Cookie會儲存使用者對網站的同意偏好設定。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此工作階段型Cookie會指示伺服器尋找同意偏好設定伺服器端。 |
| **kndctr_orgid_cluster** | 1800 | 30 分鐘 | 此Cookie會儲存為目前使用者請求提供服務的Experience Edge區域。 該區域會用於URL路徑中，以便Experience Edge將請求路由至正確的區域。 此Cookie的存留期為30分鐘，因此如果使用者連線不同的IP位址，請求可路由至最接近的地區。 |
| **mbox** | 63072000 | 2 年 | 當Target移轉設定設為true時，就會顯示此Cookie。 這將允許Target [mbox cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 設定。 |
| **mboxEdgeCluster** | 1800 | 30 分鐘 | 當Target移轉設定設為true時，就會顯示此Cookie。 此Cookie可讓Web SDK將正確的邊緣叢集通訊給at.js，讓使用者在跨網站導覽時，Target設定檔可保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 只有在啟用Adobe Experience Platform Web SDK上的ID移轉時，才會顯示此Cookie。 當網站的某些部分仍在使用visitor.js時，此Cookie在轉換至Web SDK時會有所幫助。 請參閱 [idMigrationEnabled檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) 以深入了解此設定。 |

使用Web SDK時，邊緣網路會設定上述一或多個Cookie。 邊緣網路會以 `secure` 和 `sameSite="none"` 屬性。

如果您的網站上目前同時有安全和非安全區段，這可能會干擾使用者識別。 當使用者從網站的安全區段導覽至不安全區段時，邊緣網路會產生新的 `ECID` 和請求。

## Adobe Experience Platform Web SDK支援哪些瀏覽器？

Adobe Experience Platform Web SDK的設計，可在最新版Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium中以最佳方式運作。 您在舊版瀏覽器上使用某些功能時可能遇到問題。

## 我可以在何處取得Adobe Experience Platform Web SDK的詳細資訊？

* [文件](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [原始碼](https://github.com/adobe/alloy)
