---
title: Adobe Target v2擴充功能發行說明
description: Adobe Experience Platform中Adobe Target v2標籤擴充功能的最新發行說明。
source-git-commit: 573c13f5136a4efc3accf2838783a91ea914e949
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 53%

---

# Adobe Target v2擴充功能發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

## 2021 年 5 月 19 日

### Adobe Target v2 擴充功能 0.14.1 版

- 修正v0.14版本導入的回歸，其中Load Target動作會引發全域mbox呼叫

## 2021 年 5 月 14 日

### Adobe Target v2 擴充功能 0.14 版

- 新增具有[裝置上決策](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/targetv2-extension/adobe-target-extension-v2.html?lang=en#load-target-with-on-device-decisioning)的新動作「載入Target」，其可載入at.js 2.5與裝置上決策功能
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
