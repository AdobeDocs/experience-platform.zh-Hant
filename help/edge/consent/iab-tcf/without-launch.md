---
title: 使用Adobe Experience Platform Web SDK整合IAB TCF 2.0支援
description: 了解如何不使用標籤，為網站設定IAB TCF 2.0支援。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 將IAB TCF 2.0支援與Platform Web SDK整合

本指南說明如何不使用標籤，將互動式廣告局透明與同意架構2.0版(IAB TCF 2.0)與Adobe Experience Platform Web SDK整合。 如需與IAB TCF 2.0整合的概觀，請參閱 [概述](./overview.md). 如需如何與標籤整合的指南，請參閱 [標籤適用的IAB TCF 2.0指南](./with-launch.md).

## 快速入門

本指南使用 `__tcfapi` 存取同意資訊的介面。 直接與雲端管理提供者(CMP)整合可能會更輕鬆。 不過，本指南中的資訊可能仍很實用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些範例假設在執行程式碼時， `window.__tcfapi` 在頁面上定義。 CMP可提供連結，讓您在 `__tcfapi` 物件已就緒。

若要搭配標籤和Adobe Experience Platform Web SDK擴充功能使用IAB TCF 2.0，您必須有可用的XDM結構。 如果您尚未設定其中一個，請先檢視此頁面，再繼續操作。

此外，本指南也要求您妥善了解Adobe Experience Platform Web SDK。 如需快速複習，請閱讀 [Adobe Experience Platform Web SDK概述](../../home.md) 和 [常見問題](../../web-sdk-faq.md) 檔案。

## 啟用預設同意

如果您想要對所有未知使用者一視同仁，您可以將預設同意設為 `pending` 或 `out`. 在收到同意偏好設定之前，此會讓系統排入佇列或捨棄體驗事件。

如需預設同意的詳細資訊，請參閱 [預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent) 在Platform Web SDK設定檔案中。

### 根據設定預設同意 `gdprApplies`

有些CMP能判斷一般資料保護規範(GDPR)是否適用於客戶。 若您想對未套用GDPR的客戶採取同意，可使用 `gdprApplies` 標幟。

下列範例說明執行此作業的方法：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此範例中， `configure` 命令會在 `tcData` 從TCF API取得。 若 `gdprApplies` 為true，則預設同意設為 `pending`. 若 `gdprApplies` 為false，則預設同意設為 `in`. 請務必填入 `alloyConfiguration` 變數。

>[!NOTE]
>
>當預設同意設為 `in`, `setConsent` 命令仍可用來記錄客戶同意偏好設定。

## 使用setConsent事件

IAB TCF 2.0 API提供客戶更新同意時的事件。 這發生在客戶最初設定其偏好設定和客戶更新其偏好設定時。

下列範例說明執行此作業的方法：

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

此程式碼區塊會監聽 `useractioncomplete` 事件，然後設定同意，傳遞同意字串和 `gdprApplies` 標籤。 如果您有客戶的自訂身分，請務必填入 `identityMap` 變數。 請參閱 [支援同意](../../consent/supporting-consent.md) 有關呼叫的詳細資訊 `setConsent`.

## 在sendEvent中包含同意資訊

在XDM結構中，您可以儲存Experience Events的同意偏好設定資訊。 有兩種方式可將此資訊新增至每個事件。

首先，您可以在每個 `sendEvent` 呼叫。 下列範例說明執行此作業的方法：

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

此範例會取得TCF API的同意資訊，然後傳送包含已新增至XDM結構之同意資訊的事件。 請參閱 [追蹤事件](../../fundamentals/tracking-events.md) 了解應包含在 `sendEvent` 命令。

將同意資訊新增至每個請求的另一種方式是使用 `onBeforeEventSend` 回呼。 閱讀 [全局修改事件](../../fundamentals/tracking-events.md#modifying-events-globally) ，以取得如何執行此動作的詳細資訊。

## 後續步驟

現在您已了解如何搭配Platform Web SDK擴充功能使用IAB TCF 2.0，您也可以選擇與Adobe Analytics或Adobe Real-time Customer Data Platform等其他Adobe解決方案整合。 請參閱 [IAB透明與同意架構2.0概觀](./overview.md) 以取得更多資訊。
