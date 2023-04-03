---
title: Adobe Experience Platform保障疑難排解指南
description: 本檔案概述使用Adobe Experience Platform Assurance時常見問題的解決方案。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---


# 疑難排解Adobe Experience Platform保證

如果您無法讓「保證」運作，請參閱下列問題主題下的建議，以解決常見的問題。

若要讓實作更順暢，並找出任何潛在問題，請確定您已透過 [啟用偵錯記錄](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) （在快速入門區段中）。

您可以使用 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API。

## 裝置上、應用程式問題

### QR碼未開啟應用程式

* 直接存取連結。 複製連結的來源 **工作階段詳細資料**. 貼到裝置的瀏覽器位址列以開啟它。 如果未開啟，請參閱區段 [應用程式不會開啟連結](#app-does-not-open-link).
* 使用不同的QR讀取器。 若為iOS 11或更新版本，請使用像片應用程式來閱讀QR碼。

### 應用程式未開啟連結

* 確認應用程式中的深層連結實作已正確設定。
   * **Android:** 深層連結（應用程式連結）
      * [建立應用程式內容的深層連結](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** 自訂URL配置或通用連結
      * [定義應用程式的自訂URL配置](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [支援應用程式中的通用連結](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>若為Android, `startSession` 不需明確呼叫API。 若為iOS，請依照 [Adobe Experience Platform保障](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### 驗證覆蓋會出現，但應用程式無法連線

* 通過設備Web瀏覽器確保設備的Internet連接。
* 如果應用程式從未成功連線至保證服務，請確定已正確設定以保證。 請參閱安裝 [Adobe Experience Platform保障](./tutorials/implement-assurance.md) SDK程式庫。
* 確認工作階段符合連結，且已為預期的工作階段正確輸入。 請參閱 [記錄訊息「OrgID資訊不可用」](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) （只有在您可存取多個ORG例項時，才不常見且相關）。

### Adobe Analytics除錯

**後處理狀態 — 無調試標誌**

在您的Analytics事件檢視中，如果事件因處理後狀態「無除錯標幟」而失敗，您目前的Adobe Analytics或Assurance SDK版本可能不支援Analytics除錯功能。
請將Adobe Analytics和Assurance SDK擴充功能升級至最新版本，以解決此問題。

| 最低版本需求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| 保證 | > 1.0.0 | > 1.0.0 |

### React Native MobileCore和AEPAssurance相容性

| AEP保證版本 | 行動核心版本 | 安裝指示 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您使用 `react-native-acpcore` 有了保證， React本機應用程式可能會無法建置，並出現下列其中一則錯誤訊息：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解決方法**

如果發生這種情況，請降級 `react-native-aepassurance` 使用下列npm命令：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

發生此錯誤是因為 `react-native-acpcore` 擴充功能為 **僅限** 相容 `react-native-aepassurance` 2.x.x版及更新版本。
