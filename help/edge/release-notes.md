---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK 最新版本注意事項。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 7d7a9357f17b941a8f7800be86f211bb1276698d
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 4%

---

# 發行說明

## 版本2.7.0 - 2021年10月26日

* 在Experience Edge的傳回值中公開其他資訊，來自 `sendEvent`，包括 `inferences` 和 `destinations`. 這些屬性的格式可能會有所變更，因為這些功能目前是測試版的一部分。 如需詳細資訊，請參閱 [追蹤事件。](fundamentals/tracking-events.md)

## 版本2.6.4 - 2021年9月7日

* 修正設定HTMLAdobe Target動作時，套用至 `head` 元素正在替換整個 `head` 內容。 現在，設定套用至的HTML動作 `head` 元素已變更為附加HTML。

## 版本2.6.3 - 2021年8月16日

* 修正非公用物件透過 `configure` 命令。

## 版本2.6.2 - 2021年8月4日

* 修正 `result.decisions` (由 `sendEvent` 命令)，則即使在 `result.decisions` 屬性未被存取。 存取 `result.decisions` 屬性，但屬性仍不再使用。

## 版本2.6.1 - 2021年7月29日

* 針對沒有個人化內容的單頁應用程式檢視呈現個人化內容時，系統擲回錯誤，並導致Promise從 `sendEvent` 命令被拒絕。

## 版本2.6.0 - 2021年7月27日

* 在 `sendEvent` 已解析的Promise，包括Adobe Target回應Token。 當 `sendEvent` 命令執行，並傳回promise，最終以 `result` 包含從伺服器接收的資訊的對象。 以前，此結果對象包含一個名為 `decisions`. 此 `decisions` 屬性已過時。 新屬性， `propositions`，已新增。 這個新屬性可讓客戶存取更多個人化內容，包括 [回應token](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## 版本2.5.0 - 2021年6月

* 新增對重新導向個人化選件的支援。
* 自動收集的作為負值的檢視區寬度和高度將不再傳送至伺服器。
* 當透過傳回 `false` 從 `onBeforeEventSend` 回撥，訊息現在已記錄。
* 修正多個事件中，包含特定單一事件專用XDM資料片段的問題。

## 版本2.4.0 - 2021年3月

* SDK現在可以是 [已安裝為npm套件](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* 新增對 `out` 選項 [配置預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)，會捨棄所有事件，直到收到同意為止(現有 `pending` 選項會讓事件排入佇列，並在收到同意後傳送它們)。
* 此 [onBeforeEventSend回呼](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) 現在可用來防止傳送事件。
* 現在使用XDM結構欄位群組，而非 `meta.personalization` 傳送關於呈現或點按之個人化內容的事件時。
* 此 [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) 現在會連同身分一併傳回邊緣地區ID。
* 已改善從伺服器收到的警告和錯誤，並以更適當的方式處理。
* 新增 [Adobe的同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 同意偏好設定收到後會雜湊並儲存在本機儲存空間，以便CMP、Platform Web SDK和Platform邊緣網路之間最佳化整合。 如果您要收集同意偏好設定，現在建議您呼叫 `setConsent` 在每個頁面載入時。
* 二 [監視掛接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 和 `onCommandRejected`，已新增。
* 錯誤修正：當使用者導覽至新的單頁應用程式檢視、返回原始檢視，然後按一下符合轉換資格的元素時，個人化互動通知事件會包含相同活動的重複資訊。
* 錯誤修正：如果SDK傳送的第一個事件 `documentUnloading` 設為 `true`, [`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon) 會用來傳送事件，導致有關身分的錯誤未建立。

## 版本2.3.0 - 2020年11月

* 新增Nonce支援，以允許更嚴格的內容安全性原則。
* 新增單頁應用程式的個人化支援。
* 改善與其他可能會覆寫的頁面上JavaScript程式碼的相容性 `window.console` API。
* 錯誤修正： `sendBeacon` 未使用時 `documentUnloading` 設為 `true` 或連結點按被自動追蹤時。
* 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
* 錯誤修正：包含唯讀的某些瀏覽器錯誤 `message` 屬性處理不當，導致向客戶公開其他錯誤。
* 錯誤修正：如果在iframe中執行SDK，若iframe的HTML頁面來自父視窗的HTML頁面以外的子網域，則會導致錯誤。

## 版本2.2.0 - 2020年10月

* 錯誤修正：選擇加入物件會在 `idMigrationEnabled` is `true`.
* 錯誤修正：讓Alloy知道應傳回個人化選件的請求，以避免發生忽隱忽現的問題。

## 版本2.1.0 - 2020年8月

* 移除 `syncIdentity` 命令，並支援在 `sendEvent` 命令。
* 支援IAB 2.0同意標準。
* 支援在 `setConsent` 命令。
* 支援覆寫 `datasetId` 在 `sendEvent` 命令。
* 支援合金顯示器([了解詳情](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 通過 `environment: browser` 在實作詳細資料內容資料中。
