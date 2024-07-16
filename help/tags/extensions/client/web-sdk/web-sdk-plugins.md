---
title: 常見Web SDK外掛程式擴充功能概觀
description: 瞭解Adobe Experience Platform中的常見Web SDK外掛程式標籤擴充功能。
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# 常見Web SDK外掛程式擴充功能概觀

>[!IMPORTANT]
>
>此擴充功能旨在搭配Adobe Experience Platform Web SDK擴充功能使用。 若要檢視打算與AppMeasurement搭配使用的版本資訊，請參閱[常見Analytics外掛程式擴充功能](../plugins/overview.md)的概觀。

本文介紹如何設定Web SDK外掛程式標籤擴充功能，並用來增強[Adobe Experience Platform Web SDK擴充功能](../web-sdk/overview.md)。

## 設定常見Web SDK外掛程式擴充功能

本節提供設定Web SDK外掛程式擴充功能時可用選項的參考資料。

>[!IMPORTANT]
>
>常見Web SDK外掛程式擴充功能的用意是擴充Adobe Experience Platform Web SDK擴充功能，但您不需要先安裝此擴充功能，即可正常運作。

## 將外掛程式新增至Adobe Experience Platform Web SDK擴充功能

除了使用「常用Web SDK外掛程式」擴充功能提供的下列原生資料元素之外，不需要進行設定即可初始化或新增外掛程式至您的程式庫：

* [&#39;getAndPersistValue&#39;](#getAndPersistValue)
* [&#39;getGeoCoordinates&#39;](#getGeoCoordinates)
* [&#39;getNewRepeat&#39;](#getNewRepeat)
* [&#39;getPagename&#39;](#getPagename)
* [&#39;getPreviousValue&#39;](#getPreviousValue)
* [&#39;getQueryParam&#39;](#getQueryParam)
* [&#39;getTimeParting&#39;](#getTimeParting)
* [&#39;getTimeSinceLastVisit&#39;](#getTimeSInceLastVisit)
* [&#39;getValOnce&#39;](#getValOnce)
* [&#39;getVisitDuration&#39;](#getVisitDuration)
* [&#39;getVisitNum&#39;](#getVisitNum)
* [&#39;pFo&#39;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>此資料元素會設定Cookie並允許將使用者產生的值儲存在Cookie中。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getAndPersistValue` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html)。 `getAndPersistValue`資料元素會將值儲存在Cookie中，以便稍後造訪時擷取。

`getAndPersistValue`資料元素提供下列引數：

* `vtp` （必要）：要在頁面之間保留的值
* `cn` （選用）：要儲存值的Cookie名稱。 如果此引數未設定，Cookie會命名為`"s_gapv"`
* `ex` （選用）：Cookie過期的天數。 如果此引數為`0`或未設定，Cookie會在造訪結束時過期（閒置30分鐘）。

如果`vtp`引數中的變數已設定，則資料元素會設定Cookie，然後傳回Cookie值。 如果`vtp`引數中的變數未設定，則資料元素只會傳回Cookie值。

### `getGeoCoordinates`

>[!IMPORTANT]
>
>此外掛程式需要使用者端上的位置存取權，但如果無法取得，則不會擲回例外狀況。

可讓您設定[`getGeoCoordinates` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html)。 `getGeoCoordinates`資料元素會擷取訪客裝置的經緯度。

`getGeoCoordinates`資料元素未使用任何引數。 它會傳回以下其中一個值：

* `"geo coordinates not available"`：針對外掛程式執行時沒有地理位置資料的裝置。 此值在造訪的第一次點選時很常見，尤其是當訪客需要先同意追蹤其位置時。
* `"error retrieving geo coordinates"`：當外掛程式嘗試擷取裝置位置時遇到任何錯誤時
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`：其中[LATITUDE]/[LONGITUDE]分別為經緯度

### `getNewRepeat`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getNewRepeat` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html)。 `getNewRepeat`資料元素會判斷網站訪客是新訪客還是在指定天數內回訪的重複訪客。

`getNewRepeat`資料元素使用以下引數：

* `d` （整數，選用）：將訪客重設回`"New"`的訪客距離上次造訪需間隔的最小天數。 如果未設定此引數，其預設值為30天。

如果資料元素設定的Cookie不存在或已過期，則此資料元素會傳回`"New"`的值。 如果資料元素設定的Cookie存在，且自目前點選以來的時間量及Cookie中設定的時間超過30分鐘，則會傳回`"Repeat"`值。 此方法會為整個造訪傳回相同值。

### `getPageName`

可讓您設定[`getPageName` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html)。 `getPageName`資料元素可為目前的URL建立易讀、好記的格式化版本。

`getPageName`資料元素使用以下引數：

* `si` （選用，字串）：在代表網站ID的字串開頭插入的ID。 此值可以是數值ID或好記的名稱。 若未設定，則預設為目前的網域。
* `qv` （選用，字串）：以逗號分隔的查詢字串引數清單，若在URL中找到，便會新增至字串
* `hv` （選用，字串）：在URL雜湊中找到的逗號分隔引數清單，若在URL中找到，則會新增至字串
* `de` （選用，字串）：分割字串個別部分的分隔字元。 預設為垂直號(`|`)。

資料元素會傳回包含易記格式化版URL的字串。 此字串通常會指派給`pageName`變數，但也可用於其他變數。

### `getPreviousValue`

>[!IMPORTANT]
>
>此資料元素會設定Cookie並允許將使用者產生的值儲存在Cookie中。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getPreviousValue` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html)。 `getPreviousValue`資料元素會將變數設定為先前點選上設定的值。

`getPreviousValue`資料元素使用以下引數：

* `v` （字串，必要）：具有您要傳遞至下一個影像要求之值的變數。 用來擷取上一頁值的通用變數為`s.pageName`。
* `c` （字串，選用）：儲存值的Cookie名稱。  如果未設定此引數，其預設值為`"s_gpv"`。

當您呼叫此資料元素時，它會傳回Cookie中包含的字串值。 此外掛程式會重設Cookie有效期，並從`v`引數指派變數值。 Cookie會在閒置30分鐘後過期。

### `getQueryParam`

可讓您設定[`getQueryParam` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html)。 `getQueryParam`資料元素會擷取URL中所含任何查詢字串引數的值。 若要從登陸頁面URL擷取內部和外部促銷活動程式碼，此外掛程式非常有用。 擷取搜尋詞或其他查詢字串引數時，它也很有用。 此資料元素提供完善的功能，可剖析複雜的URL，包括雜湊和包含多個查詢字串引數的URL。

`getQueryParam`資料元素使用以下引數：

* `qsp` （必要）：要在URL中尋找的查詢字串引數清單（以逗號分隔）。 不區分大小寫。
* `de` （選用）：有多個查詢字串引數相符時要使用的分隔字元。 預設為空字串。
* `url` （選用）：自訂URL、字串或變數，系統會從其中擷取查詢字串引數值。 預設為`window.location`。

若呼叫此資料元素，系統會根據上述引數和URL傳回值：

* 如果找不到相符的查詢字串引數，方法會傳回空字串。
* 如果找到相符的查詢字串引數，方法會傳回查詢字串引數值。
* 如果找到相符的查詢字串引數但值為空白，方法會傳回`true`。
* 如果找到多個相符的查詢字串引數，方法會傳回一個字串，其中每個引數值都由`de`引數中的字串分隔開。

### `getTimeParting`

可讓您設定[`getTimeParting` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html)。 `getTimeParting`資料元素會擷取網站上發生任何可測量活動的時間詳細資訊。 如果您想要依指定日期範圍內任何可重複的時間區隔來劃分量度，此資料元素就十分實用。 例如，您可以比較一週內兩天之間的轉換率，例如所有週日比較所有週四。 您也可以比較一天中的時段，例如所有早上比較所有晚上。

`getTimeParting`資料元素使用下列引數：

`t` （選用但建議使用，字串）：將訪客的當地時間轉換為該時區的時區名稱。  預設為UTC/GMT時間。 如需有效值的完整清單，請參閱Wikipedia上的[TZ資料庫時區](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)清單。

常見的有效值包括：

* 東部時間的`"America/New_York"`
* 中部時間的`"America/Chicago"`
* 山地時間的`"America/Denver"`
* 太平洋時間的`"America/Los_Angeles"`

呼叫此資料元素會傳回包含下列內容的字串，並以縱線字元(`|`)分隔：

* 目前年份
* 當月
* 該月某日
* 星期幾
* 目前時間（上午/下午）

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getTimeSinceLastVisit` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html)。 `getTimeSinceLastVisit`資料元素會追蹤訪客從上次造訪到下次回訪您網站經過的時間長度。

`getTimeSinceLastVisit`資料元素未使用任何引數。 它會傳回自訪客上次造訪網站以來經過的時間長度，並以下列格式分組：

* 自上次造訪後30分鐘至1小時之間的時間設為最接近的半分鐘基準。 例如，`"30.5 minutes"`， `"53 minutes"`
* 一小時到一天之間的時間會舍入至最接近的四分之一小時基準。 例如，`"2.25 hours"`， `"7.5 hours"`
* 大於一天的時間會舍入至最接近的天數基準。 例如，`"1 day"`，`"3 days"`，`"9 days"`，`"372 days"`
* 如果訪客之前未造訪過，或經過的時間超過兩年，則值會設為`"New Visitor"`。

### `getValOnce`

>[!IMPORTANT]
>
>此資料元素會設定Cookie並允許將使用者產生的值儲存在Cookie中。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getValOnce` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html)。 `getValOnce`資料元素可防止變數多次設為等於相同值。

`getValOnce`資料元素使用以下引數：

* `vtc` （必要，字串）：要檢查的變數，檢視它之前是否設為相同值
* `cn` （選用，字串）：包含要檢查之值的Cookie名稱。 預設為`"s_gvo"`
* `et` （選用，整數）：Cookie的有效期，單位為天（或分鐘，視`ep`引數而定）。 預設為`0`，在瀏覽器工作階段結束時到期
* `ep` （選用，字串）：只有在也設定了`et`引數時才設定此引數。 如果您希望`et`引數在幾分鐘內而不是幾天內到期，請將此引數設為`"m"`。 預設為`"d"`，以天為單位設定`et`引數。

如果`vtc`引數與Cookie值相符，此方法會傳回空字串。 如果`vtc`引數與Cookie值不符，方法會將`vtc`引數傳回為字串。

### `getVisitDuration`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getVisitDuration` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html)。 `getVisitDuration`資料元素會追蹤訪客截至該時間點為止在網站上逗留的時間長度，以分鐘為單位。

`getVisitDuration`資料元素未使用任何引數。 它會傳回以下其中一個值：

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` （其中`[x]`是訪客進到網站以來經過的分鐘數）

### `getVisitNum`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式特定檔案。

可讓您設定[`getVisitNum` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html)。 `getVisitNum`資料元素會傳回在指定天數內造訪過網站的所有訪客造訪次數。

`getVisitNum`資料元素使用以下引數：

* `rp` （選用，整數或字串）：造訪次數計數器重設前的天數。  若未設定，則預設為`365`。
   * 此引數為`"w"`時，計數器會在當週結束時（本週六晚上11:59）重設
   * 此引數為`"m"`時，計數器會在當月結束時（本月的最後一天）重設
   * 此引數為`"y"`時，計數器會在當年結束時（12月31日）重設
* `erp` （選用，布林值）：當`rp`引數為數字時，此引數會決定是否應延長造訪次數的有效期。 若設為`true`，您網站的後續點選會重設造訪次數計數器。 若設為`false`，造訪次數計數器重設時，您網站的後續點選不會延長。 預設為`true`。 當`rp`引數為字串時，此引數無效。

訪客閒置30分鐘後再返回您的網站時，造訪次數會增加。 呼叫此方法會傳回一個整數，代表訪客目前的造訪次數。

### `p_fo` （僅限頁面優先）

可讓您設定[`p_fo` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html)。 `p_fo`資料元素是公用程式，可檢查特定JavaScript物件是否存在。 如果物件不存在，則外掛程式會建立該物件並傳回`true`。 如果頁面上已存在JavaScript物件，則會傳回`false`。 若要在頁面上執行一次程式碼，此資料元素相當實用。

`p_fo`資料元素使用以下引數：

* `on` （必要，字串）：頁面上尚未存在物件時，資料元素所建立的JavaScript物件名稱。

如果物件尚不存在，則此方法會傳回`true`並建立該物件。 如果物件已存在，則此方法會傳回`false`。
