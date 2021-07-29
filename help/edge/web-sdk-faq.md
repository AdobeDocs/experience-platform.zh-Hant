---
title: Adobe Experience Platform Web SDK常見問題集
description: 取得Adobe Experience Platform Web SDK常見問題的解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 1%

---

# 常見問答

本指南提供經常詢問關於Adobe Experience Platform Web SDK問題的回答。

## 什麼是Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。

它會以不受解決方案限制的方式(XDM)傳送資料至Adobe Experience Platform Edge Network，然後由Edge Network將資料對應至解決方案的特定格式和目的地，並即時傳送資料。

**更多**
[資訊Adobe Summit簡報](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

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

**簡單性：** XDM、Web SDK、標籤、Experience Edge、Adobe Experience Cloud解決方案和Adobe Experience Platform的結合，打造了簡單易懂且易於追蹤的資料收集故事。

* **XDM:** 您用來傳送資料至Adobe的解決方案不受限制結構。不再為eVar或mbox進行標籤。
* **Adobe Experience Platform Web SDK:** 讓您輕鬆將資料傳送至Adobe Experience Platform邊緣網路。
* **標籤：** 簡化網站上Web SDK（及任何其他JavaScript標籤）的部署和設定。
* **Experience Edge:** 以所需格式輕鬆將資料路由至Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：** 啟用其價值主張。

**控制：** 因為所有資料都使用單一且連接的資料流，所以您可以邏輯上遵循並控制資料在歷程中每毫秒、應用程式之間的外觀。

**現代且面向未來：** Web SDK及其與Experience Edge Network的連線已讓Adobe大幅導入Adobe處理資料收集、個人化、同意和第三方Cookie未來的方式。(它會啟用由Adobe管理的第一方網域。)

**實現價值：** Adobe已付諸努力（並將持續），透過標籤輕鬆部署Web SDK，並將用戶端資料對應至XDM。完成該工作後，所有其他Adobe解決方案和Adobe Experience Platform服務都可在伺服器端開啟或關閉。 例如，如果您將此功能用於Adobe Analytics，而且您想要開啟Target或Experience Platform，您只需扳動Datastream設定的切換開關，然後點亮這些使用案例。

## 什麼是Alloy?

Alloy是Adobe Experience Platform Web SDK的程式碼名稱。 這會在SDK的原始碼和檔案名稱中使用，但Adobe Experience Platform Web SDK是官方名稱。

## 客戶是否需要購買Adobe Experience Platform才能使用Web SDK?

不可以。任何Adobe數位體驗客戶皆可使用。 完全自由。 任何想要使用Web SDK的客戶都可在Adobe Experience Platform UI中建立結構描述和資料集。

## Web SDK該由誰使用？

Adobe Experience Platform Web SDK已開發給下列人員：

* Adobe Experience Platform使用者

   如果您需要直接從裝置將資料傳送至Adobe Experience Platform，這是官方建議的方式。

   Adobe知道，如果客戶已有Adobe Analytics，則使用Adobe Analytics連接器會更快，但這並非資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶

   Adobe Analytics、Adobe Audience Manager和Adobe Target的新客戶應從新的Web SDK開始，而不要使用舊版程式庫。

   想要盡可能獲得最佳化實作的現有客戶應使用新的Web SDK。


## 如何存取Adobe Experience Platform Web SDK?

Web SDK目前可供一般大眾使用，且可用於傳送資料至Adobe Experience Cloud產品。 將資料傳送至協力廠商解決方案的功能即將推出。 SDK是免費的、由Adobe免費托管，且可以下載，讓您可以視需要免費在自己的伺服器上托管。 Platform Web SDK需要存取Datastream設定和Adobe Experience Platform XDM結構產生器，以便Adobe的伺服器正確處理來自SDK的傳入資料。 若想取得存取權，請聯絡客戶成功經理(CSM)以開始要求程式。

## Web SDK目前支援哪些使用案例？

Web SDK正在快速發展。 正在處理更多使用案例。 您可以在此處找到[目前支援的使用案例清單。](https://github.com/adobe/alloy/projects/5)

## 目前的客戶是否必須重新標籤其網站？

視情況而定。Adobe Experience Platform Web SDK可部署為兩種不同的樣式。 未來的移轉檔案將提供其他詳細資訊。

* **只是另一個標籤：** 如果網站已經經過解決方案的標籤，且您無法重新標籤，但您想要傳送資料至Adobe Experience Platform Edge Network，以供Experience Platform使用案例或即將推出的事件轉送功能（請參閱下方），您可以將標籤新增至網站，其作為「其他標籤」運作。 `alloy.js` 

* **唯一的標籤：** 如果您想要將Web SDK用於Experience Cloud解決方案，則必須將其用於該 __ 頁面上的所有解決方案。例如，如果您的網站已經被標籤為Adobe Analytics，而您想要將其用於Target，則您需要同時將其用於Target，以及未來的任何其他項目。

換言之，如果您決定將Adobe Experience Platform Web SDK用於非解決方案使用案例，則可以使用`alloy.js`標籤網站，並將其視為新解決方案而繼續移動。 如果您想要將其用於Adobe Analytics、Target或Audience Manager，或應用程式使用案例，您可能必須移除頁面上的任何舊版程式碼。

## 我可以在開始使用Alloy時移轉ECID，以免我的網站訪客開始顯示為新訪客嗎？

是的，Adobe Experience Platform Web SDK提供身分移轉功能。 如需詳細資訊，請依照[平台Web SDK身分檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration)中的指示移轉ID。

## Web SDK與標籤有何不同？

* **Experience Platform中的標** 記可管理裝置程式碼。使用它們可更輕鬆部署程式碼。 它們是自由而強大的。

* **Adobe Experience Platform Web** SDK是新程式碼的官方名稱，由Adobe使用案例的標籤所部署。它也是自由而強大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK程式碼的檔案名稱。

## 我是否必須使用標籤來部署Web SDK?

不可以。您可以自行下載`alloy.js`檔案。

不過：

* Adobe Experience Platform Web SDK需要資料流ID，這樣邊緣網路就能識別資料流，並決定該如何處理資料。 此ID是在Experience Platform內建立。 這並不表示您必須使用資料收集UI來建立屬性或部署JavaScript程式碼，但您確實需要使用標籤來建立設定ID。

* 標籤不僅是最佳的可用標籤和SDK管理員，還可讓您輕鬆部署`alloy.js`，並將資料對應至XDM結構。 如果您決定不使用標籤，則必須先管理`alloy.js`部署、事件，以及將資料對應至XDM，才能傳送。 這是比使用標籤更困難的&#x200B;_許多_&#x200B;程式。

* 建議您使用標籤來部署`alloy.js`，即使這是您唯一使用該標籤的標籤亦然。

## 什麼是事件轉送？

如果您使用SDK並將XDM傳送至Experience Edge，這些新功能事件轉送可讓您安裝新的伺服器端擴充功能，並將資料對應至任何位置，並從我們的邊緣網路傳送至任何位置。 將其視為「資料收集即服務」。  這項服務需支付成本，並隨Adobe Experience Platform提供整合功能。

## 什麼是CNAME或第一方網域？為什麼這很重要？

[Adobe檔案](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)中提供有關CNAME的詳細資訊

## Adobe Experience Platform Web SDK是否使用Cookie? 如果是，它會使用哪些Cookie?

是的，目前Web SDK使用的Cookie介於1到4個之間，端視您的實作而定。 以下為Web SDK中可能看到的4個Cookie清單及其使用方式：

**kndct_orgid_identity:** 身分識別Cookie可用來儲存ECID，以及一些與ECID相關的其他資訊。

**kndctr_orgid_consent:** 此cookie會儲存使用者對網站的同意偏好設定。

**kndctr_orgid_personalization:** 此cookie包含Adobe Target用來個人化網頁的工作階段資訊。

**kndctr_orgid_consentcheck:** 此以工作階段為基礎的cookie會訊息伺服器端查詢同意偏好設定。

## Adobe Experience Platform Web SDK支援哪些瀏覽器？

Adobe Experience Platform Web SDK的設計，可在最新版Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium中以最佳方式運作。 您在舊版瀏覽器上使用某些功能時可能遇到問題。

## 我可以在何處取得Adobe Experience Platform Web SDK的詳細資訊？

* [文件](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [原始碼](https://github.com/adobe/alloy)
