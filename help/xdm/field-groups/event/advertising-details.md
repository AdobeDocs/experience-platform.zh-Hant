---
title: 廣告詳細資料結構欄位群組
description: 本檔案提供廣告詳細資料結構欄位群組的概觀。
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 8%

---

# [!UICONTROL 廣告詳細資訊] 方案欄位組

[!UICONTROL 廣告詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md). 欄位群組提供單一 `advertising` 物件至結構，可擷取與廣告曝光數、點進和歸因相關的資訊。

![欄位群組結構](../../images/field-groups/advertising-details/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adAssetReference` | 物件 | 擷取廣告的資產資訊。 請參閱 [下文](#adAssetReference) 以取得此物件結構的詳細資訊。 |
| `adAssetViewDetails` | 物件 | 擷取廣告播放的檢視詳細資料。 請參閱 [下文](#adAssetViewDetails) 以取得此物件結構的詳細資訊。 |
| `adViewability` | 物件 | 擷取一般使用者所檢視的曝光次數，例如播放器量、程式庫版本、視窗狀態和廣告檢視區維度。 請參閱 [下文](#adViewability) 以取得此物件結構的詳細資訊。 |
| `clicks` | [[!UICONTROL 測量]](../../data-types/measure.md) | 廣告上的點按動作數。 |
| `completes` | [[!UICONTROL 測量]](../../data-types/measure.md) | 觀看計時媒體資產至完成的次數。 這並不代表使用者已提前略過整個視訊。 |
| `conversions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 預先定義的動作（或動作）觸發事件以進行效能評估的次數。 |
| `federated` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出體驗事件是否是透過資料同盟建立，例如客戶之間的資料共用。 |
| `firstQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位視訊廣告以正常速度播放了25%持續時間的次數。 |
| `impressions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 傳送給可能被檢視的使用者的廣告曝光次數。 |
| `midpoints` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位視訊廣告以正常速度播放超過其持續時間50%的次數。 |
| `starts` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位視訊廣告開始播放的次數。 |
| `thirdQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位視訊廣告以正常速度播放了75%持續時間的次數。 |
| `timePlayed` | [[!UICONTROL 測量]](../../data-types/measure.md) | 使用者在特定計時媒體資產上逗留的時間。 |
| `downloadedPlayback` | 布林值 | 設為時 `true`，表示點擊是因播放下載的廣告工作階段而產生。 |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

此 `adAssetReference` 物件會擷取廣告的資產資訊。

![adAssetReference結構](../../images/field-groups/advertising-details/adAssetReference.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc.title` | 字串 | 易記且人類看得懂的廣告資產名稱。 |
| `_xmpDM.duration` | 整數 | 資產的長度或持續時間（以秒為單位）。 |
| `_id` | 字串 | 廣告資產的唯一識別碼，緊接在 [廣告ID標準](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | 字串 | 廣告中精選產品的公司或品牌. |
| `campaign` | 字串 | 廣告促銷活動 ID. |
| `creativeID` | 字串 | 廣告創意 ID. |
| `creativeURL` | 字串 | 廣告創意的 URL. |
| `placementID` | 字串 | 廣告版位 ID. |
| `siteID` | 字串 | 廣告網站 ID. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

此 `adAssetViewDetails` 物件會擷取廣告播放的檢視詳細資料。

![adAssetViewDetails結構](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 廣告插播]](../../data-types/ad-break.md) | 說明如何將計時廣告插入計時媒體。 |
| `index` | 整數 | 上層廣告插播內的廣告索引。 例如，第一個廣告有索引 `0` 第二個廣告有索引 `1`. |
| `playerName` | 字串 | 負責轉譯廣告之播放器的名稱. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

此 `adViewability` 物件會擷取一般使用者所檢視的曝光次數，例如播放器量、程式庫版本、視窗狀態和廣告檢視區維度。

![adViewability結構](../../images/field-groups/advertising-details/adViewability.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 實作詳細資料]](../../data-types/implementation-details.md) | 測量可檢視度量所檢測的程式庫名稱和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出廣告在曝光時無法顯示，如可檢視性資料庫所測量。 |
| `measuredMuted` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出廣告在曝光時的靜音，由可檢視性資料庫測量。 |
| `unmeasurableIframe` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出廣告顯示在非作用中視窗中，如曝光時可檢視性資料庫所測量。 |
| `unmeasurableOther` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出可檢視性程式庫無法正確執行測量，因為廣告顯示在iframe內。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 廣告對使用所創作的可視性程式庫的最終用戶的曝光次數。 |
| `viewabilityCompletes` | [[!UICONTROL 測量]](../../data-types/measure.md) | 完成廣告給最終用戶，在完成時被可視性庫視為可視。 |
| `viewableFirstQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 廣告的第一四分位數給在可視性庫觀看的播放的第一四分位數中被認為可以觀看的最終用戶。 |
| `viewableImpressions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 在可檢視性程式庫播放兩秒後，即視為可檢視的一般使用者之廣告曝光次數。 |
| `viewableMidpoints` | [[!UICONTROL 測量]](../../data-types/measure.md) | 在可視性庫在播放的中點處被認為可以觀看的終端用戶的廣告的中點。 |
| `viewableThirdQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 廣告的第三個四分位數給被認為可以觀看的資料庫觀看的第三個四分位數播放的最終用戶。 |
| `activeWindow` | 布林值 | 指出廣告是否顯示在使用者裝置的作用中視窗上。 |
| `adHeight` | 整數 | 播放器的垂直像素數，在執行階段測量。 如果播放器有額外的控制項或縮圖，則可能大於廣告的大小。 |
| `adUnitDepth` | 整數 | 發佈商可在容器(iFrame)內嵌廣告單位，以限制廣告只能存取頁面的程式碼。 此值說明廣告單位在內顯示的容器數。 |
| `adWidth` | 整數 | 播放器的水準像素數，在執行階段測量。 如果播放器有額外的控制項或縮圖，則可能大於廣告的大小。 |
| `measurementEligible` | 布林值 | 廣告是否符合可檢視度測量的資格。 如果單位具有支援的創作格式和標籤類型，則符合廣告資格。 |
| `percentViewable` | 整數 | 在測量時可檢視的廣告中的像素百分比。 |
| `playerVolume` | 整數 | 播放器音量百分比，在執行階段測量，其中 `0` 靜音， `100` 是最大卷。 |
| `viewable` | 布林值 | 指出是否可在執行階段檢視廣告。 當至少50%的廣告可見至少一秒時，即視為可檢視顯示廣告。 視訊播放至少連續兩秒時，當至少50%的廣告可見時，視為可檢視視訊廣告。 |
| `viewportHeight` | 整數 | 執行階段時，在內部顯示體驗的視窗垂直大小（以像素為單位）。 對於Web檢視事件，此值表示瀏覽器檢視區高度。 |
| `viewportWidth` | 整數 | 執行階段時在內顯示體驗的視窗水準大小（以像素為單位）。 對於Web檢視事件，此值表示瀏覽器檢視區寬度。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
