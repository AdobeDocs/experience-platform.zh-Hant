---
title: 網頁SDK常見問答集
seo-title: Adobe Experience Platform網頁SDK常見問答集
description: 有關Adobe Experience Platform Web SDK的常見問題
seo-description: 有關Adobe Experience Platform Web SDK的常見問題
translation-type: tm+mt
source-git-commit: f51513e66945c41d06f12f4ac8f05ddad0d32898
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 2%

---


# 常見問題集

本常見問答集包含Adobe Web SDK/

## 什麼是Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。

它會以解決方案不可知的方式(XDM)傳送資料至Adobe Experience Platform Edge Network，然後將資料對應至解決方案特定的格式和目的地，並即時傳送。

**更多資訊**[Adobe峰會簡報](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK與舊版解決方案有何不同？

### 在Adobe Experience Platform SDK推出之前

目前，您必鬚根據每個解決方案部署不同的JavaScript程式庫。

* 每個解決方案都有其專屬的JavaScript程式庫、架構和網域。
* 這些圖書館都不是為了彼此合作而建的。
* 跨解決方案與Adobe Experience Platform使用案例需要這些不同的程式庫彼此依存，造成部署摩擦。

雖然Adobe Experience Platform Launch讓部署和管理這些程式庫變得盡可能簡單，但仍有下列問題：

* 資料庫大小（頁面上的Adobe程式碼太多）
* 效能（網站載入時間太長）
* 單一使用案例的多次呼叫
* 在個人化呼叫前等待ECID傳回（導致延遲）
* 已斷開的資料收集（什麼是evar?）
* 解決方案間的架構混淆(A4T)
* 其他許多不那麼好的東西

此外，目前沒有直接將資料傳送至Adobe Experience Platform的JavaScript程式庫。

### 使用Adobe Experience Platform Web SDK

新的Web SDK會將下列解決方案的資料傳送至單一目的地(AEP Edge Network)，並解決最常見的上述解決方案使用案例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

今年晚些時候，其他解決方案將陸續推出。

Adobe Experience Platform Web SDK也可以直接將資料傳送至Adobe Experience Platform。 此資料位於XDM中，並會對應至伺服器端解決方案架構。

## 此全新Web SDK有何價值？

**效能：** 網頁SDK比使用所有目前的Adobe程式庫都小，並可大幅加快頁面載入。

**簡單：** XDM、Web SDK、Launch、Experience Edge、Adobe Experience Cloud解決方案與Adobe Experience Platform的結合，可建立簡單明瞭且易於追蹤的資料收集故事。

* **XDM:** 您用來傳送資料至Adobe的解決方案不可知型架構。 evar或mbox不再加上標籤。
* **網頁SDK:** 讓您輕鬆將資料傳送及接收至Adobe Experience Platform Edge Network。
* **啟動：** 簡化網站上Web SDK（及任何其他JavaScript標籤）的部署與設定。
* **體驗優勢：** 輕鬆將資料以所需格式傳送至Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：** 實現其價值主張。

**控制：** 由於所有資料都使用單一且連接的資料串流，因此您可以邏輯上跟隨並控制資料在資料進出應用程式時的每毫秒外觀。

**現代化，面向未來：** Web SDK及其與Experience Edge Network的連線，讓Adobe得以大幅最新化Adobe處理資料收集、個人化、同意及第三方Cookie的未來。 （它可啟用由Adobe管理的第一方網域。）

**價值時間：** Adobe已盡力（並將繼續）透過Launch部署Web SDK，並將用戶端資料對應至XDM。  完成這項工作後，所有其他Adobe解決方案和Adobe Experience Platform服務都可在伺服器端開啟或關閉。 例如，如果您將此功能用於Adobe Analytics，而您想要開啟Target或Experience Platform，您只需在Experience Edge組態上切換，並指出這些使用案例。

## 什麼是 `alloy.js`?

`Alloy.js` 是Adobe Experience Platform Web SDK的檔案名稱。 Adobe Experience Platform Web SDK是正式名稱，但許多開發人員稱它為「合金」。

## 客戶是否需要購買Adobe Experience Platform才能使用Web SDK?

不能。任何Adobe Digital Experience客戶都能使用它。 完全自由。 任何想要使用Web SDK的客戶都可存取Adobe Experience Platform UI中建立結構描述和資料集。

## Web SDK應由誰使用？

Adobe Experience Platform Web SDK是專為下列人員所開發：

* Adobe Experience Platform使用者

   如果您需要直接從裝置傳送資料至Adobe Experience Platform，這是官方推薦的方式。

   Adobe知道，如果客戶已擁有Adobe Analytics，使用Adobe Analytics連接器會更快，但這並非資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶

   新的Adobe Analytics、Adobe Audience Manager和Adobe Target客戶應從新的Web SDK開始，而不要使用舊版程式庫。

   想要盡可能獲得最佳實作的現有客戶應使用新的Web SDK。


## 我要如何取得開始使用Adobe Experience Platform Web SDK的存取權？

Web SDK目前可供一般大眾使用，可用來傳送資料至Adobe Experience Cloud產品。 將資料傳送至協力廠商解決方案的能力即將推出。 如果您想要取得Web SDK的存取權，請連絡您的CSM以開始申請程式。

## 網頁SDK目前支援哪些使用案例？

Web SDK正在快速發展。 目前正在處理更多使用案例。 您可以在此處 [找到目前支援的使用案例清單。](https://github.com/adobe/alloy/projects/5)

## 目前的客戶是否必須重新標籤其網站？

視情況而定。Adobe Experience Platform Web SDK可部署為兩種不同的樣式。 未來的移轉檔案將提供其他詳細資訊。

* **只需另一個標籤：** 如果網站已針對解決方案加上標籤，而您無法重新標籤，但您想要將資料傳送至Adobe Experience Platform Edge Network for Experience Platform使用案例或即將推出的Launch伺服器端功能（請參閱下面），您可將標籤新增至網站，其中它標籤只能當成「其他標籤」。 `alloy.js`

* **唯一的標籤：** 如果您想要將Web SDK用於Experience Cloud解決方案，則必須將它用於該頁 _面上_ 的所有解決方案。 例如，如果您的網站已經標籤為Analytics，而您想要將它用於Target，則您必須同時用於Analytics，以及日後其他任何網站。

換言之，如果您決定將Adobe Experience Platform Web SDK用於非解決方案使用案例，您可以在網站上加上標籤， `alloy.js` 並將它當成新的解決方案。 如果您想要將它用於Adobe Analytics、Target或Audience Manager，或應用程式使用案例，則可能必須移除頁面上的任何舊版程式碼。

## 當我開始使用Alloy時，我是否可移轉ECID，讓我的網站訪客不會開始顯示為新訪客？

是的，Adobe Experience Platform Web SDK提供身分移轉功能。 請依照本檔案中的 [指示](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) ，取得詳細資訊。

## Web SDK與Adobe Experience Platform Launch有何不同？

* **Launch** 是裝置程式碼管理員。 使用它可更輕鬆地部署程式碼。 它既自由又強大。

* **Adobe Experience Platform Web SDK** 是Launch for Adobe使用案例所部署之新程式碼的正式名稱。 它也是自由而強大的。

* **`alloy.js`** 是Adobe Experience Platform網頁SDK程式碼的檔案名稱。

## 我是否必須使用Adobe Experience Platform Launch來部署Web SDK?

不能。您可以自行下載 `alloy.js` 檔案。

但是：

* Adobe Experience Platform Web SDK需要稱為Experience Edge組態ID的項目，讓邊緣網路可識別串流並決定如何處理資料。 此ID是在Launch中建立的。 這並不表示您必須使用Launch來建立屬性或部署JavaScript程式碼，但您確實需要使用Launch來建立設定ID。

* Adobe Experience Platform Launch不僅是最佳的標籤和SDK管理員，還讓您輕鬆部署資料並將資料 `alloy.js` 對應至XDM架構。 如果您決定不使用Launch，則必須先管理資料的部署、 `alloy.js`事件處理，以及將資料對應至XDM，再加以傳送。 這個程式 _比使用_ Launch困難得多。

* 建議您使用Launch進行部 `alloy.js`署，即使這是您唯一使用它的標籤。

## 什麼是XDM，我必須使用哪些Web SDK?

XDM是用來傳送資料至Adobe Experience Platform和Web SDK的資料格式。 網 [頁SDK檔案會逐步引導您](https://docs.adobe.com/content/help/en/experience-platform/edge/get-started/quick-start-with-launch.html#prepare-a-schema) ，瞭解如何輕鬆設定可依您特定需求自訂的架構。

## 什麼是「Adobe Experience Platform Launch Server Side?

2020年晚些時候，Launch將發佈伺服器端轉送功能。 如果您使用我們的SDK並將XDM傳送至Experience Edge，這些新功能可讓您安裝新的伺服器端擴充功能，並將資料對應至任何位置，並從我們的邊緣網路傳送至任何位置。 將其視為「資料收集即服務」。  這項服務將會收費，並隨附於Adobe Experience Platform中。

**更多資訊**[Adobe峰會簡報](https://adobe.bluejeans.com/playback/s/9LhauPOnRSUTYg6RMHAw4oJekhYfOQgdBLlNekVJdWevYktpxqX2IYyl5fz2Wxh9)

## 什麼是CNAME或第一方網域，為什麼重要？

有關CNAME的詳細資訊，請參閱 [Adobe檔案](https://docs.adobe.com/content/help/zh-Hant/id-service/using/reference/analytics-reference/cname.html)

## 我可以從哪裡取得有關Adobe Experience Platform Web SDK的更多資訊？

* [文件](https://docs.adobe.com/content/help/zh-Hant/experience-platform/edge/home.html)
* [原始碼](https://github.com/adobe/alloy)
