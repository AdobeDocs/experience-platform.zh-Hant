---
title: 使用標籤與Platform Web SDK擴充功能整合IAB TCF 2.0支援
description: 了解如何使用標籤和Adobe Experience Platform Web SDK擴充功能設定IAB TCF 2.0同意。
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 使用標籤和Platform Web SDK擴充功能整合IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援互動式廣告局透明與同意架構2.0版(IAB TCF 2.0)。 本指南會說明如何使用Adobe Experience Platform Web SDK標籤擴充功能，設定將IAB TCF 2.0同意資訊傳送至Adobe的標籤屬性。

如果您不想使用標籤，請參閱 [使用IAB TCF 2.0（不含標籤）](./without-launch.md).

## 快速入門

若要搭配標籤和Platform Web SDK擴充功能使用IAB TCF 2.0，您需要有可用的XDM結構和資料集。

此外，本指南也要求您妥善了解Adobe Experience Platform Web SDK。 如需快速複習，請閱讀 [Adobe Experience Platform Web SDK概述](../../home.md) 和 [常見問題](../../web-sdk-faq.md) 檔案。

## 設定預設同意

擴充功能設定中有預設同意的設定。 這會控制沒有同意Cookie的客戶的行為。 如果您想要將體驗事件排入沒有同意Cookie的客戶的佇列，請將此設為 `pending`. 如果您想要捨棄沒有同意Cookie之客戶的體驗事件，請將此設為 `out`. 您也可以使用資料元素來動態設定預設同意值。

如需如何設定預設同意的詳細資訊，請參閱 [預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent) （位於SDK設定指南中）。

## 使用同意資訊更新設定檔 {#consent-code-1}

若要呼叫 `setConsent` 當客戶同意偏好設定變更時，您需要建立新的標籤規則。 首先，新增事件並選擇核心擴充功能的「自訂程式碼」事件類型。

對新事件使用下列程式碼範例：

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

此自訂程式碼有兩項功能：

* 設定兩個資料元素，一個具有同意字串，另一個具有 `gdprApplies` 標籤。 稍後填寫「設定同意」動作時，這個功能會很實用。

* 在同意偏好設定變更時觸發規則。 每當同意偏好設定變更時，應使用「設定同意」動作。 在擴充功能中新增「設定同意」動作，並填寫表單如下：

* 標準：&quot;IAB TCF&quot;
* 版本：&quot;2.0&quot;
* 值：&quot;%IAB TCF同意字串%&quot;
* GDPR適用：&quot;%IAB TCF同意GDPR%&quot;

![IAB設定同意動作](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>您無法使用資料元素選取器來選擇這些資料元素，因為這些資料元素是透過自訂程式碼建立。 您必須輸入含有百分比符號的資料元素名稱。 此程式碼會在客戶變更時，使用其新的同意偏好設定來更新其設定檔。 此外，伺服器會傳回Cookie值，使Adobe Experience Platform Web SDK無法記錄體驗事件。

## 為Experience Events建立XDM資料元素

XDM體驗事件中應包含同意字串。 若要這麼做，請使用XDM物件資料元素。 首先，請建立新的XDM物件資料元素，或使用您已建立的元素來傳送事件。 如果您已將體驗事件隱私權結構欄位群組新增至結構，您應該有 `consentStrings` 鍵。

1. 選擇 **[!UICONTROL consentStrings]**.

1. 選擇 **[!UICONTROL 提供個別項目]** 選取 **[!UICONTROL 新增項目]**.

1. 展開 **[!UICONTROL consentString]** 標題，然後展開第一個項目，然後填入下列值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`:%IAB TCF同意字串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您無法使用資料元素選取器來選擇這些資料元素，因為這些資料元素是透過自訂程式碼建立。 您必須輸入含有百分比符號的資料元素名稱。

## 傳送含有IAB TCF 2.0同意資訊的初始體驗事件

如果頁面上的初始體驗事件是由頁面載入事件觸發，則同意字串可能尚未載入。 此規則旨在取代您目前的頁面載入事件。 若要確認先載入同意資訊，請建立新規則，並將下列程式碼新增為自訂程式碼事件：

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

此程式碼與先前的自訂程式碼相同，但兩者皆相同 `useractioncomplete` 和 `tcloaded` 會處理事件。 此 [上一個自訂程式碼](#consent-code-1) 只有在客戶首次選擇偏好設定時才會觸發。 當客戶已選擇偏好設定時，也會觸發此程式碼。 例如，在第二個頁面載入上。

從Platform Web SDK擴充功能新增「傳送事件」動作。 在「XDM」欄位中，選擇您在上一節中建立的XDM資料元素。

## 使用IAB TCF 2.0同意資訊傳送其他事件

當事件在初始體驗事件後觸發時，兩個資料元素仍會定義，且可用來傳送IAB同意資訊。 使用相同的XDM資料元素來傳送未來事件。 包含IAB TCF 2.0資訊。

## 後續步驟

現在您已了解如何搭配Platform Web SDK擴充功能使用IAB TCF 2.0，您也可以選擇與Adobe Analytics或Adobe Real-time Customer Data Platform等其他Adobe解決方案整合。 請參閱 [IAB透明與同意架構2.0概觀](./overview.md) 以取得更多資訊。
