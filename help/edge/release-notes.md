---
title: Adobe Experience Platform Web SDK 發行說明
description: Adobe Experience Platform Web SDK 最新版本注意事項。
keywords: Adobe Experience Platform網頁SDK；平台網頁SDK；網頁SDK；發行說明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
translation-type: tm+mt
source-git-commit: d4ed6c8fa9c86eb2beec829ab24c381b665c2f03
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# 發行說明

## 2.4.0版，2021年3月

* SDK現在可以安裝為npm套件](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html)。[
* 新增在[設定預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)時支援`out`選項，此選項會丟棄所有事件直到收到同意（現有的`pending`選項會將事件排入佇列，並在收到同意後傳送這些事件）。
* [onBeforeEventSend回呼](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend)現在可用來防止傳送事件。
* 現在，當傳送有關轉譯或點按之個人化內容的事件時，請使用XDM mixin而非`meta.personalization`。
* [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id)現在會傳回身分的邊緣區域ID。
* 從伺服器收到的警告和錯誤已改善，並以更適當的方式處理。
* 新增[Adobe同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支援。
* 許可偏好設定在收到後會雜湊並儲存在本機儲存中，以便在CMP、Platform Web SDK和Platform Edge Network之間最佳化整合。 如果您要收集同意偏好設定，我們現在鼓勵您在每次載入頁面時呼叫`setConsent`。
* 已添加兩個[監視掛接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
* 錯誤修正：當使用者導覽至新的單頁應用程式檢視、返回原始檢視，並按一下符合轉換資格的元素時，個人化互動通知事件會包含有關相同活動的重複資訊。
* 錯誤修正：如果SDK傳送的第一個事件設定`documentUnloading`為`true`，則會使用[`sendBeacon`](https://developer.mozilla.org/zh-TW/docs/Web/API/Navigator/sendBeacon)來傳送該事件，導致未建立身分的錯誤。

## 2.3.0版，2020年11月

* 新增nonce支援，以允許更嚴格的內容安全性政策。
* 新增單頁應用程式的個人化支援。
* 已改善與其他可能覆寫`window.console` API之頁面上JavaScript程式碼的相容性。
* 錯誤修正：`sendBeacon`未在`documentUnloading`設為`true`或自動追蹤連結點按時使用。
* 錯誤修正：如果錨點元素包含HTML內容，則不會自動追蹤連結。
* 錯誤修正：某些包含唯讀`message`屬性的瀏覽器錯誤處理不當，導致不同的錯誤暴露給客戶。
* 錯誤修正：如果在iframe中執行SDK，若iframe的HTML頁面來自父視窗的HTML頁面以外的子網域，則會產生錯誤。

## 2.2.0版，2020年10月

* 錯誤修正：當`idMigrationEnabled`為`true`時，Opt-in對象會阻止Alloy發出呼叫。
* 錯誤修正：讓Alloy知道應該傳回個人化優惠的要求，以避免閃爍的問題。

## 2.1.0版，2020年8月

* 刪除`syncIdentity`命令，並支援在`sendEvent`命令中傳遞這些ID。
* 支援IAB 2.0同意標準。
* 支援在`setConsent`命令中傳遞其他ID。
* 支援覆蓋`sendEvent`命令中的`datasetId`。
* 支援合金顯示器（[閱讀更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在實作詳細內容資料中傳遞`environment: browser`。
