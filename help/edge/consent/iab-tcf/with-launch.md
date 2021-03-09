---
title: 使用Platform launch和平台網頁SDK擴充功能整合IAB TCF 2.0支援
description: 瞭解如何設定IAB TCF 2.0與Adobe Experience Platform Launch及Adobe Experience Platform網頁SDK擴充功能的同意。
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---


# 使用Platform launch和平台網頁SDK擴充功能整合IAB TCF 2.0支援

Adobe Experience Platform網頁SDK支援互動式廣告局透明度與同意框架2.0版(IAB TCF 2.0)。 本指南說明如何設定Adobe Experience Platform Launch屬性，以便使用Adobe Experience PlatformWeb SDK擴充功能將IAB TCF 2.0同意資訊傳送至Adobe以進行Experience Platform Launch。

如果您不想使用Experience Platform Launch，請參閱[使用IAB TCF 2.0而不使用Experience Platform Launch](./without-launch.md)上的指南。

## 快速入門

為了搭配使用IAB TCF 2.0和Experience Platform Launch和平台網頁SDK擴充功能，您需要有XDM架構和資料集。

此外，本指南要求您對Adobe Experience Platform網頁SDK有良好的認識。 如需快速複習，請閱讀[Adobe Experience Platform網頁SDK概觀](../../home.md)和[常見問答](../../web-sdk-faq.md)檔案。

## 設定預設許可

在擴充功能設定中，有預設同意的設定。 這可控制未取得同意Cookie的客戶的行為。 如果您要為沒有同意Cookie的客戶排入「體驗事件」佇列，請將此設定為`pending`。 如果您想要針對沒有同意Cookie的客戶捨棄「體驗事件」，請將此設定為`out`。 您也可以使用資料元素動態設定預設同意值。

如需如何設定預設同意的詳細資訊，請參閱SDK設定指南中的[預設同意章節](../../fundamentals/configuring-the-sdk.md#default-consent)。

## 更新配置式並獲得許可資訊{#consent-code-1}

若要在客戶同意偏好變更時呼叫`setConsent`動作，您必須建立新的Experience Platform Launch規則。 首先新增事件，然後選擇核心擴充功能的「自訂代碼」事件類型。

針對新事件使用下列程式碼範例：

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

* 設定兩個資料元素，一個具有許可字串，一個具有`gdprApplies`標誌。 這在以後填寫「設定同意」動作時很有用。

* 在同意偏好變更時觸發規則。 「設定同意」動作應在同意偏好變更時使用。 在擴充功能中新增「設定同意」動作，並填寫如下表格：

* 標準：&quot;IAB TCF&quot;
* 版本：&quot;2.0&quot;
* 值：&quot;%IAB TCF同意字串%&quot;
* GDPR適用：&quot;%IAB TCF同意GDPR%&quot;

![IAB設定同意行動](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為這些資料元素是透過自訂代碼建立的。 您必須輸入包含百分比符號的資料元素名稱。 此程式碼會在客戶變更時，使用新的同意偏好設定來更新其個人檔案。 此外，伺服器會傳回Cookie值，這可能會阻止Adobe Experience Platform網頁SDK記錄「體驗事件」。

## 為體驗事件建立XDM資料元素

同意字串應包含在XDM體驗事件中。 若要這麼做，請使用XDM物件資料元素。 首先，請建立新的XDM物件資料元素，或使用您已建立的元素來傳送事件。 如果您已將「體驗事件隱私權」混合新增至架構，XDM物件中應該有`consentStrings`金鑰。

1. 選擇&#x200B;**[!UICONTROL conmenceStrings]**。

1. 選擇&#x200B;**[!UICONTROL 提供個別項目]**&#x200B;並選擇&#x200B;**[!UICONTROL 添加項目]**。

1. 展開&#x200B;**[!UICONTROL conmonceString]**&#x200B;標題，並展開第一個項目，然後填入下列值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`:2.0
* `consentStringValue`:%IAB TCF同意字串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為這些資料元素是透過自訂代碼建立的。 您必須輸入包含百分比符號的資料元素名稱。

## 使用IAB TCF 2.0許可資訊發送初始體驗事件

如果頁面上的初始體驗事件是以頁面載入事件觸發，則許可字串可能尚未載入。 此規則旨在取代您目前的頁面載入事件。 若要先載入同意資訊，請建立新規則，並新增下列程式碼作為自訂程式碼事件：

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

此程式碼與先前的自訂程式碼相同，但`useractioncomplete`和`tcloaded`事件皆已處理。 [先前的自訂代碼](#consent-code-1)只會在客戶第一次選擇偏好設定時觸發。 當客戶已選擇其偏好設定時，也會觸發此程式碼。 例如，在第二頁載入時。

從平台網頁SDK擴充功能新增「傳送事件」動作。 在「XDM」欄位中，選擇您在上一節中建立的XDM資料元素。

## 以IAB TCF 2.0許可資訊發送其他事件

當事件在初始「體驗事件」後觸發時，仍會定義兩個資料元素，並可用來傳送IAB同意資訊。 使用相同的XDM資料元素來傳送未來事件。 包括IAB TCF 2.0資訊。

## 後續步驟

現在您已學會如何搭配使用IAB TCF 2.0與Platform Web SDK擴充功能，您也可以選擇與其他Adobe解決方案整合，例如Adobe Analytics或即時客戶資料平台。 如需詳細資訊，請參閱[IAB透明與同意框架2.0概觀](./overview.md)。
