---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: 在歸因AI中發現見解
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: 0ea96de956adb5a6c5286433a547772118c43aee
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---


# 在歸因AI中發現見解

歸因AI服務例項可提供深入資訊，可協助您制定和衡量與行銷績效及投資報酬相關的行銷決策。 選擇服務例項可提供視覺化和篩選，協助您瞭解客戶歷程每個階段中每個客戶互動的影響。

本檔案可做為在Adobe Intelligent Services使用者介面中與服務例項深入資訊互動的指南。

## 快速入門

為了運用Attribution AI的見解，您需要有成功執行狀態的服務例項。 若要建立新的服務例項，請造訪 [Attribution AI使用者介面指南](./user-guide.md)。 如果您最近建立了一個服務例項，但它仍在訓練和計分中，請允許24小時以完成執行。

## 服務實例見解總覽

在UI中 [!DNL Adobe Experience Platform] ，按一下左 **側導覽** 中的「服務」。 「服 *務* 」瀏覽器隨即出現，並顯示可用的Adobe Intelligent Services。 在「歸因AI」的容器中，按一下「 **開啟**」。

![存取您的例項](./images/insights/open_Attribution_ai.png)

此時會顯示「歸因AI」服務頁面。 本頁列出Attribution AI的服務例項，並顯示其相關資訊，包括例項名稱、轉換事件、執行例項的頻率，以及上次更新的狀態。 按一下服務實例名稱開始。

>[!NOTE] 只能選擇已完成成功計分運行的服務實例。

![建立例項](./images/insights/select-service-instance.png)

接著，該服務例項的前瞻分析頁面隨即出現，您會在此處獲得視覺化資訊和許多篩選條件，以與資料互動。 本指南將詳細說明視覺化和濾鏡。

![設定頁面](./images/insights/landing-page.png)

### 服務實例詳細資訊

要查看服務實例的其他詳細資訊，請單 **擊右上角** 的「顯示更多」。

![顯示更多](./images/insights/show-more.png)

此時將顯示詳細清單。 如需所列任何屬性的詳細資訊，請造訪 [Attribution AI使用指南](./user-guide.md)。

![顯示詳細資訊](./images/insights/advanced-details.png)

### 編輯例項

若要編輯例項，請按一 *下右上方導覽* 中的「編輯」。
![按一下「編輯」按鈕](./images/insights/edit-button.png)

此時將出現編輯對話框，允許您編輯實例的說明和計分頻率。 若要確認變更並關閉對話方塊，請按一 *下右下* 角的「編輯」。

![編輯跨欄](./images/insights/edit-popover.png)

### 更多動作 {#more-actions}

「更 *多動作* 」按鈕位於「編輯」旁的右上導 *覽中*。 按一 **下「更多動作** 」會開啟下拉式清單，供您選取下列其中一個作業：

- **刪除**: 刪除實例。
- **下載摘要資料**: 下載包含摘要資料的CSV檔案。
- **存取分數**: 按一 *下「存取分數* 」會將您重新導向至 [「歸因AI」教學課程的存取分數](./download-scores.md)。
- **檢視執行記錄**: 此時會出現一個快顯視窗，其中包含與服務例項相關聯的所有計分執行的清單。

![更多動作](./images/insights/more-actions.png)

## 篩選資料

歸因AI見解可讓您篩選資料，並根據選取的篩選條件自動更新UI視覺效果。

>[!NOTE] 依預設，除了 ** Attribution模型篩選器設為「增量和受影響的歸因轉換」外，每個篩選器都會設為「全部」。

### 轉換事件

當您在Attribution AI中建立新例項時，其中一個必填欄位是「轉換事件」。 轉換事件是可識別行銷活動（例如電子商務訂單、店內採購和網站造訪）影響的業務目標。

在例項中，「轉 *換事件* 」下拉式清單可讓您選取為例項定義的任何事件，以篩選資料。 選取特定事件會變更UI視覺化，僅填入屬於這些事件的轉換。

![轉換事件](./images/insights/conversion-event.png)

### 歸因模型

按一 *下「歸因模型* 」會開啟下拉式清單，其中包含所有可用的不同歸因模型。 您可以選取多個模型來比較結果。 如需不同歸因模型及其運作方式的詳細資訊，請造訪 [Attribution AI](./overview.md) overview，其中包含一個表格，其中包含各模型的相關資訊。

![歸因模型](./images/insights/attribution-model.png)

### 產品

「產 *品* 」(Product)篩選器允許您從建立實例時最初吸收的任何產品中進行選擇。 按一下下拉式清單，然後使用搜尋功能快速選取您要比較的所有產品。

![產品篩選](./images/insights/product-filter.png)

### 地理位置

「地 *理位置* 」篩選器會根據地區模型填入國家代碼。 根據您的資料，此篩選器可能存在或不存在。

>[!NOTE] 國家／地區代碼有兩個字元長。 如需完整清單，請 [參閱ISO 3166-1 alpha-2](https://datahub.io/core/country-list)。

### 地區

>[!NOTE] 只有當您在建立服務例項時，在「歸因AI使用者介 [面指南」中執行選用步驟](./user-guide.md#region-based-modeling-optional) 、以地區為基礎的模型時，才會出現此篩選。

此篩選器允許您選擇在實例建立過程中設定的任何區域。

### Player Name

按一下 *渠道篩選* ，會顯示包含所有可用行銷渠道的下拉式清單。 您可以選取多個渠道來比較。

![Player Name](./images/insights/channel.png)

### 日期範圍

按一下日曆圖示以開啟日期範圍快顯視窗。 開始和結束轉換事件日期會決定在UI中填入的資料量。 您可以選擇縮小或擴大日期範圍，以集中或擴展填入的資料量。

![日期範圍](./images/insights/display-date-range.png)

## 資料概觀

「概 *述」卡* ，依歸因模型顯示您的轉換總數。 總數會根據您使用本檔案先前概述的篩選器進行搜尋的特定程度而改變。 選取更多模型會將其他社交圈新增至「概述」，每個社交圈都有對應於圖例的色彩。

![概述](./images/insights/Overview.png)

## 每週趨勢

「每 *周趨勢* 」卡會依您在篩選程式中設定的日期範圍來劃分轉換總數。

![趨勢](./images/insights/weekly-trends.png)

按一下「每週趨勢」卡右上角的省略號 *會顯示下拉式清單* ，讓您選取每日、每週或每月趨勢。

將滑鼠指標暫留在特定歸因模型的資料行上，會建立一個跨距，顯示該日期的轉換總數。

![暫留趨勢](./images/insights/weekly-trend-hover.png)

## 依頻道劃分

「依 *頻道劃分* 」卡可用來決定與每個頻道相關的轉換總數。 此資訊卡可協助您決定每個通道的成效和投資報酬率。

![劃分渠道](./images/insights/channel-breakdown.png)

按一下「依頻道劃分」資訊卡右上角的省略號 ** ，會開啟下拉式清單，讓您根據觸點填入資料。

![觸點](./images/insights/breakdown-by-touchpoints.png)

## 熱門促銷活動

「熱 *門促銷活動* 」卡片會顯示促銷活動的概述，以及促銷活動在每個通道中的執行情形。 此資訊卡可協助您的團隊瞭解特定通路的特定促銷活動成效，並提供進一步投資的深入資訊。

![熱門促銷活動](./images/insights/top-campaigns.png)

## 後續步驟

在您篩選完資料並能夠顯示適當資訊後，就可以選擇存取分數。 如需如何存取分數的深入指南，請造訪Attribution AI教 [學課程中的存取分數](./download-scores.md) 。 此外，您也可以下載摘要資料，如更多動作 [所示](#more-actions)。 選擇「下載摘要資料」會下載依日期匯總的摘要資料。

## 其他資源

以下視訊旨在協助學習如何使用「歸因AI」見解頁面來瞭解行銷通道和宣傳的投資報酬率。

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)