---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience 平台 Web SDK 最新版本注意事項。
keywords: Adobe Experience PlatformWeb SDK；平台Web SDK;Web SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 3d8e21f76b23bac3ee88702c19cf6d6a6e25a3ae
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# 發行說明

## 版本2.9.0 - 2022年3月10日

* 增加了跟蹤支援 [!DNL control (default)] Adobe Target的經歷。
* 為單頁應用程式優化了視圖更改事件。 當呈現個性化體驗時，顯示通知現在會隨視圖更改事件一起提供。
* 沒有時刪除控制台警告 `eventType` 的下界。
* 修復問題 `propositions` 僅從 `sendEvent` 命令。 的 `propositions` 屬性現在將始終定義為陣列。
* 修復了在從Adobe體驗邊返回錯誤時未顯示隱藏容器的問題。
* 修復了未在Adobe Target計算互動事件的問題。 通過將視圖名稱添加到web.webPageDetails.viewName的XDM中，可解決此問題。
* 修復控制台消息中的損壞文檔連結。

## 版本2.8.0 - 2022年1月19日

* 支援用於個性化的卷影DOM選擇器。
* 已更名個性化設定事件類型。 (`display` 和 `click` 成 `decisioning.propositionDisplay` 和 `decisioning.propositionInteract`)
* 修復了HTML提供的帶有內聯指令碼標籤的指令碼標籤將指令碼標籤添加兩次到頁面的問題，即使指令碼只運行一次。

## 版本2.7.0 - 2021年10月26日

* 從Experience Edge中公佈返回值中的其他資訊 `sendEvent`，包括 `inferences` 和 `destinations`。 這些屬性的格式可能會更改，因為這些功能當前正在作為Beta的一部分推出。 有關詳細資訊，請參見 [跟蹤事件。](fundamentals/tracking-events.md)

## 版本2.6.4 - 2021年9月7日

* 已修復將HTMLAdobe Target操作應用於 `head` 元素正在替換 `head` 內容。 現在設定應用於的HTML操作 `head` 元素被更改為追加HTML。

## 版本2.6.3 - 2021年8月16日

* 修復了未打算用於公共用途的對象通過已解決的承諾暴露的問題 `configure` 的子菜單。

## 版本2.6.2 - 2021年8月4日

* 修復了一個問題，其中對 `result.decisions` (由 `sendEvent` 命令)將記錄到控制台 `result.decisions` 未訪問屬性。 訪問 `result.decisions` 屬性，但該屬性仍不建議使用。

## 版本2.6.1 - 2021年7月29日

* 修復了為沒有個性化內容的單頁應用程式視圖呈現個性化設定將引發錯誤並導致承諾從 `sendEvent` 命令。

## 版本2.6.0 - 2021年7月27日

* 在 `sendEvent` 已解決的承諾，包括Adobe Target響應令牌。 當 `sendEvent` 執行命令，返回承諾，最終通過 `result` 包含從伺服器接收的資訊的對象。 以前，此結果對象包含名為 `decisions`。 此 `decisions` 屬性已棄用。 新房， `propositions`中。 此新屬性為客戶提供了對更多個性化內容(包括 [響應令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html)。

## 2.5.0版 — 2021年6月

* 增加了對重定向個性化服務的支援。
* 自動收集的視區寬度和高度（為負值）將不再發送到伺服器。
* 當通過返回 `false` 從 `onBeforeEventSend` 回叫，現在已記錄消息。
* 修復了在多個事件中包含用於單個事件的特定XDM資料的問題。

## 版本2.4.0 - 2021年3月

* SDK現在可以 [已作為npm包安裝](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html)。
* 為 `out` 選項 [配置預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)，它將刪除所有事件，直到收到同意(現有 `pending` 選項將事件排隊，並在收到同意後發送它們)。
* 的 [onBeforeEventSend回調](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) 現在可用於阻止發送事件。
* 現在使用XDM架構欄位組，而不是 `meta.personalization` 發送有關正在呈現或按一下的個性化內容的事件時。
* 的 [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) 現在返回邊緣區域ID和標識。
* 從伺服器收到的警告和錯誤已得到改進，並且以更適當的方式處理。
* 為 [Adobe同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)。
* 當收到同意首選項時，會對其進行散列並儲存在本地儲存中，以便在CMP、Platform Web SDK和Platform Edge Network之間進行優化整合。 如果您正在收集同意偏好，我們現在鼓勵您撥打 `setConsent` 在每頁上載入。
* 二 [監控鈎](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)。 `onCommandResolved` 和 `onCommandRejected`的子菜單。
* 錯誤修復：當用戶導航到新的單頁應用視圖、返回原始視圖並按一下符合轉換條件的元素時，個性化交互通知事件將包含有關同一活動的重複資訊。
* 錯誤修復：如果SDK發送的第一個事件 `documentUnloading` 設定為 `true`。 [`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon) 將用於發送事件，導致有關未建立身份的錯誤。

## 2.3.0版 — 2020年11月

* 添加了一次性支援，以允許實施更嚴格的內容安全策略。
* 增加了對單頁應用程式的個性化支援。
* 與可能正在覆蓋的其他頁面上JavaScript代碼的相容性得到了提高 `window.console` API。
* 錯誤修復： `sendBeacon` 在 `documentUnloading` 已設定為 `true` 或當連結點擊自動跟蹤時。
* 錯誤修復：如果錨點元素包含HTML內容，則不會自動跟蹤連結。
* 錯誤修復：包含只讀的某些瀏覽器錯誤 `message` 未正確處理屬性，導致向客戶顯示其他錯誤。
* 錯誤修復：如果在iframe中運行SDK，則如果iframe的HTML頁來自父窗口的HTML頁以外的子域，則會導致錯誤。

## 2.2.0版 — 2020年10月

* 錯誤修復：Opt-in對象阻止Alloy在 `idMigrationEnabled` 是 `true`。
* 錯誤修復：使合金瞭解應返回個性化設定的請求，以防止閃爍問題。

## 2.1.0版 — 2020年8月

* 刪除 `syncIdentity` 命令和支援在 `sendEvent` 的子菜單。
* 支援IAB 2.0同意標準。
* 支援在中傳遞其他ID `setConsent` 的子菜單。
* 支援覆蓋 `datasetId` 的 `sendEvent` 的子菜單。
* 支援合金監視器([閱讀更多內容](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 通過 `environment: browser` 在實現詳細上下文資料中。
