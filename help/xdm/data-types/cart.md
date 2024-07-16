---
title: 購物車資料型別
description: 瞭解購物車體驗資料模型(XDM)資料型別。
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 14%

---

# [!UICONTROL 購物車]資料型別

[!UICONTROL 購物車]是標準的體驗資料模型(XDM)資料型別，提供與購物車相關的屬性。 使用此資料型別來擷取銷售者(`Cart ID`)指派的唯一識別碼，以及一個或多個產品加入購物車的來源(`Cart Source`)。

![ [!UICONTROL 購物車]資料型別的圖表。](../images/data-types/cart.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL 購物車ID] | `cartID` | 字串 | 由賣家為購物車指派的唯一識別碼。 |
| [!UICONTROL 購物車Source] | `cartSource` | 字串 | 將一個或多個產品新增到購物車的位置。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
