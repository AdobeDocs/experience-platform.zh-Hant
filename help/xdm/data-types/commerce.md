---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；商業；資料類型；資料類型；
solution: Experience Platform
title: 商務資料類型
description: 本文檔概述了Commerce Experience Data Model(XDM)資料類型。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 商業] 資料類型

[!UICONTROL 商業] 是一個標準的體驗資料模型(XDM)資料類型，它描述與購買和銷售活動相關的記錄。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `order` | [[!UICONTROL 訂單]](./order.md) | 描述一個或多個產品的下達訂單。 |
| `cartAbandons` | [[!UICONTROL 度量]](./measure.md) | 用於描述產品清單何時被標識為不再可由用戶訪問或購買。 |
| `checkouts` | [[!UICONTROL 度量]](./measure.md) | 產品清單的簽出過程中的操作。 如果簽出過程中有多個步驟，則可能會出現多個簽出事件。 如果存在多個步驟，則使用事件時間資訊和參考頁面或經驗來識別按順序表示的步驟和單個事件。 |
| `inStorePurchase` | [[!UICONTROL 度量]](./measure.md) | 描述與用於分析的店內採購關聯的值。 |
| `productListAdds` | [[!UICONTROL 度量]](./measure.md) | 將產品添加到產品清單，例如將產品添加到購物車。 |
| `productListOpens` | [[!UICONTROL 度量]](./measure.md) | 新產品清單的初始化，如正在建立的購物車。 |
| `productListRemovals` | [[!UICONTROL 度量]](./measure.md) | 從產品清單中刪除或刪除產品條目，例如從購物車中刪除的產品。 |
| `productListReopens` | [[!UICONTROL 度量]](./measure.md) | 先前已放棄且已被用戶重新激活的產品清單。 |
| `productListViews` | [[!UICONTROL 度量]](./measure.md) | 描述產品清單的視圖或視圖的發生時間。 |
| `productViews` | [[!UICONTROL 度量]](./measure.md) | 描述單個產品的視圖或視圖的發生時間。 |
| `purchases` | [[!UICONTROL 度量]](./measure.md) | 用於跟蹤何時接受訂單。 採購事件是商業轉換中唯一必需的操作。 採購事件必須引用產品清單。 |
| `saveForLaters` | [[!UICONTROL 度量]](./measure.md) | 將保存產品清單供將來使用，如希望清單。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
