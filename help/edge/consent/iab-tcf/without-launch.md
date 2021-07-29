---
title: 使用Adobe Experience Platform Web SDK整合IAB TCF 2.0支援
description: 了解如何不使用標籤，為網站設定IAB TCF 2.0支援。
seo-description: 了解如何使用Adobe Experience Platform Web SDK設定IAB TCF 2.0同意
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# 將IAB TCF 2.0支援與Platform Web SDK整合

本指南說明如何不使用標籤，將互動式廣告局透明與同意架構2.0版(IAB TCF 2.0)與Adobe Experience Platform Web SDK整合。 如需與IAB TCF 2.0整合的概觀，請參閱[overview](./overview.md)。 如需如何與標籤整合的指南，請參閱[IAB TCF 2.0指南中的標籤](./with-launch.md)。

## 快速入門

本指南使用`__tcfapi`介面來存取同意資訊。 直接與雲端管理提供者(CMP)整合可能會更輕鬆。 不過，本指南中的資訊可能仍很實用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些範例假設，在執行程式碼時，已在頁面上定義`window.__tcfapi`。 `__tcfapi`物件準備就緒時，CMP可提供一個掛接，讓您在其中執行這些函式。

若要搭配標籤和Adobe Experience Platform Web SDK擴充功能使用IAB TCF 2.0，您必須有可用的XDM結構。 如果您尚未設定其中一個，請先檢視此頁面，再繼續操作。

此外，本指南也要求您妥善了解Adobe Experience Platform Web SDK。 如需快速重新整理，請參閱[Adobe Experience Platform Web SDK概述](../../home.md)和[常見問題](../../web-sdk-faq.md)檔案。

## 啟用預設同意

如果您想要對所有未知使用者一視同仁，可將預設同意設定為`pending`或`out`。 在收到同意偏好設定之前，此會讓系統排入佇列或捨棄體驗事件。

如需預設同意的詳細資訊，請參閱Platform Web SDK設定檔案中的[預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 根據`gdprApplies`設定預設同意

有些CMP能判斷一般資料保護規範(GDPR)是否適用於客戶。 若您想對未套用GDPR的客戶採取同意，可在TCF API呼叫中使用`gdprApplies`標幟。

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

在此範例中，從TCF API取得`tcData`後，會呼叫`configure`命令。 如果`gdprApplies`為true，則預設同意設為`pending`。 如果`gdprApplies`為false，則預設同意設為`in`。 請務必使用您的設定填入`alloyConfiguration`變數。

>[!NOTE]
>
>當預設同意設為`in`時，仍可使用`setConsent`命令記錄客戶同意偏好設定。

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

此程式碼區塊會監聽`useractioncomplete`事件，然後設定同意，傳遞同意字串和`gdprApplies`標幟。 如果您有客戶的自訂身分，請務必填入`identityMap`變數。 有關呼叫`setConsent`的詳細資訊，請參閱[支援同意](../../consent/supporting-consent.md)的指南。

## 在sendEvent中包含同意資訊

在XDM結構中，您可以儲存Experience Events的同意偏好設定資訊。 有兩種方式可將此資訊新增至每個事件。

首先，您可以在每次`sendEvent`呼叫時提供相關的XDM架構。 下列範例說明執行此作業的方法：

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

此範例會取得TCF API的同意資訊，然後傳送包含已新增至XDM結構之同意資訊的事件。 請參閱[追蹤事件](../../fundamentals/tracking-events.md)指南，了解`sendEvent`命令選項中應包含的內容。

將同意資訊新增至每個要求的另一種方式是使用`onBeforeEventSend`回呼。 如需如何執行此動作的詳細資訊，請參閱追蹤事件檔案中有關[全域修改事件的區段](../../fundamentals/tracking-events.md#modifying-events-globally)。

## 後續步驟

現在您已了解如何搭配Platform Web SDK擴充功能使用IAB TCF 2.0，您也可以選擇與其他Adobe解決方案整合，例如Adobe Analytics或即時客戶資料平台。 如需詳細資訊，請參閱[IAB透明與同意架構2.0概觀](./overview.md) 。
