---
title: 狀態清單開始收集資料型別
description: 瞭解狀態清單開始資料型別體驗資料模型(XDM)資料型別。
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL 狀態清單開始]資料型別

[!UICONTROL 狀態清單開始]資料型別是體驗資料模型(XDM)資料型別，設計用於表示與各種播放器屬性的開始狀態相關的資訊。 它包含表示特定屬性狀態的[!UICONTROL 播放器狀態名稱]屬性（例如，「fullscreen」、「mute」、「closedCaptioning」）。 此資料型別用於擷取及描述不同播放器狀態的初始條件。

![ [!UICONTROL 狀態清單開始]資料型別的圖表。](../images/data-types/list-of-states-start-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 播放器狀態名稱] | `name` | 字串 | 無 | 播放器狀態的名稱。 列舉： 「fullscreen」、「mute」、「closedCaptioning」、「pictureInPicture」、「inFocus」及其各自含義。 |

{style="table-layout:auto"}
