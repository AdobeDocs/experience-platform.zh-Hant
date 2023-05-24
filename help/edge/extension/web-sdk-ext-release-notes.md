---
title: Adobe Experience PlatformWeb SDK擴展發行說明
description: Adobe Experience PlatformWeb SDK標籤擴展
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: edd1745467a95804681b5d6c6d33458329641c39
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 38%

---


# Adobe Experience PlatformWeb SDK擴展發行說明

本文檔介紹Adobe Experience PlatformWeb SDK標籤擴展的發行說明。 有關SDK本身的最新發行說明，請參見 [平台Web SDK發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)。

## 版本2.17.0 - 2023年4月25日

**新功能**

* 包含Adobe Experience PlatformWeb SDK的2.16.0版。
* 為 [資料流配置覆蓋](../datastreams/overrides.md)。
* 將棄用通知添加到 `datasetId` 的上界 `sendEvent` 的子菜單。


**修正和改良**

* 修復了在Safari中滾動將關閉資料流選擇器的問題。

## 版本2.16.1 - 2023年4月14日

* 修復了XDM對象和變數資料元素的問題，在這些資料元素中，您無法從非預設沙箱中選擇方案。

## 版本2.16.0 - 2023年3月30日

**新功能**

* (Beta)已添加 **[!UICONTROL 更新變數]** 行動和 **[!UICONTROL 變數]** 資料元素。
* 已添加的配置 [`onBeforeLinkClickSend`](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) 回調函式。

**修正和改良**

* 修復了導致在錨點標籤中按一下元素時無法工作的問題 **[!UICONTROL 使用標識重定向]** 已使用操作。
* 修復了XDM對象資料元素在僅存在一個架構時無法正常工作的問題。
* 包含2.15.0版的Adobe Experience PlatformWeb SDK。


## 版本2.15.1 - 2023年1月26日

* 修復了無法訪問資料流的用戶無法編輯擴展配置的問題。
* 為中的曲面添加了支援 `sendEvent` 操作。

包含2.14.0版的Adobe Experience PlatformWeb SDK。


## 版本2.14.1 - 2022年10月13日

* 已修復Web SDK不遵守Experience CloudID服務中的ID的問題。

包含Adobe Experience PlatformWeb SDK庫的2.13.1版。

## 版本2.14.0 - 2022年9月28日

* 添加新 `targetMigrationEnabled` 啟用逐頁完全遷移的配置。
* 已添加應用響應操作以啟用混合伺服器 — 客戶端實現。
* 已添加高熵用戶代理客戶端提示上下文選項。

包含Adobe Experience PlatformWeb SDK庫的2.13.0版。

## 版本2.13.0 - 2022年6月29日

* 已在XDM對象資料元素（如eVars）中固定數值屬性的排序順序。

包含Adobe Experience PlatformWeb SDK庫的2.12.0版。

## 版本2.12.0 - 2022年6月13日

* 已更新 `identityMap` 資料元素，用於根據擴展設定定義的沙框填充命名空間選項。
* 已添加 **[!UICONTROL 使用標識重定向]** 允許跨域標識共用的操作。
* 添加到 `sendEvent` 操作。
* 已升級React Spectrum UI庫。
* 多個用戶介面增強。

包含Adobe Experience PlatformWeb SDK庫的2.11.0版。

## 版本2.11.2 - 2022年5月3日

包含Adobe Experience PlatformWeb SDK庫的2.10.1版。

## 版本2.11.1 - 2022年4月22日

* 已修復2.11.0版中的configure命令錯誤。

包含Adobe Experience PlatformWeb SDK庫的2.10.0版。

## 版本2.11.0 - 2022年4月22日

* 改進的標籤UI效能。
* 將沙盒選擇器添加到資料流擴展配置。

包含Adobe Experience PlatformWeb SDK庫的2.10.0版。

## 版本2.10.0 - 2022年3月10日

* 更新可在配置頁上複製的預隱藏代碼段，以便與更新的Adobe TargetVEC編輯器一起使用。

包含 2.9.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.9.0 - 2022年1月19日

包含 2.8.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.8.0 - 2021年10月26日

包含 2.7.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 「發送事件完成」事件中提供了「體驗邊緣」的其他資訊，包括 `inferences` 和 `destinations`。 這些屬性的格式可能會更改，因為這些功能當前正在作為Beta的一部分推出。 有關詳細資訊，請參見 [跟蹤事件。](../fundamentals/tracking-events.md)

## 版本2.7.3 - 2021年9月7日

包含 2.6.4 版的 Adobe Experience Platform Web SDK 程式庫。

* 不再有對的棄用警告 `container.buildInfo.environment.`

## 版本2.7.0 - 2021年8月16日

包含 2.6.3 版的 Adobe Experience Platform Web SDK 程式庫。

* 使用身份映射資料元素類型時，其ID解析為未填充字串的值的標識符現在將自動從身份映射中刪除。
* 修復了嘗試使用XDM對象資料元素類型保存資料元素時發生的錯誤，但未選擇任何架構。
* 改進的用戶介面排版。

## 版本2.6.2 - 2021年8月4日

包含 2.6.2 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.6.1 - 2021年7月29日

包含 2.6.1 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本2.6.0 - 2021年7月27日

包含 2.6.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 使用術語「邊緣配置」的標籤、說明和錯誤消息已更改為使用術語「datastream」與最新的Adobe Experience Platform術語對齊。
* 在擴展配置視圖中，為處理大量資料流和資料流環境添加了支援。
* 在XDM對象資料元素視圖中，添加了對處理大量架構的支援。
* 已添加「發送事件完成」事件類型，該類型可用於在將事件發送到伺服器並收到響應後運行規則。 將很快提供更多文檔。
* 已棄用「收到的決定」事件類型。 請改用「發送事件完成」事件類型。
* 用戶介面和錯誤處理得到了普遍改進。

## 版本2.5.0 - 2021年6月1日

包含 2.5.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已添加 `data` 欄位。 即將發佈的文檔將介紹在某些情形中如何使用此功能。
* 在XDM對象資料元素視圖上，如果用戶有權訪問Adobe Experience Platform沙箱，但沒有訪問配置為組織預設設定的沙箱，則問題已得到解決。
* 在XDM對象資料元素視圖上，即使父對象不包含任何值，也會將必需的架構欄位視為無效的問題得到解決。

## 版本2.4.0 - 2021年3月9日

包含 2.4.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已添加 [&quot;文檔卸載&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 複選框以發送事件操作UI。
* 為 `out` 選項 [配置預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) 刪除所有事件直到收到同意(現有 `pending` 選項將事件排隊，並在收到同意後發送它們)。
* 已將工具提示添加到預設同意欄位。
* 為 [Adobe同意2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)。
* 如果用戶的訪問令牌無效或設定不正確，則XDM對象資料元素UI中現在會顯示一個更好的錯誤。
* 已修復在瀏覽器開發人員控制台上查看XDM對象資料元素時顯示的交叉原點錯誤（這不會影響擴展的操作）。

## 版本2.3.0 - 2020年11月4日

包含 2.3.0 版的 Adobe Experience Platform Web SDK 程式庫。

* 已新增在設定預設同意時使用資料元素的支援。
* 已新增以 XDM 物件資料元素類型搜尋 XDM 結構描述的能力。
* 已新增在「傳送事件」動作類型中仿製 XDM 資料，以確保在要求中不會反映對 XDM 資料物件的後續變更。

## 版本2.2.0 - 2020年10月1日

* 客戶嘗試以沙盒結構描述建立 XDM 物件時，遇到驗證問題。調用平台的API現在知道環境，因此用戶只會顯示他們有權編輯的那些架構。
* 使用 `identityMap` 資料元素，命名空間現在已預填充到下拉清單中，因此您不必手動填充。
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
* 支援在XDM對象資料元素中選擇平台沙箱。

## 版本1.0.0 - 2020年5月26日

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
* 啟用調試使用 `_satellite` 現在啟用Adobe Experience PlatformWeb SDK中的調試。
* 新增在 XDM 物件中輸入值的相關支援：布林值、數字和小數。

## 版本0.0.10 - 2020年3月16日

* 整合 `Consent` 底下的「選擇加入」和「選擇退出」概念，並新增 `setConsent` 命令。
* 新增可從 JavaScript/JSON 對應至 XDM 的新資料元素類型 `XDM Object`。

## 版本0.0.7 - 2020年2月18日

* 移除 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 選項
* 支援在 edgeDomain 選項值中使用連字號
* ID 移轉期間提出的要求會傳送至 demdex 端點，以便在未設定 demdex Cookie 時提升跨網域識別能力
* ID 移轉期間提出的要求一律會要求回應，以確保身分識別 Cookie 正確設定
* 執行無效命令時，控制台中會記錄有效命令名稱清單
* 已添加用於將第三方cookie支援切換到標籤擴展的複選框。 這會停用對 demdex.net 的呼叫

## 版本0.0.5 - 2019年12月20日

* 將活動跟蹤器配置添加到標籤擴展
* 在事件命令上公開 EventType 和 EventMergeId
* 將onBeforeEventSend配置添加到標籤擴展
* 將edgeBasePath配置添加到標籤擴展

## 版本0.0.3 - 2019年11月25日

* 「傳送事件」動作新增「合併 ID」和「類型」欄位。將「合併 ID」對應至 XDM 結構的 `xdm.eventMergeID`，並將「類型」對應到 XDM 結構的 `xdm.eventType`。

## 版本0.0.2 - 2019年11月18日

* 首次發行
