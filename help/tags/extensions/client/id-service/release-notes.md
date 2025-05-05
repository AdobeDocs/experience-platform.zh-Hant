---
title: Adobe Experience Cloud Identity Service擴充功能發行說明
description: Adobe Experience Platform中Adobe Experience Cloud Identity服務標籤擴充功能的最新發行說明。
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 62%

---

# Adobe Experience Cloud Identity Service擴充功能發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

本檔案涵蓋Adobe Experience Cloud Identity Service標籤擴充功能的發行說明。 如需Experience CloudIdentity服務本身的發行說明，請參閱[Identity服務檔案](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=zh-Hant)。

## 2022 年 10 月 17 日

### Experience Cloud ID 擴充功能 5.5.0

* 擴充功能現在支援5.5.0版的[訪客JS使用者端](https://github.com/Adobe-Marketing-Cloud/id-service)。 如需特定更新，請參閱[訪客發行說明](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0)。

## 2022年3月9日

### Experience Cloud ID 擴充功能 5.4.0

* 此版本包含最新的Visitor 5.4.0，其中包含下列更新：

   * 能夠使用cookieLifetime設定來設定`s_ecid` Cookie的存留期
   * 更新當頁面載入子iFrame時發生的Firefox瀏覽器問題

## 2021 年 10 月 10 日

### Experience Cloud ID 擴充功能 5.3.1

* 此版本包含最新的Visitor 5.3.0，其中包含下列新更新：

   * 更新演演算法以產生本機ECID
   * 隱私權Cookie的最新選擇加入，包含`Secure`和`SameSite`旗標
   * 修正頁面載入子iFrame時的Firefox瀏覽器問題

## 2021年1月12日

### Experience Cloud ID 擴充功能 5.2.0

* 收到同意時，無法更新至VisitorJS 5.2.0修補程式並修正ECID DataElement。

## 2020 年 11 月 3 日

### Experience Cloud ID 擴充功能 5.2.1

* 此修補程式修正了 Google Chrome 瀏覽器中，從屬性為 `SameSite=None` 的 iFrame 寫入 Cookie 所發生的問題。

## 2020 年 10 月 27 日

### Experience Cloud ID 擴充功能 5.1.0

* 新增 `sameSiteCookie` 設定以指定 `AMCV` Cookie 的 `SameSite` 屬性。此設定支援下列 `SameSite` 屬性值：

   * `Strict`
   * `Lax`
   * `None`

[Web.dev](https://web.dev/samesite-cookies-explained/) 和 [chromium](https://www.chromium.org/updates/same-site) 上有這些屬性值的詳細資訊


## 2020 年 8 月 13 日

### Experience Cloud ID 擴充功能 5.0.1

* 更新至 VisitorJS 5.0.1 修補程式，並修正 IAB 同意字串變更時新增 d_cf 標幟。

## 2020 年 6 月 15 日

### Experience Cloud ID 擴充功能 5.0.0

* 新增 `IAB TCF` 支援 – 透明度與同意框架 – `Version 2.0`。

## 2020 年 4 月 13 日

### Experience Cloud ID 擴充功能 4.6.0

* 將 `loadSSL` 標幟預設為開啟。所有對 Identity 服務的呼叫均預設為透過 `https` 發出。如果客戶想從 non-ssl 頁面透過 http 呼叫 Identity 服務，可將其設為 false。
* 更新偵測 Internet-Explorer (IE) 版本的函數，以修正 ESLint 回報的問題。
* 修正 ECID 獲得 optIn 預先核准並稍後才更新時 Internet-Explorer (IE) 11 所發生的效能問題。

## 2020 年 1 月 22 日

### Experience Cloud ID 擴充功能 4.5.2

* 將 visitor.js 更新至 4.5.2
* Visitor 4.5.1 包含 Optin 的 IAB 外掛程式錯誤修正
* 更新 `setCustomerIDs` 方法，拒絕所傳送的任何空 ID。

## 2020 年 1 月 7 日

### Experience Cloud ID 擴充功能 4.4.2

* 將 visitor.js 更新至 4.4.2
* 加速擷取值的 `getVisitorValues` 方法


## 2019 年 9 月 19 日

### Experience Cloud ID 擴充功能 4.4.1

* 將 visitor.js 更新至 4.4.1
* 修正取得 Opt-In preApprovals Input 的錯誤
* 將 preOptInApprovals 中的 VIDEO_ANALYTICS 重新命名為 MEDIA_ANALYTICS

  ![](../../../images/ecid-media-analytics.png)

## 2019 年 7 月 17 日

### Experience Cloud ID 擴充功能 4.4.0

* 將 visitor.js 更新至 4.4.0
* 新增 setCustomerIDs 的 SHA256 雜湊支援

  ![](../../../images/ecid-setCustomerIDs-hash.png)

## 2019 年 5 月 13 日

### Experience Cloud ID 擴充功能 4.3.1

* 將 visitor.js 更新至 4.3
* 在標籤擴充功能中新增ECID的資料元素型別

  ![](../../../images/ecid-data-element.png)

## 2019 年 4 月 9 日

### Experience Cloud ID 擴充功能 4.2.0

* 將 visitor.js 更新至 4.2 版，包含支援 Audience Manager IAB TCF 外掛程式

## 2019 年 2 月 25 日

### Experience Cloud ID 擴充功能 4.1.0

* 將 visitor.js 更新至 4.1，4.1 已根據新 API 的變更更新 publishDestinations。透過此更新，頁面的反向連結資訊可在 ID 同步期間公開 (如有需要)。

## 2019 年 2 月 15 日

### Experience Cloud ID 擴充功能 4.0.0

* 將 visitor.js 更新至 4.0
* 為全新內建的選擇加入物件新增的設定選項。選擇加入設定可用來隱藏 Adobe 解決方案的 Cookie 和信標呼叫，以更密切支援 GDPR 等規範

  ![](../../../images/ext-mcid-opt-in.png)

## 2018 年 3 月 20 日

### Experience Cloud ID 擴充功能 3.1.0

* 將 visitor.js 更新至 3.1
* 新增兩個設定屬性：`resetBeforeVersion` 和 `serverState`
