---
title: Adobe Experience Platform Web SDK擴充功能發行說明
description: Adobe Experience Platform Web SDK標籤擴充功能
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: cf8912aea5c46b3414486f638b92eebf556528a9
workflow-type: tm+mt
source-wordcount: '2733'
ht-degree: 24%

---


# Web SDK擴充功能發行說明

本文介紹Adobe Experience Platform Web SDK標籤擴充功能的發行說明。 如需SDK本身的最新發行說明，請參閱[Experience Platform Web SDK發行說明](/help/web-sdk/release-notes.md)。

## 2.31.0版 — 2025年7月24日

**新功能**

- 包含[2.28.0](../../../../web-sdk/release-notes.md#2-28-0)版的Adobe Experience Platform Web SDK。

**修正和改良**

- 修正透過資料元素啟用資料流覆寫時擲回錯誤的問題。
- 修正空白`idSyncContainerId`覆寫會造成錯誤的問題。
- 解析媒體資料元素時，現在包含事件物件。

## 2.30.1版 — 2025年5月27日

**修正和改良**

- 修正組織未設定預設沙箱時，更新變數檢視當機的問題。

## 2.30.0版 — 2025年5月21日

**新功能**

- 您現在可以在啟用第三方Cookie時指定資料元素。
- 在程式碼欄位中新增清除按鈕。
- 包含[2.27.0](../../../../web-sdk/release-notes.md#2-27-0)版的Adobe Experience Platform Web SDK。

**修正和改良**

- 已新增驗證，以防止在啟用事件分組時設定`onBeforeLinkClickSend`。

## 2.29.1版 — 2025年5月8日

**修正和改良**

- 修正編輯後立即按一下「儲存」時，設定未儲存的問題。

## 2.29.0版 — 2025年3月5日

**新功能**

- 您現在可以建立自訂Web SDK組建，並從標籤擴充功能使用者介面選擇所需的元件。 透過排除未使用的元件，這可能會導致較小的組建。 請參閱有關[建立自訂Web SDK組建](web-sdk-extension-configuration.md#custom-build)的檔案。
- 包含[2.26.0](../../../../web-sdk/release-notes.md#2-26-0)版的Adobe Experience Platform Web SDK。

**修正和改良**

- 已在[更新變數](action-types.md#update-variable)動作中新增順利處理遺失的資料元素。 以往，在編輯缺少資料元素的更新變數動作時會顯示錯誤訊息。 現在，您可以選擇不同的資料元素，並且更新變數動作的所有設定仍會套用。 如果刪除資料元素或複製Tags屬性，資料元素可能會遺失。
- 新增支援以[識別重新導向](action-types.md#redirect-with-identity)動作開啟新標籤。 現在，使用動作時，在重新導向瀏覽器時會使用錨點標籤的`target`屬性。
- 修正無法在設定覆寫中停用Adobe Audience Manager的問題。

## 2.28.0版 — 2025年1月23日

**修正和改良**

- 修正在未啟用Audience Manager的情況下無法設定ID同步容器覆寫的問題。
- 修正升級到最新版本時，資料流設定覆寫為停用的問題。
- 修正使用者無法儲存Target自動點選集合設定的問題。

**新功能**

- 新增一項功能，可在XDM物件中的技術名稱和顯示名稱之間切換。
- 包含[2.25.0](../../../../web-sdk/release-notes.md#2-25-0)版的Adobe Experience Platform Web SDK。

## 2.27.0版 — 2024年10月31日

**新功能**

- [資料流覆寫](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides)現在包含停用Experience Cloud解決方案和Adobe Experience Platform服務的設定。
- 您現在可以為媒體工作階段建立[資料流覆寫](../web-sdk/web-sdk-extension-configuration.md)。

包含2.24.0版的Adobe Experience Platform Web SDK。

## 2.26.1版 — 2024年9月19日

**修正和改良**

- 修正在本機執行Web SDK時，Cookie未正確寫入的問題。

包含2.23.0版的Adobe Experience Platform Web SDK。

## 2.26.0版 — 2024年8月22日

**新功能**

- 已新增監視連結`triggered`事件。
- [引導式事件](action-types.md#instance)、[要求預設個人化](action-types.md#personalization)、[訂閱規則集專案](event-types.md#subscribe-ruleset-items)和[評估規則集](action-types.md#evaluate-rulesets)現已普遍可用。

**修正和改良**

- 修正重複的變數資料元素可能互相覆寫的問題。
- 使用[要求預設個人化](action-types.md#personalization)引導式事件時，現在會自動啟用視覺個人化決定。

包含2.22.0版的Adobe Experience Platform Web SDK。

## 2.25.0版 — 2024年7月18日

**新功能**

- 新增對Adobe Journey Optimizer中自動追蹤個人化的支援。
- 推出新設定，管理改善的點選集合。

包含2.21.1版的Adobe Experience Platform Web SDK。

## 2.24.0版 — 2024年6月5日

**修正和改良**

- 修正定義設定覆寫時，修改擴充功能設定時發生的錯誤。
- 允許設定媒體收集Ping間隔的空白值。
- 修正修改更新變數動作時發生的錯誤。
- 允許重設設定覆寫中的ID同步容器。

包含2.20.0版的Adobe Experience Platform Web SDK。

## 2.23.1版 — 2024年5月28日

**新功能**

- 新增擴充功能組態中[`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media)元件的支援。
- 已新增[`Send Media Event`](action-types.md#send-media-event)功能的[!DNL Streaming Media Collection]動作。
- 已新增[`Media: Quality of Experience`](data-element-types.md#quality-experience)功能的[!DNL Streaming Media Collection]資料元素。

包含2.20.0版的Adobe Experience Platform Web SDK。

**修正和改良**

- 修正搜尋[更新變數](action-types.md#update-variable)動作中的資料元素時發生的錯誤。
- 已從建議用於[!UICONTROL 動作的事件型別中移除]媒體`sendEvent`事件型別。

## 2.22.0版 — 2024年5月3日

**新功能**

- 擴充變數資料元素以支援資料物件。
- 「更新變數」動作現在支援修改傳遞Adobe Analytics、Adobe Audience Manager和Adobe Target資料。

包含2.19.2版的Adobe Experience Platform Web SDK。

## 2.21.4版 — 2024年1月10日

**修正和改良**

- 修正儲存設定覆寫但未設定所有3個環境時，擴充功能UI會當機的問題。
- 修正編輯更新變數動作時，根清除現有值核取方塊未填入的問題。

包含2.19.2版的Adobe Experience Platform Web SDK。

## 版本 2.21.3 - 2023 年 11 月 10 日

包含2.19.1版的Adobe Experience Platform Web SDK。

**修正和改良**

- 修正`Send event complete`事件中可用的主張陣列一律為空白的問題。

## 2.21.2版 — 2023年11月1日

**新功能**

- 已新增傳送事件動作的`Request default personalization`選項。
- 在「傳送事件」動作中新增頁面頂端和底部事件的支援。
- 已新增`Apply propositions`動作。
- 已新增應用程式內訊息的`Evaluate rulesets`動作和`Subscribe ruleset items`事件。
- 已新增`Decision context`以傳送事件動作。

**修正和改良**

- 包含2.19.0版的Adobe Experience Platform Web SDK。

## 2.20.3版 — 2023年8月8日

**修正和改良**

- 修正資料元素無法儲存在ID同步容器ID覆寫欄位中的問題。

## 2.20.1版 — 2023年8月3日

**修正和改良**

- 改善已儲存資料流覆寫設定的驗證。

## 2.20.0版 — 2023年7月31日

**新功能**

- 新增支援[每個命令覆寫資料串流ID](../../../../datastreams/overrides.md)。

**修正和改良**

- 已在SDK設定中棄用`edgeConfigId`而支援`datastreamId`。
- 資料流設定的多個使用者體驗增強功能會覆寫使用者介面。

## 2.19.0版 — 2023年6月21日

- **[!UICONTROL 變數]**&#x200B;資料元素和&#x200B;**[!UICONTROL 更新變數]**&#x200B;動作現在已可供一般使用。

## 2.18.0版 — 2023年5月18日

- 包含2.17.0版的Adobe Experience Platform Web SDK。

## 2.17.0版 — 2023年4月25日

**新功能**

- 包含2.16.0版的Adobe Experience Platform Web SDK。
- 已新增對[資料流組態覆寫](/help/datastreams/overrides.md)的支援。
- 在`datasetId`命令的`sendEvent`選項中新增淘汰通知。

**修正和改良**

- 修正Safari中的捲動會關閉資料流選擇器的問題。

## 2.16.1版 — 2023年4月14日

- 修正XDM物件及變數資料元素無法從非預設沙箱選取結構描述的問題。

## 2.16.0版 — 2023年3月30日

**新功能**

- (Beta)已新增&#x200B;**[!UICONTROL 更新變數]**&#x200B;動作和&#x200B;**[!UICONTROL 變數]**&#x200B;資料元素。
- 已新增[`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md)回呼函式的設定。

**修正和改良**

- 修正使用&#x200B;**[!UICONTROL 具有身分的重新導向]**&#x200B;動作時，點選錨點標籤內元素無法運作的問題。
- 修正只有一個結構描述時，XDM物件資料元素無法運作的問題。
- 包含2.15.0版的Adobe Experience Platform Web SDK。

## 2.15.1版 — 2023年1月26日

- 修正無權存取資料串流的使用者無法編輯擴充功能設定的問題。
- 在`sendEvent`動作中新增對表面的支援。

包含2.14.0版的Adobe Experience Platform Web SDK。

## 2.14.1版 — 2022年10月13日

- 修正Web SDK未遵守來自Experience Cloud ID服務的ID的問題。

包含2.13.1版的Adobe Experience Platform Web SDK資料庫。

## 2.14.0版 — 2022年9月28日

- 新增可啟用逐頁完整移轉的新`targetMigrationEnabled`設定。
- 新增套用回應動作，以啟用混合式伺服器 — 使用者端實作。
- 新增高平均資訊量使用者代理程式使用者端提示內容選項。

包含2.13.0版的Adobe Experience Platform Web SDK資料庫。

## 2.13.0版 — 2022年6月29日

- 修正XDM物件資料元素（例如eVar）中數值屬性的排序順序。

包含2.12.0版的Adobe Experience Platform Web SDK資料庫。

## 2.12.0版 — 2022年6月13日

- 更新`identityMap`資料元素，以根據擴充功能設定所定義的沙箱填入名稱空間選項。
- 已新增含身分的&#x200B;**[!UICONTROL 重新導向]**&#x200B;動作，以允許跨網域身分共用。
- 已新增檔案連結至`sendEvent`動作。
- 升級React Spectrum UI程式庫。
- 多項使用者介面增強功能。

包含2.11.0版的Adobe Experience Platform Web SDK資料庫。

## 2.11.2版 — 2022年5月3日

包含2.10.1版的Adobe Experience Platform Web SDK資料庫。

## 2.11.1版 — 2022年4月22日

- 已修正2.11.0版的設定命令錯誤。

包含2.10.0版的Adobe Experience Platform Web SDK資料庫。

## 2.11.0版 — 2022年4月22日

- 已改善標籤UI效能。
- 將沙箱選擇器新增到資料串流擴充功能設定。

包含2.10.0版的Adobe Experience Platform Web SDK資料庫。

## 2.10.0版 — 2022年3月10日

- 更新可在設定頁面上複製的預先隱藏程式碼片段，以與更新的Adobe Target VEC編輯器搭配使用。

包含 2.9.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.9.0版 — 2022年1月19日

包含 2.8.0 版的 Adobe Experience Platform Web SDK 程式庫。

## 版本 2.8.0 - 2021 年 10 月 26 日

包含 2.7.0 版的 Adobe Experience Platform Web SDK 程式庫。

- 來自Edge Network的其他資訊可在「傳送事件完成」事件中使用，包括`inferences`和`destinations`。 這些屬性的格式可能會隨著這些功能目前在Beta中推出而改變。

## 2.7.3版 — 2021年9月7日

包含 2.6.4 版的 Adobe Experience Platform Web SDK 程式庫。

- `container.buildInfo.environment.`不再有取代警告

## 2.7.0版 — 2021年8月16日

包含 2.6.3 版的 Adobe Experience Platform Web SDK 程式庫。

- 使用「身分對應」資料元素型別時，其ID解析為未填入字串之值的識別碼現在會自動從身分對應中移除。
- 修正嘗試使用XDM物件資料元素型別儲存資料元素時，在未選取任何結構描述時發生的錯誤。
- 改善使用者介面印刷樣式。

## 2.6.2版 — 2021年8月4日

包含 2.6.2 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.6.1版 — 2021年7月29日

包含 2.6.1 版的 Adobe Experience Platform Web SDK 程式庫。

## 2.6.0版 — 2021年7月27日

包含 2.6.0 版的 Adobe Experience Platform Web SDK 程式庫。

- 使用術語「邊緣組態」的標籤、說明和錯誤訊息已變更為使用術語「資料流」，以符合最新的Adobe Experience Platform術語。
- 在擴充功能組態檢視中，新增了處理大量資料串流和資料串流環境的支援。
- 在XDM物件資料元素檢視中，已新增處理大量結構描述的支援。
- 已新增「傳送事件完成」事件型別，可用於在事件已傳送至伺服器並收到回應後執行規則。 即將提供更多檔案。
- 已棄用「收到的決定」事件型別。 請改用傳送事件完成事件型別。
- 使用者介面和錯誤處理已普遍改善。

## 2.5.0版 — 2021年6月1日

包含 2.5.0 版的 Adobe Experience Platform Web SDK 程式庫。

- 已新增`data`欄位至「傳送事件」動作。 即將推出的檔案將說明如何在特定情況下使用此功能。
- 在XDM物件資料元素檢視上，已修正如果使用者有權存取Adobe Experience Platform沙箱，但沒有存取設定為組織預設的沙箱，則會擲回錯誤的問題。
- 在XDM物件資料元素檢視上，即使父物件不包含任何值，必要結構描述欄位仍會被視為無效的問題，已獲得修正。

## 2.4.0版 — 2021年3月9日

包含 2.4.0 版的 Adobe Experience Platform Web SDK 程式庫。

- 已新增[「檔案正在解除安裝」](/help/web-sdk/commands/sendevent/documentunloading.md)核取方塊以傳送事件動作UI。
- 新增對`out`選項的支援，當[設定預設同意](/help/web-sdk/commands/configure/defaultconsent.md)時，會捨棄所有事件直到收到同意為止（現有的`pending`選項會佇列事件，並在收到同意後傳送它們）。
- 新增工具提示至預設同意欄位。
- 新增使用[`setConsent`](/help/web-sdk/commands/setconsent.md)命令時對Adobe的Consent 2.0標準的支援。
- 如果使用者的存取權杖無效或布建不正確，XDM物件資料元素UI中現在會顯示更好的錯誤。
- 修正檢視XDM物件資料元素時，瀏覽器開發人員主控台顯示的跨來源錯誤（不會影響擴充功能的作業）。

## 2.3.0版 — 2020年11月4日

包含 2.3.0 版的 Adobe Experience Platform Web SDK 程式庫。

- 已新增在設定預設同意時使用資料元素的支援。
- 已新增以 XDM 物件資料元素類型搜尋 XDM 結構描述的能力。
- 已新增在「傳送事件」動作類型中仿製 XDM 資料，以確保在要求中不會反映對 XDM 資料物件的後續變更。

## 2.2.0版 — 2020年10月1日

- 客戶嘗試以沙箱結構描述建立 XDM 物件時，遇到驗證問題。呼叫Experience Platform的API現在可感知環境，因此使用者只會看到他們有權編輯的結構描述。
- 使用`identityMap`資料元素時，下拉式清單現在會預先填入名稱空間，因此您不必手動填寫。
- `xdmObject` 資料元素的 UI 已改版。在新的 UI 中，您可以看到哪些欄位已填入，不必在物件中輸入每個項目。

## 2.1.1版 — 2020年8月26日

- 修正 XDM 物件檢視中，Adobe Experience Platform 沙箱無法正常顯示的問題。使用此版本的擴充功能時，如果清單未顯示預期的沙箱，使用者應向其 Adobe Experience Platform 管理員確認是否已正確設定存取權限。

## 2.1.0版 — 2020年8月5日

- 重大變更：移除 `syncIdentity` 動作，並改為支援在 `sendEvent` 動作中傳遞這些 ID。升級擴充功能前，請使用此動作停用任何現有規則。
- 更新至 Alloy v. 2.1.0 ([發行說明](/help/web-sdk/release-notes.md))
- 在 `setConsent` 動作中支援 IAB 2.0 同意標準。
- 支援在 `sendEvent` 動作中覆寫資料集 ID。
- 新增全新的 `IdentityMap` 類型「資料元素」，可供在 XDM 物件資料元素 (現已啟用) 以及 `setConsent` 動作中填入 `identityMap` 項目。
- 支援在 `setConsent` 動作中傳遞身分識別對應。
- 支援在XDM物件資料元素中選擇Experience Platform沙箱。

## 1.0.0版 — 2020年5月26日

- 支援在「設定服務」選取環境。

## 0.1.2版 — 2020年5月4日

- 將 `configId` 重新命名為 `edgeConfigId`。
- 將 `viewStart` 重新命名為 `renderDecisions`，預設為 false。如果設為 true，系統會擷取個人化產品建議並自動轉譯。
- `Get Decisions` 相關變更：
   - 移除 `getDecisions` 命令。
   - `sendEvent` 命令新增「`scopes`」選項。決策會以 `sendEvent` 所解析的 Promise 傳回。
   - 新增內建 `__view__` 範圍，系統會傳回頁面/檢視範圍產品建議（例如Target中的VEC選件）。
唯有`sendEvent`設為false，決策才會從`renderDecisions`命令傳回。
   - 新增 `Decisions Received` 事件，決策可供使用時就會觸發。
- 整合單一伺服器呼叫中的多個個人化通知。
- 修正每次參考資料元素時，「事件合併 ID」都會重設的問題。
- 將 `setCustomerIds` 動作重新命名為 `syncIdentity`。
- 新增 `getIdentity` 命令。目前僅能透過自訂程式碼使用。
- 使用`_satellite`啟用除錯功能後，現在會在Adobe Experience Platform Web SDK中啟用除錯功能。
- 新增在 XDM 物件中輸入值的相關支援：布林值、數字和小數。

## 0.0.10版 — 2020年3月16日

- 整合 `Consent` 底下的「選擇加入」和「選擇退出」概念，並新增 `setConsent` 命令。
- 新增可從 JavaScript/JSON 對應至 XDM 的新資料元素類型 `XDM Object`。

## 0.0.7版 — 2020年2月18日

- 移除 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 選項
- 支援在 edgeDomain 選項值中使用連字號
- ID 移轉期間提出的要求會傳送至 demdex 端點，以便在未設定 demdex Cookie 時提升跨網域識別能力
- ID 移轉期間提出的要求一律會要求回應，以確保身分識別 Cookie 正確設定
- 執行無效命令時，控制台中會記錄有效命令名稱清單
- 新增核取方塊，可將第三方Cookie支援切換至標籤擴充功能。 這會停用對 demdex.net 的呼叫

## 0.0.5版 — 2019年12月20日

- 將活動追蹤器設定新增至標籤擴充功能
- 在事件命令上公開 EventType 和 EventMergeId
- 將onBeforeEventSend設定新增至標籤擴充功能
- 將edgeBasePath設定新增至標籤延伸模組

## 0.0.3版 — 2019年11月25日

- 「傳送事件」動作新增「合併 ID」和「類型」欄位。將「合併 ID」對應至 XDM 結構的 `xdm.eventMergeID`，並將「類型」對應到 XDM 結構的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

- 首次發行
