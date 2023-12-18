---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；結構描述；identityMap；身分對應；身分對應；結構描述設計；對應；事件模型；事件模型；最佳實務；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent類別
description: 瞭解XDM ExperienceEvent類別和事件資料模型化的最佳實務。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '2659'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] 類別

[!DNL XDM ExperienceEvent] 是標準的體驗資料模型(XDM)類別，可讓您在特定事件發生或達到特定條件集時，建立系統的時間戳記快照。

體驗事件是所發生事件的事實記錄，包括時間點和所涉及個人的身分。 事件可以是明確的（直接可觀察的人類動作）或內隱的（在沒有直接人類動作的情況下引發），並且記錄時不會進行彙總或解譯。 如需有關在平台生態系統中使用此類別的高層級資訊，請參閱 [XDM概覽](../home.md#data-behaviors).

此 [!DNL XDM ExperienceEvent] 類別本身為結構描述提供幾個時間序列相關的欄位。 其中兩個欄位(`_id` 和 `timestamp`)為 **必填** 適用於以類別為基礎的所有結構描述，其餘則為選用。 某些欄位的值會在擷取資料時自動填入。

![Platform UI中顯示的XDM ExperienceEvent結構](../images/classes/experienceevent/structure.png)

| 屬性 | 說明 |
| --- | --- |
| `_id`<br>**（必要）** | 體驗事件類別 `_id` 欄位可唯一識別擷取至Adobe Experience Platform的個別事件。 此欄位用於追蹤個別事件的唯一性、防止資料重複，以及在下游服務中查詢該事件。<br><br>在偵測到重複事件時，Platform應用程式和服務可能會以不同方式處理重複。 例如，如果設定檔服務中的事件相同，則會捨棄該重複事件 `_id` 設定檔存放區中已存在。<br><br>在某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://datatracker.ietf.org/doc/html/rfc4122) 或 [全域唯一識別碼(GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果您要從來源連線串流資料，或直接從Parquet檔案擷取資料，應串連特定欄位組合，讓事件具有唯一性，以產生此值。 可串連的事件範例包括主要ID、時間戳記、事件型別等。 串連值必須是 `uri-reference` 字串格式化，表示必須移除任何冒號字元。 之後，應該使用SHA-256或您選擇的其他演演算法來雜湊串連值。<br><br>請務必區分 **此欄位不代表與個人相關的身分**&#x200B;而是資料本身的記錄。 與個人相關的身分資料應委派至 [身分欄位](../schema/composition.md#identity) 由相容的欄位群組所提供。 |
| `eventMergeId` | 若使用 [Adobe Experience Platform Web SDK](../../edge/home.md) 若要內嵌資料，這代表造成建立記錄之內嵌批次的ID。 此欄位在資料擷取時由系統自動填入。 不支援在Web SDK實作的內容之外使用此欄位。 |
| `eventType` | 指出事件型別或類別的字串。 如果您想要將相同結構描述和資料集中的不同事件型別區分開來，例如將產品檢視事件與零售公司的加入購物車事件區分開來，則可以使用此欄位。<br><br>此屬性的標準值提供在 [附錄部分](#eventType)，包括預期使用案例的說明。 此欄位是可延伸的列舉，這表示您也可以使用自己的事件型別字串來分類您正在追蹤的事件。<br><br>`eventType` 限制您只能針對應用程式的每個點選使用單一事件，因此您必須使用計算欄位，讓系統知道哪個事件最重要。 如需詳細資訊，請參閱以下章節： [計算欄位的最佳實務](#calculated). |
| `producedBy` | 說明事件製作者或來源的字串值。 如有需要，此欄位可用於篩選掉某些事件產生者，以用於分段目的。<br><br>此屬性的部分建議值提供在 [附錄部分](#producedBy). 此欄位是可擴充的列舉，這表示您也可以使用自己的字串來代表不同的事件產生器。 |
| `identityMap` | 對應欄位，其中包含套用事件之個人的一組名稱空間身分識別。 系統會在擷取身分資料時自動更新此欄位。 為了正確使用此欄位， [即時客戶個人檔案](../../profile/home.md)，請勿嘗試在資料作業中手動更新欄位內容。<br /><br />請參閱以下連結中有關身分對應的章節： [結構描述組合的基本面](../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `timestamp`<br>**（必要）** | 事件發生時間的ISO 8601時間戳記，格式如下 [RFC 3339第5.6節](https://datatracker.ietf.org/doc/html/rfc3339). 此時間戳記必須發生在過去。 請參閱以下小節： [時間戳記](#timestamps) 以取得使用此欄位的最佳作法。 |

{style="table-layout:auto"}

## 事件模型化的最佳實務

以下章節涵蓋在Adobe Experience Platform中設計事件型Experience Data Model (XDM)結構描述的最佳作法。

### 時間戳記 {#timestamps}

根 `timestamp` 事件結構描述的欄位可以 **僅限** 代表觀察到的事件本身，且必須發生在過去。 如果您的分段使用案例需要使用未來可能發生的時間戳記，這些值必須在您的體驗事件結構描述中的其他位置限制。

例如，如果旅遊業及旅館業中的企業正在模型化航班訂位事件，則類別層級 `timestamp` 欄位代表觀察預訂事件的時間。 與事件相關的其他時間戳記（例如旅行預訂的開始日期）應擷取在標準或自訂欄位群組提供的個別欄位中。

![反白顯示航班預訂和開始日期的體驗事件結構描述範例。](../images/classes/experienceevent/timestamps.png)

將類別層級的時間戳記與事件結構描述中的其他相關日期時間值分開，您就可以實作靈活的分段使用案例，同時保留體驗應用程式中客戶歷程的時間戳記帳戶。

### 使用計算欄位 {#calculated}

體驗應用程式中的某些互動可能會產生多個相關事件，這些事件在技術上會共用相同的事件時間戳記，因此可以顯示為單一事件記錄。 例如，如果客戶檢視您網站上的產品，這可能會導致事件記錄具有兩種可能性 `eventType` 值： 「產品檢視」事件(`commerce.productViews`)或一般「頁面檢視」事件(`web.webpagedetails.pageViews`)。 在這些情況下，您可以在單一點選中擷取多個事件時，使用計算欄位來擷取最重要的屬性。

[Adobe Experience Platform資料準備](../../data-prep/home.md) 可讓您對應、轉換及驗證來往於XDM的資料。 使用可用的 [對應函式](../../data-prep/functions.md) 由服務提供，您可以叫用邏輯運運算元，以便在資料擷取至Experience Platform時，優先處理、轉換及/或合併多事件記錄中的資料。 在上述範例中，您可以指定 `eventType` 作為計算欄位，每當「產品檢視」和「頁面檢視」發生時，都會優先處理「產品檢視」。

如果您是透過UI手動將資料擷取到Platform，請參閱 [計算欄位](../../data-prep/ui/mapping.md#calculated-fields) ，以瞭解如何建立計算欄位的特定步驟。

如果您使用來源連線將資料串流至Platform，您可以設定來源以改為利用計算欄位。 請參閱 [您特定來源的檔案](../../sources/home.md) ，瞭解設定連線時如何實作計算欄位。

## 相容的結構描述欄位群組 {#field-groups}

>[!NOTE]
>
>數個欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../field-groups/name-updates.md) 以取得詳細資訊。

Adobe提供數個標準欄位群組，可與搭配使用 [!DNL XDM ExperienceEvent] 類別。 以下是類別的一些常用欄位群組清單：

* [[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 餘額轉帳]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 行銷活動行銷細節]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 卡片動作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 管道詳細資料]](../field-groups/event/channel-details.md)
* [[!UICONTROL 商業細節]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款細節]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 裝置折舊換新細節]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐飲預訂]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 一般使用者ID詳細資訊]](../field-groups/event/enduserids.md)
* [[!UICONTROL 環境詳細資訊]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班預訂]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿預訂]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics互動細節]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL 報價請求細節]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 預訂詳細資料]](../field-groups/event/reservation-details.md)
* [[!UICONTROL 網頁詳細資訊]](../field-groups/event/web-details.md)

## 附錄

下節包含更多關於 [!UICONTROL XDM ExperienceEvent] 類別。

### 接受的值 `eventType` {#eventType}

下表概述下列專案可接受的值 `eventType`，以及其定義：

| 值 | 定義 |
| --- | --- |
| `advertising.clicks` | 此事件會追蹤何時發生選取廣告的動作。 |
| `advertising.completes` | 此事件會追蹤定時媒體資產何時觀看完畢。 這並不一定表示檢視者看完整段影片，因為檢視者可能略過前面。 |
| `advertising.conversions` | 此事件會追蹤客戶執行的預先定義動作，該動作會觸發效能評估事件。 |
| `advertising.federated` | 此事件會追蹤體驗事件是否透過資料同盟（客戶之間的資料共用）建立。 |
| `advertising.firstQuartiles` | 此事件會追蹤數位影片廣告何時以正常速度播放其持續時間的25%。 |
| `advertising.impressions` | 此事件會追蹤客戶對有可能檢視之廣告的閱聽。 |
| `advertising.midpoints` | 此事件會追蹤數位影片廣告何時以正常速度播放其長度的50%。 |
| `advertising.starts` | 此事件會追蹤數位影片廣告何時開始播放。 |
| `advertising.thirdQuartiles` | 此事件會追蹤數位影片廣告何時以正常速度播放其長度的75%。 |
| `advertising.timePlayed` | 此事件會追蹤使用者在特定的定時媒體資產上所花費的時間。 |
| `application.close` | 此事件會追蹤應用程式何時關閉或傳送到背景。 |
| `application.launch` | 此事件會追蹤應用程式啟動或進入前景的時間。 |
| `commerce.backofficeCreditMemoIssued` | 此事件會追蹤何時向客戶發出信用通知。 |
| `commerce.backofficeOrderCancelled` | 此事件會追蹤先前起始的購買程式在完成前何時終止。 |
| `commerce.backofficeOrderItemsShipped` | 此事件會追蹤購買的專案實際運送給客戶的時間。 |
| `commerce.backofficeOrderPlaced` | 此事件會追蹤訂單的放置位置。 |
| `commerce.backofficeShipmentCompleted` | 此事件會追蹤整個出貨流程的順利完成。 |
| `commerce.checkouts` | 此事件會追蹤產品清單何時發生結帳事件。 如果結帳程式中有多個步驟，就可能有一個以上的結帳事件。 如果有多個步驟，則會使用時間戳記和每個事件的參考頁面/體驗來識別每個個別事件（步驟），並依序表示。 |
| `commerce.productListAdds` | 此事件會追蹤產品何時已新增至產品清單或購物車。 |
| `commerce.productListOpens` | 此事件會追蹤新產品清單（購物車）何時已初始化或建立。 |
| `commerce.productListRemovals` | 此事件會追蹤何時將產品專案從產品清單或購物車中移除。 |
| `commerce.productListReopens` | 此事件會追蹤客戶何時已無法存取（已捨棄）的產品清單（購物車）重新啟用，例如透過重新行銷活動。 |
| `commerce.productListViews` | 此事件會追蹤產品清單或購物車何時收到檢視。 |
| `commerce.productViews` | 此事件會追蹤產品何時收到一或多個檢視。 |
| `commerce.purchases` | 此事件會追蹤何時接受訂單。 這是商業轉換中唯一需要的動作。 購買事件必須有參考的產品清單。 |
| `commerce.saveForLaters` | 此事件會追蹤產品清單何時儲存以供日後使用，例如產品願望清單。 |
| `decisioning.propositionDisplay` | 此事件會追蹤何時向個人顯示決策主張。 |
| `decisioning.propositionDismiss` | 此事件會追蹤何時已決定不要與已呈現的優惠互動。 |
| `decisioning.propositionInteract` | 此事件會追蹤個人何時與決策主張互動。 |
| `decisioning.propositionSend` | 此事件會追蹤何時決定傳送建議或優惠給潛在客戶以供考慮。 |
| `decisioning.propositionTrigger` | 此事件會追蹤主張程式的啟用情況。 已發生特定條件或動作來提示顯示優惠方案。 |
| `delivery.feedback` | 此事件會追蹤傳送的意見反應事件，例如電子郵件傳送。 |
| `directMarketing.emailBounced` | 此事件會追蹤傳送給個人的電子郵件何時退回。 |
| `directMarketing.emailBouncedSoft` | 此事件會追蹤傳送給個人的電子郵件何時軟跳出。 |
| `directMarketing.emailClicked` | 此事件會追蹤使用者何時點按行銷電子郵件中的連結。 |
| `directMarketing.emailDelivered` | 此事件會追蹤電子郵件何時成功傳遞至個人的電子郵件服務。 |
| `directMarketing.emailOpened` | 此事件會追蹤使用者何時開啟行銷電子郵件。 |
| `directMarketing.emailSent` | 此事件會追蹤行銷電子郵件何時已傳送給個人。 |
| `directMarketing.emailUnsubscribed` | 此事件會追蹤個人何時取消訂閱行銷電子郵件。 |
| `inappmessageTracking.dismiss` | 此事件會追蹤應用程式內訊息何時被關閉。 |
| `inappmessageTracking.display` | 此事件會追蹤何時顯示應用程式內訊息。 |
| `inappmessageTracking.interact` | 此事件會追蹤應用程式內訊息何時與互動。 |
| `leadOperation.callWebhook` | 此事件會追蹤何時呼叫webhook以回應銷售機會。 |
| `leadOperation.changeCampaignStream` | 此事件表示特定業務潛在客戶的行銷或參與策略有所轉變。 |
| `leadOperation.changeEngagementCampaignCadence` | 此事件會追蹤潛在客戶在行銷活動中參與頻率的變更。 |
| `leadOperation.convertLead` | 此事件會追蹤銷售機會何時轉換。 |
| `leadOperation.interestingMoment` | 此事件會追蹤何時為個人錄製有趣的時刻。 |
| `leadOperation.mergeLeads` | 此事件會追蹤來自多個銷售機會（參考相同實體）的資訊何時合併。 |
| `leadOperation.newLead` | 此事件會追蹤銷售機會的建立時間。 |
| `leadOperation.scoreChanged` | 此事件會追蹤潛在客戶評分屬性的值何時變更。 |
| `leadOperation.statusInCampaignProgressionChanged` | 此事件會追蹤潛在客戶在行銷活動中的狀態何時已變更。 |
| `listOperation.addToList` | 此事件會追蹤何時將個人新增至行銷清單。 |
| `listOperation.removeFromList` | 此事件會追蹤何時將個人從行銷名單移除。 |
| `media.adBreakComplete` | 此事件會追蹤 `adBreakComplete` 事件已發生。 此事件會在廣告插播開始時觸發。 |
| `media.adBreakStart` | 此事件會追蹤 `adBreakStart` 事件已發生。 此事件會在廣告插播結束時觸發。 |
| `media.adComplete` | 此事件會追蹤 `adComplete` 事件已發生。 當廣告完成時，就會觸發此事件。 |
| `media.adSkip` | 此事件會追蹤 `adSkip` 事件已發生。 此事件會在略過廣告時觸發。 |
| `media.adStart` | 此事件會追蹤 `adStart` 事件已發生。 當廣告開始時，就會觸發此事件。 |
| `media.bitrateChange` | 此事件會追蹤 `bitrateChange` 事件已發生。 當位元速率發生變更時，就會觸發此事件。 |
| `media.bufferStart` | 此事件會追蹤 `bufferStart` 事件已發生。 媒體開始緩衝時會觸發此事件。 |
| `media.chapterComplete` | 此事件會追蹤 `chapterComplete` 事件已發生。 此事件會在媒體中章節完成時觸發。 |
| `media.chapterSkip` | 此事件會追蹤 `chapterSkip` 事件已發生。 當使用者向前或向後跳到媒體內容中的另一個區段或章節時，就會觸發此事件。 |
| `media.chapterStart` | 此事件會追蹤 `chapterStart` 事件已發生。 此事件會在媒體內容中的特定區段或章節開始時觸發。 |
| `media.downloaded` | 此事件會追蹤媒體下載內容何時發生。 |
| `media.error` | 此事件會追蹤 `error` 事件已發生。 當媒體播放期間發生錯誤或問題時，就會觸發此事件。 |
| `media.pauseStart` | 此事件會追蹤 `pauseStart` 事件已發生。 當使用者起始媒體播放暫停的動作時，就會觸發此事件。 |
| `media.ping` | 此事件會追蹤 `ping` 事件已發生。 這可以驗證媒體資源的可用性。 |
| `media.play` | 此事件會追蹤 `play` 事件已發生。 此事件會在媒體內容播放時觸發，表示使用者使用中的內容。 |
| `media.sessionComplete` | 此事件會追蹤 `sessionComplete` 事件已發生。 此事件會標籤媒體播放工作階段的結尾。 |
| `media.sessionEnd` | 此事件會追蹤 `sessionEnd` 事件已發生。 此事件表示媒體工作階段的結論。 此結論可能涉及關閉媒體播放器或停止播放。 |
| `media.sessionStart` | 此事件會追蹤 `sessionStart` 事件已發生。 此事件標示媒體播放工作階段的開始。 它會在使用者開始播放媒體檔案時觸發。 |
| `media.statesUpdate` | 此事件會追蹤 `statesUpdate` 事件已發生。 播放器狀態追蹤功能可附加至音訊或影片資料流。標準狀態為：fullscreen、mute、closedCaptioning、pictureInPicture 和 inFocus。 |
| `opportunityEvent.addToOpportunity` | 此事件會追蹤何時將個人新增至商機。 |
| `opportunityEvent.opportunityUpdated` | 此事件會追蹤商機何時更新。 |
| `opportunityEvent.removeFromOpportunity` | 此事件會追蹤何時將個人從機會中移除。 |
| `pushTracking.applicationOpened` | 此事件會追蹤使用者何時從推播通知開啟應用程式。 |
| `pushTracking.customAction` | 此事件會追蹤使用者何時在推播通知中選取自訂動作。 |
| `web.formFilledOut` | 此事件會追蹤某人何時在網頁上填寫表單。 |
| `web.webinteraction.linkClicks` | 此事件會追蹤何時已選取一次或多次連結。 |
| `web.webpagedetails.pageViews` | 此事件會追蹤網頁何時收到一或多個檢視。 |
| `location.entry` | 此事件會追蹤使用者或裝置進入特定位置。 |
| `location.exit` | 此事件會追蹤人員或裝置從特定位置離開。 |

{style="table-layout:auto"}

### 建議值 `producedBy` {#producedBy}

下表概述一些接受的值 `producedBy`：

| 值 | 定義 |
| --- | --- |
| `self` | 自我 |
| `system` | 系統 |
| `salesRef` | 銷售代表 |
| `customerRep` | 客戶代表 |
