---
title: 自訂中繼資料詳細資訊資料型別
description: 瞭解自訂中繼資料詳細資訊體驗資料模型(XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# [!UICONTROL 自訂中繼資料詳細資訊] 資料型別

[!UICONTROL 自訂中繼資料詳細資訊] 是標準的體驗資料模型(XDM)資料型別，會定義儲存自訂中繼資料的結構。 使用 [!UICONTROL 自訂中繼資料詳細資訊] 資料型別以擷取詳細資訊，例如與內容或互動相關聯的自訂中繼資料的名稱和值。

![「自訂中繼資料詳細資訊」資料型別的圖表。](../images/data-types/custom-metadata-details-information.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL 自訂中繼資料欄位名稱] | `name` | 字串 | 自訂欄位的名稱。 |
| [!UICONTROL 自訂中繼資料欄位值] | `value` | 字串 | 自訂欄位的值。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
