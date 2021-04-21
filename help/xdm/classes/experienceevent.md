---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；模式；標識圖；標識圖；標識圖；模式設計；映射；聯合模式；聯合模式
solution: Experience Platform
title: XDM ExperienceEvent類別
topic-legacy: overview
description: 本檔案提供XDM ExperienceEvent類別的概觀。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是標準的XDM類，它允許您在發生特定事件或達到某組條件時建立系統的時間戳快照。

「體驗事件」是所發生事件的事實記錄，包括相關個人的時間點和身分。 事件可以是顯式（直接可觀察的人類行為）或隱式（在沒有直接人類行為的情況下提出），並且記錄時不進行匯總或解釋。 有關在平台生態系統中使用此類的更高級別資訊，請參閱[XDM概述](../home.md#data-behaviors)。

[!DNL XDM ExperienceEvent]類本身為方案提供了多個與時間序列相關的欄位。 在收錄資料時，會自動填入其中某些欄位的值：

<img src="../images/classes/experienceevent.png" width="650" /><br />

| 屬性 | 說明 |
| --- | --- |
| `_id` | 事件的唯一系統產生的字串識別碼。 此欄位用於追蹤個別事件的唯一性、防止資料重複，以及在下游服務中尋找該事件。 由於此欄位是系統生成的，因此在資料接收期間不應提供顯式值。<br><br>請務必指出，此欄位不 **會** 呈現與個人相關的身分，而是資料本身的記錄。與人有關的身份資料應改為[身份欄位](../schema/composition.md#identity)。 |
| `eventMergeId` | 導致記錄建立的收錄批的ID。 系統會在擷取資料時自動填入此欄位。 |
| `eventType` | 一個字串，它指示記錄的主要事件類型。 [附錄部分](#eventType)提供了接受的值及其定義。 |
| `identityMap` | 映射欄位，包含事件所應用的個人的一組命名空間標識。 系統會在擷取身分資料時自動更新此欄位。 為了將此欄位正確用於[即時客戶概要檔案](../../profile/home.md)，請勿嘗試手動更新資料操作中的欄位內容。<br /><br />如需其使用案例的詳細資訊，請參 [閱架構構](../schema/composition.md#identityMap) 成基礎中有關身分映射的章節。 |
| `timestamp` | 事件或觀察的發生時間，按照[RFC 3339第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)節的格式設定。 |

## 相容混音{#mixins}

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../mixins/name-updates.md)上的檔案。

Adobe提供數種標準混音，以便與[!DNL XDM ExperienceEvent]類一起使用。 以下是類別中常用混合詞的清單：

* [[!UICONTROL End User ID Details]](../mixins/event/enduserids.md)
* [[!UICONTROL Environment Details]](../mixins/event/environment-details.md)

## 附錄

以下部分包含有關[!UICONTROL XDM ExperienceEvent]類別的其他資訊。

### xdm:eventType {#eventType}的接受值

下表概述`xdm:eventType`的接受值及其定義：

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
| `web.webinteraction.linkClicks` | 連結已選取一或多次。 |
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
