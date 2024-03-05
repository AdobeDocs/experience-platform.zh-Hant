---
title: 使用標籤和Platform Web SDK擴充功能整合IAB TCF 2.0支援
description: 瞭解如何使用標籤和Adobe Experience Platform Web SDK擴充功能設定IAB TCF 2.0同意。
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# 使用標籤和Platform Web SDK擴充功能整合IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援Interactive Advertising Bureau Transparency &amp; Consent Framework 2.0版(IAB TCF 2.0)。 本指南說明如何設定標籤屬性，以使用Adobe Experience Platform Web SDK標籤擴充功能傳送IAB TCF 2.0同意資訊以Adobe。

如果您不想使用標籤，請參閱以下指南： [使用不含標籤的IAB TCF 2.0](./without-tags.md).

## 快速入門

若要搭配標籤和Platform Web SDK擴充功能使用IAB TCF 2.0，您需要有XDM結構描述和資料集可以使用。

此外，本指南會要求您實際瞭解Adobe Experience Platform Web SDK。 如需快速複習內容，請閱讀 [Adobe Experience Platform Web SDK總覽](../../home.md) 和 [常見問題集](../../faq.md) 檔案。

## 設定預設同意

在擴充功能組態中，有預設同意的設定。 這會控制沒有同意Cookie之客戶的行為。 如果您想要將沒有同意Cookie的客戶的「體驗事件」加入佇列，請將此項設為 `pending`. 如果您想捨棄沒有同意Cookie之客戶的體驗事件，請將此項設為 `out`. 您也可以使用資料元素來動態設定預設同意值。 另請參閱 [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) 以取得詳細資訊。

## 使用同意資訊更新設定檔 {#consent-code-1}

若要呼叫 [`setConsent`](/help/web-sdk/commands/setconsent.md) 動作當您的客戶同意偏好設定變更時，請建立標籤規則。 從新增事件開始，然後選擇核心擴充功能的「自訂程式碼」事件型別。

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

此自訂程式碼有兩個作用：

* 設定兩個資料元素，一個包含同意字串，另一個包含 `gdprApplies` 標幟。 稍後在填寫「設定同意」動作時，這會很有用。

* 同意偏好設定變更時觸發規則。 同意偏好設定一旦變更即應使用「設定同意」動作。 在擴充功能中新增「設定同意」動作，並填寫表單，如下所示：

* 標準： 「IAB TCF」
* 版本： 「2.0」
* 值： 「%IAB TCF同意字串%」
* GDPR適用：「%IAB TCF同意GDPR%」

![IAB設定同意動作](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為它們是透過自訂程式碼建立的。 您必須輸入有百分比符號的資料元素名稱。 此程式碼會在客戶變更時，以他們新的同意偏好設定更新他們的設定檔。 此外，伺服器會傳回Cookie值，進而導致Adobe Experience Platform Web SDK無法記錄體驗事件。

## 建立體驗事件的XDM資料元素

同意字串應包含在XDM體驗事件中。 要執行此操作，請使用XDM物件資料元素。 首先，請建立新的XDM物件資料元素，或者使用您已建立的元素來傳送事件。 如果您已將「體驗事件隱私權」結構描述欄位群組新增至結構描述，您應該已有 `consentStrings` 索引鍵。

1. 選取 **[!UICONTROL consentStrings]**.

1. 選擇 **[!UICONTROL 提供個別專案]** 並選取 **[!UICONTROL 新增專案]**.

1. 展開 **[!UICONTROL consentString]** 標題，並展開第一個專案，然後填入下列值：

* `consentStandard`： IAB TCF
* `consentStandardVersion`： 2.0
* `consentStringValue`： %IAB TCF同意字串%
* `gdprApplies`： %IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為它們是透過自訂程式碼建立的。 您必須輸入有百分比符號的資料元素名稱。

## 使用IAB TCF 2.0同意資訊傳送初始體驗事件

如果頁面上的初始體驗事件是由頁面載入事件觸發，則同意字串可能尚未載入。 此規則旨在取代目前的頁面載入事件。 若要確保先載入同意資訊，請建立新規則，並將下列程式碼新增為自訂程式碼事件：

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

此程式碼與先前自訂程式碼相同，唯一例外是兩者皆有 `useractioncomplete` 和 `tcloaded` 事件已處理。 此 [先前的自訂程式碼](#consent-code-1) 客戶首次選擇偏好設定時才會觸發。 當客戶已選擇其偏好設定時，也會觸發此程式碼。 例如，在第二個頁面載入上。

從Platform Web SDK擴充功能新增「傳送事件」動作。 在XDM欄位中，選擇您在上一節中建立的XDM資料元素。

## 使用IAB TCF 2.0同意資訊傳送其他事件

在初始體驗事件後觸發事件時，兩個資料元素仍會定義，且可用於傳送IAB同意資訊。 使用相同的XDM資料元素來傳送未來的事件。 包含IAB TCF 2.0資訊。

## 後續步驟

現在您已瞭解如何使用IAB TCF 2.0搭配Platform Web SDK擴充功能，您也可以選擇與其他Adobe解決方案(例如Adobe Analytics或Adobe Real-time Customer Data Platform)整合。 請參閱 [IAB透明與同意架構2.0概覽](./overview.md) 以取得詳細資訊。
