---
title: Adobe Target擴充功能發行說明
description: Adobe Experience Platform中Adobe Target標籤擴充功能的最新發行說明。
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 70%

---

# Adobe Target發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

## 2021 年 9 月 16 日

### Adobe Target 擴充功能 0.11.4 版

* 更新至at.js v1.8.3
* 在設定Cookie時新增`SameSite=None`和`Secure`屬性

## 2020 年 7 月 24 日

### Adobe Target 擴充功能 0.11.3 版

* 修正指令碼或程式碼將 `default` 屬性新增至 `window` 或 `document` 時，擴充功能無法運作的錯誤 

## 2020 年 6 月 15 日

### Adobe Target 擴充功能 0.11.2 版

* 修正使用 CNAME 和 Edge 覆寫時，at.js 1.x 可能建立錯誤的伺服器網域，而導致 Target 請求失敗的問題

## 2020 年 3 月 25 日

### Adobe Target 擴充功能 0.11.1 版

* 已將 at.js 更新至 v1.8.1
* 修正參數和頁面載入參數未正確處理的問題

## 2019 年 10 月 10 日

### Adobe Target 擴充功能 0.11.0 版

* 已將 at.js 更新至 v1.8。
* 已改善 Experience Cloud ID 程式庫 (ECID) v4.4 與 at.js 1.8 之間整合的效能。
* 之前，ECID 程式庫要進行兩次封鎖呼叫，at.js 才能擷取體驗。這已簡化為單一呼叫，可大幅提升效能。

>[!NOTE]
>請將您適用於Adobe Experience Platform的ECID標籤擴充功能升級至v4.4.1，以運用此效能增強功能。

## 2019 年 7 月 31 日

### Adobe Target 擴充功能 0.10.1 版

* 處理Adobe Target標籤擴充功能的引數Hotfix

## 2019 年 5 月 4 日

### Adobe Target 擴充功能 0.10.0 版

* 修正因最新 Google Chrome 變更所造成的資料元素問題

## 2019 年 3 月 14 日

### Adobe Target 擴充功能 0.9.3 版

* 更新擴充功能版本，以使用 at.js 1.7.1

## 2019 年 2 月 20 日

### Adobe Target 擴充功能 0.9.2 版

* 修正 Target 與 Analytics 擴充功能之間的競爭條件

## 2019 年 2 月 12 日

### Adobe Target 擴充功能 0.9.1 版

#### **功能**

* 更新擴充功能，以使用透過標籤支援選擇加入隱私權功能的at.js 1.7.0，進而控制Target標籤的引發方式和時機。 請參閱標籤檔案，瞭解如何設定您的選擇加入實施作法。 新增自訂具有空白值的 mbox 參數是否應傳送至 Target 的可能性。

## 2019 年 1 月 23 日

### Adobe Target 擴充功能 0.8.4 版

* 將 at.js 更新至 1.6.4 版
* 擴充功能 UI 移轉至 Adobe Spectrum

## 2018 年 11 月 15 日

### Adobe Target 擴充功能 0.8.2 版

* 將 at.js 更新至 1.6.3 版

## 2018 年 10 月 24 日

### Adobe Target 擴充功能 0.8.1 版

* 將 at.js 更新至 1.6.2 版

## 2018 年 8 月 23 日

### Adobe Target 擴充功能 0.8.0 版

* 將 at.js 更新至 1.6.0 版

## 2018 年 8 月 10 日

### Adobe Target 擴充功能 0.7.2 版

* 微幅變更
* 更新 `extension.json` 檔案中的 `exchangeUrl` 屬性

## 2018 年 8 月 1 日

### Adobe Target 擴充功能 0.7.1 版

* 微幅修正

## 2018 年 6 月 18 日

### Adobe Target 擴充功能 0.7.0 版

* 將 at.js 版本更新至 1.5.0
* 修正 Media Optimizer 在 IE 11 中擲出 Null 參考錯誤的問題

## 2018 年 6 月 15 日

### Adobe Target 擴充功能 0.6.0 版

#### **功能**

* Target 擴充功能已更新，以使用 at.js v1.3.1。當您使用 Analytics 部署 Target 時，現在會等到所有 Target 呼叫 (包括重新導向選件) 都解決後，Analytics 才會引發，這樣解決了之前存在的競爭條件。

## 2018 年 2 月 22 日

### Adobe Target 擴充功能 0.4.1 版

#### **功能**

* 將 Adobe Exchange 清單新增至 extension.json
* 新增檢查，以查看 Target 是否已停用，以及 Authoring 是否已啟用

#### **錯誤修正**

* 修正Adobe Target擴充功能中，視覺化體驗撰寫器在透過標籤部署時無法取消隱藏頁面的錯誤。

## 2018 年 2 月 8 日

### Adobe Target 擴充功能 0.4.0 版

#### **功能**

* 更新擴充功能設定畫面中的檢視
* at.js 已更新至 1.2.3 版 (新增支援 JSON 選件)
