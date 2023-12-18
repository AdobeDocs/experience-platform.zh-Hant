---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；商務；資料型別；資料型別；
solution: Experience Platform
title: Commerce資料型別
description: 瞭解Commerce Experience Data Model (XDM)資料型別。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL 商務] 資料型別

[!UICONTROL 商務] 是標準的體驗資料模型(XDM)資料型別，可描述與購買和銷售相關的記錄。

![的圖表 [!UICONTROL 商務] 資料型別。](../images/data-types/commerce.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL 訂購] | `order` | [[!UICONTROL 訂購]](./order.md) | 說明一或多個產品的已下訂單。 |
| [!UICONTROL 促銷活動ID] | `promotionID` | [!UICONTROL 字串] | 已下訂單的促銷識別碼（若存在）。 |
| [!UICONTROL 購物車放棄] | `cartAbandons` | [[!UICONTROL 測量]](./measure.md) | 說明何時將產品清單識別為使用者無法再存取或購買。 |
| [!UICONTROL 結帳] | `checkouts` | [[!UICONTROL 測量]](./measure.md) | 產品清單結帳程式中的動作。 如果結帳程式中有多個步驟，就可能有一個以上的結帳事件。 如果有多個步驟，事件時間資訊和參照的頁面或體驗可用來依序識別步驟和個別事件。 |
| [!UICONTROL 產品清單（購物車）新增專案] | `productListAdds` | [[!UICONTROL 測量]](./measure.md) | 將產品新增至產品清單，例如將產品新增至購物車。 |
| [!UICONTROL 產品清單（購物車）開啟] | `productListOpens` | [[!UICONTROL 測量]](./measure.md) | 新產品清單的初始化，例如正在建立的購物車。 |
| [!UICONTROL 產品清單（購物車）移除] | `productListRemovals` | [[!UICONTROL 測量]](./measure.md) | 從產品清單移除產品專案，例如從購物車移除的產品。 |
| [!UICONTROL 產品清單（購物車）重新開啟] | `productListReopens` | [[!UICONTROL 測量]](./measure.md) | 先前捨棄且使用者已重新啟動的產品清單。 |
| [!UICONTROL 產品清單（購物車）檢視] | `productListViews` | [[!UICONTROL 測量]](./measure.md) | 描述產品清單檢視何時發生。產品清單檢視何時發生。 |
| [!UICONTROL 產品檢視] | `productViews` | [[!UICONTROL 測量]](./measure.md) | 說明何時已發生個別產品的檢視。 |
| [!UICONTROL 購買] | `purchases` | [[!UICONTROL 測量]](./measure.md) | 用於追蹤何時接受訂單。 在商業轉換中，購買事件是唯一必要的動作。 購買事件必須有參考的產品清單。 |
| [!UICONTROL 儲存供日後使用] | `saveForLaters` | [[!UICONTROL 測量]](./measure.md) | 說明何時儲存產品清單以供未來使用，例如希望清單。 |
| [!UICONTROL 店內購買] | `inStorePurchase` | [[!UICONTROL 測量]](./measure.md) | 表示「inStore」購買。 此資訊會儲存以供分析使用。 |
| [!UICONTROL 購物車] | `cart` | [[!UICONTROL 購物車]](./cart.md) | 包含一或多個產品的購物車的屬性。 |
| [!UICONTROL 送貨] | `shipping` | [[!UICONTROL 送貨]](./shipping.md) | 一或多個產品的運送詳細資料。 |
| [!UICONTROL 帳單] | `billing` | [[!UICONTROL 帳單]](#billing) | 一或多項付款的帳單細節。 |
| [!UICONTROL 立即購買] | `instantPurchase` | [[!UICONTROL 測量]](./measure.md) | 說明何時立即購買產品，可能略過購物車或結帳。 |
| [!UICONTROL 請購單清單開啟] | `requisitionListOpens` | [[!UICONTROL 測量]](./measure.md) | 指示初始化新的請購單清單。 |
| [!UICONTROL 請購單清單刪除] | `requisitionListDeletes` | [[!UICONTROL 測量]](./measure.md) | 指示請購單清單的移除。 |
| [!UICONTROL 請購單清單新增] | `requisitionListAdds` | [[!UICONTROL 測量]](./measure.md) | 表示將產品加入請購單清單。 |
| [!UICONTROL 請購單清單移除次數] | `requisitionListRemovals` | [[!UICONTROL 測量]](./measure.md) | 表示從請購單產品清單移除產品。 |
| [!UICONTROL 申請清單] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | 客戶建立的請購單清單屬性。 |
| [!UICONTROL 範圍] | `commerceScope` | [[!UICONTROL Commercescope]](./commerce-scope.md) | 發生事件的商業範圍識別碼（商店檢視、商店、網站等）。 |

{style="table-layout:auto"}

## [!UICONTROL 帳單] 資料型別 {#billing}

[!UICONTROL 帳單] 是標準的體驗資料模型(XDM)資料型別，其中包含計費詳細資料的相關資訊。 具體來說，重點在於帳單地址。

![計費資料型別的圖表。](../images/data-types/billing.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL 帳單地址] | `address` | [[!UICONTROL 郵寄地址]](./postal-address.md) | 帳單地址。 |

{style="table-layout:auto"}

如需更多詳細資訊，請參閱 [!UICONTROL 商務] 資料型別，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
