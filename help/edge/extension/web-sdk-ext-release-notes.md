---
title: Adobe Experience Platform Web SDK擴充功能發行說明
description: Adobe Experience Platform Web SDK標籤擴充功能
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: ccd02ea014d514b56a8e1bd540bb2c2c4bb2eb1b
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 38%

---


# Adobe Experience Platform Web SDK擴充功能發行說明

本檔案涵蓋Adobe Experience Platform Web SDK標籤擴充功能的發行說明。 如需SDK本身的最新發行說明，請參閱 [Platform Web SDK發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## 2.17.0版 — 2023年4月25日

**新功能**

* 新增對資料流設定覆寫的支援。
* 將淘汰通知新增至 `datasetId` 選項 `sendEvent` 命令。

**修正和改良**

* 修正在Safari中捲動會關閉資料流選取器的問題。

## 2.16.1版 — 2023年4月14日

* 修正XDM物件和變數資料元素無法從非預設沙箱選取結構的問題。

## 2.16.0版 — 2023年3月30日

**新功能**

* （測試版）新增 **[!UICONTROL 更新變數]** 行動與 **[!UICONTROL 變數]** 資料元素。
* 新增 [`onBeforeLinkClickSend`](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) 回呼函式。

**修正和改良**

* 修正當錨點標籤內的元素無法運作時， **[!UICONTROL 使用身分重新導向]** 已使用動作。
* 修正當只有一個架構時，XDM物件資料元素無法運作的問題。
* 包含2.15.0版的Adobe Experience Platform Web SDK。


## 2.15.1版 — 2023年1月26日

* 修正無法存取資料流的使用者無法編輯擴充功能設定的問題。
* 在 `sendEvent` 動作。

包含2.14.0版的Adobe Experience Platform Web SDK。


## 2.14.1版 — 2022年10月13日

* 修正Web SDK未遵守Experience CloudID服務之ID的問題。

包含Adobe Experience Platform Web SDK資料庫2.13.1版。

## 2.14.0版 — 2022年9月28日

* 新增 `targetMigrationEnabled` 啟用逐頁完整移轉的設定。
* 新增套用回應動作，以啟用混合式伺服器 — 用戶端實作。
* 添加了高熵用戶代理客戶端提示上下文選項。

包含Adobe Experience Platform Web SDK資料庫2.13.0版。

## 2.13.0版 — 2022年6月29日

* 修正了eVar等XDM物件資料元素中數值屬性的排序順序。

包含Adobe Experience Platform Web SDK資料庫2.12.0版。

## 2.12.0版 — 2022年6月13日

* 更新 `identityMap` 資料元素，以根據擴充功能設定所定義的沙箱填入命名空間選項。
* 新增 **[!UICONTROL 使用身分重新導向]** 允許跨網域身分共用的動作。
* 新增檔案連結至 `sendEvent` 動作。
* 升級React Spectrum UI程式庫。
* 增強多個使用者介面。

包含Adobe Experience Platform Web SDK資料庫2.11.0版。

## 2.11.2版 — 2022年5月3日

包含Adobe Experience Platform Web SDK資料庫2.10.1版。

## 2.11.1版 — 2022年4月22日

* 修正2.11.0版中的configure命令錯誤。

包含Adobe Experience Platform Web SDK資料庫2.10.0版。

## 2.11.0版 — 2022年4月22日

* 改善標籤UI效能。
* 新增沙箱選取器至資料流擴充功能設定。

包含Adobe Experience Platform Web SDK資料庫2.10.0版。

## 2.10.0版 — 2022年3月10日

* 更新可在設定頁面上複製的預先隱藏程式碼片段，以便與更新的Adobe Target VEC編輯器搭配使用。

包含 2.9.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.9.0 - 2022年1月19日

包含 2.8.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.8.0 - 2021年10月26日

包含 2.7.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 「傳送事件完成」事件中會提供來自Experience Edge的其他資訊，包括 `inferences` 和 `destinations`. 這些屬性的格式可能會有所變更，因為這些功能目前是測試版的一部分。 如需詳細資訊，請參閱 [追蹤事件。](../fundamentals/tracking-events.md)

## 版本2.7.3 - 2021年9月7日

包含 2.6.4 版的 Adobe Experience Platform Web SDK 程式庫。

* 不再提供 `container.buildInfo.environment.`

## 版本2.7.0 - 2021年8月16日

包含 2.6.3 版的 Adobe Experience Platform Web SDK 程式庫。

* 使用「身分對應」資料元素類型時，其ID會解析為未填入字串之值的識別碼，現在會自動從身分對應中移除。
* 修正嘗試使用XDM物件資料元素類型儲存資料元素時，未選取結構的錯誤。
* 改善使用者介面印刷樣式。

## 版本2.6.2 - 2021年8月4日

包含 2.6.2 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.6.1 - 2021年7月29日

包含 2.6.1 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.6.0 - 2021年7月27日

包含 2.6.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 使用「邊緣設定」一詞的標籤、說明和錯誤訊息已變更為使用「datastream」一詞，以符合最新的Adobe Experience Platform術語。
* 在擴充功能組態檢視中，已新增處理大量資料流和資料流環境的支援。
* 在XDM物件資料元素檢視中，已新增處理大量結構描述的支援。
* 已新增「傳送事件完成」事件類型，可用於在將事件傳送至伺服器並收到回應後執行規則。 即將推出更多檔案。
* 已棄用「收到的決定」事件類型。 請改用「傳送事件完成」事件類型。
* 使用者介面和錯誤處理已普遍改善。

## 版本2.5.0 - 2021年6月1日

包含 2.5.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 新增 `data` 欄位至「傳送事件」動作。 近期檔案將說明如何在特定情況下使用此功能。
* 在「XDM物件」資料元素檢視中，若使用者有Adobe Experience Platform沙箱的存取權，但未存取設定為組織預設的沙箱，則會擲回錯誤，此問題已獲修正。
* 在XDM物件資料元素檢視中，修正即使父物件不含任何值，必要架構欄位仍會視為無效的問題。

## 版本2.4.0 - 2021年3月9日

包含 2.4.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 新增 [&quot;檔案卸載&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 「傳送事件動作」UI的核取方塊。
* 新增對 `out` 選項 [配置預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) 會捨棄所有事件，直到收到同意為止(現有 `pending` 選項會讓事件排入佇列，並在收到同意後傳送它們)。
* 將工具提示新增至預設同意欄位。
* 新增 [Adobe的同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 如果使用者的存取權杖無效或布建不正確，XDM物件資料元素UI中現在會顯示更好的錯誤。
* 修正檢視XDM物件資料元素時，瀏覽器開發人員主控台上顯示的跨原始錯誤（不影響擴充功能的操作）。

## 版本2.3.0 - 2020年11月4日

包含 2.3.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增在設定預設同意時使用資料元素的支援。
* 已新增以 XDM 物件資料元素類型搜尋 XDM 結構描述的能力。
* 已新增在「傳送事件」動作類型中仿製 XDM 資料，以確保在要求中不會反映對 XDM 資料物件的後續變更。

## 版本2.2.0 - 2020年10月1日

* 客戶嘗試以沙盒結構描述建立 XDM 物件時，遇到驗證問題。呼叫Platform的API現在可感知環境，因此使用者只會看到他們有權編輯的結構描述。
* 使用 `identityMap` 資料元素，現在會在下拉式清單中預先填入命名空間，因此您不必手動填入。
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
* 使用啟用除錯 `_satellite` 現在會在Adobe Experience Platform Web SDK中啟用除錯。
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
* 新增切換協力廠商Cookie支援的核取方塊至標籤擴充功能。 這會停用對 demdex.net 的呼叫

## 0.0.5版 — 2019年12月20日

* 新增活動追蹤器設定至標籤擴充功能
* 在事件命令上公開 EventType 和 EventMergeId
* 新增onBeforeEventSend至標籤擴充功能的設定
* 將edgeBasePath配置添加到標籤擴展

## 0.0.3版 — 2019年11月25日

* 「傳送事件」動作新增「合併 ID」和「類型」欄位。將「合併 ID」對應至 XDM 結構的 `xdm.eventMergeID`，並將「類型」對應到 XDM 結構的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

* 首次發行
