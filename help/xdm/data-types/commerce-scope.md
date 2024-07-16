---
title: Commerce範圍資料型別
description: 瞭解Commerce Scope Experience Data Model (XDM)資料型別。
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# [!UICONTROL Commerce範圍]資料型別

[!UICONTROL Commerce範圍]是標準的體驗資料模型(XDM)資料型別，可定義在商務生態系統中發生事件的識別碼。 它會區分環境、網站、商店和商店檢視。

![Commerce範圍資料型別的圖表。](../images/data-types/commerce-scope.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 環境ID] | `environmentID` | 字串 | 環境識別碼。 32位數的英數字元ID。 |
| [!UICONTROL 網站代碼] | `websiteCode` | 字串 | 環境內的唯一網站程式碼。 |
| [!UICONTROL 存放區代碼] | `storeCode` | 字串 | 網站內的唯一商店代碼。 |
| [!UICONTROL 存放區檢視代碼] | `storeViewCode` | 字串 | 商店內的唯一商店檢視代碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
