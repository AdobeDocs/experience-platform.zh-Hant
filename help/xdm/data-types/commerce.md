---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas；商務；資料類型；資料類型；
solution: Experience Platform
title: 商務資料類型
topic-legacy: overview
description: 本檔案提供商務體驗資料模型(XDM)資料類型的概觀。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# [!UICONTROL Commerce] 資料類型

[!UICONTROL Commerce] 是標準的「體驗資料模型」(XDM)資料類型，可說明與購買和銷售活動相關的記錄。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `order` | [[!UICONTROL Order]](./order.md) | 說明一或多個產品的下單。 |
| `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | 用於描述產品清單何時被識別為使用者不再存取或可購買。 |
| `checkouts` | [[!UICONTROL Measure]](./measure.md) | 產品清單結帳程式期間的動作。 如果結帳程式中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用事件時間資訊和參考頁面或體驗來識別依順序呈現的步驟和個別事件。 |
| `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | 說明與店內購買相關的值，以供分析使用。 |
| `productListAdds` | [[!UICONTROL Measure]](./measure.md) | 將產品新增至產品清單，例如要新增至購物車的產品。 |
| `productListOpens` | [[!UICONTROL Measure]](./measure.md) | 新產品清單的初始化，例如正在建立的購物車。 |
| `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | 從產品清單中移除或移除產品項目，例如從購物車移除的產品。 |
| `productListReopens` | [[!UICONTROL Measure]](./measure.md) | 先前已放棄且由使用者重新啟動的產品清單。 |
| `productListViews` | [[!UICONTROL Measure]](./measure.md) | 說明產品清單的檢視或檢視何時發生。 |
| `productViews` | [[!UICONTROL Measure]](./measure.md) | 說明個別產品的檢視或檢視發生的時間。 |
| `purchases` | [[!UICONTROL Measure]](./measure.md) | 用於追蹤何時接受訂單。 購買事件是商務轉換中唯一必要的動作。 購買事件必須有參考的產品清單。 |
| `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | 產品清單會儲存以供日後使用，例如願望清單。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
