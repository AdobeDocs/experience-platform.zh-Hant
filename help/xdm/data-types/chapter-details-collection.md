---
title: 章節詳細資料集合資料型別
description: 瞭解章節詳細資料收集Experience Data Model (XDM)資料型別。
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL 章節詳細資料]集合資料型別

[!UICONTROL 章節詳細資料]集合是標準的體驗資料模型(XDM)資料型別，可描述與媒體內容中章節或區段相關的各種屬性。 使用[!UICONTROL 章節詳細資料]集合資料型別來擷取詳細資料，例如章節名稱、位移、持續時間和章節索引。 媒體收集欄位會擷取資料，並將其傳送至其他Adobe服務以供進一步處理。

![章節詳細資料集合資料型別的圖表。](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含由Adobe、實作值、網路引數、報表和重要考量收集之視訊廣告資料的詳細資訊。

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL 章節長度或持續時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-length) | `length` | 整數 | 是 | 章節長度 (秒數)。 |
| [[!UICONTROL 章節名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-name) | `friendlyName` | 字串 | 無 | 章節和/或區段名稱。 |
| [[!UICONTROL 章節位移]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-offset) | `offset` | 整數 | 是 | 內容內從頭開始的章節位移（以秒為單位）。 |
| [[!UICONTROL 章節位置]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=zh-Hant#chapter-position) | `index` | 整數 | 是 | 內容內的章節位置（索引、整數）。 |

{style="table-layout:auto"}
