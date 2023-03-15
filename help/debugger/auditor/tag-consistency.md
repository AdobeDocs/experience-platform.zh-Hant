---
title: 標籤一致性測試參考
description: 了解Auditor如何在Adobe Experience Platform Debugger中功能測試標籤一致性。
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 42%

---

# 標籤一致性測試參考

此參考檔案主要探討Adobe Experience Platform Debugger中的auditor功能如何測試標籤一致性，為使用者提供詳細資訊。

>[!NOTE]
>
>如需Platform Debugger中Auditor測試的詳細資訊，請參閱 [auditor功能概觀](./overview.md).

標籤一致性測試會在所有掃描的頁面上尋找不一致之處。 這些值或設定在網站的所有頁面上均應相同，以確保資料收集的正確性。

| 測試 | 寬度 | 標準 | 建議 |
| --- | --- | --- | --- |
| Adobe Analytics — 一致的程式碼版本 | 5 | 找到多個 Analytics 程式碼版本。 | 將所有 Analytics 執行個體取代為目前版本。<br><br>[其他資訊](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hant) |

{style="table-layout:auto"}
