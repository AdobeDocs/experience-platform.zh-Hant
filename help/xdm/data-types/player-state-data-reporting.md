---
title: 播放器狀態資料報告資料型別
description: 瞭解播放器狀態資料報告Experience Data Model (XDM)資料型別。
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 21%

---

# [!UICONTROL 播放器狀態資料報告]資料型別

[!UICONTROL 播放器狀態資料報告]是標準的體驗資料模型(XDM)資料型別，可描述媒體播放器中的各種狀態及其發生次數。 使用[!UICONTROL 播放器狀態資料報告]資料型別來擷取不同的播放器狀態，例如全熒幕、靜音、隱藏式字幕、子母畫面和觀看中狀態。 對於每個狀態，都會記錄狀態是否已設定、發生次數計數，以及在媒體播放期間保持作用中的總持續時間。

![播放器狀態資料報告資料型別的圖表。](../images/data-types/player-state-data-information.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL 播放器狀態名稱] | `name` | 字串 | 播放器狀態的名稱。 列舉： 「fullscreen」、「mute」、「closedCaptioning」、「pictureInPicture」、「inFocus」及其各自含義。 |
| [!UICONTROL 播放器狀態集] | `isSet` | 布林值 | 播放器狀態是否設定為該狀態。 |
| [!UICONTROL 播放器狀態計數] | `count` | 整數 | 串流上設定播放器狀態的次數。 |
| [!UICONTROL 播放器狀態時間] | `time` | 整數 | 該播放器狀態的持續時間。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
