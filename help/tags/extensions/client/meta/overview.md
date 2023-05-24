---
title: 元像素擴展概述
description: 瞭解Adobe Experience Platform的元像素標籤擴展。
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] 擴展概述

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) 是基於JavaScript的分析工具，它允許您跟蹤網站上的訪問者活動。 您跟蹤的訪問者操作（稱為轉換）將發送到 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) 可用於衡量廣告、活動、轉換渠道等的效率。

的 [!DNL Meta Pixel] 標籤擴展允許您利用 [!DNL Pixel] 功能。 本文檔介紹如何在 [規則](../../../ui/managing-resources/rules.md)。

## 先決條件

要使用副檔名，您必須具有 [!DNL Meta] 有權訪問的帳戶 [!DNL Ads Manager]。 具體來說，你必須 [新建 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) 複製 [!DNL Pixel ID] 這樣擴展就可以配置到您的帳戶。 如果您已有 [!DNL Meta Pixel]，可改用其ID。

強烈建議使用 [!DNL Meta Pixel] 與 [!DNL Meta Conversions API] 從客戶端和伺服器端分別共用和發送相同事件，因為這可能有助於恢復未由 [!DNL Meta Pixel]。 請參閱 [[!DNL Meta Conversions API] 事件轉發擴展](../../client/meta/overview.md) 有關如何將其整合到伺服器端實施中的步驟。 請注意，您的組織必須具有訪問 [事件轉發](../../../ui/event-forwarding/overview.md) 以便使用伺服器端擴展。

## 安裝擴展

安裝 [!DNL Meta Pixel] 擴展，導航到資料收集UI或Experience PlatformUI並選擇 **[!UICONTROL 標籤]** 的上界。 在此處，選擇要向其添加副檔名的屬性，或改為建立新屬性。

選擇或建立所需屬性後，選擇 **[!UICONTROL 擴展]** 在左側導航中，選擇 **[!UICONTROL 目錄]** 頁籤。 搜索 [!UICONTROL 元像素] 卡，然後選擇 **[!UICONTROL 安裝]**。

![的 [!UICONTROL 安裝] 按鈕 [!UICONTROL 元像素] 資料收集UI中的擴展。](../../../images/extensions/client/meta/install.png)

在顯示的配置視圖中，必須提供 [!DNL Pixel] 您以前複製的ID，用於將分機連結到您的帳戶。 您可以直接將ID貼上到輸入中，也可以選擇現有資料元素。

>[!TIP]
>
>使用資料元素可以動態更改 [!DNL Pixel] 使用的ID取決於其他因素，如生成環境。 請參閱附錄部分， [使用不同 [!DNL Pixel] 不同環境的ID](#id-data-element) 的子菜單。

您還可以選擇提供與擴展關聯的事件ID。 這用於消除兩者之間的相同事件 [!DNL Meta Pixel] 和 [!DNL Meta Conversions API]。 有關詳細資訊，請參閱 [事件重複消除](../../server/meta/overview.md#event-deduplication) 概述 [!DNL Conversions API] 擴展。

完成後，選擇 **[!UICONTROL 保存]**

![的 [!DNL Pixel] 作為擴展配置視圖中的資料元素提供的ID。](../../../images/extensions/client/meta/configure.png)

擴展已安裝，您現在可以在標籤規則中使用其各種操作。

## 配置標籤規則 {#rule}

[!DNL Meta Pixel] 接受一組預定義的 [標準事件](https://www.facebook.com/business/help/402791146561655)，每個都具有各自的上下文和接受的屬性。 提供的規則操作 [!DNL Pixel] 擴展與這些事件類型相關，使您能夠輕鬆地對發送到的事件進行分類和配置 [!DNL Meta] 根據類型。

為了進行演示，本節將說明如何構建將頁面視圖事件發送到的規則 [!DNL Meta]。

開始建立新標籤規則並根據需要配置其條件。 為規則選擇操作時，選擇 **[!UICONTROL 元像素]** ，然後選擇 **[!UICONTROL 發送頁面視圖]** 按鈕。

![的 [!UICONTROL 發送頁面視圖] 正在為資料收集UI中的規則選擇操作類型。](../../../images/extensions/client/meta/select-action.png)

不需要進一步配置 [!UICONTROL 發送頁面視圖] 操作。 選擇 **[!UICONTROL 保留更改]** 將操作添加到規則配置。 對規則滿意後，選擇 **[!UICONTROL 保存到庫]**。

最後，發佈新標籤 [構建](../../../ui/publishing/builds.md) 以啟用對庫的更改。

## 確認 [!DNL Meta] 正在接收資料

將更新的生成部署到您的網站後，您可以通過在瀏覽器上生成某些轉換事件並檢查這些事件是否出現在 [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180)。

## 後續步驟

本指南介紹了如何將資料發送到 [!DNL Meta] 使用 [!DNL Meta Pixel] 標籤擴展。 如果還計畫將伺服器端事件發送到 [!DNL Meta]，現在可以繼續安裝和配置 [[!DNL Conversions API] 事件轉發擴展](../../server/meta/overview.md)。

有關Experience Platform中標籤的詳細資訊，請參閱 [標籤概述](../../../home.md)。

## 附錄：使用不同 [!DNL Pixel] 不同環境的ID {#id-data-element}

如果您希望在開發或轉移環境中test實施，同時保持生產 [!DNL Meta Pixel] 分析完整，您可以使用資料元素動態選擇適當的 [!DNL Pixel] ID取決於所使用的環境。

通過使用 [!UICONTROL 自定義代碼] 資料元素(由 [[!UICONTROL 核心] 擴展](../core/overview.md))與 [`turbine` 自由變數](../../../extension-dev/turbine.md)。 在資料元素的JavaScript代碼中，使用 `turbine` 對象以查找當前環境階段，然後返回相應的 [!DNL Pixel] 基於結果的ID。

以下示例返回假生產ID `exampleProductionKey` 在生產環境中使用時，以及 `exampleTestKey` 當使用任何其他環境時。 實施此代碼時，請用實際生產和test替換每個值 [!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
