---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai深入分析
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 使用Customer AI探索深入分析
topic-legacy: Discovering insights
description: 本檔案可做為指南，協助您在Intelligent Services Customer AI使用者介面中與服務執行個體見解互動。
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: 165e5ccae5ca78b3912fef1ba0b3fd4567e231fb
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# 透過Customer AI探索見解

Customer AI是Intelligent Services的一部分，可讓行銷人員運用Adobe Sensei，預測客戶下一個動作的結果。 Customer AI 可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 完成此操作時無需將業務需求轉換為機器學習問題、挑選演算法、訓練或部署。

本檔案可做為指南，協助您在Intelligent Services Customer AI使用者介面中與服務執行個體見解互動。

## 快速入門

若要運用Customer AI的深入分析，您必須有可使用成功執行狀態的服務執行個體。 要建立新服務實例訪問 [設定Customer AI例項](./configure.md). 如果您最近建立了一個服務實例，但該實例仍在訓練和分數中，請允許24小時以完成運行。

## 服務實例概述

在 [!DNL Adobe Experience Platform] UI, select **[!UICONTROL 服務]** 的下一頁。 此 *服務* 瀏覽器隨即顯示，並顯示可用的智慧型服務。 在Customer AI的容器中，選取 **[!UICONTROL 開啟]**.

![存取您的執行個體](../images/insights/navigate-to-service.png)

此時將顯示Customer AI服務頁面。 此頁面列出Customer AI的服務例項，並顯示其相關資訊，包括例項名稱、傾向類型、執行例項的頻率，以及上次更新的狀態。

>[!NOTE]
>
>只有已完成成功計分執行的服務執行個體才有深入分析。

![建立例項](../images/insights/dashboard.png)

選擇要開始的服務實例名稱。

![建立例項](../images/insights/click-the-name.png)

接著，該服務例項的前瞻分析頁面隨即顯示，並提供可選取的選項 **[!UICONTROL 最新分數]** 或 **[!UICONTROL 效能摘要]**. 預設索引標籤 **[!UICONTROL 最新分數]** 提供資料的視覺效果。 本指南會詳細說明視覺效果以及您可以對資料執行哪些操作。

此 **[!UICONTROL 效能摘要]** 索引標籤會顯示每個傾向貯體的實際流失率或轉換率。 若要深入了解，請參閱 [績效摘要量度](#performance-metrics).

![設定頁面](../images/insights/landing_page_insights.png)

## 服務實例詳細資訊

有兩種方式可檢視服務執行個體詳細資訊：從控制面板或服務例項中。

### 服務實例儀表板

若要在控制面板中檢視服務執行個體詳細資訊的概述，請選取服務執行個體容器，以避免附加至名稱的超連結。 這會開啟右側邊欄，提供其他詳細資訊。 控制項包含下列項目：

- **[!UICONTROL 編輯]**:選取 **[!UICONTROL 編輯]** 可讓您修改現有的服務執行個體。 您可以編輯例項的名稱、說明和計分頻率。
- **[!UICONTROL 原地複製]**:選取 **[!UICONTROL 原地複製]** 複製當前選定的服務實例設定。 接著，您可以修改工作流程進行微幅調整，並重新命名為新例項。
- **[!UICONTROL 刪除]**:您可以刪除服務例項，包括任何歷史執行。
- **[!UICONTROL 資料來源]**:此例項所使用資料集的連結。
- **[!UICONTROL 執行頻率]**:打分的頻率和時間。
- **[!UICONTROL 分數定義]**:快速概述您為此執行個體設定的目標。

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>當計分執行失敗時，會提供錯誤訊息。 錯誤訊息列於 **上次運行詳細資訊** 在右側邊欄中，此欄只會顯示失敗的執行。

![失敗運行消息](../images/insights/failed-run.png)

### 顯示更多分析下拉式清單

檢視服務例項其他詳細資料的第二種方式位於前瞻分析頁面內。 選擇 **[!UICONTROL 顯示更多]** 填入下拉式清單。 會列出詳細資訊，例如分數定義、建立時、傾向類型和使用的資料集。 欲知列出的任何屬性的更多資訊，請訪問 [設定Customer AI例項](./configure.md).

![顯示更多](../images/insights/landing-show-more.png)

### Customer AI資料集預覽彈出視窗

如果Customer AI使用多個資料集，會顯示超連結，標示為 **[!UICONTROL 多個]** 後方括弧中的資料集數 `()` 中所有規則的URL區段。

![多個資料集](../images/insights/insights-multi-datasets.png)

選取多個資料集連結時，Customer AI資料集即會預覽彈出視窗。 預覽中的每種顏色代表一個資料集，如資料集欄左側的顏色索引鍵所示。 在此範例中，您只能看到 **資料集1** 包含 `PROP1` 欄。

![顯示更多](../images/insights/dataset-preview.png)

### 編輯執行個體

要編輯實例，請選擇 **[!UICONTROL 編輯]** 的下一頁。

![按一下「編輯」按鈕](../images/insights/edit-button.png)

此時將出現「編輯」對話框，允許您編輯實例的名稱、說明、狀態和計分頻率。 若要確認變更並關閉對話方塊，請選取 **[!UICONTROL 儲存]** 在右下角。

![編輯彈出視窗](../images/insights/edit-instance.png)

### 更多動作

此 **[!UICONTROL 更多動作]** 按鈕位於右上角的導覽列中 **[!UICONTROL 編輯]**. 選取 **[!UICONTROL 更多動作]** 開啟下拉式清單，供您選取下列其中一項操作：

- **[!UICONTROL 原地複製]**:選取 **[!UICONTROL 原地複製]** 複製服務實例設定。 接著，您可以修改工作流程進行微幅調整，並重新命名為新例項。
- **[!UICONTROL 刪除]**:刪除例項。
- **[!UICONTROL 存取分數]**:選取 **[!UICONTROL 存取分數]** 開啟對話方塊，提供連結至 [下載客戶AI的分數](./download-scores.md) 教學課程中，對話方塊也提供進行API呼叫所需的資料集id。
- **[!UICONTROL 查看運行歷史記錄]**:此時將顯示一個對話框，其中包含與服務實例關聯的所有計分運行的清單。

![更多動作](../images/insights/more-actions.png)

## 計分摘要 {#scoring-summary}

計分摘要會顯示計分的設定檔總數，並將其分類至包含高、中和低傾向的貯體中。 傾向貯體是根據分數範圍決定，低小於24，中小於25至74，而高大於74。 每個貯體都有對應於圖例的顏色。

>[!NOTE]
>
>如果是轉換傾向分數，高分會以綠色顯示，低分以紅色顯示。 如果您要預測流失傾向，則會反轉，高分會以紅色表示，低分會以綠色表示。 無論您選擇的傾向類型為何，中貯體都會維持黃色。

![計分摘要](../images/insights/scoring-summary.png)

您可以將滑鼠移至環上的任何顏色上，以檢視其他資訊，例如屬於貯體的設定檔百分比和總數。

![](../images/insights/scoring-ring.png)

## 分數分佈

此 **[!UICONTROL 分數分佈]** 卡片會根據分數提供母體的視覺化摘要。 您在 [!UICONTROL 分數分佈] 卡片代表產生的傾向分數類型。 將滑鼠暫留在任何計分分佈上，可提供屬於該分佈的確切計數。

![分數分佈](../images/insights/distribution-of-scores.png)

## 影響因素

系統會為每個分數貯體產生一張卡片，顯示該貯體前10個影響因素。 影響因素提供客戶為何屬於不同分數貯體的其他詳細資訊。

![影響因素](../images/insights/influential-factors.png)

### 影響因素深入分析

將滑鼠暫留在任何最重要的影響因素上，會進一步劃分資料。 系統會提供概觀，說明為何特定設定檔屬於傾向貯體。 視因素而定，您可能會獲得指定的數字、類別或布林值。 以下範例依地區顯示類別值。

![深入分析螢幕擷圖](../images/insights/drilldown.png)

此外，使用下鑽，您可以比較分佈系數（如果它發生在兩個或更多個傾向貯體中），並使用這些值建立更具體的區段。 下列範例說明第一個使用案例：

![](../images/insights/drilldown-compare.png)

您可以看到轉換傾向低的設定檔不太可能最近造訪adobe.com網頁。 「上次網站造訪間隔天數」因數的涵蓋範圍僅為8%，而中度傾向設定檔的涵蓋範圍為26%。 使用這些數字，您可以比較因子的每個貯體內的分佈。 此資訊可用來推斷網站造訪的造訪間隔在低傾向貯體中沒有中度傾向貯體中的影響。

### 建立區段

選取 **[!UICONTROL 建立區段]** 低、中、高傾向貯體中的按鈕會將您重新導向至區段產生器。

>[!NOTE]
>
>此 **[!UICONTROL 建立區段]** 按鈕僅在資料集已啟用「即時客戶設定檔」時可用。 如需如何啟用即時客戶個人檔案的詳細資訊，請造訪 [即時客戶個人檔案概觀](../../../rtcdp/overview.md).

![按一下「建立區段」](../images/insights/influential-factors-create-segment.png)

![建立區段](../images/insights/create-segment.png)

區段產生器可用來定義區段。 選取 **[!UICONTROL 建立區段]** 從「前瞻分析」頁面，Customer AI會自動將選取的貯體資訊新增至區段。 若要完成區段的建立，只需填入 **名稱** 和 **說明** 容器（位於區段產生器使用者介面的右側邊欄）。 為區段指定名稱和說明後，請選取 **[!UICONTROL 儲存]** 在右上角。

>[!NOTE]
>
>由於傾向分數會寫入個別設定檔，因此在區段產生器中可使用，如同任何其他設定檔屬性。 當您導覽至區段產生器以建立新區段時，可以在命名空間Customer AI下看到所有的不同傾向分數。

![區段填入](../images/insights/segment-saving.png)

若要在Platform UI中檢視新區段，請選取 **[!UICONTROL 區段]** 的下一頁。 此 **[!UICONTROL 瀏覽]** 頁面，並顯示所有可用的區段。

![所有區段](../images/insights/Segments-dashboard.png)

## 歷史績效 {#historical-performance}

此 **[!UICONTROL 效能摘要]** 索引標籤會顯示實際的流失率或轉換率，並分隔至「客戶AI」評分的每個傾向貯體中。

![「效能摘要」頁簽](../images/insights/summary_tab.png)

最初只顯示預期比率（虛線）。 未執行計分且資料尚未可用時，將顯示預期的比率。 但是，一旦結果窗口通過，預期比率將替換為實際比率（實線）。

將滑鼠暫留在這些行上，會顯示該貯體中該日的日期和實際/預期比率。

![貯體範例](../images/insights/churn_tab.png)

您可以篩選預計和實際顯示費率的時間範圍。 選取 **日曆圖示** ![圖示](../images/insights/calendar_icon.png)然後選取新的日期範圍。 每個貯體中的結果都會更新，以在新日期範圍內顯示。

![日期選取器](../images/insights/date_selector.png)

### 個別計分執行率

在 **[!UICONTROL 效能摘要]** 頁簽顯示每個分數運行的結果。 選取右上角的下拉式日期，以顯示不同計分執行的結果。

根據您要預測的是流失率或轉換， [!UICONTROL 分數分佈] 圖表顯示在每次增量中捨棄/轉換、不捨棄/未轉換的設定檔分佈。

![個別計分](../images/insights/scoring_tab.png)

## 模型評估 {#model-evaluation}

除了在「歷史績效」標籤上追蹤一段時間內的預測和實際結果外，行銷人員透過「模型評估」標籤在模型品質上更具透明度。 您可以使用提升度和增益圖表來判斷使用預測模型與隨機定位之間的差異。 此外，您還能決定在每個分數截止時會擷取多少正面結果。 這對於細分以及將投資報酬率與行銷行動一致非常有用。

### 提升度圖

![提升度圖](../images/user-guide/lift-chart.png)

提升度圖可測量使用預測模型（而非隨機鎖定目標）的改善。

高質量的模型指標包括：

- 前幾個十檔中的提升度值較高。 這表示模型擅長識別最有傾向採取感興趣動作的使用者。
- 遞減提升度值。 這表示分數較高的客戶比分數較低的客戶更可能採取感興趣的動作。

### 收益表

![增益圖](../images/user-guide/gains-chart.png)

累積增益圖會測量將分數鎖定在特定臨界值以上所擷取的正面結果百分比。 依傾向分數從高到低來排序客戶後，人口會分為10個大小相同的群組。 完美的模型將捕捉到最高分數十分的所有積極結果。 基線隨機定位方法會依群組大小按比例擷取正面結果，鎖定30%的使用者將擷取30%的結果。

高質量的模型指標包括：

- 累積收益迅速接近100%。
- 模型的累積增益曲線更接近圖表的左上角。
- 累積增益圖可用於判斷分段和鎖定目標的分數截斷。 例如，如果模型在前2分十中擷取到正面結果的70%，則以PercentileScore大於80的使用者為目標，預期會擷取正面結果的約70%。

### AUC（曲線下的區域）

AUC會反映依分數排名與預測目標發生之間關係的強度。 安 **AUC** 0.5表示模型並不比隨機猜測好。 安 **AUC** 1表示模型能夠完全預測出誰將採取相關行動。

## 後續步驟

本檔案概述了Customer AI服務例項提供的深入分析。 您現在可以繼續進行 [在客戶AI中下載分數](./download-scores.md) 或瀏覽其他 [AdobeIntelligent Services](../../home.md) 提供的指南。

## 其他資源

以下影片概述如何使用Customer AI來查看模型輸出和影響因素。

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
