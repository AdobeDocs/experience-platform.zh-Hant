---
title: Adobe Experience Platform保障故障排除指南
description: 本文檔概述了使用Adobe Experience Platform保障時常見問題的解決方案。
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# 診斷Adobe Experience Platform保證

如果您在使「保證」工作時遇到問題，請參閱以下問題主題下的建議，以解決常見問題。

要使實施更順利並發現任何潛在問題，請確保每次開啟SDK日誌記錄 [啟用調試日誌記錄](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) 中。

可以使用 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API。

## 設備上、應用程式問題

### QR代碼未開啟應用

* 直接訪問連結。 從複製連結 **會話詳細資訊**。 將其貼上到設備的瀏覽器地址欄中以將其開啟。 如果未開啟，請參閱 [應用程式將不會開啟連結](#app-does-not-open-link)。
* 使用其他QR讀取器。 對於iOS11或更高版本，請使用照片應用閱讀QR碼。

### 應用未開啟連結

* 驗證是否在應用中正確配置了深度連結實現。
   * **Android:** 深度連結（應用程式連結）
      * [建立深度連結到應用上下文](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** 自定義URL方案或通用連結
      * [為應用定義自定義URL方案](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [支援應用程式中的通用連結](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>對於Android, `startSession` 不需要顯式調用API。 對於iOS，使用中所述的API [Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core)。

### 出現身份驗證覆蓋，但應用無法連接

* 通過設備Web瀏覽器確保設備的Internet連接。
* 如果應用程式從未成功連接到Assurance服務，請確保已為Assurance正確設定它。 請參閱安裝 [Adobe Experience Platform](./tutorials/implement-assurance.md) SDK庫。
* 驗證會話是否與連結匹配，並且是否為預期會話正確輸入。 請參閱 [日誌消息「OrgID資訊不可用」](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) （只有在您有權訪問多個ORG實例時，這才不常見且相關）。

### Adobe Analytics調試

**後處理狀態 — 無調試標誌**

在「分析事件」視圖中，如果事件在「後處理狀態」為「無調試標誌」時失敗，則當前的Adobe Analytics或保障SDK版本可能不支援分析調試功能。
請將Adobe Analytics和Assurance SDK擴展升級到最新版本以解決此問題。

| 最低版本要求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| 保證 | > 1.0.0 | > 1.0.0 |

### 響應本機MobileCore和AEPAs保證相容性

| AEP保證版本 | 移動核心版本 | 安裝說明 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [反應本機 — acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [反應本機 — aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您使用 `react-native-acpcore` 有了保證， React Native應用程式可能無法生成以下錯誤消息之一：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解決方法**

如果出現這種情況，請降級 `react-native-aepassurance` 使用以下npm命令：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

出現此錯誤是因為 `react-native-acpcore` 擴展 **僅** 相容 `react-native-aepassurance` 版本2.x.x和更低版本。
