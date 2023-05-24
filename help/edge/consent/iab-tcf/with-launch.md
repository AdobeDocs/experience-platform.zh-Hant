---
title: 使用標籤和平台Web SDK擴展整合IAB TCF 2.0支援
description: 瞭解如何設定IAB TCF 2.0的標籤同意和Adobe Experience PlatformWeb SDK擴展。
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 使用標籤和平台Web SDK擴展整合IAB TCF 2.0支援

Adobe Experience PlatformWeb SDK支援互動式廣告局透明度和同意框架2.0版(IAB TCF 2.0)。 本指南介紹如何設定標籤屬性，以便使用Adobe Experience PlatformWeb SDK標籤擴展將IAB TCF 2.0同意資訊發送到Adobe。

如果您不想使用標籤，請參閱上的指南 [使用IAB TCF 2.0而不帶標籤](./without-launch.md)。

## 快速入門

為了將IAB TCF 2.0與標籤和平台Web SDK擴展一起使用，您需要有可用的XDM架構和資料集。

此外，本指南要求您對Adobe Experience PlatformWeb SDK有良好的瞭解。 請閱讀 [Adobe Experience PlatformWeb SDK概述](../../home.md) 和 [常見問題](../../web-sdk-faq.md) 文檔。

## 設定預設同意

在擴展配置中，存在預設同意的設定。 這控制沒有同意cookie的客戶的行為。 如果要為沒有同意cookie的客戶排隊體驗事件，請將此設定為 `pending`。 如果要放棄沒有同意cookie的客戶的體驗事件，請將此設定為 `out`。 您還可以使用資料元素動態設定預設同意值。

有關如何配置預設同意的詳細資訊，請參閱 [預設同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) SDK配置指南中。

## 使用同意資訊更新配置檔案 {#consent-code-1}

呼叫 `setConsent` 當您的客戶同意首選項發生更改時，您需要建立新的標籤規則。 首先添加新事件，然後選擇核心擴展的「自定義代碼」事件類型。

對新事件使用以下代碼示例：

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

此自定義代碼執行兩項操作：

* 設定兩個資料元素，一個具有同意字串，另一個具有 `gdprApplies` 。 這在以後填寫「設定同意」操作時非常有用。

* 當同意首選項更改時觸發規則。 當同意偏好發生更改時，應使用「設定同意」操作。 在擴展中添加「設定同意」操作，並按如下方式填寫表單：

* 標準：&quot;IAB TCF&quot;
* 版本：&quot;2.0&quot;
* 值：&quot;%IAB TCF同意字串%&quot;
* GDPR適用：&quot;%IAB TCF同意GDPR%&quot;

![IAB設定同意操作](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>無法使用資料元素選擇器選擇這些資料元素，因為它們是通過自定義代碼建立的。 必須鍵入帶有百分號的資料元素名稱。 此代碼將在客戶更改時使用其新的同意首選項更新其配置檔案。 此外，伺服器返回Cookie值，這可能會阻止Adobe Experience PlatformWeb SDK記錄「體驗事件」。

## 為體驗事件建立XDM資料元素

同意字串應包括在XDM體驗事件中。 為此，請使用XDM對象資料元素。 首先建立新的XDM對象資料元素，或者使用已建立的用於發送事件的元素。 如果已將「體驗事件隱私」架構欄位組添加到您的架構中，則應該 `consentStrings` 鍵。

1. 選擇 **[!UICONTROL connessStrings]**。

1. 選擇 **[!UICONTROL 提供單個項目]** 選擇 **[!UICONTROL 添加項]**。

1. 展開 **[!UICONTROL contenceString]** 展開第一個項，然後填寫以下值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`:%IAB TCF同意字串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>無法使用資料元素選擇器選擇這些資料元素，因為它們是通過自定義代碼建立的。 必須鍵入帶有百分號的資料元素名稱。

## 使用IAB TCF 2.0同意資訊發送初始體驗事件

如果頁面上的初始體驗事件是使用頁面載入事件觸發的，則可能尚未載入同意字串。 此規則用於替換當前頁面載入事件。 要確保首先載入同意資訊，請建立新規則並將以下代碼添加為自定義代碼事件：

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

此代碼與以前的自定義代碼相同，但是 `useractioncomplete` 和 `tcloaded` 處理事件。 的 [上一個自定義代碼](#consent-code-1) 僅當客戶首次選擇其首選項時觸發。 當客戶已選擇其首選項時，此代碼也會觸發。 例如，在第二頁載入。

從平台Web SDK擴展添加「發送事件」操作。 在「XDM」欄位中，選擇在上一節中建立的XDM資料元素。

## 使用IAB TCF 2.0同意資訊發送其他事件

當事件在初始體驗事件之後被觸發時，兩個資料元素仍被定義，並且可用於發送IAB同意資訊。 使用相同的XDM資料元素發送將來的事件。 包括IAB TCF 2.0資訊。

## 後續步驟

現在，您已經學會了如何將IAB TCF 2.0與平台Web SDK擴展一起使用，您還可以選擇與其他Adobe解決方案整合，如Adobe Analytics或Adobe Real-time Customer Data Platform。 查看 [IAB透明度和同意框架2.0概述](./overview.md) 的子菜單。
