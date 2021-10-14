---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai深入分析
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 使用Customer AI探索深入分析
topic-legacy: Discovering insights
description: 本檔案可做為指南，協助您在Intelligent Services Customer AI使用者介面中與服務執行個體見解互動。
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 1%

---

# 透過Customer AI探索見解

Customer AI是Intelligent Services的一部分，可讓行銷人員運用Adobe Sensei，預測客戶下一個動作的結果。 Customer AI 可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。完成此操作時無需將業務需求轉換為機器學習問題、挑選演算法、訓練或部署。

本檔案可做為指南，協助您在Intelligent Services Customer AI使用者介面中與服務執行個體見解互動。

## 快速入門

若要運用Customer AI的深入分析，您必須有可使用成功執行狀態的服務執行個體。 要建立新服務實例，請訪問[配置Customer AI實例](./configure.md)。 如果您最近建立了一個服務實例，但該實例仍在訓練和分數中，請允許24小時以完成運行。

## 服務實例概述

在[!DNL Adobe Experience Platform] UI中，按一下左側導覽中的&#x200B;**[!UICONTROL 服務]**。 出現&#x200B;*Services*&#x200B;瀏覽器，並顯示可用的Intelligent Services。 在Customer AI的容器中，按一下&#x200B;**[!UICONTROL 開啟]**。

![存取您的執行個體](../images/insights/navigate-to-service.png)

此時將顯示Customer AI服務頁面。 此頁面列出Customer AI的服務例項，並顯示其相關資訊，包括例項名稱、傾向類型、執行例項的頻率，以及上次更新的狀態。

>[!NOTE]
>
>只有已完成成功計分執行的服務執行個體才有深入分析。

![建立例項](../images/insights/dashboard.png)

選擇要開始的服務實例名稱。

![建立例項](../images/insights/click-the-name.png)

接著，該服務例項的前瞻分析頁面隨選項出現，可選擇&#x200B;**[!UICONTROL Latest scores]**&#x200B;或&#x200B;**[!UICONTROL Performance summary]**。 預設標籤&#x200B;**[!UICONTROL Latest scores]**&#x200B;提供資料的視覺效果。 本指南會詳細說明視覺效果以及您可以對資料執行哪些操作。

**[!UICONTROL 效能摘要]**&#x200B;標籤會顯示每個傾向貯體的實際流失率或轉換率。 若要深入了解，請參閱[效能摘要量度](#performance-metrics)上的區段。

![設定頁面](../images/insights/landing_page_insights.png)

### 服務實例詳細資訊

有兩種方式可檢視服務執行個體詳細資訊：從控制面板或服務例項中。

若要在控制面板中檢視服務執行個體詳細資訊的概述，請選取服務執行個體容器，以避免附加至名稱的超連結。 這會開啟右側邊欄，提供其他詳細資訊。 控制項包含下列項目：

- **[!UICONTROL 編輯]**:選擇 **** 「編輯」(Edit)可以修改現有服務實例。您可以編輯例項的名稱、說明和計分頻率。
- **[!UICONTROL 原地複製]**:選 **** 擇克隆當前選擇的服務實例設定。接著，您可以修改工作流程進行微幅調整，並重新命名為新例項。
- **[!UICONTROL 刪除]**:您可以刪除服務例項，包括任何歷史執行。
- **[!UICONTROL 資料來源]**:此例項所使用資料集的連結。
- **[!UICONTROL 執行頻率]**:打分的頻率和時間。
- **[!UICONTROL 分數定義]**:快速概述您為此執行個體設定的目標。

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>當計分執行失敗時，會提供錯誤訊息。 錯誤訊息會列在右側邊欄的&#x200B;**上次執行詳細資料**&#x200B;下方，而右側邊欄只會顯示失敗的執行。

![失敗運行消息](../images/insights/failed-run.png)

檢視服務例項其他詳細資料的第二種方式位於前瞻分析頁面內。 您可以按一下右上方的&#x200B;**[!UICONTROL 顯示更多]**&#x200B;以填入下拉式清單。 會列出詳細資訊，例如分數定義、建立時間和傾向類型。 如需列出任何屬性的詳細資訊，請造訪[設定Customer AI例項](./configure.md)。

![顯示更多](../images/insights/landing-show-more.png)

![顯示更多](../images/insights/show-more.png)

### 編輯執行個體

若要編輯執行個體，請按一下右上方導覽中的&#x200B;**[!UICONTROL Edit]** 。

![按一下「編輯」按鈕](../images/insights/edit-button.png)

此時將出現「編輯」對話框，允許您編輯實例的名稱、說明、狀態和計分頻率。 若要確認變更並關閉對話方塊，請選取右下角的&#x200B;**[!UICONTROL 儲存]**。

![編輯彈出視窗](../images/insights/edit-instance.png)

### 更多動作

**[!UICONTROL 更多操作]**&#x200B;按鈕位於&#x200B;**[!UICONTROL Edit]**&#x200B;旁的右上導航中。 按一下&#x200B;**[!UICONTROL 更多操作]**&#x200B;會開啟一個下拉式清單，讓您選取下列其中一個操作：

- **[!UICONTROL 原地複製]**:選 **** 擇克隆服務實例設定。接著，您可以修改工作流程進行微幅調整，並重新命名為新例項。
- **[!UICONTROL 刪除]**:刪除例項。
- **[!UICONTROL 存取分數]**:選取 **[!UICONTROL 存取]** 分數會開啟一個對話方塊，提供下載Customer AI [教學課程分數的](./download-scores.md) 連結，此對話方塊也提供進行API呼叫所需的資料集ID。
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

**[!UICONTROL 分數分佈]**&#x200B;卡片會根據分數提供人口的視覺摘要。 您在[!UICONTROL 分數分佈]卡片中看到的顏色代表產生的傾向分數類型。 將滑鼠暫留在任何計分分佈上，可提供屬於該分佈的確切計數。

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

在低、中、高傾向的任何貯體中選取「建立區段」按鈕，會將您重新導向至區段產生器。****

>[!NOTE]
>
>只有在資料集已啟用「即時客戶設定檔」時，**[!UICONTROL 「建立區段」按鈕才可使用。]**&#x200B;如需如何啟用即時客戶設定檔的詳細資訊，請造訪[即時客戶設定檔概述](../../../rtcdp/overview.md)。

![按一下「建立區段」](../images/insights/influential-factors-create-segment.png)

![建立區段](../images/insights/create-segment.png)

區段產生器可用來定義區段。 從「前瞻分析」頁面選取&#x200B;**[!UICONTROL 建立區段]**&#x200B;時，Customer AI會自動將選取的貯體資訊新增至區段。 若要完成區段的建立，只需填入位於區段產生器使用者介面右側邊欄的&#x200B;*名稱*&#x200B;和&#x200B;*說明*&#x200B;容器即可。 為區段指定名稱和說明後，按一下右上角的&#x200B;**[!UICONTROL Save]**。

>[!NOTE]
>
>由於傾向分數會寫入個別設定檔，因此在區段產生器中可使用，如同任何其他設定檔屬性。 當您導覽至區段產生器以建立新區段時，可以在命名空間Customer AI下看到所有的不同傾向分數。

![區段填入](../images/insights/segment-saving.png)

若要在Platform UI中檢視您的新區段，請按一下左側導覽中的&#x200B;**[!UICONTROL 區段]**。 此時將顯示&#x200B;**[!UICONTROL Browse]**&#x200B;頁面，並顯示所有可用的段。

![所有區段](../images/insights/Segments-dashboard.png)

## 效能摘要量度 {#performance-metrics}

**[!UICONTROL 效能摘要]**&#x200B;標籤會顯示實際的流失率或轉換率，並依客戶AI評分的每個傾向貯體加以區隔。

![「效能摘要」頁簽](../images/insights/summary_tab.png)

最初只顯示預期比率（虛線）。 未執行計分且資料尚未可用時，將顯示預期的比率。 但是，一旦結果窗口通過，預期比率將替換為實際比率（實線）。

將滑鼠暫留在這些行上，會顯示該貯體中該日的日期和實際/預期比率。

![貯體範例](../images/insights/churn_tab.png)

您可以篩選預計和實際顯示費率的時間範圍。 選擇&#x200B;**日曆表徵圖** ![表徵圖](../images/insights/calendar_icon.png)然後選擇新的日期範圍。 每個貯體中的結果都會更新，以在新日期範圍內顯示。

![日期選取器](../images/insights/date_selector.png)

### 個別計分執行率

**[!UICONTROL 效能摘要]**&#x200B;標籤的下半部顯示每個個別計分執行的結果。 選取右上角的下拉式日期，以顯示不同計分執行的結果。

根據您要預測的是流失率或轉換，[!UICONTROL 分數分佈]圖表會顯示已產生/轉換且未產生/未在每個增量中轉換的設定檔分佈。

![個別計分](../images/insights/scoring_tab.png)

## 後續步驟

本檔案概述了Customer AI服務例項提供的深入分析。 您現在可以繼續前往[在Customer AI](./download-scores.md)中下載分數的教學課程，或瀏覽其他提供的[Adobe智慧服務](../../home.md)指南。

## 其他資源

以下影片概述如何使用Customer AI來查看模型輸出和影響因素。

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
