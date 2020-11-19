---
title: 搭配Experience Platform Launch使用IAB TCF 2.0
seo-title: 取得Adobe Experience Platform Launch和Adobe Experience Platform Web SDK的IAB TCF 2.0同意
description: 瞭解如何透過Adobe Experience Platform Launch和Adobe Experience Platform Web SDK設定IAB TCF 2.0同意
seo-description: 瞭解如何透過Adobe Experience Platform Launch和Adobe Experience Platform Web SDK設定IAB TCF 2.0同意
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# 搭配使用IAB TCF 2.0和Experience Platform Launch和AEP Web SDK擴充功能

Adobe Experience Platform Web SDK支援Interactive Advertising Bureau透明度與同意框架2.0版(IAB TCF 2.0)。 本指南說明如何設定Adobe Experience Platform Launch屬性，以便使用Experience Platform Launch的AEP Web SDK擴充功能，將IAB TCF 2.0同意資訊傳送給Adobe。

如果您不想使用Experience Platform Launch，請參閱「在未使用Experience Platform Launch的情況下使用IAB TCF 2.0」 [指南](./without-launch.md)。

## 快速入門

若要搭配使用IAB TCF 2.0和Experience Platform Launch和AEP Web SDK擴充功能，您需要有可用的XDM架構和資料集。

此外，本指南要求您對Adobe Experience Platform Web SDK有良好的認識。 如需快速進階，請閱讀 [Adobe Experience Platform Web SDK概觀](../../home.md) ，以及 [Frequently asked questions](../../web-sdk-faq.md) documentation。

## 設定預設許可

在擴充功能設定中，有預設同意的設定。 這可控制未取得同意Cookie的客戶的行為。 如果您想要將「體驗事件」佇列給沒有同意Cookie的客戶，請將此設定為 `pending`。

>[!NOTE]
>
>目前，無法透過Experience Platform Launch擴充功能動態設定此項設定。

如需預設同意的詳細資訊，請參閱SDK [設定檔案中的](../../fundamentals/configuring-the-sdk.md#default-consent) 「預設同意」一節。

## 更新配置檔案並獲取許可資訊 {#consent-code-1}

若要在客戶 `setConsent` 同意偏好變更時採取行動，您需要建立新的「體驗平台啟動」規則。 首先新增事件，然後選擇核心擴充功能的「自訂代碼」事件類型。

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

* 設定兩個資料元素，一個包含同意字串，另一個包含標 `gdprApplies` 幟。 這在以後填寫「設定同意」動作時很有用。

* 在同意偏好變更時觸發規則。 「設定同意」動作應在同意偏好變更時使用。 在擴充功能中新增「設定同意」動作，並填寫如下表格：

* 標準：&quot;IAB TCF&quot;
* 版本：&quot;2.0&quot;
* 值：&quot;%IAB TCF同意字串%&quot;
* GDPR適用：&quot;%IAB TCF同意GDPR%&quot;

![IAB設定同意行動](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為這些資料元素是透過自訂代碼建立的。 您必須輸入包含百分比符號的資料元素名稱。 此程式碼會在客戶變更時，使用新的同意偏好設定來更新其個人檔案。 此外，伺服器會傳回Cookie值，這可能會使Adobe Experience Platform Web SDK無法記錄「Experience Events」。

## 為體驗事件建立XDM資料元素

同意字串應包含在XDM體驗事件中。 若要這麼做，請使用XDM物件資料元素。 首先，請建立新的XDM物件資料元素，或使用您已建立的元素來傳送事件。 如果您已將「體驗事件隱私權」混合新增至架構，則XDM物件中 `consentStrings` 應有索引鍵。

1. 選擇 **[!UICONTROL conmenceStrings]**。

1. 選擇「 **[!UICONTROL 提供個別項目]** 」並選 **[!UICONTROL 擇「新增項目」]**。

1. 展開 **[!UICONTROL connectionString標題]** ，並展開第一個項目，然後填入下列值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`:%IAB TCF同意字串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為這些資料元素是透過自訂代碼建立的。 您必須輸入包含百分比符號的資料元素名稱。

## 使用IAB TCF 2.0許可資訊發送初始體驗事件

如果頁面上的初始體驗事件是以頁面載入事件觸發，則許可字串可能尚未載入。 此規則旨在取代您目前的頁面載入事件。 若要確定先載入同意資訊，請建立新規則並新增下列程式碼作為自訂程式碼事件：

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

此程式碼與先前的自訂程式碼相同，但是會同時 `useractioncomplete` 處理 `tcloaded` 和事件。 先 [前的自訂代碼](#consent-code-1) ，只會在客戶第一次選擇偏好設定時觸發。 當客戶已選擇其偏好設定時，也會觸發此程式碼。 例如，在第二頁載入時。

從AEP Web SDK擴充功能新增「傳送事件」動作。 在「XDM」欄位中，選擇您在上一節中建立的XDM資料元素。

## 以IAB TCF 2.0許可資訊發送其他事件

當事件在初始「體驗事件」後觸發時，仍會定義兩個資料元素，並可用來傳送IAB同意資訊。 使用相同的XDM資料元素來傳送未來事件。 包括IAB TCF 2.0資訊。

## 後續步驟

現在您已學會如何搭配使用AEP Web SDK擴充功能的IAB TCF 2.0，您也可以選擇與其他Adobe解決方案整合，例如Adobe Analytics或即時客戶資料平台。 如需詳 [細資訊，請參閱IAB透明度與同意框架](./overview.md) 2.0概觀。
