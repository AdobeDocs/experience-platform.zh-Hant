---
title: Adobe Experience Platform Web SDK擴充功能發行說明
description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 擴充功能
seo-description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 擴充功能
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: dfcfdf90ae857e6a6ff0ddc7810cb6a6939c9758
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK擴充功能發行說明

本檔案涵蓋適用於Adobe Experience Platform Launch的Adobe Experience Platform Web SDK擴充功能發行說明。 如需SDK本身的最新發行說明，請參閱[平台Web SDK發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)。

## 版本2.6.0 - 2021年7月27日

* 使用「邊緣設定」一詞的標籤、說明和錯誤訊息已變更為使用「datastream」一詞，以符合最新的Adobe Experience Platform術語。
* 在擴充功能組態檢視中，已新增處理大量資料流和資料流環境的支援。
* 在XDM物件資料元素檢視中，已新增處理大量結構描述的支援。
* 已新增「傳送事件完成」事件類型，可用於在將事件傳送至伺服器並收到回應後執行規則。 即將推出更多檔案。
* 已棄用「收到的決定」事件類型。 請改用「傳送事件完成」事件類型。
* 使用者介面和錯誤處理已普遍改善。

## 版本2.5.0 - 2021年6月1日

包含 2.5.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 將`data`欄位新增至「傳送事件」動作。 近期檔案將說明如何在特定情況下使用此功能。
* 在「XDM物件」資料元素檢視中，若使用者有Adobe Experience Platform沙箱的存取權，但未存取設定為組織預設的沙箱，則會擲回錯誤，此問題已獲修正。
* 在XDM物件資料元素檢視中，修正即使父物件不含任何值，必要架構欄位仍會視為無效的問題。

## 版本2.4.0 - 2021年3月9日

包含 2.4.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增[&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)核取方塊至「傳送事件」動作UI。
* 新增[設定預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)時`out`選項的支援，該選項會在收到同意前捨棄所有事件（現有的`pending`選項會讓事件進入佇列，並在收到同意後傳送事件）。
* 將工具提示新增至預設同意欄位。
* 新增[Adobe同意2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支援。
* 如果使用者的存取權杖無效或布建不正確，XDM物件資料元素UI中現在會顯示更好的錯誤。
* 修正檢視XDM物件資料元素時，瀏覽器開發人員主控台上顯示的跨原始錯誤（不影響擴充功能的操作）。

## 版本2.3.0 - 2020年11月4日

包含 2.3.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增在設定預設同意時使用資料元素的支援。
* 已新增以 XDM 物件資料元素類型搜尋 XDM 結構描述的能力。
* 已新增在「傳送事件」動作類型中仿製 XDM 資料，以確保在要求中不會反映對 XDM 資料物件的後續變更。

## 版本2.2.0 - 2020年10月1日

* 客戶嘗試以沙盒結構描述建立 XDM 物件時，遇到驗證問題。呼叫Platform的API現在可感知環境，因此使用者只會看到他們有權編輯的結構描述。
* 使用 `identityMap` 資料元素時，下拉式清單現在會預先填入命名空間，因此您不必手動填寫。
* `xdmObject` 資料元素的 UI 已改版。在新的 UI 中，您可以看到哪些欄位已填入，不必在物件中輸入每個項目。

## 版本2.1.1 - 2020年8月26日

* 修正 XDM 物件檢視中，Adobe Experience Platform 沙盒無法正常顯示的問題。使用此版本的擴充功能時，如果清單未顯示預期的沙盒，使用者應向其 Adobe Experience Platform 管理員確認是否已正確設定存取權限。

## 版本2.1.0 - 2020年8月5日

* 重大變更：移除 `syncIdentity` 動作，並改為支援在 `sendEvent` 動作中傳遞這些 ID。升級擴充功能前，請使用此動作停用任何現有規則。
* 更新至 Alloy v. 2.1.0 ([發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* 在 `setConsent` 動作中支援 IAB 2.0 同意標準。
* 支援在 `sendEvent` 動作中覆寫資料集 ID。
* 新增全新的 `IdentityMap` 類型「資料元素」，可供在 XDM 物件資料元素 (現已啟用) 以及 `setConsent` 動作中填入 `identityMap` 項目。
* 支援在 `setConsent` 動作中傳遞身分對應。
* 支援在XDM物件資料元素中選擇平台沙箱。

## 1.0.0版 — 2020年5月26日

* 支援在「設定服務」選取環境。

## 版本0.1.2 - 2020年5月4日

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
* 使用`_satellite`啟用除錯功能後，現在會在Adobe Experience Platform Web SDK中啟用除錯功能。
* 新增在 XDM 物件中輸入值的相關支援：布林值、數字和小數。

## 0.0.10版 — 2020年3月16日

* 整合 `Consent` 底下的「選擇加入」和「選擇退出」概念，並新增 `setConsent` 命令。
* 新增可從 JavaScript/JSON 對應至 XDM 的新資料元素類型 `XDM Object`。

## 0.0.7版 — 2020年2月18日

* 移除 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 選項
* 支援在 edgeDomain 選項值中使用連字號
* ID 移轉期間提出的要求會傳送至 demdex 端點，以便在未設定 demdex Cookie 時提升跨網域識別能力
* ID 移轉期間提出的要求一律會要求回應，以確保身分識別 Cookie 正確設定
* 執行無效命令時，控制台中會記錄有效命令名稱清單
* 已新增切換協力廠商 Cookie 支援的核取方塊至 Adobe Experience Platform Launch 擴充功能。這會停用對 demdex.net 的呼叫

## 0.0.5版 — 2019年12月20日

* 新增活動追蹤器設定至 Platform Launch 擴充功能
* 在事件命令上公開 EventType 和 EventMergeId
* 新增 onBeforeEventSend 至 Platform Launch 擴充功能
* 新增 edgeBasePath 至 Platform Launch 擴充功能

## 0.0.3版 — 2019年11月25日

* 「傳送事件」動作新增「合併 ID」和「類型」欄位。將「合併 ID」對應至 XDM 結構的 `xdm.eventMergeID`，並將「類型」對應到 XDM 結構的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

* 首次發行
