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
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## v0.19.2 （2023年2月14日）

- 修正允許將逾時設為資料元素的問題。

## v0.19.1 （2023年2月3日）

- 更新以支援 `at.js` v2.10.1
- 使用者端自訂Mbox引數現在可正確支援點標籤法
- VEC中不再進行傳遞呼叫

## v0.19.0 （2022年9月19日）

- 更新以支援 `at.js` v2.10.0
- 新增跨網域追蹤支援。

## v0.18.0 （2022年6月1日）

- 更新以支援 `at.js` v2.9.0
- 新增的「使用者代理用戶端提示」支援。

## v0.17.1 （2022年1月28日）

- 更新以支援 `at.js` v2.8.1
- 固定 `pageLoad` 未對應到 `target-global-mbox` 在ODD混合執行模式下
- 已修正的分析詳細資料問題 `mbox` 請求
- 升級開發相依性以修正安全性弱點

## v0.17.0 （2022年1月7日）

- 更新以支援 `at.js` v2.8.0，現在正在收集功能使用情況和效能遙測資料。  不會收集個人資料。若要選擇退出此功能，請設定 `telemetryEnabled` 至 `false` 在 `targetGlobalSettings`.

## v0.16.0 （2021年10月28日）

- 更新以支援 `at.js` v2.7.0，現可透過Adobe Target下載。

## v0.15.1 （2021年7月20日）

- 已修正的問題 `stringify` 函式名稱衝突，導致產生的UUID值不正確 `sessionId`， `requestId`、等等。

## v0.15.0 （2021年7月16日）

- 每當發生以下情況時，為Cookie新增安全屬性： `at.js` 設定secureOnly設為true
- 回應Token現在可使用於 `triggerView()`
- 修正與相關的錯誤 `CONTENT_RENDERING_NO_OFFERS` 事件。 現在只要沒有從Target傳回內容，就會正確觸發
- 使用預先擷取請求時，會正確傳回A4T點選量度詳細資料
- UUID產生不再使用 `Math.random()`，但須仰賴 `window.crypto`
- `sessionId` Cookie過期在每次網路呼叫時會正確延長
- SPA檢視快取初始化現在可以正確處理並遵循 `viewsEnable` 設定

## v0.14.2 （2021年6月2日）

- 修正最終套件組合包含兩個的錯誤 `at.js` 版本，一個包含「裝置上決策」，另一個不包含。

## v0.14.1 （2021年5月19日）

- v0.14版本中推出的修正回歸，其中Load Target動作會引發全域mbox呼叫

## v0.14 （2021年5月14日）

- 已新增以下專案的新動作：載入Target [裝置上決策](./overview.md#load-target-with-on-device-decisioning)，會載入 `at.js` 2.5搭配裝置上決策功能
- 已更新 `at.js` 至2.5


## v0.13.7 （2021年3月25日）

- 已修正 `targetPageParams` 包含在 mbox 要求中的問題。 `targetPageParams` 僅應包含在 `pageLoad` 要求。
- 已修正標籤擴充功能中的檔案和視窗全域物件的問題，方法是用全域物件的直接參照來取代全域物件相依性。
- 已更新 `at.js` 至2.4.1。

## v0.13.6 （2021年1月25日）

- 新增可支援交付 API 客戶 ID 的統一設定檔/平台 ID
- 修正無效的樣式標籤插入作業
- 將at.s更新至2.4.0
- 未定義的引數可能導致錯誤傳送請求的問題，已解決

## v0.13.4 （2020年11月25日）

- 修正 UI 未顯示 mbox 參數的錯誤
- 品牌經營更新
- 已更新 `at.js` 2.3.3版本

## v0.13.3 （2020年7月24日）

- 修正非使用中活動 QA 模式連結無效所造成的錯誤
- 修正指令碼或程式碼將 `default` 屬性新增至 `window` 或 `document` 時，擴充功能無法運作的錯誤

## v0.13.2 （2020年6月15日）

- 修正使用CNAME和Edge覆寫時的問題，其中 `at.js` 1.x可能會錯誤建立伺服器網域，導致Target請求失敗
- 修正使用Target的v2標籤擴充功能和Adobe Analytics標籤擴充功能時，Target會延遲Analytics sendBeacon呼叫的問題
- 改善 `deviceIdLifetime` 設定，透過 `targetGlobalSettings` 將其設定為可覆寫

## v0.13.0 （2020年3月25日）

- 已更新 `at.js` 升級至v2.3。
- 在 adobe.target.getOffer API 中新增 Target 全域 Mbox 支援
- 修正參數和頁面載入參數未正確處理的問題

## v0.12.0 (2019 年 10 月 10 日)

- 已更新 `at.js` 升級至v2.2。
- 改善Experience CloudID程式庫(ECID) v4.4和之間整合的效能 `at.js` 2.2.
- 之前，ECID程式庫曾進行兩次封鎖呼叫 `at.js` 可擷取體驗。 這已簡化為單一呼叫，可大幅提升效能。

>[!NOTE]
>請將您的ECID標籤擴充功能升級至v4.4.1，以運用此效能增強功能。

## v0.11.1 （2019年7月31日）

- 更新要使用的擴充功能版本 `at.js` 2.1.1
- 新增處理參數的相關修正

## v0.11.0 （2019年6月3日）

- 要支援的新標籤延伸模組 `at.js` 2.1
