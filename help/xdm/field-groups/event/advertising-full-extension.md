---
title: Adobe Advertising Cloud ExperienceEvent完整擴充功能結構欄位群組
description: 瞭解Adobe Advertising Cloud ExperienceEvent完整擴充功能結構描述欄位群組。
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---

# [!UICONTROL Adobe Advertising Cloud ExperienceEvent完整擴充功能]結構描述欄位群組

>[!AVAILABILITY]
>
>[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]欄位群組目前是測試版。 文件和功能可能會有所變更。

[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組，可擷取Adobe Advertising （以前稱為「[!DNL Advertising Cloud]」）收集的通用量度。

本檔案說明[!DNL Advertising Cloud]擴充功能欄位群組的結構和使用案例。

>[!NOTE]
>
>您也可以在Experience Platform UI[中查詢此欄位群組](../../ui/explore.md)，或在[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)中檢視完整的結構描述。

## 欄位群組結構

欄位群組提供單一`_experience`物件給結構描述，其本身包含單一`adcloud`物件。

![&#x200B; [!DNL Advertising Cloud]欄位群組的頂層欄位](../../images/field-groups/advertising-full-extension/full-schema.png " [!DNL Advertising Cloud] 欄位群組的頂層欄位")

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adDeliveryDetails` | 物件 | 廣告傳遞細節。 如需此物件內容的詳細資訊，請參閱[物件`adDeliveryDetails`的下方](#adDeliveryDetails)子區段。 |
| `advertisement` | 物件 | 數位廣告細節。 如需此物件內容的詳細資訊，請參閱廣告物件[的下方](#advertisement)子區段。 |
| `campaign` | 物件 | 行銷活動階層詳細資料。 如需此物件內容的詳細資訊，請參閱促銷活動物件[的下方](#campaign-campaign)子區段。 |
| `conversionDetails` | 物件 | 廣告的轉換詳細資料。 如需此物件內容的詳細資訊，請參閱[下方的](#conversionDetails)子區段。 |
| `eventType` | 字串 | Adobe Advertising事件型別。 |
| `fees` | 物件 | Advertising費用詳細資料。 如需此物件內容的詳細資訊，請參閱費用物件[的下方](#fees)小節。 |
| `inventory` | 物件 | 詳細目錄資訊。 如需此物件內容的詳細資訊，請參閱[下方的](#inventory)子區段。 |
| `productDetails` | 物件 | 產品廣告詳細資料。 如需此物件內容的詳細資訊，請參閱productDetails物件[的下方](#productDetails)子區段。 |
| `stitchId` | 字串 | 來自Adobe Advertising廣告伺服器的ID，用於追蹤在封鎖第三方Cookie的瀏覽器上的點進轉換。 |

## `adDeliveryDetails` {#adDeliveryDetails}

adDeliveryDetails物件提供有關廣告傳送的位置和方式的資訊，包括刊登網站和位置識別碼。

![結構描述圖表顯示`adDeliveryDetails`物件及其欄位。](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `placementWebsite` | 字串 | 顯示廣告的網站。 |
| `siteLinkText` | 字串 | 在廣告中選取的實際網站連結。 |
| `interestLocationID` | 字串 | 從搜尋查詢推斷的位置。 例如，「Goa飯店」的查詢會傳回Goa的ID，無論使用者的實際瀏覽位置為何。 |
| `physicalLocationID` | 字串 | 使用者的瀏覽位置，由廣告網路的參考ID表示。 此ID不是可讀取的位置名稱（例如城市或國家/地區），而是廣告網路指派以識別地理目標的代碼。 |

## `advertisement` {#advertisement}

廣告物件說明數位廣告的詳細資訊，例如其識別碼、型別、創意、目標定位和相關關鍵字。

![結構描述圖表顯示`advertisement`物件及其欄位。](../../images/field-groups/advertising-full-extension/advertisement.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adId` | 字串 | 與此事件相關之廣告的識別碼。 此ID與Ad-ID產業標準無關。 |
| `runtime` | 字串 | 廣告單元的執行階段，與瀏覽器或作業系統的執行階段不同。 可能的值包括： `unknown`和`HTML5`。 |
| `adClass` | 字串 | 駕駛事件的廣告類別： `display`、`video`或`social`。 |
| `adUnitType` | 字串 | 在瀏覽器或裝置中轉譯廣告的程式碼識別碼。 可能的值包括：<ul><li>`linearVideo`：線性視訊</li><li>`interactiveVideo`：互動視訊</li><li>`banner`：橫幅，</li><li>`richMediaBanner`：多媒體橫幅，</li><li>`newsFeedVideo`：新聞摘要影片，</li><li>`newsFeedDisplay`：新聞摘要顯示，</li><li>`HTML5`： HTML5，</li><li>`inPageVideo`：在頁面影片中，</li><li>`inPageDisplay`：在頁面顯示中，</li><li>`facebook`： Facebook，</li><li>`twitter`： Twitter，</li><li>`linearTv`：線性電視，</li><li>`vod`：隨選影片</li></ul> |
| `promotedAssetId` | 字串 | 與此事件相關之廣告中促銷的資產識別碼。 |
| `creativeID` | 字串 | 與此事件相關聯的廣告創意（例如橫幅、影片或社交廣告）識別碼。 |
| `keywordID` | 字串 | 使用者在觸發此事件的搜尋查詢中輸入的關鍵字識別碼。 |
| `keyword` | 字串 | 客戶競標的清單關鍵字。 |
| `isDynamicSearchAd` | 布林值 | 指出事件是否來自動態搜尋廣告。 |
| `audienceID` | 字串 | 廣告鎖定目標的對象區段的識別碼。 |
| `adGroupID` | 字串 | 與觸發此事件之廣告相關聯的廣告群組的識別碼。 |
| `campaignID` | 字串 | 與觸發此事件的廣告相關之行銷活動的識別碼。 |
| `networkType` | 字串 | 發生事件的網路型別。 可能的值包括： <ul><li>`search`：廣告已顯示在搜尋網路上。</li><li>`content`：廣告已顯示在內容網路上。</li></ul> |
| `matchType` | 字串 | 關鍵字元合型別。 可能的值包括： <ul><li>`exact`：關鍵字的完全相符</li><li>`broad`：廣泛符合關鍵字</li><li>`phrase`：關鍵字的字詞相符</li></ul> |

## `campaign` {#campaign}

行銷活動物件會定義廣告行銷活動階層，包括帳戶、廣告商、位置和套件識別碼以及貨幣詳細資訊。

![結構描述圖表顯示`campaign`物件及其欄位。](../../images/field-groups/advertising-full-extension/campaign.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountId` | 字串 | 適用於帳戶的識別碼。 |
| `dspId` | 字串 | 定義促銷活動之Demand Side Platform (DSP)的識別碼。 此識別碼通常是Adobe Advertising Cloud DSP的ID。 |
| `campaignId` | 字串 | 適用於行銷活動的識別碼。 |
| `placementId` | 字串 | 位置的識別碼。 |
| `packageId` | 字串 | Advertising DSP套件的識別碼。 |
| `advertiserId` | 字串 | 廣告商的識別碼。 |
| `experimentId` | 字串 | 實驗的識別碼。 |
| `sampleGroupId` | 字串 | 範例群組的識別碼。 |
| `currency` | 字串 | 帳戶的ISO 4217計費貨幣代碼。 使用規則運算式模式^[A-Z]{3}$ （三個大寫字母）。 例如：USD、EUR。 |

## `conversionDetails` {#conversionDetails}

conversionDetails物件會擷取廣告轉換的追蹤資訊，包括追蹤程式碼、身分和轉換屬性。

顯示![物件及其欄位的結構描述圖表。`conversionDetails`](../../images/field-groups/advertising-full-extension/conversionDetails.png "conversionDetails欄位")

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `trackingCode` | 字串 | 事件的轉換追蹤程式碼。 如需可能的格式清單，請參閱[AMO ID格式](https://experienceleague.adobe.com/zh-hant/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats)。 |
| `trackingIdentities` | 字串 | 事件的EF ID，或追蹤身分詳細資訊。 如需可能格式的清單，請參閱[EF ID格式](https://experienceleague.adobe.com/zh-hant/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats)。 |
| `conversionProperties` | 物件 | 轉換屬性的對應，以索引鍵值配對字串的陣列表示（例如`subscriptions=253`）。 |

## `fees` {#fees}

費用物件會擷取媒體、資料和其他廣告成本，並依Advertising DSP、帳戶和廣告商細分。

![結構描述圖表顯示`fees`物件及其欄位。](../../images/field-groups/advertising-full-extension/fees.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `DSPMediaFees` | 數字 | Advertising DSP可記帳的媒體費用。 |
| `DSPDataFees` | 數字 | Advertising DSP可記帳的資料費用。 |
| `DSPOtherFees` | 數字 | Advertising DSP可記帳的其他費用。 |
| `accountMediaFees` | 數字 | 此帳戶的媒體費用，但Advertising DSP不提供帳單。 |
| `accountDataFees` | 數字 | 帳戶的資料費用，但Advertising DSP不提供計費功能。 |
| `accountOtherFees` | 數字 | 帳戶的其他費用，但Advertising DSP不提供帳單功能。 |
| `advertiserMediaFees` | 數字 | 從該帳戶向廣告商收取的媒體廣告商費用。 |
| `advertiserDataFees` | 數字 | 從該帳戶向廣告商收取的其他廣告商費用。 |
| `advertiserOtherFees` | 數字 | 從該帳戶向廣告商收取的其他廣告商費用。 |
| `billableMediaNetSpend` | 數字 | 媒體廣告的可計費淨支出。 |
| `totalMediaNetSpend` | 數字 | 媒體廣告的總淨支出。 |
| `billableDataNetSpend` | 數字 | 資料廣告的可計費淨支出。 |
| `billableOtherNetSpend` | 數字 | 其他廣告型別的可計費淨支出。 |
| `totalBillableNetSpend` | 數字 | 可記帳淨支出總計。 |
| `totalNonBillableNetSpend` | 數字 | 不可開立帳單的淨支出總計。 |
| `totalNetSpend` | 數字 | 總淨支出。 |

## `inventory` {#inventory}

詳細目錄物件會記錄有關廣告詳細目錄商機的詳細資訊，包括工作階段資料、合作夥伴代碼、網站ID、成本貨幣和分段規則。

![結構描述圖表顯示`inventory`物件及其欄位。](../../images/field-groups/advertising-full-extension/inventory.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sessionId` | 字串 | 與體驗事件相關聯的工作階段ID，用於連結相同工作階段中發生的獨立事件。 |
| `feedID` | 字串 | 發佈者、廣告交換和其他功能的複合ID。 |
| `sspPartnerCode` | 字串 | Adobe Advertising Cloud獲得詳細目錄機會的合作夥伴（交換）。 |
| `siteID` | 字串 | 提供廣告印象的網站的識別碼。 |
| `costCurrency` | 字串 | 用於為廣告機會向合作夥伴付款的ISO 4217貨幣代碼。 值必須遵循規則運算式模式^[A-Z]{3}$ （三個大寫字母）。 例如：USD、EUR。 |
| `inventorySourceId` | 字串 | 傳遞此機會的Adobe Advertising Cloud詳細目錄來源ID。 |
| `segment` | 物件 | 與使用者細分規則相關的詳細資訊。 其屬性包括：<ul><li>`attributablePartnerId` （字串）：擁有attributeSegmentId的區段提供者的識別碼。</li><li>`attributableSegmentId` （字串）：在位置的目標規則中，為使用者鎖定目標而計入的區段。 這是為了追蹤成本和支付合作夥伴。</li><li>`segments` （字串）：使用者所屬的使用者區段a\)與b\)的交集，該廣告已鎖定目標。 這不是拍賣時使用者所屬區段的完整清單。</li></ul> |
| `optimizationTag` | 字串 | 和最佳化相關的標籤。 |
| `attributableDeviceGraphId` | 字串 | 歸因於轉換事件的裝置圖表識別碼。 |

## `productDetails` {#productDetails}

`productDetails`物件包含[!DNL Adobe Advertising Search, Social, & Commerce]購物廣告中精選產品的相關資訊，包括產品識別碼、國家/地區、語言、分割、標題及廣告型別。

![結構描述圖表顯示`productDetails`物件及其欄位。](../../images/field-groups/advertising-full-extension/productDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `productID` | 字串 | 與此事件相關之廣告中所精選產品的識別碼。 |
| `country` | 字串 | 與事件相關之廣告中所精選產品的銷售國家/地區。 |
| `language` | 字串 | 您產品資訊的語言，如使用者端的商家中心資料摘要所示。 |
| `partitionID` | 字串 | 在此事件中與廣告相關聯的產品群組識別碼。 |
| `title` | 字串 | 廣告中顯示的產品標題。 |
| `adType` | 字串 | [!DNL Google]購物行銷活動中使用的產品的廣告型別。 可能的值包括：<ul><li>`pla_with_pog`：當事件來自透過購物廣告進行的購買時</li><li>`pla`：當事件來自購物廣告時。</li><li>`pla_multichannel`：當購物廣告的事件包含「線上」和「本機」購物管道的選項時。</li><li>`pla_with_promotion`：來自購物廣告的事件顯示商家促銷活動時。</li></ul> |

## 後續步驟

本檔案涵蓋[!DNL Advertising Cloud]擴充功能欄位群組的結構和使用案例。 如需欄位群組本身的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json)。

如果您使用此欄位群組來使用Adobe Experience Platform Web SDK收集[!DNL Advertising]資料，請參閱[設定資料流](../../../datastreams/overview.md)的指南，以瞭解如何將資料對應到伺服器端的XDM。
