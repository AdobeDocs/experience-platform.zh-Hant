---
title: 使用Adobe Experience Platform Web SDK整合IAB TCF 2.0支援
description: 瞭解如何設定網站的IAB TCF 2.0支援，而不使用標籤。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 將IAB TCF 2.0支援與Platform Web SDK整合

本指南說明如何在不使用標籤的情況下，整合Interactive Advertising Bureau Transparency &amp; Consent Framework 2.0版(IAB TCF 2.0)與Adobe Experience Platform Web SDK。 如需與IAB TCF 2.0整合的概述，請閱讀[概述](./overview.md)。 如需如何與標籤整合的指南，請閱讀標籤的[IAB TCF 2.0指南](./with-tags.md)。

## 快速入門

本指南使用`__tcfapi`介面來存取同意資訊。 您可以更輕鬆地直接與雲端管理提供者(CMP)整合。 不過，本指南中的資訊可能仍然有用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些範例假設在執行程式碼時，頁面上已定義`window.__tcfapi`。 CMP可提供連結，讓您在`__tcfapi`物件準備就緒時執行這些函式。

若要搭配標籤和Adobe Experience Platform Web SDK擴充功能使用IAB TCF 2.0，您需要有XDM結構描述可用。 如果您尚未設定這些專案，請先檢視此頁面再繼續。

此外，本指南會要求您實際瞭解Adobe Experience Platform Web SDK。 如需快速複查，請閱讀[Adobe Experience Platform Web SDK總覽](../../home.md)和[常見問題](../../faq.md)檔案。

## 啟用預設同意

如果您希望將所有未知的使用者視為相同，可以將[`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)設為`pending`或`out`。 這會在收到同意偏好設定之前將體驗事件加入佇列或捨棄。

### 根據`gdprApplies`設定預設同意

有些CMP提供判斷一般資料保護規範(GDPR)是否適用於客戶的功能。 如果您希望客戶同意GDPR不適用的情況，可在TCF API呼叫中使用`gdprApplies`標幟。

下列範例顯示執行此操作的一種方式：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此範例中，在從TCF API取得`tcData`之後呼叫`configure`命令。 如果`gdprApplies`為true，則預設同意設定為`pending`。 如果`gdprApplies`為false，則預設同意設定為`in`。 請務必以您的設定填入`alloyConfiguration`變數。

>[!NOTE]
>
>當預設同意設定為`in`時，`setConsent`命令仍可用於記錄您的客戶同意偏好設定。

## 使用setConsent事件

IAB TCF 2.0 API會提供客戶更新同意時適用的事件。 當客戶最初設定其偏好設定以及客戶更新其偏好設定時，就會發生這種情況。

下列範例顯示執行此操作的一種方式：

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

此程式碼區塊會接聽`useractioncomplete`事件，然後設定同意，傳遞同意字串和`gdprApplies`標幟。 如果您有客戶的自訂身分，請務必填寫`identityMap`變數。 如需詳細資訊，請參閱[setConsent](../../../web-sdk/commands/setconsent.md)上的指南。

## 在sendEvent中包含同意資訊

在XDM結構描述中，您可以儲存來自體驗事件的同意偏好設定資訊。 有兩種方式可將此資訊新增至每個事件。

首先，您可以在每`sendEvent`個呼叫中提供相關的XDM結構描述。 下列範例顯示執行此操作的一種方式：

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

此範例會取得TCF API的同意資訊，然後傳送包含已新增至XDM結構描述之同意資訊的事件。

另一種將同意資訊新增至每個要求的方式是使用[`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)回呼。

## 後續步驟

現在您已瞭解如何使用IAB TCF 2.0搭配Platform Web SDK擴充功能，您也可以選擇與其他Adobe解決方案(例如Adobe Analytics或Adobe Real-time Customer Data Platform)整合。 如需詳細資訊，請參閱[IAB透明與同意架構2.0概覽](./overview.md)。
