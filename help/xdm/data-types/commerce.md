---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；商務；資料類型；資料類型；
solution: Experience Platform
title: 商務資料類型
description: 本檔案概述Commerce Experience Data Model(XDM)資料類型。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL 商務] 資料類型

[!UICONTROL 商務] 是標準的Experience Data Model(XDM)資料類型，可說明與購買和銷售活動相關的記錄。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `order` | [[!UICONTROL 順序]](./order.md) | 說明一或多項產品的下單。 |
| `cartAbandons` | [[!UICONTROL 測量]](./measure.md) | 用於說明產品清單何時被識別為使用者不再存取或可購買。 |
| `checkouts` | [[!UICONTROL 測量]](./measure.md) | 產品清單結帳程式期間的動作。 如果結帳過程中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用事件時間資訊和參考的頁面或體驗來識別依序呈現的步驟和個別事件。 |
| `inStorePurchase` | [[!UICONTROL 測量]](./measure.md) | 說明與供分析使用之店內購買相關聯的值。 |
| `productListAdds` | [[!UICONTROL 測量]](./measure.md) | 將產品新增至產品清單，例如要新增至購物車的產品。 |
| `productListOpens` | [[!UICONTROL 測量]](./measure.md) | 新產品清單的初始化，例如正在建立的購物車。 |
| `productListRemovals` | [[!UICONTROL 測量]](./measure.md) | 從產品清單中移除或移除產品項目，例如從購物車移除的產品。 |
| `productListReopens` | [[!UICONTROL 測量]](./measure.md) | 先前放棄的產品清單，已由使用者重新啟動。 |
| `productListViews` | [[!UICONTROL 測量]](./measure.md) | 說明產品清單的檢視或檢視發生的時間。 |
| `productViews` | [[!UICONTROL 測量]](./measure.md) | 說明個別產品的檢視或檢視發生的時間。 |
| `purchases` | [[!UICONTROL 測量]](./measure.md) | 用於追蹤何時接受訂單。 購買事件是商務轉換中唯一的必要動作。 購買事件必須有參考的產品清單。 |
| `saveForLaters` | [[!UICONTROL 測量]](./measure.md) | 產品清單會儲存以供日後使用，例如願望清單。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
