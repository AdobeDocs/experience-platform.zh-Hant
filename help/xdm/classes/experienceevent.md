---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM ExperienceEvent類別
topic: overview
description: 本檔案提供XDM ExperienceEvent類別的概觀。
translation-type: tm+mt
source-git-commit: 9e55e9ef6c619a952ca7519ca05dab59da2c573b
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---


# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是標準的XDM類，它允許您在發生特定事件或達到某組條件時建立系統的時間戳快照。

「體驗事件」是所發生事件的事實記錄，包括相關個人的時間點和身分。 事件可以是顯式（直接可觀察的人類行為）或隱式（在沒有直接人類行為的情況下提出），並且記錄時不進行匯總或解釋。 有關此類在平台生態系統中使用的詳細資訊，請參閱 [XDM概述](../home.md#data-behaviors)。

類 [!DNL XDM ExperienceEvent] 本身為方案提供了多個與時間序列相關的欄位。 在收錄資料時，會自動填入其中某些欄位的值：

<img src="../images/classes/experienceevent.png" width="650" /><br />

| 屬性 | 說明 |
| --- | --- |
| `_id` | 事件的唯一系統產生的字串識別碼。 此欄位用於追蹤個別事件的唯一性、防止資料重複，以及在下游服務中尋找該事件。 由於此欄位是系統生成的，因此在資料接收期間不應提供顯式值。<br><br>請務必指出，此欄位不 **代表與個人** ，而是資料本身的記錄。 與個人有關的身份資料應該被降級到 [身份欄位](../schema/composition.md#identity) 。 |
| `eventMergeId` | 導致記錄建立的收錄批的ID。 系統會在擷取資料時自動填入此欄位。 |
| `eventType` | 一個字串，它指示記錄的主要事件類型。 附錄部分提供接受的值及其 [定義](#eventType)。 |
| `identityMap` | 映射欄位，包含事件所應用的個人的一組命名空間標識。 系統會在擷取身分資料時自動更新此欄位。 為了適當利用此欄位進行 [即時客戶配置檔案](../../profile/home.md)，請勿嘗試手動更新資料操作中該欄位的內容。<br /><br />如需其使用案例的詳細資訊，請參 [閱架構構成基礎中的識別地圖](../schema/composition.md#identityMap) 。 |
| `timestamp` | 事件或觀察發生的時間，按照 [RFC 3339第5.6節的格式](https://tools.ietf.org/html/rfc3339#section-5.6))。 |

## 相容混音 {#mixins}

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請 [參閱混合名稱更新](../mixins/name-updates.md) 的檔案。

Adobe提供數種標準混音，以搭配該類 [!DNL XDM ExperienceEvent] 使用。 以下是類別中常用混合詞的清單：

* [[!UICONTROL 用戶ID詳細資訊]](../mixins/event/enduserids.md)
* [[!UICONTROL 環境詳細資訊]](../mixins/event/environment-details.md)

## 附錄

下節包含有關 [!UICONTROL XDM ExperienceEvent類別的其他資訊] 。

### xdm:eventType的接受值 {#eventType}

下表概述的接受值 `xdm:eventType`及其定義：

| 值 | 定義 |
| --- | --- |
| `advertising.completes` | 已觀看逾時媒體資產完成。 這不一定表示檢視者已觀看整個視訊，因為檢視者可能已跳過。 |
| `advertising.timePlayed` | 說明使用者在特定定時媒體資產上逗留的時間。 |
| `advertising.federated` | 指出是否透過資料聯盟建立體驗事件（客戶之間的資料共用）。 |
| `advertising.clicks` | 按一下廣告上的動作。 |
| `advertising.conversions` | 由客戶執行的預先定義動作，觸發事件進行效能評估。 |
| `advertising.firstQuartiles` | 數位視訊廣告以正常速度播放了25%的時間。 |
| `advertising.impressions` | 對有可能被檢視之客戶的廣告印象。 |
| `advertising.midpoints` | 數位視訊廣告以正常速度播放了50%的時間。 |
| `advertising.starts` | 數位視訊廣告已開始播放。 |
| `advertising.thirdQuartiles` | 數位視訊廣告以正常速度播放了75%的時間。 |
| `web.webpagedetails.pageViews` | 網頁已收到一或多個檢視。 |
| `web.webinteraction.linkClicks` | 連結已收到一或多次點按。 |
| `commerce.checkouts` | 產品清單已發生結帳事件。 如果結帳程式中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用每個事件的時間戳記和參考頁面／體驗來識別依順序呈現的每個個別事件（步驟）。 |
| `commerce.productListAdds` | 產品已新增至產品清單或購物車。 |
| `commerce.productListOpens` | 已初始化或建立新的產品清單（購物車）。 |
| `commerce.productListRemovals` | 一個或多個產品項目已從產品清單或購物車中移除。 |
| `commerce.productListReopens` | 客戶已重新啟動不再存取（放棄）的產品清單（購物車），例如透過再行銷活動。 |
| `commerce.productListViews` | 產品清單或購物車已收到一或多個檢視。 |
| `commerce.productViews` | 產品已收到一或多個檢視。 |
| `commerce.purchases` | 已接受命令。 這是商務轉換中唯一必要的動作。 購買事件必須有參考的產品清單。 |
| `commerce.saveForLaters` | 產品清單已儲存以供日後使用，例如產品願望清單。 |
| `delivery.feedback` | 傳送的意見回應事件，例如電子郵件傳送。 |
| `message.feedback` | 傳送給客戶之訊息的回饋事件，例如傳送／彈回／錯誤。 |
| `message.tracking` | 追蹤傳送給客戶之訊息的開啟／點按／自訂動作等事件。 |