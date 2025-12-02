---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK 最新版本注意事項。
keywords: Adobe Experience Platform Web SDK；Experience Platform Web SDK；Web SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: dc333f30f9a2cb7cd485d1cb13272c078da0bd76
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 2%

---


# Web SDK發行說明

本文介紹Adobe Experience Platform Web SDK的發行說明。
如需SDK標籤擴充功能網頁的最新發行說明，請參閱[SDK標籤擴充功能發行說明](/help/tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md)。

## 2.30.0版 — 2025年9月24日

**新功能**

- 新增顯示推播通知的支援。

## 2.29.0版 — 2025年9月4日

**新功能**

- 新增對Adobe Journey Analytics收集Adobe廣告資料的支援
- 新增可在使用者設定檔中記錄推播訂閱詳細資料的支援。

**修正和改良**

- 修正合併而非取代設定覆寫區段的問題。
- 修正連結集合以連結名稱傳送整個檔案內容的情況。
- 修正無法重新呈現某些主張的問題。

## 2.28.1版 — 2025年7月31日

**修正和改良**

- 修正無法執行自訂組建的問題。

## 2.28.0版 — 2025年7月24日

**新功能**

- 新增Adobe Journey Optimizer取消資格規則的支援。

**修正和改良**

- 修正[Media Analytics追蹤器](commands/getmediaanalyticstracker.md)中媒體物件的`length`屬性不正確接受無效資料型別的錯誤。
- 改善[身分管理](../use-cases/identity/id-overview.md)錯誤處理，以便在身分查詢失敗時正確處理Promise拒絕。
- 解決具有HTML內容專案的個人化內容無法呈現的問題，並出現與遺失`renderStatusHandler`相關的錯誤。
- 修正Activity Map [URL集合](commands/configure/clickcollectionenabled.md)以正確處理非HTTP URL。

**已知問題**

- 使用[的](/help/collection/js/install/create-custom-build.md)自訂組建`npx @adobe/alloy`程式目前在2.28.0版中無法如預期運作。所有元件都包含在產生的組建中，無論選取的模組為何。 此問題不會影響CDN上可用的標準JavaScript檔案。 正在進行修正。

## 2.27.0版 — 2025年5月20日

**修正和改良**

- 修正未正確套用自訂樣式的應用程式內訊息問題。
- 已變更事件記錄的格式。 這會導致刪除舊的歷史記錄資料時，重新顯示應用程式內訊息和內容卡。
- 修正在SPA使用案例中重新套用主張的問題。
- 已修正對陰影DOM元素進行點選追蹤的問題。

## 2.26.0版 — 2025年3月5日

**新功能**

- 您現在可以使用Web SDK NPM套件建立自訂Web SDK組建，並僅選取您需要的程式庫元件。 這可讓程式庫大小得以縮小，並最佳化載入時間。 請參閱有關如何使用NPM套件[建立自訂Web SDK組建的檔案](install/create-custom-build.md)。
- [`getIdentity`](commands/getidentity.md)命令現在會自動直接從`kndctr`身分Cookie讀取ECID。 如果您使用`getIdentity`名稱空間呼叫`ECID`，而且已有身分Cookie，Web SDK將不再向Edge Network要求取得身分。 現在會從Cookie讀取身分識別。

**修正和改良**

- 修正傳送`getIdentity`呼叫後，`collect`命令未傳回身分的問題。
- 修正個人化重新導向導致內容在重新導向發生前忽隱忽現的問題。

## 2.25.0版 — 2025年1月23日

**修正和改良**

- 已新增選項驗證至`setDebug`命令。
- 在設定`onBeforeLinkClickSend`函式或下載連結限定詞時新增警告（當點選集合停用時）。
- 修正顯示通知中未包含轉譯主張的問題。

**新功能**

- 當啟用協力廠商Cookie並封鎖對adobedc.demdex.net的請求時，對已設定的Edge網域實施遞補。

## 2.24.1版 — 2024年12月6日

**修正和改良**

- 解決與[Adobe Experience Platform規則引擎](https://github.com/adobe/aepsdk-rulesengine-typescript/)相關的相依性問題，此問題會導致部分客戶整合發生錯誤。 Web SDK現在需要[Adobe Experience Platform Rules Engine](https://github.com/adobe/aepsdk-rulesengine-typescript/) 2.0.3或更新版本。

## 2.24.0版 — 2024年10月31日

**新功能**

- 啟動媒體工作階段時現在支援[資料流覆寫](/help/datastreams/overrides.md)。

- 在[`onContentRendering`](monitoring-hooks.md#onContentRendering)監視勾點中新增對Adobe Target回應Token的支援。

**修正和改良**

- 傳回多個應用程式內訊息時，只會顯示優先順序最高的訊息。 其他則被記錄為隱抑。
- 空的資料流覆寫不再傳送至Edge Network，減少與伺服器端路由設定的潛在衝突。
- 已重新命名下列記錄訊息元件名稱，以與其他Adobe SDK一致：
   - `DecisioningEngine`已重新命名為`RulesEngine`
   - `LegacyMediaAnalytics`已重新命名為`MediaAnalyticsBridge`
   - `Privacy`已重新命名為`Consent`
- 修正透過[`applyPropositions`](commands/applypropositions.md)轉譯預設內容專案時發生的錯誤。
- 修正Adobe Target移動和調整動作大小時的CSS錯誤。
- 已從`machineLearning`回應中移除[`sendEvent`](commands/sendevent/overview.md)金鑰。

## 2.23.0版 — 2024年9月19日

**新功能**

- 新增在[getIdentity](/help/collection/use-cases/identity/id-overview.md)命令中要求[CORE ID](commands/getidentity.md)的支援。

**修正和改良**

- 修正在本機執行Web SDK時，Cookie未正確寫入的問題。

## 2.22.0版 — 2024年8月22日

**新功能**

- 新增對個人化監控鉤點的支援。

**修正和改良**

- 移除對Internet Explorer的支援，將資料庫gzip大小減少9%。
- 修正呼叫`onInstanceConfigured`監視器連結時，Activity Map連結詳細資料未初始化的問題。
- 修正Cookie目的地未設定為正確路徑的問題。
- 修正客戶呼叫具有的問題。
- 修正`adobe_mc`引數中的無效URL編碼導致[sendEvent](commands/sendevent/overview.md)呼叫失敗的問題。

## 2.21.1版 — 2024年7月18日

**修正和改良**

- 修正使用NPM程式庫時的組建錯誤。

## 2.21.0版 — 2024年7月16日

**新功能**

- 新增對自動主張互動追蹤的支援。
- 新增提供alloy.js檔案的自訂建置指令碼。
- 改善具有ActivityMap和事件群組支援的點選收集。

## 2.20.0版 — 2024年5月21日

**新功能**

- 已新增對[串流媒體集合](commands/configure/streamingmedia.md)的支援。

**修正和改良**

- 修正在選擇退出同意時，預先隱藏程式碼片段會隱藏預設內容的錯誤。

## 2.19.2版 — 2024年1月10日

**修正和改良**

- 修正身分錯誤遮罩其他錯誤，並將身分錯誤變更為警告的問題。
- 修正當`renderDecisions`設為`false`的頁面呼叫頂端時，頁面呼叫底部絕不會傳送的問題。
- 修正當有多個`adobe_mc`查詢字串引數時，Web SDK無法讀取跨網域身分識別的問題。

## 版本 2.19.1 - 2023 年 11 月 10 日

**修正和改良**

- 修正從`sendEvent`呼叫傳回的主張陣列一律為空白的問題。

## 2.19.0版 — 2023年11月1日

**新功能**

- 新增從Adobe Journey Optimizer轉譯應用程式內訊息的支援。
- 新增對[頁面事件頂端和底端的支援](../use-cases/personalization/top-bottom-page-events.md)。
- 將[`defaultPersonalizationEnabled`](commands/sendevent/personalization.md)選項新增至`sendEvent`命令，以控制要求全頁範圍與預設介面。

**修正和改良**

- 呈現多種型別的個人化時，合併的個人化會顯示事件。
- 修正單頁應用程式檢視名稱區分大小寫的問題。
- 修正影子DOM個人化優惠選擇器的問題。

## 2.18.0版 — 2023年7月31日

**新功能**

- 新增支援[每個命令覆寫資料串流ID](/help/datastreams/overrides.md)。

**修正和改良**

- 修正因網域是查詢的一部分而導致退出連結不符合資格的問題。
- 已棄用`edgeConfigId`，改用網頁SDK設定中的`datastreamId`。

## 2.17.0版 — 2023年5月17日

**修正和改良**

- Web SDK現在會編碼Audience Manager Cookie目的地值，類似於[Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hant)。

## 2.16.0版 — 2023年4月25日

**新功能**

- 已新增對[資料流組態覆寫](/help/datastreams/overrides.md)的支援。

## 2.15.0版 — 2023年3月30日

**新功能**

- 新增對[`onBeforeLinkClickSend`](commands/configure/onbeforelinkclicksend.md)連結點選回撥的支援。
- 新增Adobe Journey Optimizer點選追蹤支援。

**修正和改良**

- 連結集合現在包含連結名稱和訪客地區。
- 已移除失敗URL目的地的主控台錯誤。

## 2.14.0版 — 2023年1月25日

- (Beta)新增對Adobe Journey Optimizer介面和主張的支援。

**修正和改良**

- 修正Adobe Target VEC自訂程式碼動作將程式碼插入到[!DNL at.js]以外的其他位置的問題。
- 修正某些邊緣案例中，向Edge Network提出的請求未正確設定「referer」標題的問題。
- 修正[使用者代理程式使用者端提示](../use-cases/client-hints.md)屬性可能設定為不正確型別的問題。
- 修正`placeContext.localTime`不符合結構描述的問題。

## 2.13.1版 — 2022年10月13日

- 修正設定後定義window.Visitor時，訪客移轉無法運作的問題。 使用Adobe標籤執行時，這個問題尤其嚴重。
- 修正`device.screenWidth`和`device.screenHeight`在某些環境中填入為字串的問題。

## 2.13.0版 — 2022年9月28日

**新功能**

- 新增對「逐頁完整移轉」的支援。 現在，當訪客在at.js和SDK網頁之間移動時，Adobe Target設定檔將會保留。
- 新增可設定的[高平均資訊量使用者代理程式使用者端提示](../use-cases/client-hints.md)支援。
- 新增對[`applyResponse`](commands/applyresponse.md)命令的支援。 透過[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)啟用混合式個人化。
- QA模式連結現在可跨多個頁面運作。

**修正和改良**

- 修正當連結追蹤停用時，個人化點選追蹤量度未更新的問題。
- 更新命令，以在指定未知選項時擲回驗證錯誤。
- 自動傳送顯示和互動個人化事件時，現在會填入`_experience.decisioning.propositionEventType`屬性。
- 已為`getIdentity`命令新增重複的名稱空間驗證。
- 已為`sendEvent`命令新增重複的決定範圍驗證。

## 2.12.0版 — 2022年6月29日

- 變更對Edge Network的請求，以使用`cluster` Cookie位置提示作為URL的一部分。 這可確保在工作階段中變更位置（例如，透過VPN或透過行動裝置駕駛等）的使用者點選相同的邊緣，並具有相同的個人化設定檔。
- 將getLibraryInfo命令回應中設定的函式字串化。

## 2.11.0版 — 2022年6月13日

**新功能**

- 您現在可以在行動應用程式和行動網站內容之間，而且跨網域共用訪客ID，更準確地提供個人化體驗。 請參閱[專屬檔案](../use-cases/identity/id-sharing.md)以瞭解更多資訊。
- 您現在可以將[!DNL Adobe Target]中的主張陣列轉譯或執行為單頁應用程式，而不需要增加分析量度。 這樣可以減少報告錯誤，並提升分析準確度。 請參閱[專屬檔案](../use-cases/personalization/rendering-personalization-content.md)以瞭解更多資訊。
- 已新增其他資訊至`getLibraryInfo`命令，包括可用的命令和執行個體的最終組態。

**修正和改良**

- 已更新Cookie設定以在`sameSite="none"`頁面上使用`secure`和[!DNL HTTPS]標幟。
- 修正使用`eq`虛擬選取器時，個人化內容未正確套用的問題。
- 修正`localTimezoneOffset`無法通過Experience Platform驗證的問題。

## 2.10.1版 — 2022年5月3日

- 修正為ID同步和區段目的地建立多個永久iframe的問題。

## 2.10.0版 — 2022年4月22日

- 對所有ID同步和區段目的地使用永續性iframe。
- 修正合併的量度主張在`sendEvent`結果中重複的問題。

## 2.9.0版 — 2022年3月10日

- 新增追蹤[!DNL control (default)]個Adobe Target體驗的支援。
- 已針對單頁應用程式最佳化檢視 — 變更事件。 呈現個人化體驗時，顯示通知現在會包含在檢視 — 變更事件中。
- 已移除不存在`eventType`的主控台警告。
- 修正當從快取要求或擷取體驗時，`propositions`屬性只從`sendEvent`命令傳回的問題。 `propositions`屬性現在一律會定義為陣列。
- 修正從Edge Network傳回錯誤時，未顯示隱藏容器的問題。
- 修正Adobe Target中未計算Interact事件的問題。 已透過在web.webPageDetails.viewName將檢視名稱新增至XDM來修正此問題。
- 修正主控台訊息中的中斷檔案連結。

## 2.8.0版 — 2022年1月19日

- 支援個人化的影子DOM選取器。
- 已重新命名個人化事件型別。 （`display`和`click`成為`decisioning.propositionDisplay`和`decisioning.propositionInteract`）
- 修正內嵌指令碼標籤的HTML選件將指令碼標籤新增兩次至頁面的問題，即使指令碼僅執行一次。

## 版本 2.7.0 - 2021 年 10 月 26 日

- 在來自`sendEvent`的傳回值中公開來自Edge Network的其他資訊，包括`inferences`和`destinations`。 這些屬性的格式可能會隨著這些功能目前在Beta中推出而改變。

## 2.6.4版 — 2021年9月7日

- 修正套用至`head`元素的設定HTML Adobe Target動作會取代整個`head`內容的問題。 現在，套用至`head`元素的HTML動作已變更為附加HTML。

## 2.6.3版 — 2021年8月16日

- 修正非公開用途的物件透過`configure`命令中已解析的Promise公開的問題。

## 2.6.2版 — 2021年8月4日

- 修正了即使未存取`result.decisions`屬性，`sendEvent` （由`result.decisions`命令提供）棄用的警告仍會記錄到主控台的問題。 存取`result.decisions`屬性時不會記錄任何警告，但該屬性仍被取代。

## 2.6.1版 — 2021年7月29日

- 修正呈現沒有個人化內容的單頁應用程式檢視的個人化內容會擲回錯誤，並導致`sendEvent`命令傳回的Promise遭到拒絕的問題。

## 2.6.0版 — 2021年7月27日

- 在`sendEvent`已解析的Promise中提供更多個人化內容，包括Adobe Target回應Token。 執行`sendEvent`命令時，會傳回Promise，這最終會以包含從伺服器接收之資訊的`result`物件來解析。 以前，此結果物件包含名為`decisions`的屬性。 此`decisions`屬性已過時。 已新增屬性`propositions`。 這個新屬性可讓客戶存取更多個人化內容，包括回應Token。

## 2.5.0版 — 2021年6月

- 新增重新導向個人化選件的支援。
- 自動收集的檢視區寬度和高度如果是負值，將不再傳送至伺服器。
- 當從`false`回呼傳回`onBeforeEventSend`以取消事件時，現在會記錄訊息。
- 修正將用於單一事件的特定XDM資料片段包含於多個事件中的問題。

## 2.4.0版 — 2021年3月

- SDK現在可以安裝為[NPM套件](install/npm.md)。
- 新增在`out`設定預設同意[時對](commands/configure/defaultconsent.md)選項的支援，在收到同意之前會捨棄所有事件（現有的`pending`選項會將事件排入佇列，並在收到同意後傳送這些事件）。
- [`onBeforeEventSend`](commands/configure/onbeforeeventsend.md)回呼現在可用來防止傳送事件。
- 現在傳送有關個人化內容呈現或點按的事件時，會使用XDM結構描述欄位群組，而非`meta.personalization`。
- [`getIdentity`](commands/getidentity.md)命令現在會連同身分一併傳回邊緣區域ID。
- 已改善從伺服器收到的警告和錯誤，並以更適當的方式加以處理。
- 新增對Adobe的[`setConsent`](commands/setconsent.md)命令同意2.0標準的支援。
- 收到同意偏好設定時，會進行雜湊處理，並儲存在本機儲存體中，以最佳化CMP、Experience Platform Web SDK和Experience Platform Edge Network之間的整合。 如果您正在收集同意偏好設定，我們現在鼓勵您在每次載入頁面時呼叫`setConsent`。
- 已新增兩個[監視鉤點](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
- 錯誤修正：當使用者導覽至新的單頁應用程式檢視、返回原始檢視，並按一下符合轉換資格的元素時，Personalization互動通知事件會包含相同活動的重複資訊。
- 錯誤修正：如果SDK傳送的第一個事件將`documentUnloading`設為`true`，則會使用[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)傳送事件，導致有關未建立身分的錯誤。

## 2.3.0版 — 2020年11月

- 新增Nonce支援，以允許更嚴格的內容安全性原則。
- 新增對單頁應用程式的個人化支援。
- 改善與其他可能覆寫`window.console` API的頁面上JavaScript程式碼的相容性。
- 錯誤修正： `sendBeacon`設為`documentUnloading`或自動追蹤連結點選時，未使用`true`。
- 錯誤修正：如果錨點元素包含HTML內容，系統不會自動追蹤連結。
- 錯誤修正：某些包含唯讀`message`屬性的瀏覽器錯誤未適當處理，導致向客戶公開不同的錯誤。
- 錯誤修正：如果iframe的SDKHTML頁面來自與上層視窗的HTML頁面不同的子網域，則在iframe內執行iframe會導致錯誤。

## 2.2.0版 — 2020年10月

- 錯誤修正：當`idMigrationEnabled`為`true`時，選擇加入物件會封鎖Web SDK進行呼叫。
- 錯誤修正：讓網頁SDK知道應傳回個人化選件的請求，以避免發生閃爍問題。

## 2.1.0版 — 2020年8月

- 移除`syncIdentity`命令，並支援在`sendEvent`命令中傳遞這些ID。
- 支援IAB 2.0同意標準。
- 支援在`setConsent`命令中傳遞其他ID。
- 支援覆寫`datasetId`命令中的`sendEvent`。
- 支援監視掛接（[瞭解詳情](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
- 傳遞實作詳細資料內容資料中的`environment: browser`。
