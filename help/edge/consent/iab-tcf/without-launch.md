---
title: 使用Adobe Experience PlatformWeb SDK整合IAB TCF 2.0支援
description: 瞭解如何在不使用標籤的情況下為網站設定IAB TCF 2.0支援。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 將IAB TCF 2.0支援與平台Web SDK整合

本指南說明如何在不使用標籤的情況下將互動式廣告局透明度和同意框架2.0版(IAB TCF 2.0)與Adobe Experience PlatformWeb SDK整合。 有關與IAB TCF 2.0整合的概述，請閱讀 [概述](./overview.md)。 有關如何與標籤整合的指南，請閱讀 [IAB TCF 2.0標籤指南](./with-launch.md)。

## 快速入門

本指南使用 `__tcfapi` 用於訪問同意資訊的介面。 直接與雲管理提供商(CMP)整合可能會更容易。 但是，本指南中的資訊可能仍然有用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些示例假定在運行代碼時， `window.__tcfapi` 定義。 CMP可提供掛接，在 `__tcfapi` 對象已就緒。

要將IAB TCF 2.0與標籤和Adobe Experience PlatformWeb SDK擴展一起使用，需要有XDM架構可用。 如果尚未設定其中任何一個，請先查看此頁，然後繼續。

此外，本指南要求您對Adobe Experience PlatformWeb SDK有良好的瞭解。 請閱讀 [Adobe Experience PlatformWeb SDK概述](../../home.md) 和 [常見問題](../../web-sdk-faq.md) 文檔。

## 啟用預設同意

如果希望對所有未知用戶都一視同仁，可以將預設同意設定為 `pending` 或 `out`。 在收到同意首選項之前，此隊列或丟棄體驗事件。

有關預設同意的詳細資訊，請參閱 [預設同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) 在平台Web SDK配置文檔中。

### 根據 `gdprApplies`

某些CMP提供了確定一般資料保護法規(GDPR)是否適用於客戶的能力。 如果您想為不適用GDPR的客戶承諾同意，則可以使用 `gdprApplies` TCF API調用中的標誌。

以下示例顯示了執行此操作的一種方法：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此示例中， `configure` 命令在 `tcData` 從TCF API獲得。 如果 `gdprApplies` 為true，預設同意設定為 `pending`。 如果 `gdprApplies` 為false，預設同意設定為 `in`。 一定要填寫 `alloyConfiguration` 變數。

>[!NOTE]
>
>預設同意設定為 `in`，也請參見Wiki頁。 `setConsent` 命令仍可用於記錄客戶同意首選項。

## 使用setConnessent事件

IAB TCF 2.0 API提供客戶更新同意時的事件。 當客戶最初設定其首選項以及更新其首選項時，就會發生這種情況。

以下示例顯示了執行此操作的一種方法：

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

此代碼塊偵聽 `useractioncomplete` 事件，然後設定同意，通過同意字串和 `gdprApplies` 。 如果您有客戶的自定義身份，請確保填寫 `identityMap` 變數。 請參閱上的指南 [支援同意](../../consent/supporting-consent.md) 有關呼叫的詳細資訊 `setConsent`。

## 在sendEvent中包括同意資訊

在XDM架構中，可以儲存「體驗事件」中的同意首選項資訊。 將此資訊添加到每個事件有兩種方法。

首先，您可以在每個 `sendEvent` 呼叫。 以下示例顯示了執行此操作的一種方法：

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

此示例獲取TCF API的同意資訊，然後發送包含添加到XDM架構的同意資訊的事件。 查看 [跟蹤事件](../../fundamentals/tracking-events.md) 指導您瞭解應在 `sendEvent` 選項。

將同意資訊添加到每個請求的另一種方法是 `onBeforeEventSend` 回叫。 閱讀上的部分 [全局修改事件](../../fundamentals/tracking-events.md#modifying-events-globally) 的子菜單。

## 後續步驟

現在，您已經學會了如何將IAB TCF 2.0與平台Web SDK擴展一起使用，您還可以選擇與其他Adobe解決方案整合，如Adobe Analytics或Adobe Real-time Customer Data Platform。 查看 [IAB透明度和同意框架2.0概述](./overview.md) 的子菜單。
