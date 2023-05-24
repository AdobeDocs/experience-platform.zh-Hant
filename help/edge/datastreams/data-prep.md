---
title: 資料收集的資料準備
description: 瞭解如何在為Adobe Experience PlatformWeb和移動SDK配置資料流時將資料映射到體驗資料模型(XDM)事件模式。
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# 資料收集的資料準備

資料準備是一種Adobe Experience Platform服務，它允許您將資料映射、轉換和驗證資料 [體驗資料模型(XDM)](../../xdm/home.md)。 配置啟用平台時 [資料流](./overview.md)，在將源資料發送到平台邊緣網路時，可以使用資料準備功能將其映射到XDM。

>[!NOTE]
>
>有關所有資料準備功能（包括計算欄位的轉換函式）的全面指導，請參閱以下文檔：
>
>* [資料準備概述](../../data-prep/home.md)
>* [資料準備映射函式](../../data-prep/functions.md)
>* [使用資料準備處理資料格式](../../data-prep/data-handling.md)


本指南介紹如何在UI中映射資料。 要遵循這些步驟，請啟動建立資料流至（包括） [基本配置步驟](./overview.md#create)。

有關資料收集資料準備過程的快速演示，請參閱以下視頻：

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL 選擇資料] {#select-data}

選擇 **[!UICONTROL 保存和添加映射]** 完成資料流的基本配置後， **[!UICONTROL 選擇資料]** 的上界。 在此處，您必須提供一個示例JSON對象，該對象表示您計畫發送到平台的資料的結構。

要直接從資料層捕獲屬性，JSON對象必須具有單個根屬性 `data`。 的子屬性 `data` 然後，應以映射到要捕獲的資料層屬性的方式構建對象。 選擇下面的部分，查看帶有 `data` 根。

+++示例JSON檔案，帶 `data` 根

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

要從XDM對象資料元素捕獲屬性，相同的規則適用於JSON對象，但根屬性必須被鍵控為 `xdm` 的雙曲餘切值。 選擇下面的部分，查看帶有 `xdm` 根。

+++示例JSON檔案，帶 `xdm` 根

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

您可以選擇將對象作為檔案上載的選項，或將原始對象貼上到提供的文本框中。 如果JSON有效，則在右面板中顯示預覽架構。 選取&#x200B;**[!UICONTROL 「下一步」]**&#x200B;以繼續。

![預期傳入資料的JSON示例](../assets/datastreams/data-prep/select-data.png)

## [!UICONTROL 對應]

的 **[!UICONTROL 映射]** 步驟，允許您將源資料中的欄位映射到平台中目標事件模式的欄位。 在此處，可以通過兩種方式配置映射：

* [建立新映射規則](#create-mapping) 通過手動流程來獲取。
* [導入映射規則](#import-mapping) 從現有資料流中。

### 建立新映射 {#create-mapping}

要開始，請選擇 **[!UICONTROL 添加新映射]** 的子菜單。

![添加新映射](../assets/datastreams/data-prep/add-new-mapping.png)

選擇源表徵圖(![源表徵圖](../assets/datastreams/data-prep/source-icon.png))，並在顯示的對話框中選擇要在提供的畫布中映射的源欄位。 選擇欄位後，使用 **[!UICONTROL 選擇]** 按鈕繼續。

![選擇要在源架構中映射的欄位](../assets/datastreams/data-prep/source-mapping.png)

接下來，選擇架構表徵圖(![「架構」表徵圖](../assets/datastreams/data-prep/schema-icon.png))開啟目標事件架構的類似對話框。 選擇在確認之前要將資料映射到的欄位 **[!UICONTROL 選擇]**。

![選擇目標架構中要映射的欄位](../assets/datastreams/data-prep/target-mapping.png)

此時將重新顯示映射頁，並顯示已完成的欄位映射。 的 **[!UICONTROL 映射進度]** 部分更新以反映已成功映射的欄位總數。

![已成功映射反映進度的欄位](../assets/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>如果要將對象陣列（在源欄位中）映射到不同對象陣列（在目標欄位中），請添加 `[*]` 位於源和目標欄位路徑中的陣列名稱后，如下所示。
>
>![陣列對象映射](../assets/datastreams/data-prep/array-object-mapping.png)

### 導入現有映射規則 {#import-mapping}

如果您以前建立過資料流，則可以重新使用其配置的映射規則來建立新資料流。

>[!WARNING]
>
>從另一個資料流導入映射規則將覆蓋導入之前可能添加的任何欄位映射。

要開始，請選擇 **[!UICONTROL 導入映射]**。

![顯示 [!UICONTROL 導入映射] 按鈕](../assets/datastreams/data-prep/import-mapping-button.png)

在顯示的對話框中，選擇要導入其映射規則的資料流。 選擇資料流後，選擇 **[!UICONTROL 預覽]**。

![顯示正在選擇的現有資料流的影像](../assets/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>只能在同一資料流中導入資料流 [沙坑](../../sandboxes/home.md)。 換句話說，無法將資料流從一個沙箱導入到另一個沙箱。

下一螢幕顯示所選資料流的已保存映射規則的預覽。 確保顯示的映射是您期望的，然後選擇 **[!UICONTROL 導入]** 確認映射並將其添加到新資料流。

![顯示要導入的映射規則的影像](../assets/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>如果導入的映射規則中的任何源欄位未包含在示例JSON資料中 [提前](#select-data)，這些欄位映射將不包括在導入中。

### 完成映射

繼續執行上述步驟，將其餘欄位映射到目標架構。 雖然您不必映射所有可用的源欄位，但必須映射目標架構中根據需要設定的任何欄位才能完成此步驟。 的 **[!UICONTROL 必填欄位]** counter表示當前配置中尚未映射的必填欄位數。

一旦必填欄位數達到零且您對映射感到滿意，請選擇 **[!UICONTROL 保存]** 完成更改。

![映射完成](../assets/datastreams/data-prep/mapping-complete.png)

## 後續步驟

本指南介紹了在UI中設定資料流時如何將資料映射到XDM。 如果您正在遵循常規資料流教程，則現在可以返回到上的步驟 [查看資料流詳細資訊](./overview.md)。
