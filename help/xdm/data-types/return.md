---
title: 傳回資料型別
description: 瞭解回訪體驗資料模型(XDM)資料型別。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 6%

---

# [!UICONTROL 傳回] 資料型別

[!UICONTROL 傳回] 是標準的體驗資料模型(XDM)資料型別，可擷取與退貨商品授權(RMA)相關的基本資訊。

![Return資料型別的圖表。](../images/data-types/return.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL 傳回ID] | `returnID` | 字串 | 此RMA的唯一識別碼。 |
| [!UICONTROL 傳回狀態] | `returnStatus` | 字串 | RMA的目前狀態（例如，擱置或已關閉）。 |
| [!UICONTROL 訂單購買ID] | `purchaseID` | 字串 | RMA所屬之訂單/採購的唯一識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

