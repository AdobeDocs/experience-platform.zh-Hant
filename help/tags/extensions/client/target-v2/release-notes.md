---
title: Adobe Target v2擴充功能發行說明
description: Adobe Experience Platform中Adobe Target v2標籤擴充功能的最新發行說明。
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: ffbb68c9c84b834984e1adb2640d8806ce9f9962
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 24%

---

# Adobe Target v2擴充功能發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## v0.19.2（2023年2月14日）

- 修正允許將逾時設為資料元素的問題。

## v0.19.1（2023年2月3日）

- 更新以支援 `at.js` v2.10.1
- 用戶端自訂Mbox參數現在可以正確支援點記號
- VEC中不再進行傳送呼叫

## v0.19.0（2022年9月19日）

- 更新以支援 `at.js` v2.10.0
- 新增跨網域追蹤支援。

## v0.18.0（2022年6月1日）

- 更新以支援 `at.js` v2.9.0
- 新增的「使用者代理用戶端提示」支援。

## v0.17.1（2022年1月28日）

- 更新以支援 `at.js` v2.8.1
- 固定 `pageLoad` 未對應至 `target-global-mbox` 在ODD混合執行模式中
- 修正 `mbox` 請求
- 升級開發相依性以修正安全漏洞

## v0.17.0（2022年1月7日）

- 更新以支援 `at.js` v2.8.0，現在正在收集功能使用和效能遙測資料。  不會收集個人資料。若要退出此功能，請設定 `telemetryEnabled` to `false` in `targetGlobalSettings`.

## v0.16.0（2021年10月28日）

- 更新以支援 `at.js` v2.7.0現已可從Adobe Target下載。

## v0.15.1（2021年7月20日）

- 修正 `stringify` 函式名稱衝突，導致產生不正確的UUID值 `sessionId`, `requestId`等。

## v0.15.0（2021年7月16日）

- 每當 `at.js` settings secureOnly設定為true
- 現在，回應Token可在使用 `triggerView()`
- 修正 `CONTENT_RENDERING_NO_OFFERS` 事件。 現在，只要沒有從Target傳回內容，就會正確觸發
- 使用預先擷取請求時，可正確傳回A4T點按量度詳細資料
- UUID產生不再使用 `Math.random()`，但需仰賴 `window.crypto`
- `sessionId` 每個網路呼叫的Cookie過期時間皆正確延長
- SPA檢視快取初始化現在已正確處理，並遵循 `viewsEnable` 設定

## v0.14.2（2021年6月2日）

- 修正最終套件組合包含兩個 `at.js` 版本：一個有裝置決策功能，另一個沒有。

## v0.14.1（2021年5月19日）

- 修正v0.14版本導入的回歸，其中Load Target動作會引發全域mbox呼叫

## v0.14（2021年5月14日）

- 新增「載入Target」的新動作，其具有 [裝置上決策](./overview.md#load-target-with-on-device-decisioning)，會載入 `at.js` 2.5具備裝置決策功能
- 已更新 `at.js` 到2.5


## v0.13.7（2021年3月25日）

- 已修正 `targetPageParams` 包含在 mbox 要求中的問題。 `targetPageParams` 只應包含在 `pageLoad` 要求。
- 修正標籤擴充功能中的檔案和視窗全域物件問題，方法是以直接參照取代全域物件相依性。
- 已更新 `at.js` 2.4.1。

## v0.13.6（2021年1月25日）

- 新增可支援交付 API 客戶 ID 的統一設定檔/平台 ID
- 修正無效的樣式標籤插入作業
- 將at.s更新至2.4.0
- 已解決未定義的參數可能導致傳送請求錯誤的問題

## v0.13.4（2020年11月25日）

- 修正 UI 未顯示 mbox 參數的錯誤
- 品牌經營更新
- 更新 `at.js` 2.3.3版

## v0.13.3（2020年7月24日）

- 修正非使用中活動 QA 模式連結無效所造成的錯誤
- 修正指令碼或程式碼將 `default` 屬性新增至 `window` 或 `document` 時，擴充功能無法運作的錯誤

## v0.13.2（2020年6月15日）

- 修正使用CNAME和Edge覆寫時， `at.js` 1.x可能會錯誤建立伺服器網域，導致Target請求失敗
- 修正使用Target的v2標籤擴充功能和Adobe Analytics標籤擴充功能時，Target會延遲Analytics sendBeacon呼叫的問題
- 改善 `deviceIdLifetime` 設定，透過 `targetGlobalSettings` 將其設定為可覆寫

## v0.13.0（2020年3月25日）

- 已更新 `at.js` 到v2.3。
- 在 adobe.target.getOffer API 中新增 Target 全域 Mbox 支援
- 修正參數和頁面載入參數未正確處理的問題

## v0.12.0 (2019 年 10 月 10 日)

- 已更新 `at.js` 到v2.2。
- 改善Experience CloudID程式庫(ECID)v4.4與 `at.js` 2.2。
- 之前，ECID程式庫會先執行兩次封鎖呼叫 `at.js` 可擷取體驗。 這已簡化為單一呼叫，可大幅提升效能。

>[!NOTE]
>請將您的ECID標籤擴充功能升級至v4.4.1，以運用此效能增強功能。

## v0.11.1（2019年7月31日）

- 更新擴充功能版本以使用 `at.js` 2.1.1
- 新增處理參數的相關修正

## v0.11.0（2019年6月3日）

- 支援的全新標籤擴充功能 `at.js` 2.1
