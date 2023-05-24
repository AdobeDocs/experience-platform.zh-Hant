---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；模式；身份映射；身份映射；模式設計；映射；事件建模；事件建模；最佳實踐；事件；事件；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent類
description: 本文檔概述了XDM ExperienceEvent類以及事件資料建模的最佳做法。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] 類

[!DNL XDM ExperienceEvent] 是標準的體驗資料模型(XDM)類，它允許您在特定事件發生或達到特定條件集時建立系統的時間戳快照。

「體驗事件」是所發生事件的事實記錄，包括所涉及個人的時間點和身份。 事件可以是顯性（直接可觀察的人類行為）或隱性（在沒有直接人類行為的情況下引起），並記錄時不進行匯總或解釋。 有關此類在平台生態系統中使用的更高級別資訊，請參閱 [XDM概述](../home.md#data-behaviors)。

的 [!DNL XDM ExperienceEvent] 類本身為架構提供多個與時間序列相關的欄位。 其中兩個欄位(`_id` 和 `timestamp`) **要求** 對於基於類的所有架構，其餘為可選。 在接收資料時，會自動填充某些欄位的值。

![XDM ExperienceEvent在平台UI中顯示的結構](../images/classes/experienceevent/structure.png)

| 屬性 | 說明 |
| --- | --- |
| `_id`<br>**(必填)** | 事件的唯一字串標識符。 此欄位用於跟蹤單個事件的唯一性、防止重複資料並在下游服務中查找該事件。 有時， `_id` 可以是 [通用唯一標識符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一標識符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果是從源連接流式傳輸資料或直接從Parce檔案接收資料，則應通過連接使事件唯一的特定欄位組合來生成此值，如主ID、時間戳、事件類型等。 連接的值必須是 `uri-reference` 格式化字串，表示必須刪除任何冒號字元。 然後，應使用SHA-256或您選擇的其他算法對連接值進行散列。<br><br>必須要區分 **此欄位不表示與個人相關的標識**&#x200B;而是資料本身的記錄。 與個人有關的身份資料應降級到 [標識欄位](../schema/composition.md#identity) 由相容欄位組提供。 |
| `eventMergeId` | 如果使用 [Adobe Experience PlatformWeb SDK](../../edge/home.md) 要接收資料，這表示導致建立記錄的接收批的ID。 資料接收時，系統會自動填充此欄位。 不支援在Web SDK實現的上下文之外使用此欄位。 |
| `eventType` | 一個字串，它指示事件的類型或類別。 如果要區分同一架構和資料集中的不同事件類型，例如區分零售公司的產品視圖事件和購物車附加事件，則可以使用此欄位。<br><br>此屬性的標準值在 [附錄部分](#eventType)包括其預期用例的說明。 此欄位是可擴展枚舉，這意味著您也可以使用自己的事件類型字串對正在跟蹤的事件進行分類。<br><br>`eventType` 限制您每次在應用程式上點擊時只使用一個事件，因此您必須使用計算欄位讓系統知道哪個事件最重要。 有關詳細資訊，請參閱 [計算欄位的最佳實踐](#calculated)。 |
| `producedBy` | 描述事件的生成者或來源的字串值。 如果需要，該欄位可用於過濾某些事件生成者以用於分段。<br><br>中提供了此屬性的一些建議值 [附錄部分](#producedBy)。 此欄位是可擴展的枚舉，這意味著您也可以使用自己的字串來表示不同的事件生成者。 |
| `identityMap` | 一個映射欄位，包含事件所應用的個體的一組命名空間標識。 當接收身份資料時，系統會自動更新此欄位。 為了正確利用此欄位 [即時客戶配置檔案](../../profile/home.md)，不要嘗試手動更新資料操作中欄位的內容。<br /><br />請參閱中有關標識映射的章節 [架構組合基礎](../schema/composition.md#identityMap) 的子菜單。 |
| `timestamp`<br>**(必填)** | 事件發生時的ISO 8601時間戳，格式為 [RFC 3339第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6)。 此時間戳必須發生在過去。 請參閱下面的章節 [時間戳](#timestamps) 用於此欄位的最佳做法。 |

{style="table-layout:auto"}

## 事件建模的最佳做法

以下各節介紹在Adobe Experience Platform設計基於事件的經驗資料模型(XDM)架構的最佳做法。

### 時間戳 {#timestamps}

根 `timestamp` 事件架構欄位 **僅** 代表事件本身的觀察，並且必須在過去發生。 如果您的分段使用案例要求使用將來可能發生的時間戳，則這些值必須在「體驗事件」架構的其他位置受到約束。

例如，如果旅行和接待行業的企業正在為航班預訂活動建模，則類別級別 `timestamp` 欄位表示觀察保留事件的時間。 與事件相關的其他時間戳，如旅行預訂的開始日期，應在標準或自定義欄位組提供的單獨欄位中捕獲。

![突出顯示了「航班預訂」和「開始日期」的「體驗事件」模式示例。](../images/classes/experienceevent/timestamps.png)

通過在事件模式中將類級別時間戳與其他相關日期時間值分開，可以實施靈活的分段使用情形，同時在體驗應用程式中保留客戶行程的時間戳帳戶。

### 使用計算欄位 {#calculated}

您的體驗應用程式中的某些交互可能會導致多個相關事件，這些事件在技術上共用相同的事件時間戳，因此可以表示為單個事件記錄。 例如，如果客戶在您的網站上查看產品，則可能會生成具有兩個潛在可能性的事件記錄 `eventType` 值：「產品視圖」事件(`commerce.productViews`)或泛型「頁面視圖」事件(`web.webpagedetails.pageViews`)。 在這些情況下，在一次命中捕獲多個事件時，可以使用計算欄位來捕獲最重要的屬性。

[Adobe Experience Platform資料準備](../../data-prep/home.md) 允許您將資料映射、轉換和驗證到XDM。 使用可用 [映射函式](../../data-prep/functions.md) 您可以調用邏輯運算子，以便在將多事件記錄資料接收到Experience Platform時對其進行優先順序排序、轉換和/或合併。 在上例中，可指定 `eventType` 作為計算欄位，在「產品視圖」和「頁面視圖」同時出現時，將「產品視圖」置於優先順序。

如果要通過UI手動將資料導入平台，請參閱上的指南 [計算欄位](../../data-prep/ui/mapping.md#calculated-fields) 有關如何建立計算欄位的特定步驟。

如果使用源連接將資料流式傳輸到平台，則可以將源配置為使用計算欄位。 請參閱 [特定來源的文檔](../../sources/home.md) 有關如何在配置連接時實現計算欄位的說明。

## 相容架構欄位組 {#field-groups}

>[!NOTE]
>
>幾個欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../field-groups/name-updates.md) 的子菜單。

Adobe提供幾個標準欄位組，用於 [!DNL XDM ExperienceEvent] 類。 以下是類中一些常用欄位組的清單：

* [[!UICONTROL Adobe AnalyticsExperienceEvent完全擴展]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 餘額轉移]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 市場活動市場營銷詳細資訊]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 卡操作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 渠道詳細資訊]](../field-groups/event/channel-details.md)
* [[!UICONTROL 商業詳細資訊]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款詳細資訊]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 設備折價詳細資訊]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐廳預訂]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 最終用戶ID詳細資訊]](../field-groups/event/enduserids.md)
* [[!UICONTROL 環境詳細資訊]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班預訂]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿預訂]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL 報價請求詳細資訊]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 保留詳細資訊]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web詳細資訊]](../field-groups/event/web-details.md)

## 附錄

以下部分包含有關 [!UICONTROL XDM體驗事件] 類。

### 接受的值 `eventType` {#eventType}

下表概述了 `eventType`以及它們的定義：

| 值 | 定義 |
| --- | --- |
| `advertising.clicks` | 按一下廣告上的操作。 |
| `advertising.completes` | 已監視定時媒體資產完成。 這並不一定意味著觀眾觀看了整個視頻，因為觀眾本可以跳過前面。 |
| `advertising.conversions` | 由客戶執行的預定義操作，該操作觸發用於績效評估的事件。 |
| `advertising.federated` | 指示是否通過資料聯合（客戶之間的資料共用）建立了體驗事件。 |
| `advertising.firstQuartiles` | 一個數字視頻廣告以正常速度播放了25%的持續時間。 |
| `advertising.impressions` | 對有可能被觀看的客戶的廣告的印象。 |
| `advertising.midpoints` | 一個數字視頻廣告以正常速度播放了其50%的持續時間。 |
| `advertising.starts` | 一個數字視頻廣告已經開始播放。 |
| `advertising.thirdQuartiles` | 一個數字視頻廣告以正常速度播放了75%的持續時間。 |
| `advertising.timePlayed` | 描述用戶在特定定時媒體資產上花費的時間。 |
| `application.close` | 應用程式已關閉或已發送到後台。 |
| `application.launch` | 已啟動或將應用程式置於前台。 |
| `commerce.checkouts` | 產品清單已發生簽出事件。 如果簽出過程中有多個步驟，則可能會出現多個簽出事件。 如果存在多個步驟，則使用每個事件的時間戳和引用的頁/體驗來標識按順序表示的每個單獨事件（步驟）。 |
| `commerce.productListAdds` | 產品已添加到產品清單或購物車中。 |
| `commerce.productListOpens` | 新產品清單（購物車）已初始化或建立。 |
| `commerce.productListRemovals` | 已從產品清單或購物車中刪除一個或多個產品條目。 |
| `commerce.productListReopens` | 客戶已重新激活不再可訪問（已放棄）的產品清單（購物車），例如通過再營銷活動。 |
| `commerce.productListViews` | 產品清單或購物車已收到一個或多個視圖。 |
| `commerce.productViews` | 產品已收到一個或多個視圖。 |
| `commerce.purchases` | 已接受訂單。 這是商業轉換中唯一必需的操作。 採購事件必須引用產品清單。 |
| `commerce.saveForLaters` | 已保存產品清單供將來使用，例如產品願望清單。 |
| `decisioning.propositionDisplay` | 一個決策命題被展示給一個人。 |
| `decisioning.propositionInteract` | 一個人與一個決策命題互動。 |
| `delivery.feedback` | 傳遞的反饋事件，如電子郵件傳遞。 |
| `directMarketing.emailBounced` | 一封電子郵件被拒。 |
| `directMarketing.emailBouncedSoft` | 給一個人的電郵被軟性拒發。 |
| `directMarketing.emailClicked` | 一個人點擊了營銷電子郵件中的連結。 |
| `directMarketing.emailDelivered` | 已成功將電子郵件發送到個人電子郵件服務 |
| `directMarketing.emailOpened` | 一個人開啟了營銷電子郵件。 |
| `directMarketing.emailUnsubscribed` | 取消訂閱營銷電子郵件的人。 |
| `inappmessageTracking.dismiss` | 應用內消息已被刪除。 |
| `inappmessageTracking.display` | 顯示應用內消息。 |
| `inappmessageTracking.interact` | 一個應用內資訊被互動。 |
| `leadOperation.callWebhook` | 為了響應線索，調用了網鈎。 |
| `leadOperation.convertLead` | 已轉換潛在顧客。 |
| `leadOperation.interestingMoment` | 為一個人錄制了一個有趣的時刻。 |
| `leadOperation.newLead` | 已建立潛在顧客。 |
| `leadOperation.scoreChanged` | 潛在客戶的得分屬性值已更改。 |
| `leadOperation.statusInCampaignProgressionChanged` | 銷售線索在市場活動中的狀態已更改。 |
| `listOperation.addToList` | 已將人員添加到市場營銷清單。 |
| `listOperation.removeFromList` | 已從市場營銷清單中刪除人員。 |
| `message.feedback` | 向客戶發送的消息的反饋事件（如發送/退回/錯誤）。 |
| `message.tracking` | 跟蹤事件，如對發送給客戶的消息的開啟/按一下/自定義操作。 |
| `opportunityEvent.addToOpportunity` | 已向機會添加人員。 |
| `opportunityEvent.opportunityUpdated` | 已更新機會。 |
| `opportunityEvent.removeFromOpportunity` | 某人被從機會中刪除。 |
| `pushTracking.applicationOpened` | 從推送通知中開啟應用程式的人員。 |
| `pushTracking.customAction` | 某人按一下了推送通知中的自定義操作。 |
| `web.formFilledOut` | 一個人在紙頁上填寫了表格。 |
| `web.webinteraction.linkClicks` | 已選擇一個或多個連結。 |
| `web.webpagedetails.pageViews` | 網頁已收到一個或多個視圖。 |

{style="table-layout:auto"}

### 建議的值 `producedBy` {#producedBy}

下表概述了某些已接受的值 `producedBy`:

| 值 | 定義 |
| --- | --- |
| `self` | 自我 |
| `system` | 系統 |
| `salesRef` | 銷售代表 |
| `customerRep` | 客戶代表 |
