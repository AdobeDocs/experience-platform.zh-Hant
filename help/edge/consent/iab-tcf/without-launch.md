---
title: 不使用Experience Platform Launch使用IAB TCF 2.0
seo-title: 以Adobe Experience Platform Web SDK設定IAB TCF 2.0同意
description: 瞭解如何透過Adobe Experience Platform Web SDK設定IAB TCF 2.0同意
seo-description: 瞭解如何透過Adobe Experience Platform Web SDK設定IAB TCF 2.0同意
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---


# 搭配使用IAB TCF 2.0和AEP Web SDK擴充功能

本指南說明如何在不使用Experience Platform Launch的情況下，將Interactive Advertising Bureau透明度與同意框架2.0版(IAB TCF 2.0)與Adobe Experience Platform Web SDK整合。 有關與IAB TCF 2.0整合的概述，請閱讀 [概述](./overview.md)。 如需如何與Experience Platform Launch整合的指南，請閱讀 [IAB TCF 2.0的Experience Platform Launch指南](./with-launch.md)。

## 快速入門

本指南使用介 `__tcfapi` 面來存取同意資訊。 直接與雲端管理提供者(CMP)整合可能會更輕鬆。 但是，本指南中的資訊可能仍然有用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些範例假設在執行程式碼時，已在頁 `window.__tcfapi` 面上定義程式碼。 CMP可提供掛接，在對象就緒時，可在其中運 `__tcfapi` 行這些函式。

若要搭配使用IAB TCF 2.0和Experience Platform Launch和AEP Web SDK擴充功能，您必須有可用的XDM架構。 如果您未設定其中任一設定，請先檢視此頁面，再繼續。

此外，本指南要求您對Adobe Experience Platform Web SDK有良好的認識。 如需快速進階，請閱讀 [Adobe Experience Platform Web SDK概觀](../../home.md) ，以及 [Frequently asked questions](../../web-sdk-faq.md) documentation。

## 啟用預設許可

如果您想要對所有未知的使用者視為相同，可將預設同意設為 `pending`。 這會將「體驗事件」排入佇列，直到收到同意偏好設定。

如需預設同意的詳細資訊，請參閱「平台網 [頁SDK設定檔案](../../fundamentals/configuring-the-sdk.md#default-consent) 」中的「預設同意」一節。

### 根據 `gdprApplies`

有些CMP可讓您判斷通用資料保護規則(GDPR)是否適用於客戶。 如果您想要為不適用GDPR的客戶徵得同意，則可以在TCF API呼 `gdprApplies` 叫中使用標幟。

下列範例說明執行此動作的一種方式：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此示例中， `configure` 從TCF API獲取命 `tcData` 令後調用該命令。 如果 `gdprApplies` 為真，則預設同意會設為 `pending`。 如果 `gdprApplies` 為false，則預設同意會設為 `in`。 請務必以您的設定 `alloyConfiguration` 填入變數。

>[!NOTE]
>
>當預設同意設為 `in`時， `setConsent` 仍可使用命令記錄客戶同意偏好。

## 使用setConnence事件

IAB TCF 2.0 API提供客戶更新同意書的事件。 當客戶最初設定其偏好設定，以及客戶更新其偏好設定時，就會發生此情況。

下列範例說明執行此動作的一種方式：

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

此程式碼區塊會監聽 `useractioncomplete` 事件，然後設定同意，傳遞同意字串和 `gdprApplies` 旗標。 如果您有客戶的自訂身分識別，請務必填入變 `identityMap` 數。 有關呼叫的詳細信 [息，請參](../../consent/supporting-consent.md) 閱支援許可指南 `setConsent`。

## 在sendEvent中包含同意資訊

在XDM結構中，您可以儲存「體驗事件」的同意偏好資訊。 有兩種方式可將這項資訊新增至每個事件。

首先，您可以在每次呼叫時提供相關的XDM `sendEvent` 架構。 下列範例說明執行此動作的一種方式：

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

此示例獲取TCF API的許可資訊，然後發送包含添加到XDM模式的許可資訊的事件。 請參 [閱追蹤事件](../../fundamentals/tracking-events.md) 指南，瞭解命令選項中應包含 `sendEvent` 的內容。

將同意資訊新增至每個請求的另一種方式是使用回 `onBeforeEventSend` 呼。 請閱讀追蹤事 [件檔案中](../../fundamentals/tracking-events.md#modifying-events-globally) ，全域修改事件的章節，以取得如何執行此動作的詳細資訊。

## 後續步驟

現在您已學會如何搭配使用AEP Web SDK擴充功能的IAB TCF 2.0，您也可以選擇與其他Adobe解決方案整合，例如Adobe Analytics或即時客戶資料平台。 如需詳 [細資訊，請參閱IAB透明度與同意框架](./overview.md) 2.0概觀。
