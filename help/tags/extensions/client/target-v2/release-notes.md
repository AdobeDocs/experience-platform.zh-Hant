---
title: Adobe Targetv2擴展版發行說明
description: Adobe Targetv2標籤擴展在Adobe Experience Platform的最新發行說明。
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: ffbb68c9c84b834984e1adb2640d8806ce9f9962
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 24%

---

# Adobe Targetv2擴展發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## v0.19.2（2023年2月14日）

- 解決了允許將超時設定為資料元素的問題。

## v0.19.1（2023年2月3日）

- 已更新為支援 `at.js` v2.10.1
- 客戶端自定義Mbox參數現在正確支援點標籤
- 不再在VEC中進行傳遞呼叫

## v0.19.0（2022年9月19日）

- 已更新為支援 `at.js` v2.10.0
- 添加了跨域跟蹤支援。

## v0.18.0（2022年6月1日）

- 已更新為支援 `at.js` v2.9.0
- 新增的「使用者代理用戶端提示」支援。

## v0.17.1（2022年1月28日）

- 已更新為支援 `at.js` v2.8.1
- 固定 `pageLoad` 未映射到 `target-global-mbox` 在ODD混合執行模式中
- 已修復分析詳細資訊的問題 `mbox` 請求
- 已升級開發依賴項以修復安全漏洞

## v0.17.0（2022年1月7日）

- 已更新為支援 `at.js` v2.8.0，它正在收集功能使用和效能遙測資料。  不會收集個人資料。要選擇退出此功能，請設定 `telemetryEnabled` 至 `false` 在 `targetGlobalSettings`。

## v0.16.0（2021年10月28日）

- 已更新為支援 `at.js` v2.7.0，現在可從Adobe Target下載。

## v0.15.1（2021年7月20日）

- 已修復與 `stringify` 函式名稱衝突，導致生成的UUID值不正確 `sessionId`。 `requestId`等等。

## v0.15.0（2021年7月16日）

- 在任何時間將安全屬性添加到Cookie `at.js` 設定secureOnly設定為true
- 現在，當使用 `triggerView()`
- 已修復與 `CONTENT_RENDERING_NO_OFFERS` 的子菜單。 現在，只要沒有從目標返回內容，就會正確觸發它
- 使用預回遷請求時，A4T按一下度量詳細資訊會正確返回
- UUID生成不再使用 `Math.random()`，但依賴 `window.crypto`
- `sessionId` 每次網路呼叫的cookie到期時間都正確延長
- 視SPA圖快取初始化現在已正確處理，並且 `viewsEnable` 設定

## v0.14.2（2021年6月2日）

- 修復最終捆綁包包含兩個 `at.js` 版本，一個帶有設備上決策，一個沒有。

## v0.14.1（2021年5月19日）

- 修復v0.14版本引入的回歸，其中Load Target操作正在觸發全局mbox調用

## v0.14（2021年5月14日）

- 已添加新操作載入目標 [設備上決策](./overview.md#load-target-with-on-device-decisioning)，載入 `at.js` 2.5，具有設備上決策功能
- 已更新 `at.js` 至2.5


## v0.13.7（2021年3月25日）

- 已修正 `targetPageParams` 包含在 mbox 要求中的問題。 `targetPageParams` 應僅包括在 `pageLoad` 請求。
- 通過將全局對象相關性替換為對它們的直接引用，解決了標籤擴展中的文檔和窗口全局對象的問題。
- 已更新 `at.js` 到2.4.1。

## v0.13.6（2021年1月25日）

- 新增可支援交付 API 客戶 ID 的統一設定檔/平台 ID
- 修正無效的樣式標籤插入作業
- 更新時間：2.4.0
- 已解決的問題，其中未定義的參數可能導致錯誤的傳遞請求

## v0.13.4（2020年11月25日）

- 修正 UI 未顯示 mbox 參數的錯誤
- 品牌經營更新
- 已更新 `at.js` 版本至2.3.3

## v0.13.3（2020年7月24日）

- 修正非使用中活動 QA 模式連結無效所造成的錯誤
- 修正指令碼或程式碼將 `default` 屬性新增至 `window` 或 `document` 時，擴充功能無法運作的錯誤

## v0.13.2（2020年6月15日）

- 使用CNAME和邊覆蓋時修復問題，其中 `at.js` 1.x可能錯誤地建立伺服器域，導致目標請求失敗
- 解決了在將v2標籤擴展用於目標和Adobe Analytics標籤擴展時目標延遲分析sendBeacon調用的問題
- 改善 `deviceIdLifetime` 設定，透過 `targetGlobalSettings` 將其設定為可覆寫

## v0.13.0（2020年3月25日）

- 已更新 `at.js` 到2.3版。
- 在 adobe.target.getOffer API 中新增 Target 全域 Mbox 支援
- 修正參數和頁面載入參數未正確處理的問題

## v0.12.0 (2019 年 10 月 10 日)

- 已更新 `at.js` 到2.2版。
- Experience CloudID庫(ECID)v4.4與 `at.js` 2.2
- 以前，ECID庫曾進行兩次阻塞呼叫 `at.js` 能獲得經驗。 這已簡化為單一呼叫，可大幅提升效能。

>[!NOTE]
>請將ECID標籤擴展升級到v4.4.1以利用此效能增強。

## v0.11.1（2019年7月31日）

- 要使用的更新擴展版本 `at.js` 2.1.1
- 新增處理參數的相關修正

## v0.11.0（2019年6月3日）

- 要支援的新標籤擴展 `at.js` 2.1
