---
keywords: Experience Platform；洞察力；客戶ai；熱門主題；客戶ai洞察力
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 通過客戶AI發現見解
topic-legacy: Discovering insights
description: 本文檔是與智慧服務客戶AI用戶介面中的服務實例洞察進行交互的指南。
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 1%

---

# 通過客戶AI發現見解

客戶AI作為智慧服務的一部分，為營銷人員提供了利用Adobe Sensei預測客戶下一步行動的能力。 Customer AI 可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。這無需將業務需要轉換為機器學習問題、選擇算法、培訓或部署即可完成。

本文檔是與智慧服務客戶AI用戶介面中的服務實例洞察進行交互的指南。

## 快速入門

為了利用客戶AI的洞察力，您需要有一個運行狀態成功的服務實例。 建立新服務實例訪問 [配置客戶AI實例](./configure.md)。 如果您最近建立了一個服務實例，但該實例仍在訓練和評分，請允許它24小時才能完成運行。

## 服務實例概述

在 [!DNL Adobe Experience Platform] UI，選擇 **[!UICONTROL 服務]** 的子菜單。 的 *服務* 瀏覽器出現並顯示可用的智慧服務。 在客戶AI的容器中，選擇 **[!UICONTROL 開啟]**。

![訪問實例](../images/insights/navigate-to-service.png)

此時將顯示「客戶AI服務」頁。 此頁列出客戶AI的服務實例並顯示有關這些實例的資訊，包括實例名稱、傾向類型、實例運行頻率以及上次更新的狀態。

>[!NOTE]
>
>只有成功完成計分運行的服務實例才具有洞見。

![建立實例](../images/insights/dashboard.png)

選擇要開始的服務實例名稱。

![建立實例](../images/insights/click-the-name.png)

接下來，將顯示該服務實例的透視頁面，並選擇 **[!UICONTROL 最新分數]** 或 **[!UICONTROL 效能摘要]**。 預設頁籤 **[!UICONTROL 最新分數]** 提供資料的可視化效果。 在本指南中，將更詳細地說明可視化效果以及您可以如何處理資料。

的 **[!UICONTROL 效能摘要]** 頁籤顯示每個傾向時段的實際匯率或折換率。 要瞭解更多資訊，請參閱 [效能摘要指標](#performance-metrics)。

![設定頁面](../images/insights/landing_page_insights.png)

## 服務實例詳細資訊

查看服務實例詳細資訊有兩種方法：或服務實例中。

### 服務實例儀表板

要查看儀表板中服務實例詳細資訊的概覽，請選擇一個服務實例容器，避免附加到名稱的超連結。 這會開啟一個右欄，提供更多細節。 控制項包含以下內容：

- **[!UICONTROL 編輯]**:選擇 **[!UICONTROL 編輯]** 允許您修改現有服務實例。 您可以編輯實例的名稱、說明和記分頻率。
- **[!UICONTROL 克隆]**:選擇 **[!UICONTROL 克隆]** 複製當前選定的服務實例設定。 然後，您可以修改工作流以進行小微調整，並將其更名為新實例。
- **[!UICONTROL 刪除]**:您可以刪除服務實例，包括任何歷史運行。
- **[!UICONTROL 資料源]**:此實例使用的資料集的連結。
- **[!UICONTROL 運行頻率]**:打分的頻率和時間。
- **[!UICONTROL 分數定義]**:您為此實例配置的目標的快速概述。

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>在計分運行失敗時，會提供錯誤消息。 錯誤消息列在 **上次運行詳細資訊** 在右滑軌中，該滑軌僅對失敗運行可見。

![失敗運行消息](../images/insights/failed-run.png)

### 顯示更多見解下拉清單

查看服務實例的其他詳細資訊的第二種方法位於「洞察」頁面中。 選擇 **[!UICONTROL 顯示更多]** 的下界。 詳細資訊將列出，如分數定義、建立時間、傾向類型和使用的資料集。 有關所列任何屬性的詳細資訊，請訪問 [配置客戶AI實例](./configure.md)。

![顯示更多](../images/insights/landing-show-more.png)

### 客戶AI資料集預覽跨距

如果客戶AI使用了多個資料集，則會顯示一個標有 **[!UICONTROL 多重]** 後跟括弧中的資料集數 `()` 的下界。

![多個資料集](../images/insights/insights-multi-datasets.png)

選擇多個資料集連結可開啟Customer AI資料集預覽跨距。 預覽中的每種顏色表示資料集，如資料集列左側的顏色鍵所示。 在此示例中，您只能看到 **資料集1** 包含 `PROP1` 的雙曲餘切值。

![顯示更多](../images/insights/dataset-preview.png)

### 編輯實例

要編輯實例，請選擇 **[!UICONTROL 編輯]** 的上界。

![按一下「編輯」按鈕](../images/insights/edit-button.png)

此時將出現「編輯」對話框，允許您編輯實例的名稱、說明、狀態和記分頻率。 要確認更改並關閉對話框，請選擇 **[!UICONTROL 保存]** 在右下角。

![編輯跨距](../images/insights/edit-instance.png)

### 更多操作

的 **[!UICONTROL 更多操作]** 按鈕位於右上角的導航中 **[!UICONTROL 編輯]**。 選擇 **[!UICONTROL 更多操作]** 開啟一個下拉清單，您可以選擇以下操作之一：

- **[!UICONTROL 克隆]**:選擇 **[!UICONTROL 克隆]** 複製服務實例設定。 然後，您可以修改工作流以進行小微調整，並將其更名為新實例。
- **[!UICONTROL 刪除]**:刪除實例。
- **[!UICONTROL 訪問分數]**:選擇 **[!UICONTROL 訪問分數]** 開啟提供指向 [下載客戶AI的分數](./download-scores.md) 教程，該對話框還提供進行API調用所需的資料集id。
- **[!UICONTROL 查看運行歷史記錄]**:此時將顯示一個對話框，其中包含與服務實例關聯的所有計分運行的清單。

![更多操作](../images/insights/more-actions.png)

## 評分摘要 {#scoring-summary}

記分匯總顯示得分的配置檔案總數，並將它們分類到包含高、中和低傾向的時段。 傾向時段根據得分範圍確定，低小於24，中為25-74，高大於74。 每個桶都具有與圖例對應的顏色。

>[!NOTE]
>
>如果是轉換傾向得分，則高分以綠色表示，低分以紅色表示。 如果你預測的是流失傾向，這個結果會反轉，那麼高分是紅色，低分是綠色。 無論您選擇何種傾向類型，中間時段都保持黃色。

![評分摘要](../images/insights/scoring-summary.png)

您可以將滑鼠懸停在環上的任何顏色上，以查看附加資訊，如屬於時段的配置檔案的百分比和總數。

![](../images/insights/scoring-ring.png)

## 分數分佈

的 **[!UICONTROL 分數分佈]** 卡可以根據分數來直觀地概括人口。 您在 [!UICONTROL 分數分佈] card表示生成的傾向得分類型。 懸停在任何計分分佈上提供屬於該分佈的確切計數。

![分數分佈](../images/insights/distribution-of-scores.png)

## 影響因素

對於每個記分桶，生成一張顯示該桶前10個影響因素的卡片。 這些影響因素為您提供了有關客戶為何屬於不同分數時段的附加詳細資訊。

![影響因素](../images/insights/influential-factors.png)

### 影響因素細化

徘徊在任何最主要影響因素之上，會進一步破壞資料。 您將獲得關於某些配置檔案為何屬於傾向時段的概覽。 根據因子，可以給定數字、類別或布爾值。 下面的示例按區域顯示分類值。

![細化螢幕快照](../images/insights/drilldown.png)

此外，使用追溯，如果分配系數出現在兩個或更多傾向時段中，則您可以比較它，並使用這些值建立更具體的段。 以下示例說明了第一個使用案例：

![](../images/insights/drilldown-compare.png)

您可以看到，轉換傾向低的配置檔案最近訪問adobe.com網頁的可能性較小。 &quot;自上次網路訪問以來的天數&quot;因子只有8%的覆蓋率，而中等傾向的覆蓋率為26%。 使用這些數字，您可以比較每個時段內因素的分配。 該資訊可用於推斷，在低傾向時段，網路訪問的頻率沒有中傾向時段的影響。

### 建立段

選擇 **[!UICONTROL 建立段]** 按鈕可將您重定向到段生成器。

>[!NOTE]
>
>的 **[!UICONTROL 建立段]** 按鈕僅在為資料集啟用「即時客戶配置檔案」時可用。 有關如何啟用即時客戶概要資訊的詳細資訊，請訪問 [即時客戶概要資訊概述](../../../rtcdp/overview.md)。

![按一下建立段](../images/insights/influential-factors-create-segment.png)

![建立段](../images/insights/create-segment.png)

段生成器用於定義段。 選擇 **[!UICONTROL 建立段]** 從「洞察」頁，客戶AI會自動將選定的時段資訊添加到段。 要完成段的建立，只需填寫 **名稱** 和 **說明** 容器，位於段生成器用戶介面的右滑軌中。 為段指定名稱和說明後，選擇 **[!UICONTROL 保存]** 右上角。

>[!NOTE]
>
>由於傾向分數被寫入到單個配置檔案，因此在「段」生成器中，它們與任何其他配置檔案屬性一樣可用。 當您導航到段生成器以建立新段時，您可以在命名空間「客戶AI」下看到所有不同的傾向得分。

![段填充](../images/insights/segment-saving.png)

要在平台UI中查看新段，請選擇 **[!UICONTROL 段]** 的子菜單。 的 **[!UICONTROL 瀏覽]** 頁面，並顯示所有可用段。

![所有細分](../images/insights/Segments-dashboard.png)

## 效能摘要度量 {#performance-metrics}

的 **[!UICONTROL 效能摘要]** 頁籤顯示由客戶AI劃分的每個傾向時段中分隔的實際流失率或折換率。

![「效能摘要」頁籤](../images/insights/summary_tab.png)

最初只顯示預期的比率（虛線）。 當未執行計分運行且資料不可用時，將顯示預期費率。 但是，一旦結果窗口通過，則預期費率將替換為實際費率（實線）。

懸停在行上顯示該時段中該日的日期和實際/預期費率。

![桶示例](../images/insights/churn_tab.png)

您可以篩選顯示的預期費率和實際費率的時間範圍。 選擇 **日曆表徵圖** ![表徵圖](../images/insights/calendar_icon.png)然後選擇新日期範圍。 將更新每個時段中的結果，以在新日期範圍內顯示。

![日期選擇器](../images/insights/date_selector.png)

### 個人評分運行率

下半部分 **[!UICONTROL 效能摘要]** 頁籤顯示每個計分運行的結果。 選擇右上角的下拉日期，以顯示其他計分運行的結果。

根據您是否在預測流失或轉化， [!UICONTROL 分數分佈] 圖形顯示在每個增量中更改/轉換和未更改/未轉換的配置檔案的分佈。

![個人評分](../images/insights/scoring_tab.png)

## 後續步驟

本文檔概述了客戶AI服務實例提供的見解。 現在，您可以繼續上的教程 [在客戶AI中下載分數](./download-scores.md) 或瀏覽其他 [Adobe智慧服務](../../home.md) 提供的指南。

## 其他資源

以下視頻概述了如何使用客戶AI查看模型的輸出和影響因素。

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
