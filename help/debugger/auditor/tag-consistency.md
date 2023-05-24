---
title: 標籤一致性Test參考
description: 瞭解審計者如何在Adobe Experience Platform調試器中為標籤一致性設定test。
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 42%

---

# 標籤一致性test引用

此參考提供了有關審計者如何在Adobe Experience Platform調試器test中進行標籤一致性功能的詳細資訊。

>[!NOTE]
>
>有關平台調試器中審計者test的詳細資訊，請參見 [審計器功能概述](./overview.md)。

標籤一致性test查找所有掃描頁面的不一致。 這些值或設定在網站的所有頁面上均應相同，以確保資料收集的正確性。

| 測試 | 重量 | 標準 | 建議 |
| --- | --- | --- | --- |
| Adobe Analytics — 一致的代碼版本 | 5 | 找到多個 Analytics 程式碼版本。 | 將所有 Analytics 執行個體取代為目前版本。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |

{style="table-layout:auto"}
