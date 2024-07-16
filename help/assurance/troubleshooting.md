---
title: Adobe Experience Platform Assurance 疑難排解指南
description: 本文件會概述使用 Adob​​e Experience Platform Assurance 時常見問題的解決方案。
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 100%

---

# 對 Adobe Experience Platform Assurance 進行疑難排解

如果您使用 Assurance 時發生問題，請查看下列問題主題項下的建議，即可解決會遇到的常見問題。

為了實現更順暢的實作並探索任何可能的問題，請確保您已依照「快速入門」一節中的「[啟用偵錯記錄](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/)」開啟 SDK 記錄。

您可以使用 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API 變更 SDK 紀錄層級。

## 裝置上的應用程式問題

### QR 碼無法開啟應用程式

* 直接存取連結。從&#x200B;**工作階段詳細資料**&#x200B;複製連結。將其貼到裝置的瀏覽器網址列中以將其開啟。如果無法開啟，請參閱「[應用程式無法開啟連結](#app-does-not-open-link)」一節。
* 使用不同的 QR 助讀程式。若為 iOS 11 或更高版本，請使用 Photo 應用程式讀取 QR 碼。

### 應用程式無法開啟連結

* 驗證應用程式中的深度連結設定是否正確。
   * **Android：**&#x200B;深度連結 (應用程式連結)
      * [建立應用程式內容的深度連結](https://developer.android.com/training/app-links/deep-linking)
   * **iOS：**&#x200B;自訂 URL 綱要或通用連結
      * [定義您的應用程式的自訂 URL 綱要](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [支援您的應用程式中的通用連結](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>若為 Android，不需要明確呼叫 `startSession` API。若為 iOS，請依照 [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core) 中的說明使用 API。

### 驗證覆蓋會隨即顯示，但應用程式無法連線

* 透過裝置 Web 瀏覽器確保裝置的網際網路連線能力。
* 如果應用程式一直都無法和 Assurance 服務連線成功，請確保 Assurance 的設定正確。請參閱有關安裝 [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK 資料庫的說明。
* 驗證工作階段是否和連結相符，以及是否已正確輸入預期的工作階段。請參閱[紀錄訊息「無法取得 OrgID 資訊」](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (這並非常見情況，而且只有在您有權存取多個 ORG 執行個體時才相關)。

### Adobe Analytics 偵錯

**後續處理狀態 - 無偵錯標幟**

在您的 Analytics 事件檢視中，如果事件失敗並顯示「無偵錯標幟」的後續處理狀態，則您目前的 Adob&#x200B;&#x200B;e Analytics 或 Assurance SDK 版本可能不支援 Analytics 偵錯功能。
請將 Adob&#x200B;&#x200B;e Analytics 和 Assurance SDK 擴充功能升級為最新版本，即可解決此問題。

| 最低版本需求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### React Native MobileCore 和 AEPAssurance 的相容性

| AEP Assurance 版本 | Mobile Core 版本 | 安裝說明 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您正在使用具有 Assurance 的 `react-native-acpcore`，則出現下列其中一則錯誤訊息時，React Native 應用程式即可能無法建置：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解決方案**

如果發生這種情況，請使用以下 npm 命令將您的 `react-native-aepassurance` 降級：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

會出現此錯誤是因為 `react-native-acpcore` 擴充功能&#x200B;**只和** `react-native-aepassurance` 2.xx 及以下版本相容。
