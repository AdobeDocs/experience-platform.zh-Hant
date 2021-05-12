---
title: Adobe Experience Platform網頁SDK常見問答集
description: 取得有關Adobe Experience Platform網頁SDK的常見問題解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 5ead9dc72b8b9fe89e0a1bc8365ceff8affd3c85
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 2%

---

# 常見問題集

本指南提供有關Adobe Experience Platform網頁SDK常問之問題的解答。

## 什麼是Adobe Experience Platform網頁SDK?

Adobe Experience Platform網頁SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。

它以解決方案不可知的方式(XDM)傳送資料至Adobe Experience Platform邊緣網路，然後將資料對應至解決方案特定的格式和目的地，並即時傳送。

**更多資**
[訊Adobe峰會簡報](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform網頁SDK與先前解決方案有何不同？

### 在Adobe Experience PlatformSDK之前

目前，您必鬚根據每個解決方案部署不同的JavaScript程式庫。

* 每個解決方案都有其專屬的JavaScript程式庫、架構和網域。
* 這些圖書館都不是為了彼此合作而建的。
* 跨解決方案和Adobe Experience Platform的使用案例要求這些不同的程式庫彼此依存，造成部署摩擦。

儘管Adobe Experience Platform Launch使部署和管理這些庫盡可能容易，但仍存在以下問題：

* 程式庫大小(頁面上的Adobe程式碼太多)
* 效能（網站載入時間太長）
* 單一使用案例的多次呼叫
* 在個人化呼叫前等待ECID傳回（導致延遲）
* 已斷開的資料收集（什麼是evar?）
* 解決方案間的架構混淆(A4T)
* 其他許多不那麼好的東西

此外，目前沒有直接將資料傳送至Adobe Experience Platform的JavaScript程式庫。

### 使用Adobe Experience Platform網頁SDK

新的Web SDK會將下列解決方案的資料傳送至單一目的地(Adobe Experience Platform邊緣網路)，並解決最常見的上述解決方案使用案例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

今年晚些時候，其他解決方案將陸續推出。

Adobe Experience Platform網頁SDK也可以直接傳送資料至Adobe Experience Platform。 此資料位於XDM中，並會對應至伺服器端解決方案架構。

## 此全新Web SDK有何價值？

**效能：** 網頁SDK比使用所有目前的Adobe程式庫都小，並可大幅加快頁面載入。

**簡單性：** 結合XDM、Web SDK、Experience Platform Launch、Experience Edge、Adobe Experience Cloud解決方案和Adobe Experience Platform，可建立簡單易懂且易於追蹤的資料收集故事。

* **XDM：用** 於向Adobe發送資料的不確定解決方案模式。evar或mbox不再加上標籤。
* **Adobe Experience Platform網頁SDK:** 讓您輕鬆傳送和接收資料至Adobe Experience Platform邊緣網路。
* **Experience Platform Launch:** 簡化網站上Web SDK（及任何其他JavaScript標籤）的部署與設定。
* **體驗邊緣：輕** 松將資料以所需格式傳送至Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：** 啟用其價值主張。

**控制：** 由於所有資料都使用單一且連接的資料串流，因此您可以邏輯上跟隨並控制資料在資料進出應用程式時的每毫秒外觀。

**現代且面向未來：** Web SDK及其與Experience Edge Network的連線讓Adobe得以大幅最新化Adobe處理資料收集、個人化、同意和第三方Cookie的未來。(它啟用由Adobe管理的第一方域。)

**價值時間：** Adobe已努力（並將繼續）透過Experience Platform Launch將用戶端資料對應至XDM，讓部署Web SDK變得盡可能簡單。完成此項工作後，所有其他Adobe解決方案和Adobe Experience Platform服務都可在伺服器端開啟或關閉。 例如，如果您將此項用於Adobe Analytics，而您想要開啟Target或Experience Platform，您只需在Datastream設定上切換，並指出這些使用案例。

## 什麼是合金？

Alloy是Adobe Experience Platform網頁SDK的程式碼名稱。 它用於SDK的原始碼和檔案名稱中，但Adobe Experience Platform網頁SDK是正式名稱。

## 客戶是否需要購買Adobe Experience Platform才能使用Web SDK?

否。任何Adobe數位體驗客戶都能使用。 完全自由。 任何想要使用Web SDK的客戶都可存取在Adobe Experience PlatformUI中建立結構描述和資料集。

## Web SDK應由誰使用？

Adobe Experience Platform網頁SDK已開發給以下人員：

* Adobe Experience Platform用戶

   如果您需要直接從裝置傳送資料至Adobe Experience Platform，這是官方推薦的方式。

   Adobe知道，如果客戶已經擁有Adobe Analytics，使用Adobe Analytics連接器會更快，但這不是資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶

   新Adobe Analytics、Adobe Audience Manager和Adobe Target客戶應從新的Web SDK開始，而不要使用舊版程式庫。

   想要盡可能獲得最佳實作的現有客戶應使用新的Web SDK。


## 我要如何取得使用Adobe Experience Platform網頁SDK的存取權？

Web SDK目前可供一般大眾使用，可用來傳送資料至Adobe Experience Cloud產品。 將資料傳送至協力廠商解決方案的能力即將推出。 SDK是免費的，由Adobe免費代管，而且可以下載，如此您就可以視需要免費在自己的伺服器上代管。 平台Web SDK需要存取資料串流組態和Adobe Experience PlatformXDM架構建立器，以讓Adobe的伺服器正確處理來自SDK的傳入資料。 如果您想要取得存取權，請連絡您的客戶成功經理(CSM)以開始申請程式。

## 網頁SDK目前支援哪些使用案例？

Web SDK正在快速發展。 目前正在處理更多使用案例。 您可以在這裡找到[目前支援的使用案例清單。](https://github.com/adobe/alloy/projects/5)

## 目前的客戶是否必須重新標籤其網站？

視情況而定。Adobe Experience Platform網頁SDK可部署為兩種不同的樣式。 未來的移轉檔案將提供其他詳細資訊。

* **只有另一個標籤：**  `alloy.js` 如果網站已針對解決方案加上標籤，而您無法重新標籤，但您想要傳送資料至Adobe Experience Platform邊緣網路以供Experience Platform使用案例或即將推出的Experience Platform Launch伺服器端功能（請參閱下文），您可將標籤新增至網站，其作用就是「其他標籤」。

* **唯一的標籤：** 如果您想要將Web SDK用於Experience Cloud解決方案，則必須將它用於該 __ 頁上的所有解決方案。例如，如果您的網站已經標籤為Adobe Analytics，而您想將它用於Target，則您必須同時用於這兩個網站，以及未來其他網站。

換言之，如果您決定將Adobe Experience Platform網頁SDK用於非解決方案使用案例，您可以使用`alloy.js`來標籤網站，並將它當成新的解決方案。 如果您想要將它用於Adobe Analytics、Target或Audience Manager，或應用程式使用案例，則可能必須移除頁面上的任何舊版程式碼。

## 當我開始使用Alloy時，我是否可移轉ECID，讓我的網站訪客不會開始顯示為新訪客？

是的，Adobe Experience Platform網頁SDK提供身分移轉功能。 如需詳細資訊，請依照[平台網頁SDK識別檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration)中的ID移轉指示進行。

## 網頁SDK與Adobe Experience Platform Launch有何不同？

* **Experience Platform啟** 動是裝置程式碼管理員。使用它可更輕鬆地部署程式碼。 它既自由又強大。

* **Adobe Experience Platform網** 頁SDK是新程式碼的正式名稱，由Experience Platform Launch部署以用於Adobe使用案例。它也是自由而強大的。

* **`alloy.js`** 是Adobe Experience Platform網頁SDK程式碼的檔案名稱。

## 我是否必須使用Adobe Experience Platform Launch來部署Web SDK?

否。您可以自行下載`alloy.js`檔案。

但是：

* Adobe Experience Platform網頁SDK需要稱為資料流ID的項目，讓邊緣網路可識別資料流並決定如何處理資料。 此ID是在Experience Platform Launch中建立。 這並不表示您必須使用Experience Platform Launch來建立屬性或部署JavaScript程式碼，但您確實需要使用Experience Platform Launch來建立設定ID。

* Adobe Experience Platform Launch不僅是最佳的標籤和SDK管理器，而且讓部署`alloy.js`和將資料對應至XDM架構變得十分簡單。 如果您決定不使用Experience Platform Launch，則必須先管理部署`alloy.js`、事件，然後將您的資料對應至XDM，然後再傳送。 這是一個比使用Experience Platform Launch更困難的&#x200B;_多_&#x200B;過程。

* 建議您使用Experience Platform Launch來部署`alloy.js`，即使它是您唯一使用的標籤。

## 什麼是「Adobe Experience Platform Launch伺服器端」?

2020年晚些時候，Experience Platform Launch將推出伺服器端轉送功能。 如果您使用我們的SDK並將XDM傳送至Experience Edge，這些新功能可讓您安裝新的伺服器端擴充功能，並將資料對應至任何位置，並從我們的邊緣網路傳送至任何位置。 將它視為「資料收集即服務」。  這項服務將提供收費，並作為Adobe Experience Platform的一部分提供。

## 什麼是CNAME或第一方網域，為什麼重要？

[Adobe檔案](https://docs.adobe.com/content/help/zh-Hant/id-service/using/reference/analytics-reference/cname.html)中提供有關CNAME的更多資訊

## Adobe Experience Platform網頁SDK是否使用Cookie? 如果是，它會使用哪些Cookie?

是的，目前Web SDK使用1-4個Cookie之間的任何位置（視您的實作而定）。 以下是您在Web SDK中可能看到的4個Cookie清單及其使用方式：

**kndct_orgid_identity:** 使用識別Cookie來儲存ECID，以及與ECID相關的其他資訊。

**kndctr_orgid_connency:** 此Cookie儲存使用者對網站的同意偏好。

**kndctr_orgid_personalization：此** Cookie包含Adobe Target用於個人化網頁的作業資訊。

**kndctr_orgid_consentcheck：此以會** 話為基礎的Cookie會訊息伺服器端查詢同意偏好設定。

## Adobe Experience Platform網頁SDK支援哪些瀏覽器？

Adobe Experience Platform網頁SDK的設計最適合最新版Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium。 您在舊版瀏覽器上使用某些功能時可能遇到問題。

## 我可以從哪裡取得有關Adobe Experience Platform網頁SDK的更多資訊？

* [文件](https://docs.adobe.com/content/help/zh-Hant/experience-platform/edge/home.html)
* [原始碼](https://github.com/adobe/alloy)
