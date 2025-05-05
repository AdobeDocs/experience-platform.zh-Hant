---
title: QoE （體驗品質）資料詳細資料報告資料型別
description: 瞭解QoE （體驗品質）資料詳細資料報告資料型別體驗資料模型(XDM)資料型別。
exl-id: 608baa9b-12ca-466c-a962-1401abc0344e
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# QoE （體驗品質）資料詳細資料報表資料型別

[!UICONTROL QoE資料詳細資料]報告是標準的體驗資料模型(XDM)資料型別，在媒體播放期間提供與體驗品質(QoE)相關的詳細量度。 使用[!UICONTROL QoE資料詳細資料]報表資料型別來擷取詳細資料，例如位元速率資訊、影格速率、緩衝事件、掉格等。 Adobe服務會使用媒體報表欄位來分析使用者傳送的「媒體收集」欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。 此資料型別可啟用播放品質分析，深入分析串流效能、使用者體驗和播放工作階段期間遇到的潛在問題。

+++選取此項可顯示「QoE資料詳細資料報表」資料型別。
![QoE （體驗品質）資料詳細資料報告資料型別的圖表。](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含由Adobe、實作值、網路引數、報表和重要考量收集之視訊廣告資料的詳細資訊。

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL 平均位元速率]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#average-bitrate-1) | `bitrateAverage` | 數字 | 平均位元速率（以每秒位元組數為單位，須為整數）。 計算為位元速率值的加權平均。 |
| [[!UICONTROL 平均位元貯體]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#average-bitrate) | `bitrateAverageBucket` | 字串 | 以100kbps間隔分類在預先定義值區內的平均位元速率（以kbps為單位）。 |
| [[!UICONTROL 位元速率]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#average-bitrate) | `bitrate` | 整數 | 位元速率值（以每秒位元組數為單位）。 |
| [[!UICONTROL 位元速率變更影響的資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | 布林值 | 表示資料流在播放期間是否受到位元速率變更的影響。 |
| [[!UICONTROL 位元速率變更]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#bitrate-changes) | `bitrateChangeCount` | 整數 | 錄放期間位元速率變更的總計數。 |
| [[!UICONTROL 緩衝事件]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#buffer-events) | `bufferCount` | 整數 | 錄放期間不同緩衝狀態的計數。 |
| [[!UICONTROL 緩衝影響的資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#buffer-impacted-streams) | `hasBufferImpactedStreams` | 布林值 | 指出資料流在播放期間是否受到緩衝影響。 |
| [[!UICONTROL 掉格影響的資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | 布林值 | 表示串流在播放期間是否受到掉格的影響。 |
| [[!UICONTROL 掉格]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#dropped-frames-1) | `droppedFrames` | 整數 | 播放期間掉格的總數。 |
| [[!UICONTROL 開始前掉格]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#drops-before-start) | `isDroppedBeforeStart` | 布林值 | 指出使用者是否在影片開始前結束（無論是否有廣告）。 |
| [[!UICONTROL 錯誤影響的資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#error-impacted-streams) | `hasErrorImpactedStreams` | 布林值 | 指出資料流在播放期間是否發生錯誤。 |
| [[!UICONTROL 錯誤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#errors-%2F-error-events) | `errorCount` | 整數 | 錄放期間發生的錯誤總數。 |
| [[!UICONTROL 外部錯誤識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#external-error-ids) | `externalErrors` | 字串陣列 | 來自外部來源的唯一錯誤ID （例如CDN錯誤）。 |
| 每秒[[!UICONTROL 個影格]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#frames-per-second) | `framesPerSecond` | 整數 | 目前的串流影格速率（以每秒的影格數為單位）。 |
| [[!UICONTROL 媒體SDK錯誤ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#media-sdk-error-ids) | `mediaSdkErrors` | 字串陣列 | Media SDK在播放期間產生的唯一錯誤ID。 |
| [[!UICONTROL 播放器SDK錯誤ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#player-sdk-error-ids) | `playerSdkErrors` | 字串陣列 | 播放器SDK在播放期間產生的唯一錯誤ID。 |
| [[!UICONTROL 延遲事件]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#stalling-events) | `stallCount` | 整數 | 錄放期間延遲事件的計數。 |
| [[!UICONTROL 延遲受影響的資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#stalling-impacted-streams) | `hasStallImpactedStreams` | 布林值 | 指出串流在播放期間是否發生延遲。 |
| [[!UICONTROL 開始時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#time-to-start-1) | `timeToStart` | 整數 | 視訊載入與開始之間的持續時間（以秒為單位）。 |
| [[!UICONTROL 總緩衝期間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#total-buffer-duration-1) | `bufferTime` | 整數 | 播放期間花費在緩衝的總時間（以秒為單位）。 |
| [[!UICONTROL 總延遲期間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hant#total-stalling-duration) | `stallTime` | 整數 | 錄放期間錄放停頓的總時間（以秒為單位）。 |

{style="table-layout:auto"}
