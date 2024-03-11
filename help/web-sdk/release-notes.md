---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK 最新版本注意事項。
keywords: Adobe Experience Platform Web SDK；Platform Web SDK；Web SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 1%

---


# 發行說明

本文介紹Adobe Experience Platform Web SDK的發行說明。
如需Web SDK標籤擴充功能的最新發行說明，請參閱 [Web SDK標籤擴充功能發行說明](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## 2.19.2版 — 2024年1月10日

**修正和改良**

* 修正身分錯誤遮罩其他錯誤，並將身分錯誤變更為警告的問題。
* 修正當具有的頁面呼叫頂端時，頁面底部絕不會傳送的問題 `renderDecisions` 設為 `false`.
* 修正Web SDK無法讀取多個網域中的跨身分識別的問題 `adobe_mc` 查詢字串引數。

## 2.19.1版 — 2023年11月10日

**修正和改良**

* 修正來自的建議陣列傳回的問題 `sendEvent` 呼叫一律為空白。

## 2.19.0版 — 2023年11月1日

**新功能**

* 新增從Adobe Journey Optimizer轉譯應用程式內訊息的支援。
* 新增的支援 [頁面事件的頂端和底部](use-cases/top-bottom-page-events.md).
* 已新增 [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) 的選項 `sendEvent` 控制要求全頁範圍與預設曲面的指令。

**修正和改良**

* 呈現多種型別的個人化時，合併的個人化會顯示事件。
* 修正單頁應用程式檢視名稱區分大小寫的問題。
* 修正影子DOM個人化優惠選擇器的問題。

## 2.18.0版 — 2023年7月31日

**新功能**

* 新增的支援 [每個命令會覆寫資料串流ID](../datastreams/overrides.md).

**修正和改良**

* 修正因網域是查詢的一部分而導致退出連結不符合資格的問題。
* 已棄用 `edgeConfigId` 贊成 `datastreamId` 在Web SDK設定中。

## 2.17.0版 — 2023年5月17日

**修正和改良**

* Web SDK現在會編碼Audience ManagerCookie目的地值，類似於 [Data Integration Library(DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hant).

## 2.16.0版 — 2023年4月25日

**新功能**

* 新增的支援 [資料流設定覆寫](../datastreams/overrides.md).

## 2.15.0版 — 2023年3月30日

**新功能**

* 新增的支援 [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) 連結按一下回撥。
* 新增Adobe Journey Optimizer點選追蹤支援。

**修正和改良**

* 連結集合現在包含連結名稱和訪客地區。
* 已移除失敗URL目的地的主控台錯誤。

## 2.14.0版 — 2023年1月25日

* （測試版）新增對Adobe Journey Optimizer介面和主張的支援。

**修正和改良**

* 修正Adobe Target VEC自訂程式碼動作將程式碼插入至替代位置的問題，而非使用 [!DNL at.js].
* 修正部分邊緣案例中，對Edge Network的請求未正確設定「referer」標題的問題。
* 修正以下問題： [使用者代理使用者端提示](/help/web-sdk/use-cases/client-hints.md) 屬性可能設定為不正確的型別。
* 修正以下問題： `placeContext.localTime` 不符合結構描述。

## 2.13.1版 — 2022年10月13日

* 修正設定後定義window.Visitor時，訪客移轉無法運作的問題。 使用Adobe標籤執行時，這個問題尤其嚴重。
* 修正以下問題： `device.screenWidth` 和 `device.screenHeight` 在某些環境中填入為字串。

## 2.13.0版 — 2022年9月28日

**新功能**

* 新增的支援 [逐頁完整移轉](home.md#migrating-to-web-sdk). 當訪客在at.js和Web SDK頁面之間移動時，Adobe Target設定檔現在會保留。
* 新增可設定的支援 [高平均資訊量使用者代理使用者端提示](/help/web-sdk/use-cases/client-hints.md).
* 新增對 [`applyResponse`](/help/web-sdk/commands/applyresponse.md) 命令。 如此可透過以下方式啟用混合個人化： [Edge Network伺服器API](../server-api/overview.md).
* QA模式連結現在可跨多個頁面運作。

**修正和改良**

* 修正當連結追蹤停用時，個人化點選追蹤量度未更新的問題。
* 更新命令，以在指定未知選項時擲回驗證錯誤。
* 此 `_experience.decisioning.propositionEventType` 屬性現在會在自動傳送顯示和互動個人化事件時填入。
* 已為「 」新增重複的名稱空間驗證 `getIdentity` 命令。
* 已為「 」新增重複的決定範圍驗證 `sendEvent` 命令。

## 2.12.0版 — 2022年6月29日

* 變更對Edge Network的請求，以使用 `cluster` URL中的Cookie位置提示。 這可確保在工作階段中變更位置（例如，透過VPN或透過行動裝置駕駛等）的使用者點選相同的邊緣，並具有相同的個人化設定檔。
* 將getLibraryInfo命令回應中設定的函式字串化。

## 2.11.0版 — 2022年6月13日

**新功能**

* 您現在可以在行動應用程式和行動網站內容之間，而且跨網域共用訪客ID，更準確地提供個人化體驗。 請參閱 [專屬檔案](identity/id-sharing.md) 以進一步瞭解。
* 您現在可以從以下位置呈現或執行主張陣列 [!DNL Adobe Target] 至單頁應用程式，而不增加分析量度。 這樣可以減少報告錯誤，並提升分析準確度。 請參閱 [專屬檔案](personalization/rendering-personalization-content.md#applypropositions) 以進一步瞭解。
* 已新增其他資訊至 `getLibraryInfo` 指令，包括可用的指令和例項的最終組態。

**修正和改良**

* 更新要使用的Cookie設定 `sameSite="none"` 和 `secure` 標幟於 [!DNL HTTPS] 頁面。
* 修正使用時，個人化內容未正確套用的問題。 `eq` 虛擬選取器。
* 修正以下問題： `localTimezoneOffset` 可能會導致Experience Platform驗證失敗。

## 2.10.1版 — 2022年5月3日

* 修正為ID同步和區段目的地建立多個永久iframe的問題。

## 2.10.0版 — 2022年4月22日

* 對所有ID同步和區段目的地使用永續性iframe。
* 修正合併量度主張在 `sendEvent` 結果。

## 2.9.0版 — 2022年3月10日

* 新增追蹤支援 [!DNL control (default)] Adobe Target體驗。
* 已針對單頁應用程式最佳化檢視 — 變更事件。 呈現個人化體驗時，顯示通知現在會包含在檢視 — 變更事件中。
* 沒有時移除主控台警告 `eventType` 存在。
* 修正的問題： `propositions` 屬性只從 `sendEvent` 要求或從快取中擷取體驗時的命令。 此 `propositions` 屬性現在一律會定義為陣列。
* 修正從Edge Network傳回錯誤時，未顯示隱藏容器的問題。
* 修正Adobe Target中未計算Interact事件的問題。 已透過在web.webPageDetails.viewName將檢視名稱新增至XDM來修正此問題。
* 修正主控台訊息中的中斷檔案連結。

## 2.8.0版 — 2022年1月19日

* 支援個人化的影子DOM選取器。
* 已重新命名個人化事件型別。 (`display` 和 `click` 成為 `decisioning.propositionDisplay` 和 `decisioning.propositionInteract`)
* 修正具有內嵌指令碼標籤的HTML選件將指令碼標籤新增兩次至頁面的問題，即使指令碼僅執行一次。

## 2.7.0版 — 2021年10月26日

* 在來自的傳回值中公開來自Edge Network的其他資訊 `sendEvent`，包括 `inferences` 和 `destinations`. 這些屬性的格式可能會隨著這些功能目前在Beta版中推出而改變。

## 2.6.4版 — 2021年9月7日

* 修正將「設定HTMLAdobe Target」動作套用至 `head` 元素正在取代整個 `head` 內容。 現在設定HTML動作套用至 `head` 元素會變更為附加HTML。

## 2.6.3版 — 2021年8月16日

* 修正非公開用途的物件透過已解析的Promise公開 `configure` 命令。

## 2.6.2版 — 2021年8月4日

* 修正有關棄用的警告問題 `result.decisions` (由 `sendEvent` （命令）將記錄到主控台，即使 `result.decisions` 未存取屬性。 存取時不會記錄任何警告 `result.decisions` 屬性，但屬性仍被取代。

## 2.6.1版 — 2021年7月29日

* 修正呈現沒有個人化內容的單頁應用程式檢視的個人化內容時，會擲回錯誤，並導致從傳回的Promise的問題。 `sendEvent` 要拒絕的命令。

## 2.6.0版 — 2021年7月27日

* 在中提供更多個人化內容 `sendEvent` 已解決Promise，包括Adobe Target回應Token。 當 `sendEvent` 會執行命令，並傳回promise，最後以 `result` 包含從伺服器收到的資訊的物件。 以前，此結果物件包含一個名為的屬性 `decisions`. 這個 `decisions` 屬性已過時。 新屬性， `propositions`，已新增。 這個新屬性可讓客戶存取更多個人化內容，包括 [回應Token](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## 2.5.0版 — 2021年6月

* 新增重新導向個人化選件的支援。
* 自動收集的檢視區寬度和高度如果是負值，將不再傳送至伺服器。
* 當透過傳回取消事件時 `false` 從 `onBeforeEventSend` callback，現在會記錄訊息。
* 修正將用於單一事件的特定XDM資料片段包含於多個事件中的問題。

## 2.4.0版 — 2021年3月

* SDK現在可安裝為 [NPM套件](/help/web-sdk/install/npm.md).
* 新增對的支援 `out` 選項條件 [設定預設同意](/help/web-sdk/commands/configure/defaultconsent.md)，會捨棄所有事件，直到收到同意為止(現有 `pending` 選項會將事件排入佇列，並在收到同意後傳送事件)。
* 此 [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) 現在可使用callback來避免傳送事件。
* 現在使用XDM結構描述欄位群組，而非 `meta.personalization` 傳送有關正在轉譯或點按的個人化內容的事件時。
* 此 [`getIdentity`](/help/web-sdk/commands/getidentity.md) 命令現在會連同身分傳回邊緣區域ID。
* 已改善從伺服器收到的警告和錯誤，並以更適當的方式加以處理。
* 新增對Adobe同意書2.0標準的支援 [`setConsent`](/help/web-sdk/commands/setconsent.md) 命令。
* 收到同意偏好設定時，會進行雜湊處理，並儲存在本機儲存體中，以最佳化CMP、Platform Web SDK和Platform Edge Network之間的整合。 如果您正在收集同意偏好設定，我們現在鼓勵您致電 `setConsent` 在每次載入頁面時。
* 兩個 [監視鉤點](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)， `onCommandResolved` 和 `onCommandRejected`，已新增。
* 錯誤修正：當使用者導覽至新的單頁應用程式檢視、返回原始檢視，並按一下符合轉換資格的元素時，個人化互動通知事件將包含有關相同活動的重複資訊。
* 錯誤修正：如果SDK傳送的第一個事件已 `documentUnloading` 設為 `true`， [`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon) 會用於傳送事件，導致有關未建立身分的錯誤。

## 2.3.0版 — 2020年11月

* 新增Nonce支援，以允許更嚴格的內容安全性原則。
* 新增對單頁應用程式的個人化支援。
* 改善與其他可能遭覆寫之頁面上JavaScript程式碼的相容性 `window.console` API。
* 錯誤修正： `sendBeacon` 未使用時機 `documentUnloading` 已設為 `true` 或是在連結點選次數已自動追蹤時。
* 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
* 錯誤修正：某些包含唯讀的瀏覽器錯誤 `message` 屬性未適當處理，導致向客戶公開不同的錯誤。
* 錯誤修正：如果iframe的HTML頁面來自與上層視窗的HTML頁面不同的子網域，則在iframe內執行SDK會導致錯誤。

## 2.2.0版 — 2020年10月

* 錯誤修正：「選擇加入」物件之前阻止Web SDK進行呼叫，當 `idMigrationEnabled` 是 `true`.
* 錯誤修正：讓Web SDK知道應傳回個人化選件的請求，以避免發生忽隱忽現的問題。

## 2.1.0版 — 2020年8月

* 移除 `syncIdentity` 命令並支援將這些ID傳遞至 `sendEvent` 命令。
* 支援IAB 2.0同意標準。
* 支援在中傳遞其他ID `setConsent` 命令。
* 支援覆寫 `datasetId` 在 `sendEvent` 命令。
* 支援監視掛接([閱讀全文](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 通過 `environment: browser` （在實施詳細資訊內容資料中）。
