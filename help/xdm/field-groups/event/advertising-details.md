---
title: 廣告詳細資訊架構欄位組
description: 此文檔提供「廣告詳細資訊」架構欄位組的概述。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 9%

---

# [!UICONTROL 廣告詳細資訊] 架構欄位組

[!UICONTROL 廣告詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `advertising` 對象到架構，該架構捕獲與廣告印象、點擊和屬性相關的資訊。

![欄位組結構](../../images/field-groups/advertising-details/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adAssetReference` | 物件 | 捕獲有關廣告的資產資訊。 查看 [下文](#adAssetReference) 的子菜單。 |
| `adAssetViewDetails` | 物件 | 捕獲廣告播放的視圖詳細資訊。 查看 [下文](#adAssetViewDetails) 的子菜單。 |
| `adViewability` | 物件 | 捕獲最終用戶所看到的印象數，如播放器卷、庫版本、窗口狀態和廣告視區尺寸。 查看 [下文](#adViewability) 的子菜單。 |
| `clicks` | [[!UICONTROL 度量]](../../data-types/measure.md) | 播發上的按一下操作數。 |
| `completes` | [[!UICONTROL 度量]](../../data-types/measure.md) | 已定時媒體資產被監視完成的次數。 這並不一定意味著最終用戶在觀看整個視頻時會跳過。 |
| `conversions` | [[!UICONTROL 度量]](../../data-types/measure.md) | 預定義操作（或操作）觸發用於效能評估的事件的次數。 |
| `federated` | [[!UICONTROL 度量]](../../data-types/measure.md) | 指示是否通過資料聯合建立體驗事件，如客戶之間的資料共用。 |
| `firstQuartiles` | [[!UICONTROL 度量]](../../data-types/measure.md) | 數字視頻廣告以正常速度播放其25%持續時間的次數。 |
| `impressions` | [[!UICONTROL 度量]](../../data-types/measure.md) | 發送給具有被查看可能性的最終用戶的廣告印象數。 |
| `midpoints` | [[!UICONTROL 度量]](../../data-types/measure.md) | 數字視頻廣告以正常速度播放其持續時間50%的次數。 |
| `starts` | [[!UICONTROL 度量]](../../data-types/measure.md) | 數字視頻廣告開始播放的次數。 |
| `thirdQuartiles` | [[!UICONTROL 度量]](../../data-types/measure.md) | 數字視頻廣告以正常速度播放其持續時間75%的次數。 |
| `timePlayed` | [[!UICONTROL 度量]](../../data-types/measure.md) | 最終用戶在特定定時介質資產上花費的時間。 |
| `downloadedPlayback` | 布林值 | 設定為時 `true`，表示由於播放下載的廣告會話而生成命中。 |

{style=&quot;table-layout:auto&quot;}

## `adAssetReference` {#adAssetReference}

的 `adAssetReference` object捕獲有關廣告的資產資訊。

![adAssetReference結構](../../images/field-groups/advertising-details/adAssetReference.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc.title` | 字串 | 廣告資產的友好、可讀的名稱。 |
| `_xmpDM.duration` | 整數 | 資產的長度或持續時間（以秒為單位）。 |
| `_id` | 字串 | 廣告資產的唯一標識符，與 [廣告ID標準](https://datatracker.ietf.org/doc/html/rfc8107)。 |
| `advertiser` | 字串 | 廣告中精選產品的公司或品牌. |
| `campaign` | 字串 | 廣告促銷活動 ID. |
| `creativeID` | 字串 | 廣告創意 ID. |
| `creativeURL` | 字串 | 廣告創意的 URL. |
| `placementID` | 字串 | 廣告版位 ID. |
| `siteID` | 字串 | 廣告網站 ID. |

{style=&quot;table-layout:auto&quot;&quot;

## `adAssetViewDetails` {#adAssetViewDetails}

的 `adAssetViewDetails` 對象捕獲廣告播放的視圖詳細資訊。

![adAssetViewDetails結構](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 廣告分段]](../../data-types/ad-break.md) | 描述如何將定時廣告插入到定時媒體中。 |
| `index` | 整數 | 父廣告分段內廣告的索引。 例如，第一個廣告具有索引 `0` 第二個廣告有索引 `1`。 |
| `playerName` | 字串 | 負責轉譯廣告之播放器的名稱. |

{style=&quot;table-layout:auto&quot;&quot;

## `adViewability` {#adViewability}

的 `adViewability` object可捕獲最終用戶看到的印象數，如播放器卷、庫版本、窗口狀態和廣告視區尺寸。

![可視性結構](../../images/field-groups/advertising-details/adViewability.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 實作詳細資料]](../../data-types/implementation-details.md) | 用於度量可查看性度量的庫的名稱和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 度量]](../../data-types/measure.md) | 指示廣告在印象時間由可查看性庫測量時不可見。 |
| `measuredMuted` | [[!UICONTROL 度量]](../../data-types/measure.md) | 指示廣告在印象時間由可查看性庫測量而靜音。 |
| `unmeasurableIframe` | [[!UICONTROL 度量]](../../data-types/measure.md) | 指示廣告顯示在非活動窗口中，該窗口由印象時間的可視性庫測量。 |
| `unmeasurableOther` | [[!UICONTROL 度量]](../../data-types/measure.md) | 指示可查看性庫無法正確執行測量，因為在iframe內顯示廣告。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 度量]](../../data-types/measure.md) | 利用可查看性庫對最終用戶進行指示的廣告印象。 |
| `viewabilityCompletes` | [[!UICONTROL 度量]](../../data-types/measure.md) | 在完成時被可視性庫視為可視的最終用戶完成廣告。 |
| `viewableFirstQuartiles` | [[!UICONTROL 度量]](../../data-types/measure.md) | 在可視性庫播放的第一四分位中，將廣告的第一四分位發送給被認為可觀看的終端用戶。 |
| `viewableImpressions` | [[!UICONTROL 度量]](../../data-types/measure.md) | 在可觀看性庫播放兩秒後，向被認為可觀看的最終用戶展示廣告的印象。 |
| `viewableMidpoints` | [[!UICONTROL 度量]](../../data-types/measure.md) | 在可觀看性庫播放的中點處被認為可觀看的廣告給最終用戶的中點。 |
| `viewableThirdQuartiles` | [[!UICONTROL 度量]](../../data-types/measure.md) | 廣告的第三四分位給被可視性庫認為在播放的第三四分位上可視的最終用戶。 |
| `activeWindow` | 布林值 | 指示廣告是否顯示在用戶設備的活動窗口中。 |
| `adHeight` | 整數 | 在運行時測量的播放器的垂直像素數。 如果播放器具有額外的控制項或縮略圖，則此大小可能大於廣告的大小。 |
| `adUnitDepth` | 整數 | 發佈者可以在容器(iFrames)內嵌入廣告單元，以限制廣告僅訪問頁面代碼。 此值描述廣告單元在中顯示的容器數。 |
| `adWidth` | 整數 | 在運行時測量的播放器的水準像素數。 如果播放器具有額外的控制項或縮略圖，則此大小可能大於廣告的大小。 |
| `measurementEligible` | 布林值 | 廣告是否符合可查看性度量條件。 如果單元具有支援的創作格式和標籤類型，則廣告符合條件。 |
| `percentViewable` | 整數 | 廣告中在測量時被視為可查看的像素百分比。 |
| `playerVolume` | 整數 | 運行時測量的播放器音量百分比，其中 `0` 靜音， `100` 是最大卷。 |
| `viewable` | 布林值 | 指示在運行時是否可查看廣告。 當至少50%的廣告在至少一秒內可見時，顯示廣告被視為可視。 當視頻連續播放至少兩秒時，至少50%的廣告可見時，視頻廣告被視為可視。 |
| `viewportHeight` | 整數 | 運行時在內部測量的顯示體驗的窗口的垂直大小（像素）。 對於Web視圖事件，此值指示瀏覽器視區高度。 |
| `viewportWidth` | 整數 | 運行時在內部測量的顯示體驗的窗口水準大小（以像素為單位）。 對於Web視圖事件，此值表示瀏覽器視圖寬度。 |

{style=&quot;table-layout:auto&quot;&quot;

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json)。
