---
title: Advertising詳細資料結構欄位群組
description: 瞭解Advertising詳細資料結構欄位群組。
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 27%

---

# [!UICONTROL Advertising詳細資料]結構描述欄位群組

[!UICONTROL Advertising詳細資料]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組。 欄位群組提供單一`advertising`物件給結構描述，擷取與廣告曝光、點進和歸因相關的資訊。

![欄位群組結構](../../images/field-groups/advertising-details/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adAssetReference` | 物件 | 擷取有關廣告的資產資訊。 如需此物件結構的詳細資訊，請參閱[&#128279;](#adAssetReference)下方的子區段。 |
| `adAssetViewDetails` | 物件 | 擷取廣告播放的檢視細節。 如需此物件結構的詳細資訊，請參閱[&#128279;](#adAssetViewDetails)下方的子區段。 |
| `adViewability` | 物件 | 擷取一般使用者看到的曝光次數，例如播放器音量、資料庫版本、視窗狀態和廣告檢視區維度。 如需此物件結構的詳細資訊，請參閱[&#128279;](#adViewability)下方的子區段。 |
| `clicks` | [[!UICONTROL 量值]](../../data-types/measure.md) | 廣告上的點按動作次數。 |
| `completes` | [[!UICONTROL 量值]](../../data-types/measure.md) | 定時媒體資產觀看至結束的次數。 這並不一定表示使用者看完整段影片，他們有可能略過前面。 |
| `conversions` | [[!UICONTROL 量值]](../../data-types/measure.md) | 預先定義的動作（或動作）觸發效能評估事件的次數。 |
| `federated` | [[!UICONTROL 量值]](../../data-types/measure.md) | 表示是否透過資料同盟 (例如客戶間的資料共用) 建立體驗事件。 |
| `firstQuartiles` | [[!UICONTROL 量值]](../../data-types/measure.md) | 數位影片廣告以正常速度播放其長度的25%的次數。 |
| `impressions` | [[!UICONTROL 量值]](../../data-types/measure.md) | 傳送給一般使用者且可能被檢視的廣告曝光次數。 |
| `midpoints` | [[!UICONTROL 量值]](../../data-types/measure.md) | 數位影片廣告以正常速度播放其長度的50%的次數。 |
| `starts` | [[!UICONTROL 量值]](../../data-types/measure.md) | 數位影片廣告開始播放的次數。 |
| `thirdQuartiles` | [[!UICONTROL 量值]](../../data-types/measure.md) | 數位影片廣告以正常速度播放其長度的75%的次數。 |
| `timePlayed` | [[!UICONTROL 量值]](../../data-types/measure.md) | 一般使用者在特定的定時媒體資產上所花費的時間。 |
| `downloadedPlayback` | 布林值 | 設定為`true`時，表示點選是由於播放已下載的廣告工作階段所產生。 |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

`adAssetReference`物件會擷取廣告的資產資訊。

![adAssetReference結構](../../images/field-groups/advertising-details/adAssetReference.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc.title` | 字串 | 易記且易讀的廣告資產名稱。 |
| `_xmpDM.duration` | 整數 | 資產長度或持續時間（以秒為單位）。 |
| `_id` | 字串 | [廣告ID標準](https://datatracker.ietf.org/doc/html/rfc8107)之後的廣告資產的唯一識別碼。 |
| `advertiser` | 字串 | 廣告中精選產品的公司或品牌。 |
| `campaign` | 字串 | 廣告行銷活動的ID。 |
| `creativeID` | 字串 | 廣告創意的 ID。 |
| `creativeURL` | 字串 | 廣告創意的 URL。 |
| `placementID` | 字串 | 廣告版位ID。 |
| `siteID` | 字串 | 廣告網站ID。 |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

`adAssetViewDetails`物件會擷取廣告播放的檢視詳細資料。

![adAssetViewDetails結構](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 廣告插播]](../../data-types/ad-break.md) | 說明如何將計時廣告插入定時媒體。 |
| `index` | 整數 | 上層廣告插播內的廣告索引。 例如，第一個廣告索引為`0`，第二個廣告索引為`1`。 |
| `playerName` | 字串 | 負責轉譯廣告的播放器名稱。 |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

`adViewability`物件會擷取一般使用者看到的曝光次數，例如播放器音量、資料庫版本、視窗狀態和廣告檢視區維度。

![adViewability結構](../../images/field-groups/advertising-details/adViewability.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 實作詳細資料]](../../data-types/implementation-details.md) | 用於測量可檢視度指標的資料庫名稱和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 量值]](../../data-types/measure.md) | 表示由閱聽時間的可檢視度資料庫測量為不顯示廣告。 |
| `measuredMuted` | [[!UICONTROL 量值]](../../data-types/measure.md) | 表示廣告在閱聽時間由可檢視度資料庫測量為靜音。 |
| `unmeasurableIframe` | [[!UICONTROL 量值]](../../data-types/measure.md) | 表示廣告會顯示在非使用中視窗中，由閱聽時間的可檢視度資料庫測量。 |
| `unmeasurableOther` | [[!UICONTROL 量值]](../../data-types/measure.md) | 表示可檢視度資料庫無法正確執行測量，因為廣告會顯示在iframe內。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 量值]](../../data-types/measure.md) | 使用者透過所使用的可檢視度資料庫對廣告的閱聽。 |
| `viewabilityCompletes` | [[!UICONTROL 量值]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫完成時的廣告完成度。 |
| `viewableFirstQuartiles` | [[!UICONTROL 量值]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放至第一個四分位時的第一四分位廣告。 |
| `viewableImpressions` | [[!UICONTROL 量值]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放兩秒之後對廣告的閱聽。 |
| `viewableMidpoints` | [[!UICONTROL 量值]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放至中點時的廣告中點。 |
| `viewableThirdQuartiles` | [[!UICONTROL 量值]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放至第三個四分位時的第三四分位廣告。 |
| `activeWindow` | 布林值 | 指出廣告是否顯示在使用者裝置的作用中視窗。 |
| `adHeight` | 整數 | 播放器在運作時測量出的垂直像素數量。如果播放器有額外控制或縮圖，這個數量可能會大於廣告大小。 |
| `adUnitDepth` | 整數 | 發佈者可能會在容器(iFrame)中內嵌廣告單位，以限制廣告的存取權為僅限頁面代碼。 此值說明廣告單位顯示在多少個容器內。 |
| `adWidth` | 整數 | 播放器在運作時測量出的水平像素數量。如果播放器有額外控制或縮圖，這個數量可能會大於廣告大小。 |
| `measurementEligible` | 布林值 | 無論廣告是否符合可檢視度測量的條件。如果單位有受支援的創意格式和標籤類型，廣告即符合條件。 |
| `percentViewable` | 整數 | 測量時間中在視為可檢視的廣告中的畫素百分比。 |
| `playerVolume` | 整數 | 播放器音量百分比（在執行階段測量），其中`0`為靜音，`100`為最大音量。 |
| `viewable` | 布林值 | 表示是否可在執行階段檢視廣告。 當廣告的至少50%可見至少一秒時，顯示廣告會被視為可檢視。 當視訊播放至少連續兩秒期間，顯示至少50%的廣告時，視訊廣告會被視為可檢視。 |
| `viewportHeight` | 整數 | 執行階段所測量內部所顯示體驗的視窗垂直大小（畫素）。 若為網頁檢視事件，此值代表瀏覽器檢視區高度。 |
| `viewportWidth` | 整數 | 執行階段所測量內部所顯示體驗的視窗水準大小（畫素）。 若為網頁檢視事件，此值代表瀏覽器檢視區寬度。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json)。
