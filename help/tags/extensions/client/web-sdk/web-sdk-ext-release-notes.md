---
title: Adobe Experience Platform Web SDK擴充功能發行說明
description: Adobe Experience Platform Web SDK標籤擴充功能
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 8cec606849489ef1e8845254117d184d5dc3c70a
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 36%

---


# Adobe Experience Platform Web SDK擴充功能發行說明

本文介紹Adobe Experience Platform Web SDK標籤擴充功能的發行說明。 如需SDK本身的最新發行說明，請參閱 [Platform Web SDK發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## 2.21.3版 — 2023年11月10日

包含2.19.1版的Adobe Experience Platform Web SDK。

**修正和改良**

* 修正中可用的主張陣列問題 `Send event complete` 事件一律為空白。

## 2.21.2版 — 2023年11月1日

**新功能**

* 已新增 `Request default personalization` 用於傳送事件動作的選項。
* 在「傳送事件」動作中新增頁面頂端和底部事件的支援。
* 已新增 `Apply propositions` 動作。
* 已新增 `Evaluate rulesets` 動作和 `Subscribe ruleset items` 應用程式內訊息的事件。
* 已新增 `Decision context` 以傳送事件動作。

**修正和改良**

* 包含2.19.0版的Adobe Experience Platform Web SDK。

## 2.20.3版 — 2023年8月8日

**修正和改良**

* 修正資料元素無法儲存在ID同步容器ID覆寫欄位中的問題。

## 2.20.1版 — 2023年8月3日

**修正和改良**

* 改善已儲存資料流覆寫設定的驗證。

## 2.20.0版 — 2023年7月31日

**新功能**

* 新增的支援 [每個命令會覆寫資料串流ID](../../../../datastreams/overrides.md).

**修正和改良**

* 已棄用 `edgeConfigId` 贊成 `datastreamId` 在SDK設定中。
* 資料流設定的多個使用者體驗增強功能會覆寫使用者介面。

## 2.19.0版 — 2023年6月21日

* 此 **[!UICONTROL 變數]** 資料元素和 **[!UICONTROL 更新變數]** 動作現已開放使用。

## 2.18.0版 — 2023年5月18日

* 包含2.17.0版的Adobe Experience Platform Web SDK。

## 2.17.0版 — 2023年4月25日

**新功能**

* 包含2.16.0版的Adobe Experience Platform Web SDK。
* 新增的支援 [資料流設定覆寫](../../../../datastreams/overrides.md).
* 將淘汰通知新增至 `datasetId` 上的選項 `sendEvent` 命令。


**修正和改良**

* 修正Safari中的捲動會關閉資料流選擇器的問題。

## 2.16.1版 — 2023年4月14日

* 修正XDM物件及變數資料元素無法從非預設沙箱選取結構描述的問題。

## 2.16.0版 — 2023年3月30日

**新功能**

* （測試版）已新增 **[!UICONTROL 更新變數]** 動作和 **[!UICONTROL 變數]** 資料元素。
* 已新增以下專案的設定： [`onBeforeLinkClickSend`](../../../../edge/fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) 回呼函式。

**修正和改良**

* 修正在錨點標籤內按一下元素時無法運作的問題。 **[!UICONTROL 使用身分重新導向]** 已使用動作。
* 修正只有一個結構描述時，XDM物件資料元素無法運作的問題。
* 包含2.15.0版的Adobe Experience Platform Web SDK。


## 2.15.1版 — 2023年1月26日

* 修正無權存取資料串流的使用者無法編輯擴充功能設定的問題。
* 新增對中的曲面的支援 `sendEvent` 動作。

包含2.14.0版的Adobe Experience Platform Web SDK。


## 2.14.1版 — 2022年10月13日

* 修正Web SDK未接受來自Experience CloudID服務的ID的問題。

包含2.13.1版的Adobe Experience Platform Web SDK程式庫。

## 2.14.0版 — 2022年9月28日

* 已新增 `targetMigrationEnabled` 可啟用逐頁完整移轉的設定。
* 新增套用回應動作，以啟用混合式伺服器 — 使用者端實作。
* 新增高平均資訊量使用者代理程式使用者端提示內容選項。

包含2.13.0版的Adobe Experience Platform Web SDK程式庫。

## 2.13.0版 — 2022年6月29日

* 修正XDM物件資料元素（例如eVar）中數值屬性的排序順序。

包含2.12.0版的Adobe Experience Platform Web SDK程式庫。

## 2.12.0版 — 2022年6月13日

* 已更新 `identityMap` 資料元素，以根據擴充功能設定所定義的沙箱填入名稱空間選項。
* 已新增 **[!UICONTROL 使用身分重新導向]** 允許跨網域身分共用的動作。
* 新增檔案連結至 `sendEvent` 動作。
* 升級React Spectrum UI程式庫。
* 多項使用者介面增強功能。

包含2.11.0版的Adobe Experience Platform Web SDK程式庫。

## 2.11.2版 — 2022年5月3日

包含2.10.1版的Adobe Experience Platform Web SDK程式庫。

## 2.11.1版 — 2022年4月22日

* 已修正2.11.0版的設定命令錯誤。

包含2.10.0版的Adobe Experience Platform Web SDK程式庫。

## 2.11.0版 — 2022年4月22日

* 已改善標籤UI效能。
* 將沙箱選擇器新增到資料串流擴充功能設定。

包含2.10.0版的Adobe Experience Platform Web SDK程式庫。

## 2.10.0版 — 2022年3月10日

* 更新可在設定頁面上複製的預先隱藏程式碼片段，以與更新的Adobe Target VEC編輯器搭配使用。

包含 2.9.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.9.0版 — 2022年1月19日

包含 2.8.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.8.0版 — 2021年10月26日

包含 2.7.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 在「傳送事件完成」事件中可取得來自Edge Network的其他資訊，包括 `inferences` 和 `destinations`. 這些屬性的格式可能會隨著這些功能目前在Beta版中推出而改變。 如需詳細資訊，請參閱 [追蹤事件。](../../../../edge/fundamentals/tracking-events.md)

## 2.7.3版 — 2021年9月7日

包含 2.6.4 版的 Adobe Experience Platform Web SDK 程式庫。

* 「 」不再有「淘汰」警告 `container.buildInfo.environment.`

## 2.7.0版 — 2021年8月16日

包含 2.6.3 版的 Adobe Experience Platform Web SDK 程式庫。

* 使用「身分對應」資料元素型別時，其ID解析為未填入字串之值的識別碼現在會自動從身分對應中移除。
* 修正嘗試使用XDM物件資料元素型別儲存資料元素時，在未選取任何結構描述時發生的錯誤。
* 改善使用者介面印刷樣式。

## 2.6.2版 — 2021年8月4日

包含 2.6.2 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.6.1版 — 2021年7月29日

包含 2.6.1 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.6.0版 — 2021年7月27日

包含 2.6.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 使用術語「邊緣組態」的標籤、說明和錯誤訊息已變更為使用術語「資料流」，以符合最新的Adobe Experience Platform術語。
* 在擴充功能組態檢視中，新增了處理大量資料串流和資料串流環境的支援。
* 在XDM物件資料元素檢視中，已新增處理大量結構描述的支援。
* 已新增「傳送事件完成」事件型別，可用於在事件已傳送至伺服器並收到回應後執行規則。 即將提供更多檔案。
* 已棄用「收到的決定」事件型別。 請改用傳送事件完成事件型別。
* 使用者介面和錯誤處理已普遍改善。

## 2.5.0版 — 2021年6月1日

包含 2.5.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增 `data` 「傳送事件」動作的欄位。 即將推出的檔案將說明如何在特定情況下使用此功能。
* 在XDM物件資料元素檢視上，已修正如果使用者有權存取Adobe Experience Platform沙箱，但沒有存取設定為組織預設的沙箱，則會擲回錯誤的問題。
* 在XDM物件資料元素檢視上，即使父物件不包含任何值，必要結構描述欄位仍會被視為無效的問題，已獲得修正。

## 2.4.0版 — 2021年3月9日

包含 2.4.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增 [&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html#using-the-sendbeacon-api) 核取方塊以傳送事件動作UI。
* 新增對的支援 `out` 選項條件 [設定預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) 會在收到同意前捨棄所有事件(現有 `pending` 選項會將事件排入佇列，並在收到同意後傳送事件)。
* 新增工具提示至預設同意欄位。
* 新增的支援 [Adobe同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 如果使用者的存取權杖無效或布建不正確，XDM物件資料元素UI中現在會顯示更好的錯誤。
* 修正檢視XDM物件資料元素時，瀏覽器開發人員主控台顯示的跨來源錯誤（不會影響擴充功能的作業）。

## 2.3.0版 — 2020年11月4日

包含 2.3.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增在設定預設同意時使用資料元素的支援。
* 已新增以 XDM 物件資料元素類型搜尋 XDM 結構描述的能力。
* 已新增在「傳送事件」動作類型中仿製 XDM 資料，以確保在要求中不會反映對 XDM 資料物件的後續變更。

## 2.2.0版 — 2020年10月1日

* 客戶嘗試以沙盒結構描述建立 XDM 物件時，遇到驗證問題。呼叫Platform的API現在可感知環境，因此使用者只會看到他們有權編輯的結構描述。
* 使用時 `identityMap` 資料元素中，下拉式清單現在會預先填入名稱空間，因此您不必手動填寫。
* `xdmObject` 資料元素的 UI 已改版。在新的 UI 中，您可以看到哪些欄位已填入，不必在物件中輸入每個項目。

## 2.1.1版 — 2020年8月26日

* 修正 XDM 物件檢視中，Adobe Experience Platform 沙盒無法正常顯示的問題。使用此版本的擴充功能時，如果清單未顯示預期的沙盒，使用者應向其 Adobe Experience Platform 管理員確認是否已正確設定存取權限。

## 2.1.0版 — 2020年8月5日

* 重大變更：移除 `syncIdentity` 動作，並改為支援在 `sendEvent` 動作中傳遞這些 ID。升級擴充功能前，請使用此動作停用任何現有規則。
* 更新至 Alloy v. 2.1.0 ([發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* 在 `setConsent` 動作中支援 IAB 2.0 同意標準。
* 支援在 `sendEvent` 動作中覆寫資料集 ID。
* 新增全新的 `IdentityMap` 類型「資料元素」，可供在 XDM 物件資料元素 (現已啟用) 以及 `setConsent` 動作中填入 `identityMap` 項目。
* 支援在 `setConsent` 動作中傳遞身分對應。
* 支援在XDM物件資料元素中選擇Platform沙箱。

## 1.0.0版 — 2020年5月26日

* 支援在「設定服務」選取環境。

## 0.1.2版 — 2020年5月4日

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
* 使用啟用偵錯 `_satellite` 現在會在Adobe Experience Platform Web SDK中啟用除錯功能。
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
* 新增核取方塊，可將第三方Cookie支援切換至標籤擴充功能。 這會停用對 demdex.net 的呼叫

## 0.0.5版 — 2019年12月20日

* 將活動追蹤器設定新增至標籤擴充功能
* 在事件命令上公開 EventType 和 EventMergeId
* 將onBeforeEventSend設定新增至標籤擴充功能
* 將edgeBasePath設定新增至標籤延伸模組

## 0.0.3版 — 2019年11月25日

* 「傳送事件」動作新增「合併 ID」和「類型」欄位。將「合併 ID」對應至 XDM 結構的 `xdm.eventMergeID`，並將「類型」對應到 XDM 結構的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

* 首次發行
