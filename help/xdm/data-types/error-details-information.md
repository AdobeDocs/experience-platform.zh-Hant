---
title: 錯誤詳細資訊資料型別
description: 瞭解錯誤詳細資訊Experience Data Model (XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 5%

---

# [!UICONTROL 錯誤詳細資訊] 資料型別

[!UICONTROL 錯誤詳細資訊] 是標準的體驗資料模型(XDM)資料型別，可描述錯誤詳細資料。 使用 [!UICONTROL 錯誤詳細資訊] 擷取錯誤來源和識別詳細資料的資料型別。 錯誤ID會識別錯誤，而錯誤來源會指定錯誤是否源自播放器或外部來源。

![「錯誤詳細資訊」資料型別的圖表。](../images/data-types/error-details-information.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL 錯誤ID] | `name` | 字串 | 錯誤識別碼。 |
| [!UICONTROL 錯誤來源] | `source` | 字串 | 錯誤來源。 列舉： 「player」、「external」，分別具意義。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
