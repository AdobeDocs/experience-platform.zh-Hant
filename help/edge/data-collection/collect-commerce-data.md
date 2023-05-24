---
title: 使用Adobe Experience PlatformWeb SDK收集商業和產品資訊
description: 瞭解如何使用Adobe Experience PlatformWeb SDK添加與產品或購物車相關的資料。
keywords: 產品；商業；度量；度量；訂單；放棄；簽出；productListAdds;productListOpens;productListReopens;productListViews;productViews;purces;saveForLaters;currencyCode;paymentAmount;paymentType;transactionID;price合計；purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# 收集商業和產品資訊

如果您的站點上有產品，則這是您可能希望發送的預設內容集，以便從Adobe中啟用最大功能。 雖然這是個建議，但它從一開始就提供了一套非常強大的資料。

此文檔使用 [ExperienceEvent Commerce詳細資訊](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 架構欄位組。 的 `commerce` 欄位組分為兩部分：這樣 `commerce` 對象和 `productListItems` 陣列。 的 `commerce` 對象用於指明正在對哪些操作執行 `productListItems` 陣列。

>[!TIP]
>
>如果你熟悉Adobe Analytics, `commerce` 與 `events` 變數。 的 `productListItems` 與 `products` 變數。

## 與產品相關的操作

下面是 `measures` 的 `commerce` 的雙曲餘切值。

>[!TIP]
>
>度量包含兩個欄位： `id` 和 `value`。 大多數時候，你會用 `value` 僅欄位(例如， `'value':1`)。 的 `id` 欄位允許您設定唯一標識符，您可以使用該標識符跟蹤度量的發送時間。 有關 [度量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md)。

| **度量** | **建議** | **說明** |
|---|---|---|
| [購物車放棄](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 選填 | 用戶不再可訪問或可購買購物車。 |
| [檢查](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 強烈建議 | 用戶不再瀏覽產品，但正在購買產品。 |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 強烈建議 | 產品將添加到清單。 確保在 `productListItems` 同時。 |
| [產品清單開啟](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 選填 | 將建立新的產品清單。 （例如，將建立新購物車。） |
| [productList刪除](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 強烈建議 | 從產品清單中刪除產品。 |
| [產品清單重新開啟](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 選填 | 用戶重新激活產品清單。 這通常發生在再營銷活動中。 |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 強烈建議 | 查看產品清單。 |
| [產品視圖](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 強烈建議 | 出現產品視圖。 確保在中設定查看的產品 `productListItems`。 |
| [購買](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 強烈建議 | 接受訂單。 必須有產品清單。 |
| [為Laters保存](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 選填 | 產品將保存以備將來使用。 |

下面是如何設定這些 `Measures` 的下界。

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

該商業對象還具有一個特殊欄位，用於收集稱為 `order`。

| **訂單** | **Option** | **建議** | **說明** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 訂單合計的幣種。 |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 訂單上的付款清單。 A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 包括以下內容。 |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 選填 | 的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 此付款方法的幣種。 |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 強烈建議 | 以指定的幣種代碼表示的付款值。 |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 強烈建議 | 付款類型(例如， `credit_card`。 `gift_card`。 `paypal`)。 請參閱 [已知值](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 的雙曲餘切值。 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 選填 | 此付款交易記錄的唯一ID。 |
| [價格合計](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 強烈建議 | 已應用所有折扣和稅後此訂單的合計。 |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 高度推薦 | 賣方為此採購分配的唯一標識符。 |
| [採購訂單編號](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 選填 | 購買者為此採購分配的唯一標識符。 |

下面是SDK中典型購買的示例。

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

## 產品清單

產品清單指示哪些產品與相應操作相關。 這是 [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md)。 每個產品都有許多可選欄位。

| **欄位** | **建議** | **說明** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 選填 | 的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 產品的幣種。 只有當您可以擁有具有不同幣種代碼的產品，並且該產品在應用時，此功能才有用。 例如，當存在採購或添加到購物車時。 |
| [價格合計](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 強烈建議 | 應僅在適用時設定。 例如，可能無法設定 `productView` 事件，因為不同產品的不同可能有不同的價格，但 `productListAdds` 的子菜單。 |
| [產品](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 強烈建議 | 產品的XDM ID。 |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 強烈建議 | 用於將產品項添加到訪問者清單的方法。 設定為 `productListAdds` 度量，並且僅當將產品添加到清單時才應使用。 範例包括 `add to cart button`、`quick add`、 和 `upsell`。 |
| [產品名稱](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 強烈建議 | 此值設定為產品的顯示名稱或可讀名稱。 |
| [數量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 強烈建議 | 客戶表示需要產品的單位數。 應設定為 `productListAdds`。 `productListRemoves`。 `purchases`。 `saveForLaters`等等。 |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 強烈建議 | 儲存保留單元。 它是產品的唯一標識符。 |

## 範例

`productViews` 事件

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

`productListAdds` 事件

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

`checkouts` 事件

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

`order` 事件

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
