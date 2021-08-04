---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK 最新版本注意事項。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: f3821176b0cbc4ad07fbd2e0e20caa1205324a44
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 4%

---

# 發行說明

## 版本2.6.2 - 2021年8月4日

* 修正即使未存取`result.decisions`屬性，`sendEvent`命令提供的`result.decisions`淘汰警告仍會記錄到主控台的問題。 存取`result.decisions`屬性時不會記錄任何警告，但該屬性仍被取代。

## 版本2.6.1 - 2021年7月29日

* 修正針對沒有個人化內容的單頁應用程式檢視呈現個人化內容時，會擲回錯誤，並導致從`sendEvent`命令傳回的Promise遭拒的問題。

## 版本2.6.0 - 2021年7月27日

* 在`sendEvent`解析的Promise中提供更多個人化內容，包括Adobe Target回應Token。 執行`sendEvent`命令時，會傳回Promise，最終以`result`物件解析，該物件包含從伺服器收到的資訊。 以前，此結果對象包含名為`decisions`的屬性。 此`decisions`屬性已過時。 已新增新屬性`propositions`。 這個新屬性可讓客戶存取更多個人化內容，包括[回應Token](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html)。

## 版本2.5.0 - 2021年6月

* 新增對重新導向個人化選件的支援。
* 自動收集的作為負值的檢視區寬度和高度將不再傳送至伺服器。
* 從`onBeforeEventSend`回呼傳回`false`來取消事件時，現在會記錄訊息。
* 修正多個事件中，包含特定單一事件專用XDM資料片段的問題。

## 版本2.4.0 - 2021年3月

* SDK現在可以[安裝為npm套件](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=zh-Hant)。
* 新增[設定預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)時`out`選項的支援，這會在收到同意前捨棄所有事件（現有的`pending`選項會讓事件進入佇列，並在收到同意後傳送事件）。
* [onBeforeEventSend回呼](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend)現在可用來防止傳送事件。
* 現在傳送呈現或點按之個人化內容的相關事件時，會使用XDM結構欄位群組，而非`meta.personalization`。
* [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id)現在會連同身分一併傳回邊緣區域ID。
* 已改善從伺服器收到的警告和錯誤，並以更適當的方式處理。
* 新增[Adobe同意2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支援。
* 同意偏好設定收到後會雜湊並儲存在本機儲存空間，以便CMP、Platform Web SDK和Platform邊緣網路之間最佳化整合。 如果您要收集同意偏好設定，現在建議您在每次載入頁面時呼叫`setConsent`。
* 已新增兩個[監控鈎點](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
* 錯誤修正：當使用者導覽至新的單頁應用程式檢視、返回原始檢視，然後按一下符合轉換資格的元素時，個人化互動通知事件會包含相同活動的重複資訊。
* 錯誤修正：如果SDK傳送的第一個事件`documentUnloading`設為`true`，則會使用[`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon)來傳送事件，導致未建立身分的錯誤。

## 版本2.3.0 - 2020年11月

* 新增Nonce支援，以允許更嚴格的內容安全性原則。
* 新增單頁應用程式的個人化支援。
* 改善與其他可能覆寫`window.console` API的頁面上JavaScript程式碼的相容性。
* 錯誤修正：`documentUnloading`設為`true`或自動追蹤連結點按時，未使用`sendBeacon`。
* 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
* 錯誤修正：包含唯讀`message`屬性的某些瀏覽器錯誤未得到適當處理，導致向客戶公開不同錯誤。
* 錯誤修正：如果在iframe內執行SDK，若iframe的HTML頁面來自父視窗的HTML頁面以外的子網域，則會導致錯誤。

## 版本2.2.0 - 2020年10月

* 錯誤修正：當`idMigrationEnabled`為`true`時，選擇加入物件會阻擋Alloy進行呼叫。
* 錯誤修正：讓Alloy知道應傳回個人化選件的請求，以避免發生忽隱忽現的問題。

## 版本2.1.0 - 2020年8月

* 移除`syncIdentity`命令，並支援在`sendEvent`命令中傳遞這些ID。
* 支援IAB 2.0同意標準。
* 支援在`setConsent`命令中傳遞其他ID。
* 支援在`sendEvent`命令中覆蓋`datasetId`。
* 支援合金顯示器（[了解詳情](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在實作詳細資料內容資料中傳遞`environment: browser`。
