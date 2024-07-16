---
title: 傳回資料型別
description: 瞭解回訪體驗資料模型(XDM)資料型別。
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL 傳回]資料型別

[!UICONTROL Return]是標準的體驗資料模型(XDM)資料型別，可擷取與Return Merchandise Authorization (RMA)相關的基本資訊。

![傳回資料型別的圖表。](../images/data-types/return.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL 傳回ID] | `returnID` | 字串 | 此RMA的唯一識別碼。 |
| [!UICONTROL 傳回狀態] | `returnStatus` | 字串 | RMA的目前狀態（例如，擱置或已關閉）。 |
| [!UICONTROL 訂單購買ID] | `purchaseID` | 字串 | RMA所屬之訂單/採購的唯一識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
