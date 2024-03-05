---
title: 使用Adobe Experience Platform Web SDK收集商務、產品和訂單資訊
description: 瞭解如何使用Adobe Experience Platform Web SDK新增與產品或購物車相關的資料。
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# 收集商務、產品和訂單資訊

如果您的組織銷售產品或服務，您可以使用此頁面作為追蹤這些產品和服務的指南。

此頁面使用XDM [商務結構描述](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) 欄位群組。

此欄位群組包含兩個主要部分：

* 此 `commerce` 物件。 此物件可讓您指出哪些動作發生於 `productListItems` 陣列。
* 此 `productListItems` 陣列。

>[!TIP]
>
>如果您熟悉Adobe Analytics，請參閱 `commerce` 物件包含與中的商務事件類似的資料 `events` 變數中。 此 `productListItems` 物件陣列包含的資料與 `products` 變數中。

## 此 `commerce` 物件 {#commerce-object}

本節說明 `commerce` 物件。

>[!TIP]
>
>測量有兩個欄位： `id` 和 `value`. 大部分時間，您只使用 `value` 欄位(例如 `'value':1`)。 此 `id` 欄位可讓您設定唯一識別碼，以追蹤傳送量值的時間。 請參閱XDM檔案以瞭解 [測量](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) 以取得詳細資訊。

| 測量 | 建議 | 說明 |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | 選填 | 使用者無法再存取或購買購物車。 |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | 強烈建議 | 使用者不再瀏覽產品，但正在購買產品。 |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | 強烈建議 | 產品會新增至清單。 請務必在「 」中設定產品 `productListItems` 同時。 |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | 選填 | 新產品清單隨即建立。 例如，會建立新的購物車。 |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | 強烈建議 | 產品會從產品清單中移除。 |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | 選填 | 使用者會重新啟用產品清單。 此動作經常發生在再行銷活動中。 |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | 強烈建議 | 已檢視的產品清單。 |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | 強烈建議 | 產品檢視已發生。 請務必設定在中檢視的產品 `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | 強烈建議 | 已接受訂單。 必須有產品清單。 |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | 選填 | 儲存產品以供日後使用。 |

{style="table-layout:auto"}

### `Commerce` 物件範例

展開以下區段，檢視使用欄位的Web SDK命令範例。 `commerce` 物件。

+++`productViews`

基本Web SDK `sendEvent` 呼叫設定 `productViews` 欄位至 `1`：

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

+++

## 此 `order` 物件 {#order-object}

此 `commerce` 物件包含用於收集訂單詳細資料的專用物件。 這稱為 `order` 物件。

本節將說明 `order` 物件。

| 欄位 | 選項 | 建議 | 說明 |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 訂單總計的貨幣。 |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | 訂單上的付款清單。 A [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) 包含下列專案。 |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | 選填 | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 此付款方式的貨幣。 |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | 強烈建議 | 以指定貨幣代碼表示的付款值。 |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | 強烈建議 | 付款型別(例如： `credit_card`， `gift_card`， `paypal`)。 檢視清單 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) 以取得詳細資訊。 |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | 選填 | 此付款交易的唯一識別碼。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | 強烈建議 | 此訂單套用所有折扣和稅金後的總計。 |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | 強烈建議 | 賣家為此購買所指派的唯一識別碼。 |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | 選填 | 購買者為此購買所指派的唯一識別碼。 |

### 排序物件範例

展開以下區段，檢視使用之Web SDK命令的範例。 `commerce` 物件。

+++`Order` 物件範例

Web SDK `sendEvent` 呼叫設定 `order` 套用至中多個產品的物件 `productListItems` 陣列：

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

+++

## 產品清單物件 {#product-list-object}

產品清單會指出哪些產品與對應動作相關。 此清單包含 [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). 每個產品都有數個選用欄位。

| 欄位 | 建議 | 說明 |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | 選填 | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 產品的貨幣。 此欄位通常僅適用於產品清單中有多個產品具有不同的貨幣代碼時。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | 強烈建議 | 僅在適用時設定此欄位。 例如，它可能無法設定在 `productView` 事件，因為不同產品變化可能有不同的價格，但 `productListAdds` 事件。 |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | 強烈建議 | 產品的XDM ID。 |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | 強烈建議 | 訪客用來將產品專案新增至清單的方法。 設定方式 `productListAdds` 測量且僅當將產品新增至清單時使用。 範例包括 `add to cart button`、`quick add`、 和 `upsell`。 |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | 強烈建議 | 產品的顯示名稱或人類看得懂的名稱。 |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | 強烈建議 | 客戶已表示所需的產品單位數。 應設定於 `productListAdds`， `productListRemoves`， `purchases`， `saveForLaters`、等等。 |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | 強烈建議 | 存放區維護單位。 這是產品的唯一識別碼。 |

### 產品清單範例

展開下列各節來檢視使用之Web SDK命令的範例。 `productListItems` 物件。

+++`productListItems` 範例

Web SDK `sendEvent` 呼叫設定 `productViews` 中多個產品的 `productListItems` 陣列：

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

+++

+++`productListAdds` 範例

Web SDK `sendEvent` 呼叫設定 `productListAdds` 中多個產品的事件 `productListItems` 陣列：

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

+++

+++`checkouts` 範例

Web SDK `sendEvent` 呼叫設定 `checkouts` 中多個產品的事件 `productListItems` 陣列：

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

+++
