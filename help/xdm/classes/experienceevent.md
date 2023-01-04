---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；身分對應；身分對應；結構設計；對應；事件模型；最佳作法；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent類別
topic-legacy: overview
description: 本檔案概述XDM ExperienceEvent類別，以及事件資料模型的最佳實務。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] 類

[!DNL XDM ExperienceEvent] 是標準的體驗資料模型(XDM)類別，可讓您在特定事件發生時或達到特定條件集時，建立系統的時間戳記快照。

體驗事件是所發生事件的事實記錄，包括相關個人的時間點和身分。 事件可以是顯性（直接可觀察的人類行為）或隱性（不直接人類行為而引發），記錄時不加匯總或解釋。 如需在Platform生態系統中使用此類別的詳細資訊，請參閱 [XDM概觀](../home.md#data-behaviors).

此 [!DNL XDM ExperienceEvent] 類本身為架構提供了多個與時間序列相關的欄位。 其中兩個欄位(`_id` 和 `timestamp`) **必填** 適用於以類別為基礎的所有結構，其餘則為選用。 擷取資料時，會自動填入部分欄位的值。

![XDM ExperienceEvent的結構，如同顯示在Platform UI中一樣](../images/classes/experienceevent/structure.png)

| 屬性 | 說明 |
| --- | --- |
| `_id`<br>**(必填)** | 事件的唯一字串識別碼。 此欄位可用來追蹤個別事件的獨特性、防止資料重複，以及在下游服務中尋找該事件。 在某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一標識符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果您是從來源連線串流資料，或直接從Parquet檔案內嵌資料，應串連使事件唯一的特定欄位組合（例如主要ID、時間戳記、事件類型等），以產生此值。 串連值必須是 `uri-reference` 格式字串，表示必須移除任何冒號字元。 之後，串連值應該會使用SHA-256或您選擇的其他演算法來雜湊。<br><br>必須區分 **此欄位不代表與個人相關的身分**，而是資料本身的記錄。 與個人有關的身份資料應被降級為 [身分欄位](../schema/composition.md#identity) 由相容的欄位群組提供。 |
| `eventMergeId` | 若使用 [Adobe Experience Platform Web SDK](../../edge/home.md) 若要內嵌資料，這代表內嵌批次的ID，該批次導致建立記錄。 資料擷取時，系統會自動填入此欄位。 不支援在Web SDK實作內容之外使用此欄位。 |
| `eventType` | 指出事件類型或類別的字串。 如果您想要區分相同結構和資料集中的不同事件類型，例如區分零售公司的產品檢視事件與購物車附加事件，則可使用此欄位。<br><br>此屬性的標準值提供於 [附錄](#eventType)，包括其預定使用案例的說明。 此欄位是可擴充的列舉，這表示您也可以使用自己的事件類型字串，將您追蹤的事件分類。<br><br>`eventType` 限制您在應用程式上每次點擊只使用單一事件，因此您必須使用計算欄位，讓系統知道最重要的事件。 如需詳細資訊，請參閱 [計算欄位的最佳作法](#calculated). |
| `producedBy` | 描述事件產生者或來源的字串值。 如果需要，此欄位可用來篩選特定事件產生器以用於細分。<br><br>此屬性的一些建議值提供於 [附錄](#producedBy). 此欄位是可擴充的列舉，這表示您也可以使用自己的字串來代表不同的事件產生者。 |
| `identityMap` | 一個地圖欄位，其中包含事件所套用之個人的命名空間身分識別集。 系統會在擷取身分資料時自動更新此欄位。 為了正確利用此欄位 [即時客戶個人檔案](../../profile/home.md)，請勿嘗試手動更新資料操作中欄位的內容。<br /><br />請參閱 [綱要構成基本知識](../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `timestamp`<br>**(必填)** | 事件發生時的ISO 8601時間戳記，格式如下 [RFC 3339第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6). 此時間戳記必須發生在過去。 請參閱下方的章節，內容如下： [時間戳記](#timestamps) 以了解使用此欄位的最佳實務。 |

{style=&quot;table-layout:auto&quot;}

## 事件模型的最佳作法

以下章節涵蓋在Adobe Experience Platform中設計事件型Experience Data Model(XDM)結構的最佳作法。

### 時間戳記 {#timestamps}

根 `timestamp` 事件架構的欄位可 **僅限** 代表事件本身的觀察，且必須發生在過去。 如果您的分段使用案例需要使用未來可能發生的時間戳記，這些值必須在體驗事件結構的其他位置受到限制。

例如，如果旅行和旅館業中的企業正在為航班預訂事件建模，則類別級別 `timestamp` 欄位代表觀察保留事件的時間。 與事件相關的其他時間戳記，例如旅行預訂的開始日期，應在標準或自訂欄位群組提供的個別欄位中擷取。

![](../images/classes/experienceevent/timestamps.png)

通過將類級時間戳記與事件結構中的其他相關日期時間值分開，您可以實施靈活的分段使用案例，同時保留體驗應用程式中客戶歷程的時間戳記帳戶。

### 使用計算欄位 {#calculated}

您的體驗應用程式中的某些互動可能會產生多個相關事件，技術上會共用相同的事件時間戳記，因此可以呈現為單一事件記錄。 例如，如果客戶檢視了您網站上的產品，則可能會產生兩個潛在事件記錄 `eventType` 值：「產品檢視」事件(`commerce.productViews`)或一般「頁面檢視」事件(`web.webpagedetails.pageViews`)。 在這些情況下，當單一點擊中擷取多個事件時，您可以使用計算欄位來擷取最重要的屬性。

[Adobe Experience Platform資料準備](../../data-prep/home.md) 可讓您將資料對應、轉換及驗證至XDM。 使用可用 [映射函式](../../data-prep/functions.md) 由服務提供，您可以叫用邏輯運算子，以便在將資料擷取到Experience Platform時，對來自多事件記錄的資料進行優先排序、轉換和/或合併。 在上例中，您可以指定 `eventType` 計算欄位，可在「產品檢視」和「頁面檢視」同時發生時，將「產品檢視」優先順序置於「頁面檢視」之上。

如果您要透過UI手動將資料內嵌至Platform，請參閱 [計算欄位](../../data-prep/ui/mapping.md#calculated-fields) ，以了解如何建立計算欄位的特定步驟。

如果您使用來源連線將資料串流至Platform，您可以設定來源，改為使用計算欄位。 請參閱 [特定來源的檔案](../../sources/home.md) ，以了解在設定連線時如何實作計算欄位的說明。

## 相容的架構欄位組 {#field-groups}

>[!NOTE]
>
>數個欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../field-groups/name-updates.md) 以取得更多資訊。

Adobe提供數個標準欄位群組，以搭配 [!DNL XDM ExperienceEvent] 類別。 以下是類別一些常用欄位群組的清單：

* [[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 餘額轉移]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 促銷活動行銷詳細資料]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 卡片動作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 管道詳細資料]](../field-groups/event/channel-details.md)
* [[!UICONTROL 商務詳細資訊]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款詳細資訊]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 設備更換詳細資訊]](../field-groups/event/device-trade-in-details.md)
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

下節包含 [!UICONTROL XDM ExperienceEvent] 類別。

### 的接受值 `eventType` {#eventType}

下表概述 `eventType`，及其定義：

| 值 | 定義 |
| --- | --- |
| `advertising.clicks` | 按一下廣告上的動作。 |
| `advertising.completes` | 已觀看計時媒體資產至完成。 這並不代表觀看者已觀看了整個影片，因為觀看者可能已提前略過。 |
| `advertising.conversions` | 由客戶執行的預先定義動作，會觸發事件進行績效評估。 |
| `advertising.federated` | 指出體驗事件是否是透過資料同盟建立（客戶之間的資料共用）。 |
| `advertising.firstQuartiles` | 數位視訊廣告以正常速度播放了25%的持續時間。 |
| `advertising.impressions` | 廣告給可能被檢視的客戶的曝光次數。 |
| `advertising.midpoints` | 數位視訊廣告以正常速度播放了50%的持續時間。 |
| `advertising.starts` | 數位視訊廣告已開始播放。 |
| `advertising.thirdQuartiles` | 數位視訊廣告以正常速度播放了75%的持續時間。 |
| `advertising.timePlayed` | 說明使用者在特定計時媒體資產上所花的時間量。 |
| `application.close` | 應用程式已關閉或發送到後台。 |
| `application.launch` | 應用程式已啟動或帶入前景。 |
| `commerce.checkouts` | 產品清單已發生結帳事件。 如果結帳過程中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用每個事件的時間戳記和參考頁面/體驗，以依序識別每個個別事件（步驟）。 |
| `commerce.productListAdds` | 產品已新增至產品清單或購物車。 |
| `commerce.productListOpens` | 新產品清單（購物車）已初始化或建立。 |
| `commerce.productListRemovals` | 已從產品清單或購物車中移除一或多個產品項目。 |
| `commerce.productListReopens` | 客戶已重新啟動不再存取（放棄）的產品清單（購物車），例如透過再行銷活動。 |
| `commerce.productListViews` | 產品清單或購物車已收到一或多個檢視。 |
| `commerce.productViews` | 產品已收到一或多個檢視。 |
| `commerce.purchases` | 已接受命令。 這是商務轉換中唯一的必要動作。 購買事件必須有參考的產品清單。 |
| `commerce.saveForLaters` | 已保存產品清單以供將來使用，例如產品願望清單。 |
| `decisioning.propositionDisplay` | 決策主張會顯示給人員。 |
| `decisioning.propositionInteract` | 人員與決策建議互動。 |
| `delivery.feedback` | 傳遞的意見事件，例如電子郵件傳遞。 |
| `directMarketing.emailBounced` | 已退信給人員的電子郵件。 |
| `directMarketing.emailBouncedSoft` | 傳送給人員的電子郵件已軟退信。 |
| `directMarketing.emailClicked` | 有人點按了行銷電子郵件中的連結。 |
| `directMarketing.emailDelivered` | 已成功將電子郵件傳送至人員的電子郵件服務 |
| `directMarketing.emailOpened` | 有人開啟了行銷電子郵件。 |
| `directMarketing.emailUnsubscribed` | 從行銷電子郵件取消訂閱的人員。 |
| `inappmessageTracking.dismiss` | 應用程式內訊息已關閉。 |
| `inappmessageTracking.display` | 已顯示應用程式內訊息。 |
| `inappmessageTracking.interact` | 已與應用程式內訊息互動。 |
| `leadOperation.callWebhook` | 系統因鉛而呼叫了網頁鈎點。 |
| `leadOperation.convertLead` | 銷售機會已轉換。 |
| `leadOperation.interestingMoment` | 錄下了一個有趣的時刻。 |
| `leadOperation.newLead` | 已建立銷售機會。 |
| `leadOperation.scoreChanged` | 銷售機會的分數屬性值已更改。 |
| `leadOperation.statusInCampaignProgressionChanged` | 促銷活動中的銷售機會狀態已變更。 |
| `listOperation.addToList` | 已將人員新增至行銷清單。 |
| `listOperation.removeFromList` | 從行銷清單中移除人員。 |
| `message.feedback` | 傳送給客戶之訊息的意見事件，例如傳送/退回/錯誤。 |
| `message.tracking` | 對傳送給客戶的訊息追蹤事件，例如開啟/點按/自訂動作。 |
| `opportunityEvent.addToOpportunity` | 將人員新增至機會。 |
| `opportunityEvent.opportunityUpdated` | 更新了機會。 |
| `opportunityEvent.removeFromOpportunity` | 某人被從機會中刪除。 |
| `pushTracking.applicationOpened` | 使用者從推播通知開啟應用程式。 |
| `pushTracking.customAction` | 使用者在推播通知中按一下自訂動作。 |
| `web.formFilledOut` | 有人在WEP頁上填寫了表格。 |
| `web.webinteraction.linkClicks` | 連結已選取一或多次。 |
| `web.webpagedetails.pageViews` | 網頁已接收到一個或多個視圖。 |

{style=&quot;table-layout:auto&quot;}

### 的建議值 `producedBy` {#producedBy}

下表概述 `producedBy`:

| 值 | 定義 |
| --- | --- |
| `self` | Self |
| `system` | 系統 |
| `salesRef` | 銷售代表 |
| `customerRep` | 客戶代表 |
