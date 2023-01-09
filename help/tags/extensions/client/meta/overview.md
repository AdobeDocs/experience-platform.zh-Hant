---
title: 中繼像素擴充功能概觀
description: 了解Adobe Experience Platform中的Meta Pixel標籤擴充功能。
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] 擴充功能概觀

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) 是JavaScript型分析工具，可讓您追蹤網站上的訪客活動。 您追蹤的訪客動作（稱為轉換）會傳送至 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) 可用來測量廣告、行銷活動、轉換漏斗等內容的效益。

此 [!DNL Meta Pixel] 標籤擴充功能可讓您運用 [!DNL Pixel] 功能。 本檔案說明如何安裝擴充功能，並在 [規則](../../../ui/managing-resources/rules.md).

## 先決條件

若要使用擴充功能，您必須具備有效 [!DNL Meta] 有權存取的帳戶 [!DNL Ads Manager]. 具體來說，您必須 [建立新 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) 複製 [!DNL Pixel ID] 這樣擴充功能就能設定至您的帳戶。 如果您已有 [!DNL Meta Pixel]，您可以改用其ID。

強烈建議使用 [!DNL Meta Pixel] 與 [!DNL Meta Conversions API] 分別從用戶端和伺服器端共用和傳送相同事件，因為這可能有助於復原未擷取的事件 [!DNL Meta Pixel]. 請參閱 [[!DNL Meta Conversions API] 事件轉送擴充功能](../../client/meta/overview.md) 以了解如何將其整合至伺服器端實作的步驟。 請注意，您的組織必須擁有 [事件轉送](../../../ui/event-forwarding/overview.md) 以使用伺服器端擴充功能。

## 安裝擴充功能

若要安裝 [!DNL Meta Pixel] 擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後選取 **[!UICONTROL 標籤]** 從左側導覽。 從此處，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需屬性後，請選取 **[!UICONTROL 擴充功能]** 在左側導覽器中，選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL 元像素] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕 [!UICONTROL 元像素] 擴充功能。](../../../images/extensions/client/meta/install.png)

在顯示的設定檢視中，您必須提供 [!DNL Pixel] 您先前複製的ID，將擴充功能連結至您的帳戶。 您可以直接將ID貼入輸入，也可以改為選取現有資料元素。

>[!TIP]
>
>使用資料元素可讓您選擇動態變更 [!DNL Pixel] 視其他因素（例如建置環境）而使用的ID。 請參閱附錄一節 [使用不同 [!DNL Pixel] 不同環境的ID](#id-data-element) 以取得更多資訊。

您也可以選擇提供事件ID以與擴充功能建立關聯。 這可用來去除 [!DNL Meta Pixel] 和 [!DNL Meta Conversions API]. 如需詳細資訊，請參閱 [事件去重複化](../../server/meta/overview.md#event-deduplication) 在 [!DNL Conversions API] 擴充功能。

完成後，請選取 **[!UICONTROL 儲存]**

![此 [!DNL Pixel] 在擴充功能組態檢視中以資料元素形式提供的ID。](../../../images/extensions/client/meta/configure.png)

擴充功能已安裝，您現在可以在標籤規則中運用其各種動作。

## 設定標籤規則 {#rule}

[!DNL Meta Pixel] 接受一組預先定義的 [標準事件](https://www.facebook.com/business/help/402791146561655)，每個都具有其自己的內容和接受的屬性。 由提供的規則動作 [!DNL Pixel] 擴充功能可關聯至這些事件類型，讓您輕鬆分類並設定要傳送至的事件 [!DNL Meta] 根據其類型。

為了示範，本區段說明如何建立規則，將頁面檢視事件傳送至 [!DNL Meta].

開始建立新標籤規則，並視需要設定其條件。 選取規則的動作時，請選取 **[!UICONTROL 元像素]** 對於擴充功能，請選取 **[!UICONTROL 傳送頁面檢視]** （針對動作類型）。

![此 [!UICONTROL 傳送頁面檢視] 在資料收集UI中為規則選取的動作類型。](../../../images/extensions/client/meta/select-action.png)

不需要進一步設定 [!UICONTROL 傳送頁面檢視] 動作。 選擇 **[!UICONTROL 保留變更]** 將動作新增至規則設定。 對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新標籤 [建置](../../../ui/publishing/builds.md) 啟用程式庫的變更。

## 確認 [!DNL Meta] 正在接收資料

在將更新的組建部署至您的網站後，您可以在瀏覽器上產生一些轉換事件並檢查這些事件是否出現在，以確認資料是否如預期般傳送 [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## 後續步驟

本指南說明如何將資料傳送至 [!DNL Meta] 使用 [!DNL Meta Pixel] 標籤擴充功能。 如果您也打算將伺服器端事件傳送至 [!DNL Meta]，您現在可以繼續安裝及設定 [[!DNL Conversions API] 事件轉送擴充功能](../../server/meta/overview.md).

如需Experience Platform中標籤的詳細資訊，請參閱 [標籤概述](../../../home.md).

## 附錄：使用不同 [!DNL Pixel] 不同環境的ID {#id-data-element}

如果您想要在開發或測試環境中測試實作，同時保留生產環境 [!DNL Meta Pixel] analytics保持不變，您可以使用資料元素來動態選擇適當 [!DNL Pixel] ID視使用的環境而定。

您可以使用 [!UICONTROL 自訂程式碼] 資料元素(由 [[!UICONTROL 核心] 擴充功能](../core/overview.md))結合 [`turbine` 自由變數](../../../extension-dev/turbine.md). 在資料元素的JavaScript程式碼中，使用 `turbine` 對象以查找當前環境階段，然後返回適當的 [!DNL Pixel] 根據結果的ID。

下列範例會傳回假的生產ID `exampleProductionKey` 當用於生產環境時，以及不同的ID `exampleTestKey` 當使用任何其他環境時。 實作此程式碼時，請將每個值取代為您實際的生產與測試 [!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
