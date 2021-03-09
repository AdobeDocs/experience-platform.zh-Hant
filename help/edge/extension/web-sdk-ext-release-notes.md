---
title: Adobe Experience Platform網頁SDK擴充功能發行說明
description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 擴充功能
seo-description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 擴充功能
translation-type: tm+mt
source-git-commit: 14cf62084c88956906cd9454176619ed08081a0e
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 79%

---


# Adobe Experience Platform網頁SDK擴充功能發行說明

本檔案涵蓋適用於Adobe Experience Platform Launch的Adobe Experience Platform網頁SDK擴充功能的發行說明。 如需SDK本身的最新發行說明，請參閱[平台網頁SDK發行說明](https://docs.adobe.com/content/help/zh-Hant/experience-platform/edge/release-notes.html)。

## 2020 年 3 月 9 日

### Adobe Experience Platform Web SDK 2.4.0

包含 2.4.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增[「檔案卸載」](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)核取方塊至「傳送事件動作UI」。
* 新增在[設定預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)時支援`out`選項，此預設同意會丟棄所有事件直到收到同意（現有的`pending`選項會佇列事件，並在收到同意後傳送這些事件）。
* 新增工具提示至預設的同意欄位。
* 新增[Adobe同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支援。
* 如果使用者的存取Token無效或未正確布建，XDM物件資料元素UI現在會顯示更好的錯誤。
* 修正檢視XDM物件資料元素時，瀏覽器開發人員主控台上顯示的跨原始碼錯誤（不影響擴充功能的運作）。

## 2020 年 11 月 4 日

### Adobe Experience Platform Web SDK 2.3.0

包含 2.3.0 版的 Adobe Experience Platform Web SDK 程式庫。

#### 功能

* 已新增在設定預設同意時使用資料元素的支援。
* 已新增以 XDM 物件資料元素類型搜尋 XDM 結構描述的能力。
* 已新增在「傳送事件」動作類型中仿製 XDM 資料，以確保在要求中不會反映對 XDM 資料物件的後續變更。

## 2020 年 10 月 1 日

### Adobe Experience Platform Web SDK 2.2.0

#### 錯誤修正

* 客戶嘗試以沙盒結構描述建立 XDM 物件時，遇到驗證問題。呼叫平台的API現在已知道環境，因此使用者只會看到有權編輯的架構。

#### 功能

* 使用 `identityMap` 資料元素時，下拉式清單現在會預先填入命名空間，因此您不必手動填寫。
* `xdmObject` 資料元素的 UI 已改版。在新的 UI 中，您可以看到哪些欄位已填入，不必在物件中輸入每個項目。


## 2020 年 8 月 26 日

### Adobe Experience Platform Web SDK 2.1.1

#### 功能

* 修正 XDM 物件檢視中，Adobe Experience Platform 沙盒無法正常顯示的問題。使用此版本的擴充功能時，如果清單未顯示預期的沙盒，使用者應向其 Adobe Experience Platform 管理員確認是否已正確設定存取權限。


## 2020 年 8 月 5 日

### Adobe Experience Platform Web SDK 2.1.0

#### 功能

* 重大變更：移除 `syncIdentity` 動作，並改為支援在 `sendEvent` 動作中傳遞這些 ID。升級擴充功能前，請使用此動作停用任何現有規則。
* 更新至 Alloy v. 2.1.0 ([發行說明](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html))
* 在 `setConsent` 動作中支援 IAB 2.0 同意標準。
* 支援在 `sendEvent` 動作中覆寫資料集 ID。
* 新增全新的 `IdentityMap` 類型「資料元素」，可供在 XDM 物件資料元素 (現已啟用) 以及 `setConsent` 動作中填入 `identityMap` 項目。
* 支援在 `setConsent` 動作中傳遞身分對應。
* 支援在XDM物件資料元素中選擇平台沙盒。


## 2020 年 5 月 26 日

### Adobe Experience Platform Web SDK 1.0.0

#### 功能

* 支援在「設定服務」選取環境。


## 2020 年 5 月 4 日

### Adobe Experience Platform Web SDK 0.1.2

#### 功能

* 將 `configId` 重新命名為 `edgeConfigId`。
* 將 `viewStart` 重新命名為 `renderDecisions`，預設為 false。如果設為 true，系統會擷取個人化選件並自動轉譯。
* `Get Decisions` 相關變更：
   * 移除 `getDecisions` 命令。
   * `sendEvent` 命令新增「`scopes`」選項。決策會以 `sendEvent` 所解析的 Promise 傳回。
   * 新增內建 `__view__` 範圍，系統會傳回頁面/檢視範圍選件(例如 Target 的 VEC 選件)。唯有將 `renderDecisions` 設為 false，決策才會從 `sendEvent` 命令傳回。
   * 新增 `Decisions Received` 事件，決策可供使用時就會觸發。
* 整合單一伺服器呼叫中的多個個人化通知。
* 修正每次參考資料元素時，「事件合併 ID」都會重設的問題。
* 將 `setCustomerIds` 動作重新命名為 `syncIdentity`。
* 新增 `getIdentity` 命令。目前僅能透過自訂程式碼使用。
* 使用`_satellite`啟用除錯\&#39;b5\&#39;7b在可啟用Adobe Experience Platform網頁SDK中的除錯\&#39;a5\&#39;5c能。
* 新增在 XDM 物件中輸入值的相關支援：布林值、數字和小數。

## 2020 年 3 月 16 日

### Adobe Experience Platform Web SDK 0.0.10

#### 功能

* 整合 `Consent` 底下的「選擇加入」和「選擇退出」概念，並新增 `setConsent` 命令。
* 新增可從 JavaScript/JSON 對應至 XDM 的新資料元素類型 `XDM Object`。

## 2020 年 2 月 18 日

### Adobe Experience Platform Web SDK 0.0.7

#### 功能

* 移除 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 選項
* 支援在 edgeDomain 選項值中使用連字號
* ID 移轉期間提出的要求會傳送至 demdex 端點，以便在未設定 demdex Cookie 時提升跨網域識別能力
* ID 移轉期間提出的要求一律會要求回應，以確保身分識別 Cookie 正確設定
* 執行無效命令時，控制台中會記錄有效命令名稱清單
* 已新增切換協力廠商 Cookie 支援的核取方塊至 Adobe Experience Platform Launch 擴充功能。這會停用對 demdex.net 的呼叫

## 2019 年 12 月 20 日

### Adobe Experience Platform Web SDK 0.0.5

#### 功能

* 新增活動追蹤器設定至 Platform Launch 擴充功能
* 在事件命令上公開 EventType 和 EventMergeId
* 新增 onBeforeEventSend 至 Platform Launch 擴充功能
* 新增 edgeBasePath 至 Platform Launch 擴充功能

#### 更新至 Alloy v. 0.0.10，其中包含下列變更：

* 實作客戶端儲存：狀態和 Cookie 邏輯已移至伺服器
* 在事件命令上公開 EventType 和 EventMergeId
* 使用 sendBeacon 追蹤退出連結以外的連結
* 回復 ID 同步功能 (除去檢查過期)
* setCustomerIds 命令並未對非 SSL (http) 頁面上的 ID 進行雜湊處理
* 將 APEX 網域傳遞至伺服器，以便在設定狀態/Cookie 時使用
* 使用新的控點類型，從回應中提取 ECID
* 移除「啟用與身分」設定的預設值
* 重新命名 + 將查詢選項移至中繼
* 舊版 ECID 移轉

#### 錯誤修正

* 在非預期的狀態代碼上，剖析錯誤訊息的回應本文並設定其格式
* 執行偵錯命令或使用 alloy_debug 由設定覆寫

## 2019 年 11 月 25 日

### Adobe Experience Platform Web SDK 0.0.3

#### 功能

* 「傳送事件」動作新增「合併 ID」和「類型」欄位。將「合併 ID」對應至 XDM 結構的 `xdm.eventMergeID`，並將「類型」對應到 XDM 結構的 `xdm.eventType`。
* 改善的錯誤處理和報告功能
* 現在，所有連結一律使用 `sendBeacon`

#### 錯誤修正

* 修正切換查詢字串參數或 `debug` 命令時，除錯作業不延續的問題。

## 2019 年 11 月 18 日

### Adobe Experience Platform Web SDK 0.0.2

#### 功能

* 擴充功能突然出現
* ECID 支援，不需額外程式庫或網路呼叫
* 選擇加入支援
* 支援將XDM傳送至平台
* 第一方網域支援
* 自動收集瀏覽器內容
* 完全開放原始碼 ([擴充功能](https://github.com/adobe/reactor-extension-alloy)、[SDK](https://github.com/adobe/reactor-extension-alloy))
* 詳細記錄
* 隱藏生產中錯誤的功能
