---
title: 產品
seo-title: 使用Adobe Experience Platform Web SDK的支援產品
description: 瞭解如何使用Experience Platform Web SDK新增產品或購物車的資料
seo-description: 瞭解如何使用Experience Platform Web SDK新增產品或購物車的資料
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 5%

---


# 產品

如果您的網站上有產品，則這是您可能想要傳送的預設項目集，以啟用Adobe的最多功能。 雖然這是一個建議，但它從一開始就提供了一組非常強大的資料。

本檔案使用「 [ExperienceEvent商務詳細資訊](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 」混合。 混 `commerce` 合蛋白分為兩部分： 對象 `commerce` 和數 `productListItems` 組。 該對 `commerce` 像可讓您指示陣列正在執行哪些 `productListItems` 操作。

>[!Tip]
>如果您熟悉Adobe Analytics，則與 `commerce` 變數最密切相 `events` 關。 變數 `productListItems` 與變數的關聯性更 `products` 密切。

## 與產品相關的動作

以下是物件中 `measures` 可用的清 `commerce` 單。

>[!Tip]
>度量包含兩個欄位： `id` 和 `value`。 大部分時候，您只會使 `value` 用欄位(例如 `'value':1`)。 此 `id` 欄位可讓您設定唯一識別碼，用來追蹤測量的傳送時間。 請參閱XDM測量文 [件](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md)。

| **測量** | **建議** | **說明** |
|---|---|---|
| [cartAndons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 可選 | 使用者無法再存取或購買購物車。 |
| [結帳](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 強烈建議 | 使用者不再瀏覽產品，而是正在購買產品。 |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 強烈建議 | 產品會新增至清單。 請務必同時設定 `productListItems` 產品。 |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 可選 | 會建立新的產品清單。 （例如，會建立新的購物車。） |
| [productListRemoves](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 強烈建議 | 產品會從產品清單中移除。 |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 可選 | 產品清單會由使用者重新啟動。 這在再行銷促銷活動中通常會發生。 |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 強烈建議 | 會檢視產品清單。 |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 強烈建議 | 發生產品檢視。 請務必在中設定已檢視的產品 `productListItems`。 |
| [購買](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 強烈建議 | 接受訂單。 必須有產品清單。 |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 可選 | 產品會儲存以供日後使用。 |

以下是如何在SDK中設定這些 `Measures` 項目的範例。

```javascript
alloy("event", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

商務物件也有一個特殊欄位，用於收集名為的訂單詳細資訊 `order`。

| **訂單** | **選項** | **建議** | **說明** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 訂 [單合計的](https://en.wikipedia.org/wiki/ISO_4217) ISO 4217貨幣。 |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 訂單的付款清單。 paymentItem [包含](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 下列項目。 |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 可選 | 此付 [款方法的ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 貨幣。 |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 強烈建議 | 以指定貨幣代碼表示的付款值。 |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 強烈建議 | 付款類型(例如， `credit_card`、 `gift_card`、 `paypal`)。 如需詳細資訊，請 [參閱已知值](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 清單。 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 可選 | 此付款交易的唯一ID。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 強烈建議 | 在套用所有折扣和稅後，此訂單的總計。 |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 高度推薦 | 賣方為此購買指派的唯一識別碼。 |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 可選 | 購買者為此購買指派的唯一識別碼。 |

以下是SDK中典型購買的範例。

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```

## 產品清單

產品清單會指出哪些產品與對應的動作相關。 它是productListItems的 [清單](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md)。 每個產品都有許多可選欄位。

| **欄位** | **建議** | **說明** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 可選 | 產 [品的ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 貨幣。 只有當您可以擁有不同貨幣代碼的產品，以及產品套用時，才有用。 例如，當有購買或新增至購物車時。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 強烈建議 | 只應在適用時設定。 例如，可能無法設定，因為 `productView` 不同產品的不同版本可能有不同的價格，但是價格 `productListAdds`。 |
| [產品](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 強烈建議 | 產品的XDM ID。 |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 強烈建議 | 訪客用來新增產品項目至清單的方法。 使用度 `productListAdds` 量設定，且僅應在產品新增至清單時使用。 例如 `add to cart button`、 `quick add`和 `upsell`。 |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 強烈建議 | 這會設為產品的顯示名稱或人類可讀名稱。 |
| [數量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 強烈建議 | 客戶表示他們需要產品的件數。 應設定在 `productListAdds`、 `productListRemoves`、 `purchases`、 `saveForLaters`等上。 |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 強烈建議 | 存放單元。 它是產品的唯一識別碼。 |

## 範例

`productView` 事件

```javascript
alloy("event",{
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

`productView` 事件

```javascript
alloy("event",{
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

`checkout` 事件

```javascript
alloy("event",{
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

`purchase` 事件

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```
