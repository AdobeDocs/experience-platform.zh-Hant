---
title: 章節詳細資訊資料型別
description: 瞭解章節詳細資訊Experience Data Model (XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 6%

---

# [!UICONTROL 章節詳細資訊] 資料型別

[!UICONTROL 章節詳細資訊] 是標準的體驗資料模型(XDM)資料型別，可描述與媒體內容中章節或區段相關的各種屬性。 使用 [!UICONTROL 章節詳細資訊] 擷取章節名稱、持續時間、位置、ID、播放狀態（已開始/完成）和每個章節逗留時間等詳細資料的資料型別。

![「章節詳細資訊」資料型別的圖表。](../images/data-types/chapter-details-information.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL 章節名稱] | `friendlyName` | 字串 | 章節和/或區段名稱。 |
| [!UICONTROL 章節長度或持續時間] | `length` | 整數 | **必填** 章節長度（以秒為單位）。 |
| [!UICONTROL 章節位移] | `offset` | 整數 | **必填** 內容內從頭開始的章節位移（以秒為單位）。 |
| [!UICONTROL 章節位置] | `index` | 整數 | **必填** 內容內的章節位置（索引、整數）。 |
| [!UICONTROL 章節識別碼] | `ID` | 字串 | 自動產生的章節識別碼。 |
| [!UICONTROL 章節已開始] | `isStarted` | 布林值 | 章節是否已開始。 |
| [!UICONTROL 章節已完成] | `isCompleted` | 布林值 | 章節是否已完成。 |
| [!UICONTROL 章節時間已播放] | `timePlayed` | 整數 | 章節逗留時間（秒數）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
