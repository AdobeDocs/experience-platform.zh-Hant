---
title: Adobe Analytics Product String擴充功能概述
description: 瞭解Adobe Experience Platform中的Adobe Analytics Product String標籤擴充功能。
exl-id: a49feb4e-f166-41d2-9f85-639f6ff8bb8f
source-git-commit: 36ca1e63c043baa776f27b627cdbe493b2ced674
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 85%

---

# Adobe Analytics Product String擴充功能概述

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

`products` 變數會追蹤使用者在您的網站上與產品的互動情形。例如，`products` 變數可追蹤某項產品被檢視、新增至購物車、結帳和購買的次數。此外也可追蹤您的網站上各種商品銷售類別的相對成效。

`products` 變數一律應與成功事件一起設定。

[!DNL Adobe Analytics Product String Builder] 擴充功能會透過循環資料層、擷取所有必要的產品資料，並以下列正確語法格式化，自動為您設定 `products` 變數。您不必再自行撰寫及維護自訂 JavaScript，即可執行這些複雜動作。

## 產品變數語法

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

如需完整文件，請造訪[產品](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=zh-Hant)。

## 擴充功能說明

### 動作設定

將「Adobe Analytics Product String - 設定 s.products」動作新增至規則。

![動作設定](./images/screenshot-action-config.png)

### 設定標準產品資料

接著，定義您的資料層變數。依照上一步所述設定動作後，系統會顯示下列畫面：

![標準欄位](./images/screenshot-standard-fields.png)

依照您要在產品字串中加入的每個資料點，輸入適當資料層變數的路徑。

例如，如果您的資料層結構如下：

```json
digitalData = {
  "transaction": {
    "item": [{
      "productInfo": {
        "productName": "My Product"
      }
    }]
  }
};
```

您可在「產品 ID/名稱的變數」欄位中輸入以下路徑，以擷取 `productName` 變數：

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>如果您使用資料元素來填寫欄位，應使用「常數」或「自訂程式碼」資料元素類型來設定欄位，且必須將上方路徑以字串文字的形式傳回。

### 價格類型

[!DNL Adobe Analytics] 產品字串中的「`price`」參數必須反映該產品購買件數的總價，而非單價。在擴充功能的動作中啟用「價格」欄位時，您必須指定資料層要顯示總價或單價。若使用單價，[!DNL Adobe Analytics Product String] 擴充功能會自動將單價乘以數量得出總價，並正確設定產品字串。

![價格類型](./images/screenshot-price-type.png)

### 自訂事件與銷售 eVar

![事件與 eVar](./images/screenshot-events-evars.png)

如果實作時要使用自訂事件或銷售 eVar，請按照下列步驟操作：

1. 選取相關的&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕。
1. 在下拉式清單中選擇您需設定的事件或 eVar。
1. 使用上方所述語法，輸入適當資料層變數的路徑。

### 動作順序

此動作必須搭配「Adobe Analytics - 設定變數」動作和「Adobe Analytics - 傳送信標」動作，以設定相對應的成功事件。以下說明正確的動作順序。

![標準欄位](./images/screenshot-action-type.png)

### 需求

* 變數的物件[資料層](https://theblog.adobe.com/data-layers-buzzword-best-practice/)需具有適用於所有產品相關資料 (例如產品 ID、數量、價格)。此擴充功能不適用於陣列資料層。
* 需先安裝 [Adobe Analytics](../analytics/overview.md) 擴充功能。
