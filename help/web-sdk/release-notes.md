---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK 最新版本注意事項。
keywords: Adobe Experience Platform Web SDK；Platform Web SDK；Web SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 73a82825dd6c9ae97db76018df5462ab20c7d15e
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 2%

---


# 發行說明

本文介紹Adobe Experience Platform Web SDK的發行說明。
如需Web SDK標籤擴充功能的最新發行說明，請參閱[Web SDK標籤擴充功能發行說明](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md)。

## 2.22.0版 — 2024年8月22日

**新功能**

- 新增個人化監視器。

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

- 已新增對[串流媒體集合](../web-sdk/commands/configure/streamingmedia.md)的支援。

**修正和改良**

- 修正在選擇退出同意時，預先隱藏程式碼片段會隱藏預設內容的錯誤。

## 2.19.2版 — 2024年1月10日

**修正和改良**

- 修正身分錯誤遮罩其他錯誤，並將身分錯誤變更為警告的問題。
- 修正當`renderDecisions`設為`false`的頁面呼叫頂端時，頁面呼叫底部絕不會傳送的問題。
- 修正當有多個`adobe_mc`查詢字串引數時，Web SDK無法讀取跨網域身分識別的問題。

## 2.19.1版 — 2023年11月10日

**修正和改良**

- 修正從`sendEvent`呼叫傳回的主張陣列一律為空白的問題。

## 2.19.0版 — 2023年11月1日

**新功能**

- 新增從Adobe Journey Optimizer轉譯應用程式內訊息的支援。
- 新增對[頁面事件頂端和底端的支援](use-cases/top-bottom-page-events.md)。
- 將[`defaultPersonalizationEnabled`](commands/sendevent/personalization.md)選項新增至`sendEvent`命令，以控制要求全頁範圍與預設介面。

**修正和改良**

- 呈現多種型別的個人化時，合併的個人化會顯示事件。
- 修正單頁應用程式檢視名稱區分大小寫的問題。
- 修正影子DOM個人化優惠選擇器的問題。

## 2.18.0版 — 2023年7月31日

**新功能**

- 新增支援[每個命令覆寫資料串流ID](../datastreams/overrides.md)。

**修正和改良**

- 修正因網域是查詢的一部分而導致退出連結不符合資格的問題。
- 已棄用`edgeConfigId`，而改用Web SDK設定中的`datastreamId`。

## 2.17.0版 — 2023年5月17日

**修正和改良**

- Web SDK現在會對Audience ManagerCookie目的地值進行編碼，類似於[Data Integration Library(DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hant)。

## 2.16.0版 — 2023年4月25日

**新功能**

- 已新增對[資料流組態覆寫](../datastreams/overrides.md)的支援。

## 2.15.0版 — 2023年3月30日

**新功能**

- 新增對[`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md)連結點選回撥的支援。
- 新增Adobe Journey Optimizer點選追蹤支援。

**修正和改良**

- 連結集合現在包含連結名稱和訪客地區。
- 已移除失敗URL目的地的主控台錯誤。

## 2.14.0版 — 2023年1月25日

- (Beta)新增對Adobe Journey Optimizer介面和主張的支援。

**修正和改良**

- 修正Adobe Target VEC自訂程式碼動作將程式碼插入到[!DNL at.js]以外的其他位置的問題。
- 修正某些邊緣案例中，向Edge Network提出的請求未正確設定「referer」標題的問題。
- 修正[使用者代理程式使用者端提示](/help/web-sdk/use-cases/client-hints.md)屬性可能設定為不正確型別的問題。
- 修正`placeContext.localTime`不符合結構描述的問題。

## 2.13.1版 — 2022年10月13日

- 修正設定後定義window.Visitor時，訪客移轉無法運作的問題。 使用Adobe標籤執行時，這個問題尤其嚴重。
- 修正`device.screenWidth`和`device.screenHeight`在某些環境中填入為字串的問題。

## 2.13.0版 — 2022年9月28日

**新功能**

- 新增對[Page by Page Full Migration](home.md#migrating-to-web-sdk)的支援。 當訪客在at.js和Web SDK頁面之間移動時，Adobe Target設定檔現在會保留。
- 新增可設定的[高平均資訊量使用者代理程式使用者端提示](/help/web-sdk/use-cases/client-hints.md)支援。
- 新增對[`applyResponse`](/help/web-sdk/commands/applyresponse.md)命令的支援。 這會透過[Edge Network伺服器API](../server-api/overview.md)啟用混合式個人化。
- QA模式連結現在可跨多個頁面運作。

**修正和改良**

- 修正當連結追蹤停用時，個人化點選追蹤量度未更新的問題。
- 更新命令，以在指定未知選項時擲回驗證錯誤。
- 自動傳送顯示和互動個人化事件時，現在會填入`_experience.decisioning.propositionEventType`屬性。
- 已為`getIdentity`命令新增重複的名稱空間驗證。
- 已為`sendEvent`命令新增重複的決定範圍驗證。

## 2.12.0版 — 2022年6月29日

- 將請求變更為Edge Network以使用`cluster` Cookie位置提示做為URL的一部分。 這可確保在工作階段中變更位置（例如，透過VPN或透過行動裝置駕駛等）的使用者點選相同的邊緣，並具有相同的個人化設定檔。
- 將getLibraryInfo命令回應中設定的函式字串化。

## 2.11.0版 — 2022年6月13日

**新功能**

- 您現在可以在行動應用程式和行動網站內容之間，而且跨網域共用訪客ID，更準確地提供個人化體驗。 請參閱[專屬檔案](identity/id-sharing.md)以瞭解更多資訊。
- 您現在可以將[!DNL Adobe Target]中的主張陣列轉譯或執行為單頁應用程式，而不需要增加分析量度。 這樣可以減少報告錯誤，並提升分析準確度。 請參閱[專屬檔案](personalization/rendering-personalization-content.md#applypropositions)以瞭解更多資訊。
- 已新增其他資訊至`getLibraryInfo`命令，包括可用的命令和執行個體的最終組態。

**修正和改良**

- 已更新Cookie設定以在[!DNL HTTPS]頁面上使用`sameSite="none"`和`secure`標幟。
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
- 修正具有內嵌指令碼標籤的HTML選件將指令碼標籤新增兩次至頁面的問題，即使指令碼僅執行一次。

## 2.7.0版 — 2021年10月26日

- 在來自`sendEvent`的傳回值中公開來自Edge Network的其他資訊，包括`inferences`和`destinations`。 這些屬性的格式可能會隨著這些功能目前在Beta中推出而改變。

## 2.6.4版 — 2021年9月7日

- 修正套用至`head`元素的設定HTMLAdobe Target動作會取代整個`head`內容的問題。 現在，套用至`head`專案的HTML動作已變更為附加HTML。

## 2.6.3版 — 2021年8月16日

- 修正非公開用途的物件透過`configure`命令中已解析的Promise公開的問題。

## 2.6.2版 — 2021年8月4日

- 修正了即使未存取`result.decisions`屬性，`result.decisions` （由`sendEvent`命令提供）棄用的警告仍會記錄到主控台的問題。 存取`result.decisions`屬性時不會記錄任何警告，但該屬性仍被取代。

## 2.6.1版 — 2021年7月29日

- 修正呈現沒有個人化內容的單頁應用程式檢視的個人化內容會擲回錯誤，並導致`sendEvent`命令傳回的Promise遭到拒絕的問題。

## 2.6.0版 — 2021年7月27日

- 在`sendEvent`已解析的Promise中提供更多個人化內容，包括Adobe Target回應Token。 執行`sendEvent`命令時，會傳回Promise，這最終會以包含從伺服器接收之資訊的`result`物件來解析。 以前，此結果物件包含名為`decisions`的屬性。 此`decisions`屬性已過時。 已新增屬性`propositions`。 這個新屬性可讓客戶存取更多個人化內容，包括[回應Token](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md)。

## 2.5.0版 — 2021年6月

- 新增重新導向個人化選件的支援。
- 自動收集的檢視區寬度和高度如果是負值，將不再傳送至伺服器。
- 當從`onBeforeEventSend`回呼傳回`false`以取消事件時，現在會記錄訊息。
- 修正將用於單一事件的特定XDM資料片段包含於多個事件中的問題。

## 2.4.0版 — 2021年3月

- SDK現在可以安裝為[NPM套件](/help/web-sdk/install/npm.md)。
- 新增在[設定預設同意](/help/web-sdk/commands/configure/defaultconsent.md)時對`out`選項的支援，在收到同意之前會捨棄所有事件（現有的`pending`選項會將事件排入佇列，並在收到同意後傳送這些事件）。
- [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)回呼現在可用來防止傳送事件。
- 現在傳送有關個人化內容呈現或點按的事件時，會使用XDM結構描述欄位群組，而非`meta.personalization`。
- [`getIdentity`](/help/web-sdk/commands/getidentity.md)命令現在會連同身分一併傳回邊緣區域ID。
- 已改善從伺服器收到的警告和錯誤，並以更適當的方式加以處理。
- 新增對[`setConsent`](/help/web-sdk/commands/setconsent.md)命令之Adobe同意2.0標準的支援。
- 收到同意偏好設定時，會進行雜湊處理，並儲存在本機儲存體中，以最佳化CMP、Platform Web SDK和PlatformEdge Network之間的整合。 如果您正在收集同意偏好設定，我們現在鼓勵您在每次載入頁面時呼叫`setConsent`。
- 已新增兩個[監視鉤點](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
- 錯誤修正：當使用者導覽至新的單頁應用程式檢視、返回原始檢視，並按一下符合轉換資格的元素時，Personalization互動通知事件會包含相同活動的重複資訊。
- 錯誤修正：如果SDK傳送的第一個事件將`documentUnloading`設為`true`，則會使用[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)傳送事件，導致有關未建立身分的錯誤。

## 2.3.0版 — 2020年11月

- 新增Nonce支援，以允許更嚴格的內容安全性原則。
- 新增對單頁應用程式的個人化支援。
- 改善與其他可能覆寫`window.console` API的頁面上JavaScript程式碼的相容性。
- 錯誤修正： `documentUnloading`設為`true`或自動追蹤連結點選時，未使用`sendBeacon`。
- 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
- 錯誤修正：某些包含唯讀`message`屬性的瀏覽器錯誤未適當處理，導致向客戶公開不同的錯誤。
- 錯誤修正：如果iframe的HTML頁面來自與上層視窗的HTML頁面不同的子網域，則在iframe內執行SDK會導致錯誤。

## 2.2.0版 — 2020年10月

- 錯誤修正：當`idMigrationEnabled`為`true`時，選擇加入物件會封鎖Web SDK進行呼叫。
- 錯誤修正：讓Web SDK知道應傳回個人化選件的請求，以避免發生忽隱忽現的問題。

## 2.1.0版 — 2020年8月

- 移除`syncIdentity`命令，並支援在`sendEvent`命令中傳遞這些ID。
- 支援IAB 2.0同意標準。
- 支援在`setConsent`命令中傳遞其他ID。
- 支援覆寫`sendEvent`命令中的`datasetId`。
- 支援監視掛接（[瞭解詳情](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
- 傳遞實作詳細資料內容資料中的`environment: browser`。
