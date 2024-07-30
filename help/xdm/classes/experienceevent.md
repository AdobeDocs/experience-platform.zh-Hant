---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；結構描述；identityMap；身分對應；身分對應；結構描述設計；對應；事件模型；事件模型；最佳實務；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent類別
description: 瞭解XDM ExperienceEvent類別和事件資料模型化的最佳實務。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 5537485206c1625ca661d6b33f7bba08538a0fa3
workflow-type: tm+mt
source-wordcount: '2761'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent]類別

[!DNL XDM ExperienceEvent]是標準的體驗資料模型(XDM)類別。 當特定事件發生或達到特定條件集合時，使用此類別建立系統的時間戳記快照。

體驗事件是所發生事件的事實記錄，包括時間點和所涉及個人的身分。 事件可以是明確的（直接可觀察的人類動作）或內隱的（在沒有直接人類動作的情況下引發），並且記錄時不會進行彙總或解譯。 如需在Platform生態系統中使用此類別的高階資訊，請參閱[XDM概觀](../home.md#data-behaviors)。

[!DNL XDM ExperienceEvent]類別本身為結構描述提供數個時間序列相關欄位。 其中兩個欄位（`_id`和`timestamp`）是基於此類別的所有結構描述都是&#x200B;**必要**，其餘則是選擇性的。 某些欄位的值會在擷取資料時自動填入。

![ XDM ExperienceEvent在Platform UI中顯示的結構。](../images/classes/experienceevent/structure.png)

| 屬性 | 說明 |
| --- | --- |
| `_id`<br>**（必要）** | 體驗事件類別`_id`欄位可唯一識別擷取至Adobe Experience Platform的個別事件。 此欄位用於追蹤個別事件的唯一性、防止資料重複，以及在下游服務中查詢該事件。<br><br>在偵測到重複事件的地方，Platform應用程式和服務可能會以不同的方式處理重複。 例如，如果設定檔存放區中已存在具有相同`_id`的事件，則會捨棄設定檔服務中的重複事件。<br><br>在某些情況下，`_id`可以是[通用唯一識別碼(UUID)](https://datatracker.ietf.org/doc/html/rfc4122)或[全域唯一識別碼(GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果您要從來源連線串流資料，或直接從Parquet檔案擷取資料，您應該串連特定欄位組合，讓事件具有唯一性，以產生此值。 可串連的事件範例包括主要ID、時間戳記、事件型別等。 串連值必須是`uri-reference`格式字串，這表示必須移除任何冒號字元。 之後，應該使用SHA-256或您選擇的其他演演算法來雜湊串連值。<br><br>請務必注意，**此欄位不代表與個人相關的身分**，而是資料本身的記錄。 與個人相關的身分資料應委派給相容欄位群組所提供的[身分欄位](../schema/composition.md#identity)。 |
| `eventMergeId` | 如果使用[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)來內嵌資料，這表示所內嵌批次導致建立記錄的識別碼。 此欄位在資料擷取時由系統自動填入。 不支援在Web SDK實作的內容之外使用此欄位。 |
| `eventType` | 指出事件型別或類別的字串。 如果您想要將相同結構描述和資料集中的不同事件型別區分開來，例如將產品檢視事件與零售公司的加入購物車事件區分開來，則可以使用此欄位。<br><br>此屬性的標準值在[附錄區段](#eventType)中提供，包括預期使用案例的說明。 此欄位是可延伸的列舉，這表示您也可以使用自己的事件型別字串來分類您正在追蹤的事件。<br><br>`eventType`限制您在應用程式上每個點選只能使用單一事件，因此您必須使用計算欄位，讓系統知道哪個事件最重要。 如需詳細資訊，請參閱[計算欄位](#calculated)的最佳實務一節。 |
| `producedBy` | 說明事件製作者或來源的字串值。 如有需要，此欄位可用於篩選掉某些事件產生者，以用於分段目的。<br><br>在[附錄區段](#producedBy)中提供了這個屬性的某些建議值。 此欄位是可擴充的列舉，這表示您也可以使用自己的字串來代表不同的事件產生器。 |
| `identityMap` | 對應欄位，其中包含套用事件之個人的一組名稱空間身分識別。 系統會在擷取身分資料時自動更新此欄位。 若要針對[即時客戶設定檔](../../profile/home.md)正確使用此欄位，請勿嘗試在您的資料作業中手動更新欄位內容。<br /><br />如需有關其使用案例的詳細資訊，請參閱[結構描述組合基本概念](../schema/composition.md#identityMap)中身分對應一節。 |
| `timestamp`<br>**（必要）** | 事件發生時間的ISO 8601時間戳記，格式為[RFC 3339第5.6](https://datatracker.ietf.org/doc/html/rfc3339)節。 此時間戳記&#x200B;**必須**&#x200B;發生在過去，但&#x200B;**必須**&#x200B;發生在1970年以後。 如需使用此欄位的最佳實務，請參閱以下有關[時間戳記](#timestamps)的章節。 |

{style="table-layout:auto"}

## 事件模型化的最佳實務

以下章節涵蓋在Adobe Experience Platform中設計事件型Experience Data Model (XDM)結構描述的最佳作法。

### 時間戳記 {#timestamps}

事件結構描述的根`timestamp`欄位&#x200B;**只能**&#x200B;代表事件本身的觀察結果，而且必須發生在過去。 但是，事件&#x200B;**必須**&#x200B;從1970年開始進行。 如果您的分段使用案例需要使用未來可能發生的時間戳記，這些值必須在您的體驗事件結構描述中的其他位置限制。

例如，如果旅遊及旅館業的企業正在模型化航班訂位事件，則類別層級`timestamp`欄位代表觀察訂位事件的時間。 與事件相關的其他時間戳記（例如旅行預訂的開始日期）應擷取在標準或自訂欄位群組提供的個別欄位中。

![已反白航班預訂和開始日期的範例體驗事件結構描述。](../images/classes/experienceevent/timestamps.png)

將類別層級的時間戳記與事件結構描述中的其他相關日期時間值分開，您就可以實作靈活的分段使用案例，同時保留體驗應用程式中客戶歷程的時間戳記帳戶。

### 使用計算欄位 {#calculated}

體驗應用程式中的某些互動可能會產生多個相關事件，這些事件在技術上會共用相同的事件時間戳記，因此可以顯示為單一事件記錄。 例如，如果客戶檢視您網站上的產品，這可能會導致事件記錄有兩個潛在的`eventType`值：「產品檢視」事件(`commerce.productViews`)或一般的「頁面檢視」事件(`web.webpagedetails.pageViews`)。 在這些情況下，您可以在單一點選中擷取多個事件時，使用計算欄位來擷取最重要的屬性。

使用[Adobe Experience Platform資料準備](../../data-prep/home.md)來對XDM與來自XDM的資料進行對應、轉換及驗證。 使用服務提供的可用[對應函式](../../data-prep/functions.md)，您可以叫用邏輯運運算元，以便在資料擷取到Experience Platform時，優先處理、轉換及/或合併多事件記錄中的資料。 在上述範例中，您可以指定`eventType`為計算欄位，每當「產品檢視」與「頁面檢視」同時發生時，就會優先處理「產品檢視」。

如果您是透過UI手動將資料擷取到Platform，請參閱[計算欄位](../../data-prep/ui/mapping.md#calculated-fields)的指南，以瞭解如何建立計算欄位的特定步驟。

如果您使用來源連線將資料串流至Platform，您可以設定來源以改為利用計算欄位。 請參閱您特定來源](../../sources/home.md)的[檔案，瞭解設定連線時如何實作計算欄位的指示。

## 相容的結構描述欄位群組 {#field-groups}

>[!NOTE]
>
>數個欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../field-groups/name-updates.md)的檔案。

Adobe提供數個標準欄位群組以與[!DNL XDM ExperienceEvent]類別搭配使用。 以下是類別的一些常用欄位群組清單：

* [[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 餘額轉帳]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 行銷活動行銷詳細資料]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 卡片動作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 管道詳細資料]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce詳細資料]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款詳細資料]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 裝置折舊換新細節]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐飲預訂]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 一般使用者ID詳細資料]](../field-groups/event/enduserids.md)
* [[!UICONTROL 環境詳細資料]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班預訂]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿預訂]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics互動詳細資料]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL 報價請求詳細資料]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 預訂詳細資料]](../field-groups/event/reservation-details.md)
* [[!UICONTROL 網頁詳細資料]](../field-groups/event/web-details.md)

## 附錄

以下區段包含有關[!UICONTROL XDM ExperienceEvent]類別的其他資訊。

### `eventType`的接受值 {#eventType}

下表概述`eventType`的可接受值及其定義：

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
| `click` | **已棄用**&#x200B;而改用`decisioning.propositionInteract`。 |
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
| `decisioning.propositionDisplay` | 當Web SDK自動傳送頁面上所顯示內容的相關資訊時，就會使用此事件。 不過，如果您已透過其他方式（例如頁面點選的頂端和底部）包含顯示資訊，則不需要此事件型別。 在頁面點選的底部，您可以選擇任何您喜歡的事件型別。 |
| `decisioning.propositionDismiss` | 當Adobe Journey Optimizer應用程式內訊息或內容卡被解除時，會使用此事件型別。 |
| `decisioning.propositionFetch` | 用於表示事件主要是為了擷取決策。 Adobe Analytics會自動刪除此事件。 |
| `decisioning.propositionInteract` | 此事件型別用於追蹤個人化內容上的互動，例如點按。 |
| `decisioning.propositionSend` | 此事件會追蹤何時決定傳送建議或優惠給潛在客戶以供考慮。 |
| `decisioning.propositionTrigger` | [Web SDK](../../web-sdk/home.md)會將此型別的事件儲存在本機儲存體中，但不會傳送至Experience Edge。 每次滿足規則集時，就會產生事件並儲存在本機儲存體中（如果已啟用該設定）。 |
| `delivery.feedback` | 此事件會追蹤傳送的意見反應事件，例如電子郵件傳送。 |
| `directMarketing.emailBounced` | 此事件會追蹤傳送給個人的電子郵件何時退回。 |
| `directMarketing.emailBouncedSoft` | 此事件會追蹤傳送給個人的電子郵件何時軟跳出。 |
| `directMarketing.emailClicked` | 此事件會追蹤使用者何時點按行銷電子郵件中的連結。 |
| `directMarketing.emailDelivered` | 此事件會追蹤電子郵件何時成功傳遞至個人的電子郵件服務。 |
| `directMarketing.emailOpened` | 此事件會追蹤使用者何時開啟行銷電子郵件。 |
| `directMarketing.emailSent` | 此事件會追蹤行銷電子郵件何時已傳送給個人。 |
| `directMarketing.emailUnsubscribed` | 此事件會追蹤個人何時取消訂閱行銷電子郵件。 |
| `display` | **已棄用**&#x200B;而改用`decisioning.propositionDisplay`。 |
| `inappmessageTracking.dismiss` | 此事件會追蹤應用程式內訊息何時被關閉。 |
| `inappmessageTracking.display` | 此事件會追蹤何時顯示應用程式內訊息。 |
| `inappmessageTracking.interact` | 此事件會追蹤應用程式內訊息何時與互動。 |
| `leadOperation.callWebhook` | 此事件會追蹤何時呼叫webhook以回應銷售機會。 |
| `leadOperation.changeCampaignStream` | 此事件表示特定業務潛在客戶的行銷或參與策略有所轉變。 |
| `leadOperation.changeEngagementCampaignCadence` | 此事件會追蹤潛在客戶在行銷活動中參與頻率的變更。 |
| `leadOperation.convertLead` | 此事件會追蹤銷售機會何時轉換。 |
| `leadOperation.interestingMoment` | 此事件會追蹤何時為個人錄製有趣的時刻。 |
| `leadOperation.mergeLeads` | 此事件會追蹤來自參照相同實體的多個銷售機會的資訊何時合併。 |
| `leadOperation.newLead` | 此事件會追蹤銷售機會的建立時間。 |
| `leadOperation.scoreChanged` | 此事件會追蹤潛在客戶評分屬性的值何時變更。 |
| `leadOperation.statusInCampaignProgressionChanged` | 此事件會追蹤潛在客戶在行銷活動中的狀態何時已變更。 |
| `listOperation.addToList` | 此事件會追蹤何時將個人新增至行銷清單。 |
| `listOperation.removeFromList` | 此事件會追蹤何時將個人從行銷名單移除。 |
| `media.adBreakComplete` | 此事件代表廣告插播完成。 |
| `media.adBreakStart` | 此事件代表廣告插播開始。 |
| `media.adComplete` | 此事件代表廣告完成。 |
| `media.adSkip` | 此事件會在廣告被略過時發出訊號。 |
| `media.adStart` | 此事件代表廣告開始。 |
| `media.bitrateChange` | 這個事件會在位元速率發生變更時發出訊號。 |
| `media.bufferStart` | 緩衝開始時會傳送`media.bufferStart`事件型別。 沒有特定的`bufferResume`事件型別；在`bufferStart`事件後傳送`play`事件時，緩衝會被視為已繼續。 |
| `media.chapterComplete` | 此事件代表章節結束。 |
| `media.chapterSkip` | 當使用者向前或向後跳到另一個區段或章節時，就會觸發此事件。 |
| `media.chapterStart` | 此事件代表章節開始。 |
| `media.downloaded` | 此事件會追蹤媒體下載內容何時發生。 |
| `media.error` | 此事件代表媒體播放期間發生錯誤。 |
| `media.pauseStart` | 此事件會追蹤`pauseStart`事件何時發生。 當使用者起始媒體播放暫停的動作時，就會觸發此事件。 沒有繼續事件型別。 在`pauseStart`之後傳送播放事件時會推斷為繼續。 |
| `media.ping` | `media.ping`事件型別用於表示持續播放狀態。 針對主要內容，在播放期間必須每10秒傳送此事件，從播放開始後的10秒開始。 對於廣告內容，在廣告追蹤期間必須每秒傳送一次。 Ping事件不應在要求內文中包含引數對應。 |
| `media.play` | 當播放器從其他狀態(例如`buffering,` `paused` （當使用者繼續時）或`error` （當復原時）)轉換為`playing`狀態時（包括自動播放等情況），會傳送`media.play`事件型別。 此事件由播放器的`on('Playing')`回呼觸發。 |
| `media.sessionComplete` | 到達主要內容的結尾時，會傳送此事件。 |
| `media.sessionEnd` | `media.sessionEnd`事件型別會通知Media Analytics後端，在使用者放棄檢視且不太可能返回時立即關閉工作階段。 如果未傳送此事件，工作階段將在閒置10分鐘或播放點未移動30分鐘後逾時。 將會忽略任何使用該工作階段ID的後續媒體呼叫。 |
| `media.sessionStart` | `media.sessionStart`事件型別會隨工作階段起始呼叫傳送。 在收到回應時，將會從Location標題擷取工作階段ID，並使用於對收集伺服器的所有後續事件呼叫。 |
| `media.statesUpdate` | 此事件會追蹤`statesUpdate`事件何時發生。 播放器狀態追蹤功能可附加至音訊或視訊資料流。 標準狀態為： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`和`inFocus`。 |
| `opportunityEvent.addToOpportunity` | 此事件會追蹤何時將個人新增至商機。 |
| `opportunityEvent.opportunityUpdated` | 此事件會追蹤商機何時更新。 |
| `opportunityEvent.removeFromOpportunity` | 此事件會追蹤何時將個人從機會中移除。 |
| `personalization.request` | **已棄用**&#x200B;而改用`decisioning.propositionFetch`。 |
| `pushTracking.applicationOpened` | 此事件會追蹤使用者何時從推播通知開啟應用程式。 |
| `pushTracking.customAction` | 此事件會追蹤使用者何時在推播通知中選取自訂動作。 |
| `web.formFilledOut` | 此事件會追蹤某人何時在網頁上填寫表單。 |
| `web.webinteraction.linkClicks` | 事件代表Web SDK已自動記錄連結點選。 |
| `web.webpagedetails.pageViews` | 此事件型別是將點選標示為頁面檢視的標準方法。 |
| `location.entry` | 此事件會追蹤使用者或裝置進入特定位置。 |
| `location.exit` | 此事件會追蹤人員或裝置從特定位置離開。 |

{style="table-layout:auto"}

### `producedBy`的建議值 {#producedBy}

下表概述`producedBy`的一些接受值：

| 值 | 定義 |
| --- | --- |
| `self` | 自我 |
| `system` | 系統 |
| `salesRef` | 銷售代表 |
| `customerRep` | 客戶代表 |
