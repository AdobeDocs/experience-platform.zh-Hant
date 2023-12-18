---
title: 商務範圍資料型別
description: 瞭解Commerce Scope Experience Data Model (XDM)資料型別。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---

# [!UICONTROL 商業範圍] 資料型別

[!UICONTROL 商業範圍] 是標準的體驗資料模型(XDM)資料型別，可定義商業生態系統中發生事件的識別碼。 它會區分環境、網站、商店和商店檢視。

![商務範圍資料型別的圖表。](../images/data-types/commerce-scope.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 環境ID] | `environmentID` | 字串 | 環境識別碼。 32位數的英數字元ID。 |
| [!UICONTROL 網站程式碼] | `websiteCode` | 字串 | 環境內的唯一網站程式碼。 |
| [!UICONTROL 存放區代碼] | `storeCode` | 字串 | 網站內的唯一商店代碼。 |
| [!UICONTROL 存放區檢視代碼] | `storeViewCode` | 字串 | 商店內的唯一商店檢視代碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
