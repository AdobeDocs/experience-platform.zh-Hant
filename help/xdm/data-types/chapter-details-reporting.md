---
title: 章節詳細資料報表資料型別
description: 瞭解關於報告體驗資料模型(XDM)資料型別的章節詳細資訊。
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL 章節詳細資料]報告資料型別

[!UICONTROL 章節詳細資料]報表是標準的體驗資料模型(XDM)資料型別，可描述與媒體內容中章節或區段相關的各種屬性。 使用[!UICONTROL 章節詳細資料]報告資料型別來擷取章節名稱、持續時間、位置、ID、播放狀態（已開始/完成）和每個章節逗留時間等詳細資料。 Adobe服務會使用媒體報表欄位來分析使用者傳送的「媒體收集」欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。

![章節詳細資料報表資料型別的圖表。](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含由Adobe、實作值、網路引數、報表和重要考量收集之視訊廣告資料的詳細資訊。

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL 章節已完成]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-complete) | `isCompleted` | 布林值 | 章節是否已完成。 |
| [[!UICONTROL 章節識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter) | `ID` | 字串 | 自動產生的章節識別碼。 |
| [[!UICONTROL 章節長度或持續時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-length) | `length` | 整數 | 章節長度 (秒數)。 |
| [[!UICONTROL 章節名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-name) | `friendlyName` | 字串 | 章節和/或區段名稱。 |
| [[!UICONTROL 章節位移]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-offset) | `offset` | 整數 | 內容內從頭開始的章節位移（以秒為單位）。 |
| [[!UICONTROL 章節位置]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-position) | `index` | 整數 | 內容內的章節位置（索引、整數）。 |
| [[!UICONTROL 章節已開始]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-start) | `isStarted` | 布林值 | 章節是否已開始。 |
| [[!UICONTROL 章節時間已播放]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-time-spent) | `timePlayed` | 整數 | 章節逗留時間（秒數）。 |
