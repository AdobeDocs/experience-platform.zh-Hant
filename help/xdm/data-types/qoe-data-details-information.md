---
title: QoE （體驗品質）資料詳細資訊資料型別
description: 瞭解QoE （體驗品質）資料詳細資訊資料型別體驗資料模型(XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# QoE （體驗品質）資料詳細資訊資料型別

[!UICONTROL QoE資料詳細資訊] 是標準的體驗資料模型(XDM)資料型別，在媒體播放期間提供與體驗品質(QoE)相關的詳細量度。 使用 [!UICONTROL QoE資料詳細資訊] 資料型別以擷取詳細資訊，例如位元速率資訊、影格速率、緩衝事件、掉格等。 此資料型別可啟用播放品質分析，深入分析串流效能、使用者體驗和播放工作階段期間遇到的潛在問題。

+++選取此選項可顯示「QoE資料詳細資訊」資料型別。
![QoE （體驗品質）資料詳細資訊資料資料型別的圖表。](../images/data-types/qoe-data-details-information.png)
+++

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL 平均位元貯體] | `bitrateAverageBucket` | 字串 | 以100kbps間隔分類在預先定義值區內的平均位元速率（以kbps為單位）。 |
| [!UICONTROL 位元速率] | `bitrate` | 整數 | 位元速率值（以每秒位元組數為單位）。 |
| [!UICONTROL 平均位元速率] | `bitrateAverage` | 數字 | 平均位元速率（以每秒位元組數為單位，須為整數）。 計算為位元速率值的加權平均。 |
| [!UICONTROL 位元速率變更影響的資料流] | `hasBitrateChangeImpactedStreams` | 布林值 | 表示資料流在播放期間是否受到位元速率變更的影響。 |
| [!UICONTROL 位元速率變更] | `bitrateChangeCount` | 整數 | 錄放期間位元速率變更的總計數。 |
| [!UICONTROL 掉格影響的資料流] | `hasDroppedFrameImpactedStreams` | 布林值 | 表示串流在播放期間是否受到掉格的影響。 |
| [!UICONTROL 掉格] | `droppedFrames` | 整數 | 播放期間掉格的總數。 |
| [!UICONTROL 開始前掉格] | `isDroppedBeforeStart` | 布林值 | 指出使用者是否在影片開始前結束（無論是否有廣告）。 |
| [!UICONTROL 每秒影格數] | `framesPerSecond` | 整數 | 目前的串流影格速率（以每秒的影格數為單位）。 |
| [!UICONTROL 開始時間] | `timeToStart` | 整數 | 視訊載入與開始之間的持續時間（以秒為單位）。 |
| [!UICONTROL 緩衝影響的資料流] | `hasBufferImpactedStreams` | 布林值 | 指出資料流在播放期間是否受到緩衝影響。 |
| [!UICONTROL 緩衝事件] | `bufferCount` | 整數 | 錄放期間不同緩衝狀態的計數。 |
| [!UICONTROL 總緩衝期間] | `bufferTime` | 整數 | 播放期間花費在緩衝的總時間（以秒為單位）。 |
| [!UICONTROL 錯誤影響的資料流] | `hasErrorImpactedStreams` | 布林值 | 指出資料流在播放期間是否發生錯誤。 |
| [!UICONTROL 錯誤] | `errorCount` | 整數 | 錄放期間發生的錯誤總數。 |
| [!UICONTROL 停頓影響的資料流] | `hasStallImpactedStreams` | 布林值 | 指出串流在播放期間是否發生延遲。 |
| [!UICONTROL 延遲事件] | `stallCount` | 整數 | 錄放期間延遲事件的計數。 |
| [!UICONTROL 總停頓期間] | `stallTime` | 整數 | 錄放期間錄放停頓的總時間（以秒為單位）。 |
| [!UICONTROL 播放器SDK錯誤ID] | `playerSdkErrors` | 字串陣列 | 播放器SDK在播放期間產生的唯一錯誤ID。 |
| [!UICONTROL 外部錯誤ID] | `externalErrors` | 字串陣列 | 來自外部來源的唯一錯誤ID （例如CDN錯誤）。 |
| [!UICONTROL Media SDK錯誤ID] | `mediaSdkErrors` | 字串陣列 | Media SDK在播放期間產生的唯一錯誤ID。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

