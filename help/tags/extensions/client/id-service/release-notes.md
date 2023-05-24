---
title: Adobe Experience Cloud身份服務擴展發行說明
description: Adobe Experience Cloud身份服務標籤擴展在Adobe Experience Platform的最新發行說明。
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 64%

---

# Adobe Experience CloudIdentity Service擴展發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

本文檔介紹Adobe Experience Cloud身份服務標籤擴展的發行說明。 有關Experience Cloud身份服務本身的發行說明，請參閱 [Identity Service文檔](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html)。

## 2022年10月17日

### Experience Cloud ID 擴充功能 5.5.0

* 擴展現在支援5.5.0版 [訪問者JS客戶端](https://github.com/Adobe-Marketing-Cloud/id-service)。 請參閱 [訪問者發佈說明](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0) 的子菜單。

## 2022年3月9日

### Experience Cloud ID 擴充功能 5.4.0

* 此版本包含最新的訪問者5.4.0，該訪問者具有以下更新：

   * 能夠配置 `s_ecid` cookie使用cookieLifetime配置
   * 在子iFrame中載入頁面時發生的Firefox瀏覽器問題的更新

## 2021年10月10日

### Experience Cloud ID 擴充功能 5.3.1

* 此版本包含最新的訪問者5.3.0，該訪問者具有以下新更新：

   * 更新的算法以生成本地ECID
   * 最新選擇加入 `Secure` 和 `SameSite` 隱私cookie的標誌
   * 在子iFrame中載入頁面時修復Firefox瀏覽器問題

## 2021 年 1 月 12 日

### Experience Cloud ID 擴充功能 5.2.0

* 在接收同意後，無法使用ECID DataElement的修復程式更新到VisitorJS 5.2.0修補程式。

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
* 作為標籤擴展的一部分為ECID添加的資料元素類型

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
