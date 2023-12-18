---
title: 購物車資料型別
description: 瞭解購物車體驗資料模型(XDM)資料型別。
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 5%

---

# [!UICONTROL 購物車] 資料型別

[!UICONTROL 購物車] 是標準的體驗資料模型(XDM)資料型別，提供與購物車相關的屬性。 使用此資料型別來擷取賣家指派的唯一識別碼(`Cart ID`)和來源(`Cart Source`)，其中一或多個產品已新增至購物車。

![的圖表 [!UICONTROL 購物車] 資料型別。](../images/data-types/cart.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL 購物車ID] | `cartID` | 字串 | 賣家為購物車指派的唯一識別碼。 |
| [!UICONTROL 購物車來源] | `cartSource` | 字串 | 將一個或多個產品新增到購物車的位置。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
