---
title: 資料收集的資料準備
description: 了解如何為Adobe Experience Platform Web和Mobile SDK設定資料流時，將資料對應至Experience Data Model(XDM)事件結構。
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# 資料收集的資料準備

資料準備是一項Adobe Experience Platform服務，可讓您將資料對應、轉換及驗證資料，以及從資料到資料 [Experience Data Model(XDM)](../../xdm/home.md). 設定已啟用平台時 [資料流](./overview.md)，您可以在將來源資料傳送至Platform Edge Network時，使用資料準備功能將其對應至XDM。

>[!NOTE]
>
>有關所有資料準備功能的全面指導，包括計算欄位的轉換函式，請參閱以下文檔：
>
>* [資料準備概述](../../data-prep/home.md)
>* [資料準備映射函式](../../data-prep/functions.md)
>* [使用資料準備處理資料格式](../../data-prep/data-handling.md)


本指南說明如何在UI中對應資料。 若要遵循這些步驟，請開始建立資料流的程式，直到（並包括） [基本配置步驟](./overview.md#create).

有關資料收集資料準備過程的快速演示，請參閱以下視頻：

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL 選擇資料] {#select-data}

選擇 **[!UICONTROL 儲存並新增對應]** 完成資料流的基本設定後， **[!UICONTROL 選擇資料]** 步驟。 您必須在此提供範例JSON物件，該物件代表您打算傳送至Platform的資料結構。

若要直接從資料層擷取屬性，JSON物件必須具有單一根屬性 `data`. 的子屬性 `data` 然後，物件的建構方式應對應至您要擷取的資料層屬性。 選取下方的區段，檢視格式正確的JSON物件範例，並搭配 `data` 根。

+++範例JSON檔案，包含 `data` 根

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

若要從XDM物件資料元素中擷取屬性，相同的規則會套用至JSON物件，但根屬性必須輸入為 `xdm` 。 選取下方的區段，檢視格式正確的JSON物件範例，並搭配 `xdm` 根。

+++範例JSON檔案，包含 `xdm` 根

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

您可以選取以檔案形式上傳物件的選項，或將原始物件貼到提供的文字方塊中。 如果JSON有效，右側面板中會顯示預覽結構。 選擇 **[!UICONTROL 下一個]** 繼續。

![預期傳入資料的JSON範例](../assets/datastreams/data-prep/select-data.png)

## [!UICONTROL 對應]

此 **[!UICONTROL 對應]** 步驟，可讓您將來源資料中的欄位對應至Platform中目標事件結構的欄位。 從這裡，您可以透過兩種方式來設定對應：

* [建立新的對應規則](#create-mapping) 以透過手動程式處理此資料流。
* [導入映射規則](#import-mapping) 來自現有資料流。

### 建立新對應 {#create-mapping}

若要開始，請選取 **[!UICONTROL 新增對應]** 建立新映射行。

![新增對應](../assets/datastreams/data-prep/add-new-mapping.png)

選擇源表徵圖(![源表徵圖](../assets/datastreams/data-prep/source-icon.png))，並在出現的對話方塊中，選取您要在提供的畫布中對應的來源欄位。 選取欄位後，請使用 **[!UICONTROL 選擇]** 按鈕繼續。

![選擇要在源架構中映射的欄位](../assets/datastreams/data-prep/source-mapping.png)

接下來，選取結構圖示(![結構圖示](../assets/datastreams/data-prep/schema-icon.png))，以開啟target事件架構的類似對話方塊。 在確認前，選擇您要將資料對應至的欄位 **[!UICONTROL 選擇]**.

![選取要在目標架構中對應的欄位](../assets/datastreams/data-prep/target-mapping.png)

重新顯示映射頁，並顯示已完成的欄位映射。 此 **[!UICONTROL 映射進度]** 區段更新，以反映已成功映射的欄位總數。

![欄位已成功映射並反映進度](../assets/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>如果要將對象陣列（在源欄位中）映射到不同對象的陣列（在目標欄位中），請添加 `[*]` 位於來源和目的地欄位路徑中的陣列名稱后面，如下所示。
>
>![陣列物件對應](../assets/datastreams/data-prep/array-object-mapping.png)

### 導入現有映射規則 {#import-mapping}

如果您先前已建立資料流，則可以對新資料流重新使用其配置的映射規則。

>[!WARNING]
>
>從其他資料流匯入對應規則將會覆寫您在匯入之前可能新增的任何欄位對應。

若要開始，請選取 **[!UICONTROL 導入映射]**.

![顯示 [!UICONTROL 導入映射] 按鈕](../assets/datastreams/data-prep/import-mapping-button.png)

在顯示的對話方塊中，選取您要匯入其對應規則的資料流。 選擇資料流後，選擇 **[!UICONTROL 預覽]**.

![顯示所選現有資料流的影像](../assets/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>資料流只能匯入相同 [沙箱](../../sandboxes/home.md). 換言之，您無法將資料流從一個沙箱匯入到另一個沙箱。

下一個畫面會顯示所選資料流儲存的對應規則預覽。 請確定顯示的對應符合您的期望，然後選取 **[!UICONTROL 匯入]** 確認對應並新增至新資料流。

![顯示要匯入之對應規則的影像](../assets/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>如果匯入對應規則中的任何來源欄位未包含在您的範例JSON資料中 [提前提供](#select-data)，這些欄位對應將不會包含在匯入中。

### 完成對應

請繼續執行上述步驟，將其餘欄位對應至目標結構。 雖然您不需要映射所有可用的源欄位，但目標架構中設定為必需的任何欄位必須映射，才能完成此步驟。 此 **[!UICONTROL 必填欄位]** 計數器表示目前設定中尚未對應的必要欄位數。

當必填欄位計數達到零且您對對應感到滿意時，請選取 **[!UICONTROL 儲存]** 完成變更。

![映射完成](../assets/datastreams/data-prep/mapping-complete.png)

## 後續步驟

本指南說明在UI中設定資料流時，如何將資料對應至XDM。 如果您遵循一般資料流教學課程，現在可以返回 [查看資料流詳細資訊](./overview.md).
