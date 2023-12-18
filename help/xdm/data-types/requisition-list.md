---
title: 請購單清單資料型別
description: 瞭解請購單清單體驗資料模型(XDM)資料型別。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 5%

---

# [!UICONTROL 請購單清單] 資料型別

[!UICONTROL 請購單清單] 是標準的體驗資料模型(XDM)資料型別，可描述用於採購或購買的組織專案集合。 使用 [!UICONTROL 請購單清單] 用於識別及描述請購單清單的資料型別。

![的圖表 [!UICONTROL 請購單清單] 資料型別。](../images/data-types/requisition-list.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL 請購單清單識別碼] | `ID` | 字串 | 請購單清單的唯一識別碼。 |
| [!UICONTROL 請購單清單名稱] | `name` | 字串 | 客戶指定的請購單清單名稱。 |
| [!UICONTROL 請購單清單說明] | `description` | 字串 | 客戶所指定之請購單清單的說明。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
