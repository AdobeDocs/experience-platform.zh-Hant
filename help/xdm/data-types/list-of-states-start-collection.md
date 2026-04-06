---
title: 狀態清單開始收集資料型別
description: 瞭解狀態清單開始資料型別體驗資料模型(XDM)資料型別。
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 8%

---

# [!UICONTROL List of States Start]資料型別

[!UICONTROL List of States Start]資料型別是Experience Data Model (XDM)資料型別，設計用於表示與各種播放器屬性的開始狀態相關的資訊。 其中包含指出特定屬性狀態的[!UICONTROL Player State Name]屬性（例如，「fullscreen」、「mute」、「closedCaptioning」）。 此資料型別用於擷取及描述不同播放器狀態的初始條件。

![&#x200B; [!UICONTROL List of States Start]資料型別的圖表。](../images/data-types/list-of-states-start-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | 字串 | 無 | 播放器狀態的名稱。 列舉： 「fullscreen」、「mute」、「closedCaptioning」、「pictureInPicture」、「inFocus」及其各自含義。 |

{style="table-layout:auto"}
