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

此頁面使用XDM [Commerce結構描述](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md)欄位群組。

此欄位群組包含兩個主要部分：

* `commerce`物件。 此物件可讓您指出哪些動作發生在`productListItems`陣列上。
* `productListItems`陣列。

>[!TIP]
>
>如果您熟悉Adobe Analytics，`commerce`物件則包含與`events`變數中的商務事件類似的資料。 `productListItems`物件陣列包含與`products`變數類似的資料。

## `commerce`物件 {#commerce-object}

本節說明`commerce`物件中可用的欄位。

>[!TIP]
>
>量值有兩個欄位： `id`和`value`。 大部分時間，您只使用`value`欄位（例如，`'value':1`）。 `id`欄位可讓您設定唯一識別碼，以便在傳送量值時進行追蹤。 如需詳細資訊，請參閱[量值](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md)的XDM檔案。

| 測量 | 建議 | 說明 |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | 選填 | 使用者無法再存取或購買購物車。 |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | 強烈建議 | 使用者不再瀏覽產品，但正在購買產品。 |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | 強烈建議 | 產品會新增至清單。 請確定同時在`productListItems`中設定產品。 |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | 選填 | 新產品清單隨即建立。 例如，會建立新的購物車。 |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | 強烈建議 | 產品會從產品清單中移除。 |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | 選填 | 使用者會重新啟用產品清單。 此動作經常發生在再行銷活動中。 |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | 強烈建議 | 已檢視的產品清單。 |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | 強烈建議 | 產品檢視已發生。 請務必設定在`productListItems`中檢視的產品。 |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | 強烈建議 | 已接受訂單。 必須有產品清單。 |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | 選填 | 儲存產品以供日後使用。 |

{style="table-layout:auto"}

### `Commerce`物件範例

展開以下區段以檢視使用`commerce`物件欄位的Web SDK命令範例。

+++`productViews`

基本Web SDK `sendEvent`呼叫將`productViews`欄位設定為`1`：

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

## `order`物件 {#order-object}

`commerce`物件包含用於收集訂單詳細資料的專用物件。 這稱為`order`物件。

本節說明`order`物件支援的所有欄位。

| 欄位 | 選項 | 建議 | 說明 |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | 訂單總計的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣。 |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | 訂單上的付款清單。 [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md)包含下列專案。 |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | 選填 | 此付款方式的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣。 |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | 強烈建議 | 以指定貨幣代碼表示的付款值。 |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | 強烈建議 | 付款型別（例如，`credit_card`、`gift_card`、`paypal`）。 如需詳細資訊，請參閱[已知值](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values)的清單。 |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | 選填 | 此付款交易的唯一識別碼。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | 強烈建議 | 此訂單套用所有折扣和稅金後的總計。 |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | 強烈建議 | 賣家為此購買所指派的唯一識別碼。 |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | 選填 | 購買者為此購買所指派的唯一識別碼。 |

### 排序物件範例

展開以下區段以檢視使用`commerce`物件的Web SDK命令範例。

+++`Order`物件範例

Web SDK `sendEvent`呼叫設定套用至`productListItems`陣列中多個產品的`order`物件：

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

產品清單會指出哪些產品與對應動作相關。 它是[productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md)的清單。 每個產品都有數個選用欄位。

| 欄位 | 建議 | 說明 |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | 選填 | 產品的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣。 此欄位通常僅適用於產品清單中有多個產品具有不同的貨幣代碼時。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | 強烈建議 | 僅在適用時設定此欄位。 例如，可能無法在`productView`事件上設定，因為產品的不同變數可能會有不同的價格，但針對`productListAdds`事件。 |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | 強烈建議 | 產品的XDM ID。 |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | 強烈建議 | 訪客用來將產品專案新增至清單的方法。 設定為`productListAdds`個測量值，且僅在產品新增至清單時使用。 範例包括`add to cart button`、`quick add`和`upsell`。 |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | 強烈建議 | 產品的顯示名稱或人類看得懂的名稱。 |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | 強烈建議 | 客戶已表示所需的產品單位數。 應該設定在`productListAdds`、`productListRemoves`、`purchases`、`saveForLaters`等。 |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | 強烈建議 | 存放區維護單位。 這是產品的唯一識別碼。 |

### 產品清單範例

展開下列各節來檢視使用`productListItems`物件的Web SDK命令範例。

+++`productListItems`範例

為`productListItems`陣列中的多個產品設定`productViews`的Web SDK `sendEvent`呼叫：

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

+++`productListAdds`範例

為`productListItems`陣列中的多個產品設定`productListAdds`事件的Web SDK `sendEvent`呼叫：

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

+++`checkouts`範例

為`productListItems`陣列中的多個產品設定`checkouts`事件的Web SDK `sendEvent`呼叫：

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
