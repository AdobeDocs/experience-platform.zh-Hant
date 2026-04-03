---
title: 狀態清單結束集合資料型別
description: 瞭解狀態清單結束集合資料型別體驗資料模型(XDM)資料型別。
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# [!UICONTROL List of States End]資料型別

狀態清單結束集合資料型別資料型別是Experience Data Model (XDM)資料型別，設計用於表示與各種播放器屬性的結束狀態相關的資訊。 其中包含指出特定屬性狀態的[!UICONTROL Player State Name]屬性（例如，「fullscreen」、「mute」、「closedCaptioning」）。 此資料型別用於擷取及描述不同播放器狀態的初始條件。

![狀態清單的圖表結束集合資料型別。](../images/data-types/list-of-states-end-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | 字串 | 無 | 播放器狀態的名稱。 列舉： 「fullscreen」、「mute」、「closedCaptioning」、「pictureInPicture」、「inFocus」及其各自含義。 |

{style="table-layout:auto"}
