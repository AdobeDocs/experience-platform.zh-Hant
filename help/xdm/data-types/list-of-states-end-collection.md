---
title: 狀態清單結束集合資料型別
description: 瞭解狀態清單結束集合資料型別體驗資料模型(XDM)資料型別。
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 狀態清單結束] 資料型別

狀態清單結束集合資料型別資料型別是Experience Data Model (XDM)資料型別，設計用於表示與各種播放器屬性的結束狀態相關的資訊。 其中包括 [!UICONTROL 播放器狀態名稱] 指出特定屬性狀態的屬性（例如「fullscreen」、「mute」、「closedCaptioning」）。 此資料型別用於擷取及描述不同播放器狀態的初始條件。

![狀態清單結束集合資料型別的圖表。](../images/data-types/list-of-states-end-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 播放器狀態名稱] | `name` | 字串 | 無 | 播放器狀態的名稱。 列舉： 「fullscreen」、「mute」、「closedCaptioning」、「pictureInPicture」、「inFocus」及其各自含義。 |

{style="table-layout:auto"}
