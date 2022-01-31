---
title: Release Notes for the Adobe Target v2 Extension
description: The latest release notes for the Adobe Target v2 tag extension in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 824fea41bc7e7082814648efd58184f5208e5e6f
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 36%

---

# Adobe Targetv2擴展發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## 2022 年 1 月 28 日

### Adobe Target v2 擴充功能 0.17.1 版

- 已更新為支援 `at.js` v2.8.1
- 固定 `pageLoad` 未映射到 `target-global-mbox` 在ODD混合執行模式中
- 已修復分析詳細資訊的問題 `mbox` 請求
- 已升級開發依賴項以修復安全漏洞

## 2022 年 1 月 7 日

### Adobe Target v2 擴充功能 0.17.0 版

- 已更新為支援 `at.js` v2.8.0，它正在收集功能使用和效能遙測資料。  不會收集個人資料。要選擇退出此功能，請設定 `telemetryEnabled` 至 `false` 在 `targetGlobalSettings`。

## 2021 年 10 月 28 日

### Adobe Target v2 擴充功能 0.16.0 版

- 已更新為支援 `at.js` v2.7.0，現在可從Adobe Target下載。

## 2021 年 7 月 20 日

### Adobe Target v2 擴充功能 0.15.1 版

- 已修復與 `stringify` 函式名稱衝突，導致生成的UUID值不正確 `sessionId`。 `requestId`等等。

## 2021 年 7 月 16 日

### Adobe Target v2 擴充功能 0.15.0 版

- 在任何時間將安全屬性添加到Cookie `at.js` 設定secureOnly設定為true
- Response tokens are now available when using `triggerView()`
- 已修復與 `CONTENT_RENDERING_NO_OFFERS` 的子菜單。 Now it is triggered correctly whenever there is not content returned from Target
- 使用預回遷請求時，A4T按一下度量詳細資訊會正確返回
- UUID生成不再使用 `Math.random()`，但依賴 `window.crypto`
- `sessionId` cookie expiry is correctly extended on every network call
- 視SPA圖快取初始化現在已正確處理，並且 `viewsEnable` 設定

## 2021 年 6 月 2 日

### Adobe Target v2 擴充功能 0.14.2 版

- Fix a bug where the final bundle contains two `at.js` versions, one with On-Device Decisioning and one without.

## 2021 年 5 月 19 日

### Adobe Target v2 擴充功能 0.14.1 版

- 修復v0.14版本引入的回歸，其中Load Target操作正在觸發全局mbox調用

## 2021 年 5 月 14 日

### Adobe Target v2 擴充功能 0.14 版

- 已添加新操作載入目標 [設備上決策](./overview.md#load-target-with-on-device-decisioning)，載入 `at.js` 2.5，具有設備上決策功能
- 已更新 `at.js` 至2.5


## 2021 年 3 月 25 日

### Adobe Target v2 擴充功能 0.13.7 版

- 已修正 `targetPageParams` 包含在 mbox 要求中的問題。 `targetPageParams` should only be included in `pageLoad` requests.
- Fixed an issue with document and window global objects in the tag extension by replacing global object dependencies with direct references to them.
- 已更新 `at.js` 到2.4.1。

## 2021 年 1 月 25 日

### Adobe Target v2 擴充功能 0.13.6 版

- 新增可支援交付 API 客戶 ID 的統一設定檔/平台 ID
- 修正無效的樣式標籤插入作業
- Updated at.s to 2.4.0
- Resolved issue where undefined params can result in bad delivery requests

## 2020 年 11 月 25 日

### Adobe Target v2 擴充功能 0.13.4 版

- 修正 UI 未顯示 mbox 參數的錯誤
- 品牌經營更新
- 已更新 `at.js` 版本至2.3.3

## 2020 年 7 月 24 日

### Adobe Target v2 擴充功能 0.13.3 版

- 修正非使用中活動 QA 模式連結無效所造成的錯誤
- 修正指令碼或程式碼將 `default` 屬性新增至 `window` 或 `document` 時，擴充功能無法運作的錯誤

## 2020 年 6 月 15 日

### Adobe Target v2 擴充功能 0.13.2 版

- Fixed an issue when using CNAME and edge override, where `at.js` 1.x might incorrectly create the server domain, resulting in the Target request failing
- 解決了在將v2標籤擴展用於目標和Adobe Analytics標籤擴展時目標延遲分析sendBeacon調用的問題
- 改善 `deviceIdLifetime` 設定，透過 `targetGlobalSettings` 將其設定為可覆寫

## 2020 年 3 月 25 日

### Adobe Target v2 擴充功能 0.13.0 版

- 已更新 `at.js` 到2.3版。
- 在 adobe.target.getOffer API 中新增 Target 全域 Mbox 支援
- 修正參數和頁面載入參數未正確處理的問題

## 2019 年 10 月 10 日

### Adobe Target v2 擴充功能 0.12.0 版

- Updated `at.js` to v2.2.
- Improved performance for integrations between Experience Cloud ID library (ECID) v4.4 and `at.js` 2.2.
- 以前，ECID庫曾進行兩次阻塞呼叫 `at.js` 能獲得經驗。 這已簡化為單一呼叫，可大幅提升效能。

>[!NOTE]
>請將ECID標籤擴展升級到v4.4.1以利用此效能增強。

## 2019 年 7 月 31 日

### Adobe Target v2 擴充功能 0.11.1 版

- Updated extension version to use `at.js` 2.1.1
- 新增處理參數的相關修正

## 2019 年 6 月 3 日

### Adobe Target v2 擴充功能 0.11.0 版

- New tag extension to support `at.js` 2.1
