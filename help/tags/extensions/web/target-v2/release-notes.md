---
title: Adobe Target v2擴充功能發行說明
description: Adobe Experience Platform中Adobe Target v2標籤擴充功能的最新發行說明。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 44%

---

# Adobe Target v2擴充功能發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

## 2021 年 7 月 20 日

### Adobe Target v2 擴充功能 0.15.1 版

- 修正`stringify`函式名稱衝突，導致`sessionId`、`requestId`等產生錯誤UUID值的問題。

## 2021 年 7 月 16 日

### Adobe Target v2 擴充功能 0.15.0 版

- 每當at.js設定secureOnly設為true時，將安全屬性新增至Cookie
- 現在使用`triggerView()`時可使用回應Token
- 修正`CONTENT_RENDERING_NO_OFFERS`事件的相關錯誤。 現在，只要沒有從Target傳回內容，就會正確觸發
- 使用預先擷取請求時，可正確傳回A4T點按量度詳細資料
- UUID產生不再使用`Math.random()`，而是仰賴`window.crypto`
- `sessionId` 每個網路呼叫的Cookie過期時間皆正確延長
- SPA檢視快取初始化現在已正確處理，且會執行`viewsEnable`設定

## 2021 年 6 月 2 日

### Adobe Target v2 擴充功能 0.14.2 版

- 修正最終套件組合包含兩個at.js版本的錯誤，一個具有On-Device Decisioning，另一個沒有。

## 2021 年 5 月 19 日

### Adobe Target v2 擴充功能 0.14.1 版

- 修正v0.14版本導入的回歸，其中Load Target動作會引發全域mbox呼叫

## 2021 年 5 月 14 日

### Adobe Target v2 擴充功能 0.14 版

- 新增具有[裝置上決策](./overview.md#load-target-with-on-device-decisioning)的新動作「載入Target」，其可載入at.js 2.5與裝置上決策功能
- 將at.js更新至2.5


## 2021 年 3 月 25 日

### Adobe Target v2 擴充功能 0.13.7 版

- 已修正 `targetPageParams` 包含在 mbox 要求中的問題。 `targetPageParams` 只應包含在要 `pageLoad` 求中。
- 修正標籤擴充功能中的檔案和視窗全域物件問題，方法是以直接參照取代全域物件相依性。
- 將at.js更新至2.4.1。

## 2021 年 1 月 25 日

### Adobe Target v2 擴充功能 0.13.6 版

- 新增可支援交付 API 客戶 ID 的統一設定檔/平台 ID
- 修正無效的樣式標籤插入作業
- 將at.s更新至2.4.0
- 已解決未定義的參數可能導致傳送請求錯誤的問題

## 2020 年 11 月 25 日

### Adobe Target v2 擴充功能 0.13.4 版

- 修正 UI 未顯示 mbox 參數的錯誤
- 品牌經營更新
- 將 at.js 版本更新至 2.3.3

## 2020 年 7 月 24 日

### Adobe Target v2 擴充功能 0.13.3 版

- 修正非使用中活動 QA 模式連結無效所造成的錯誤
- 修正指令碼或程式碼將 `default` 屬性新增至 `window` 或 `document` 時，擴充功能無法運作的錯誤

## 2020 年 6 月 15 日

### Adobe Target v2 擴充功能 0.13.2 版

- 修正使用 CNAME 和 Edge 覆寫時，at.js 1.x 可能建立錯誤的伺服器網域，而導致 Target 要求失敗的問題
- 修正使用Target的v2標籤擴充功能和Adobe Analytics標籤擴充功能時，Target會延遲Analytics sendBeacon呼叫的問題
- 改善 `deviceIdLifetime` 設定，透過 `targetGlobalSettings` 將其設定為可覆寫

## 2020 年 3 月 25 日

### Adobe Target v2 擴充功能 0.13.0 版

- 已將 at.js 更新至 v2.3。
- 在 adobe.target.getOffer API 中新增 Target 全域 Mbox 支援
- 修正參數和頁面載入參數未正確處理的問題

## 2019 年 10 月 10 日

### Adobe Target v2 擴充功能 0.12.0 版

- 已將 at.js 更新至 v2.2。
- 已改善 Experience Cloud ID 程式庫 (ECID) v4.4 與 at.js 2.2 之間整合的效能。
- 之前，ECID 程式庫要進行兩次封鎖呼叫，at.js 才能擷取體驗。這已簡化為單一呼叫，可大幅提升效能。

>[!NOTE]
>請將您的ECID標籤擴充功能升級至v4.4.1，以運用此效能增強功能。

## 2019 年 7 月 31 日

### Adobe Target v2 擴充功能 0.11.1 版

- 更新擴充功能版本，以使用 at.js 2.1.1
- 新增處理參數的相關修正

## 2019 年 6 月 3 日

### Adobe Target v2 擴充功能 0.11.0 版

- 支援at.js 2.1的新標籤擴充功能
