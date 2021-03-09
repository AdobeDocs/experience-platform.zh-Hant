---
title: 使用Adobe Experience PlatformWeb SDK整合IAB TCF 2.0支援
description: 瞭解如何在不使用Adobe Experience Platform Launch的情況下為您的網站設定IAB TCF 2.0支援。
seo-description: 瞭解如何透過Adobe Experience PlatformWeb SDK設定IAB TCF 2.0同意
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# 將IAB TCF 2.0支援與平台網頁SDK整合

本指南說明如何在不使用Experience Platform Launch的情況下，將互動式廣告局透明度與同意框架2.0版(IAB TCF 2.0)與Adobe Experience Platform網頁SDK整合。 有關與IAB TCF 2.0整合的概述，請閱讀[overview](./overview.md)。 有關如何與Experience Platform Launch整合的指南，請閱讀[IAB TCF 2.0指南中的Experience Platform Launch](./with-launch.md)。

## 快速入門

本指南使用`__tcfapi`介面訪問許可資訊。 直接與雲端管理提供者(CMP)整合可能會更輕鬆。 但是，本指南中的資訊可能仍然有用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些範例假設在執行程式碼時，會在頁面上定義`window.__tcfapi`。 CMP可提供掛接，在`__tcfapi`對象就緒時，您可在其中運行這些函式。

若要搭配使用IAB TCF 2.0和Experience Platform Launch及Adobe Experience Platform網頁SDK擴充功能，您必須有可用的XDM架構。 如果您未設定其中任一設定，請先檢視此頁面，再繼續。

此外，本指南要求您對Adobe Experience Platform網頁SDK有良好的認識。 如需快速複習，請閱讀[Adobe Experience Platform網頁SDK概觀](../../home.md)和[常見問答](../../web-sdk-faq.md)檔案。

## 啟用預設許可

如果您想要對所有未知的使用者視為相同，可以將預設同意設定為`pending`或`out`。 在收到許可偏好設定之前，此會佇列或放棄體驗事件。

有關預設許可的詳細資訊，請參閱平台Web SDK配置文檔中的[預設許可部分](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 根據`gdprApplies`設定預設同意

有些CMP可讓您判斷通用資料保護規則(GDPR)是否適用於客戶。 如果您想要向不適用GDPR的客戶徵求同意，則可使用TCF API呼叫中的`gdprApplies`旗標。

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

在此示例中，從TCF API獲取`tcData`後，將調用`configure`命令。 如果`gdprApplies`為true，則預設同意設為`pending`。 如果`gdprApplies`為false，預設同意會設為`in`。 請務必使用您的設定填入`alloyConfiguration`變數。

>[!NOTE]
>
>當預設同意設為`in`時，`setConsent`命令仍可用來記錄客戶同意偏好設定。

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

此代碼塊監聽`useractioncomplete`事件，然後設定同意，傳遞同意字串和`gdprApplies`標幟。 如果您有客戶的自訂身分識別，請務必填入`identityMap`變數。 有關呼叫`setConsent`的詳細資訊，請參閱[支援同意](../../consent/supporting-consent.md)指南。

## 在sendEvent中包含同意資訊

在XDM結構中，您可以儲存「體驗事件」的同意偏好資訊。 有兩種方式可將這項資訊新增至每個事件。

首先，您可以在每次`sendEvent`呼叫中提供相關的XDM架構。 下列範例說明執行此動作的一種方式：

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

此示例獲取TCF API的許可資訊，然後發送包含添加到XDM模式的許可資訊的事件。 請參閱[追蹤事件](../../fundamentals/tracking-events.md)指南，瞭解`sendEvent`命令選項中應包含的內容。

將同意資訊新增至每個請求的另一種方式是使用`onBeforeEventSend`回呼。 請參閱追蹤事件檔案中有關全域修改事件[的章節，以取得如何執行此動作的詳細資訊。](../../fundamentals/tracking-events.md#modifying-events-globally)

## 後續步驟

現在您已學會如何搭配使用IAB TCF 2.0與Platform Web SDK擴充功能，您也可以選擇與其他Adobe解決方案整合，例如Adobe Analytics或即時客戶資料平台。 如需詳細資訊，請參閱[IAB透明與同意框架2.0概觀](./overview.md)。
