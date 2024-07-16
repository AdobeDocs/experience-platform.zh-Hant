---
title: 錯誤詳細資料集合資料型別
description: 瞭解錯誤詳細資料收集Experience Data Model (XDM)資料型別。
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL 錯誤詳細資料]集合資料型別

[!UICONTROL 錯誤詳細資料]集合是描述錯誤詳細資料的標準體驗資料模型(XDM)資料型別。 使用[!UICONTROL 錯誤詳細資料]集合資料型別來擷取錯誤來源和識別的詳細資料。 錯誤ID會識別錯誤，而錯誤來源會指定錯誤是否源自播放器或外部來源。

![錯誤詳細資訊資料型別的圖表。](../images/data-types/error-details-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL 錯誤識別碼] | `name` | 字串 | 無 | 錯誤 ID。 |
| [!UICONTROL 錯誤Source] | `source` | 字串 | 無 | 錯誤來源。 列舉： 「player」、「external」，分別具意義。 |

{style="table-layout:auto"}
