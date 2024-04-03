---
title: 錯誤詳細資料集合資料型別
description: 瞭解錯誤詳細資料收集Experience Data Model (XDM)資料型別。
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL 錯誤詳細資料] 集合資料型別

[!UICONTROL 錯誤詳細資料] 集合是標準的體驗資料模型(XDM)資料型別，可描述錯誤詳細資料。 使用 [!UICONTROL 錯誤詳細資料] 用於擷取錯誤來源和識別詳細資料的集合資料型別。 錯誤ID會識別錯誤，而錯誤來源會指定錯誤是否源自播放器或外部來源。

![「錯誤詳細資訊」資料型別的圖表。](../images/data-types/error-details-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL 錯誤ID] | `name` | 字串 | 無 | 錯誤識別碼。 |
| [!UICONTROL 錯誤來源] | `source` | 字串 | 無 | 錯誤來源。 列舉： 「player」、「external」，分別具意義。 |

{style="table-layout:auto"}
