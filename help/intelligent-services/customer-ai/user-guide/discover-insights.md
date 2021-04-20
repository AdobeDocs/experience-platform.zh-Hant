---
keywords: Experience Platform；見解；客戶智慧；熱門主題；客戶智慧
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 透過客戶人工智慧發掘見解
topic: Discovering insights
description: 本檔案可做為在智慧型服務客戶AI使用者介面中與服務例項見解互動的指南。
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
translation-type: tm+mt
source-git-commit: ff953cf0aed2b9122b78126a87625e88f1ca4506
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 1%

---

# 透過客戶人工智慧發掘見解

客戶人工智慧(Customer AI)是智慧型服務的一部分，可讓行銷人員運用Adobe Sensei來預測客戶的下一步行動。 Customer AI 可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。完成此項作業時，不需將業務需求轉換為機器學習問題、選擇演算法、訓練或部署。

本檔案可做為在智慧型服務客戶AI使用者介面中與服務例項見解互動的指南。

## 快速入門

為了利用客戶AI的見解，您需要有一個運行狀態成功的服務實例。 要建立新服務實例，請訪問[配置客戶AI實例](./configure.md)。 如果您最近建立了一個服務例項，但它仍在訓練和計分中，請允許24小時以完成執行。

## 服務實例概述

在[!DNL Adobe Experience Platform] UI中，按一下左側導覽中的&#x200B;**[!UICONTROL Services]**。 出現&#x200B;*Services*&#x200B;瀏覽器並顯示可用的智慧服務。 在客戶AI的容器中，按一下&#x200B;**[!UICONTROL Open]**。

![存取您的例項](../images/insights/navigate-to-service.png)

此時將顯示「客戶AI服務」頁。 本頁列出客戶AI的服務例項，並顯示其相關資訊，包括例項名稱、傾向類型、執行例項的頻率，以及上次更新的狀態。

>[!NOTE]
>
>只有已完成成功計分執行的服務例項才有見解。

![建立例項](../images/insights/dashboard.png)

選擇要開始的服務實例名稱。

![建立例項](../images/insights/click-the-name.png)

接著，該服務實例的前瞻分析頁面隨即顯示，並帶有選擇&#x200B;**[!UICONTROL Latest scores]**&#x200B;或&#x200B;**[!UICONTROL Performance summary]**&#x200B;的選項。 預設標籤&#x200B;**[!UICONTROL Latest scores]**&#x200B;提供資料的視覺化。 本指南將詳細說明視覺化以及您可以如何處理資料。

**[!UICONTROL Performance summary]**&#x200B;標籤顯示每個傾向時段的實際流失率或轉換率。 如需詳細資訊，請參閱[效能摘要量度](#performance-metrics)一節。

![設定頁面](../images/insights/landing_page_insights.png)

### 服務實例詳細資訊

查看服務實例詳細資訊有兩種方法：從儀表板或服務實例中。

若要在儀表板中查看服務實例詳細資訊的概述，請選擇服務實例容器，避免附加到名稱的超連結。 這會開啟右邊欄，提供其他詳細資訊。 控制項包含下列項目：

- **[!UICONTROL Edit]**:選擇 **[!UICONTROL Edit]** 允許修改現有服務實例。您可以編輯實例的名稱、說明和計分頻率。
- **[!UICONTROL Clone]**:選擇 **[!UICONTROL Clone]** 將複製當前選定的服務實例設定。然後，您可以修改工作流程，進行微調，並將其重新命名為新例項。
- **[!UICONTROL Delete]**:您可以刪除服務實例，包括任何歷史運行。
- **[!UICONTROL Data source]**:此例項所使用之資料集的連結。
- **[!UICONTROL Run Frequency]**:打分的頻率和時間。
- **[!UICONTROL Score definition]**:快速概述您為此例項設定的目標。

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>當計分執行失敗時，會提供錯誤訊息。 錯誤訊息會列在右邊欄的&#x200B;**上次執行詳細資訊**&#x200B;下，而失敗的執行則看不到。

![失敗的運行消息](../images/insights/failed-run.png)

檢視服務例項其他詳細資訊的第二個方法位於前瞻分析頁面。 您可以按一下右上角的&#x200B;**[!UICONTROL Show more]**&#x200B;來填入下拉式清單。 詳細資訊會列出，例如分數定義、建立時間和傾向類型。 有關所列任何屬性的更多資訊，請訪問[配置客戶AI實例](./configure.md)。

![顯示更多](../images/insights/landing-show-more.png)

![顯示更多](../images/insights/show-more.png)

### 編輯例項

若要編輯例項，請按一下右上方導覽中的&#x200B;**[!UICONTROL Edit]**。

![按一下「編輯」按鈕](../images/insights/edit-button.png)

此時將出現編輯對話框，允許您編輯實例的名稱、說明、狀態和計分頻率。 要確認更改並關閉對話框，請選擇右下角的&#x200B;**[!UICONTROL Save]**。

![編輯跨欄](../images/insights/edit-instance.png)

### 更多動作

**[!UICONTROL More actions]**&#x200B;按鈕位於&#x200B;**[!UICONTROL Edit]**&#x200B;旁的右上導覽中。 按一下&#x200B;**[!UICONTROL More actions]**&#x200B;開啟一個下拉菜單，允許您選擇以下操作之一：

- **[!UICONTROL Clone]**:選擇 **[!UICONTROL Clone]** 將複製設定的服務實例。然後，您可以修改工作流程，進行微調，並將其重新命名為新例項。
- **[!UICONTROL Delete]**:刪除實例。
- **[!UICONTROL Access scores]**:選取 **[!UICONTROL Access scores]** 會開啟對話方塊，提供客戶AI教 [學課程的下載](./download-scores.md) 分數連結，該對話方塊也提供進行API呼叫所需的資料集ID。
- **[!UICONTROL View run history]**:此時將顯示一個對話框，其中包含與服務實例關聯的所有計分運行的清單。

![更多動作](../images/insights/more-actions.png)

## 計分摘要{#scoring-summary}

計分摘要會顯示計分的描述檔總數，並將其分類至包含高、中和低傾向的區間。 傾向區間是根據得分範圍而決定，低於24，中度為25至74，高於74。 每個桶都有對應於圖例的顏色。

>[!NOTE]
>
>如果是轉換傾向分數，高分以綠色顯示，低分以紅色顯示。 如果您預測客戶流失傾向，這會反轉，高分會以紅色顯示，低分會是綠色。 無論您選擇何種傾向類型，中時段都會保持黃色。

![計分摘要](../images/insights/scoring-summary.png)

您可以將滑鼠指標暫留在滑鼠指環上的任何顏色上，以檢視其他資訊，例如屬於某個儲存貯體的描述檔百分比和總數。

![](../images/insights/scoring-ring.png)

## 分數分佈

**[!UICONTROL Distribution of Scores]**&#x200B;卡會根據分數提供人口的視覺化摘要。 您在[!UICONTROL Distribution of Scores]卡片中看到的顏色代表產生的傾向分數類型。 將滑鼠指標暫留在任何計分分配上，可提供屬於該分配的確切計數。

![分數分佈](../images/insights/distribution-of-scores.png)

## 影響因素

對於每個分數貯體，會產生一張卡片，顯示該貯體的前10個影響因素。 這些影響因素提供您更多有關客戶為何屬於不同分數區間的詳細資訊。

![影響因素](../images/insights/influential-factors.png)

### 影響因素細化

將滑鼠指標暫留在任何主要影響因素上，會進一步劃分資料。 您會獲得有關特定描述檔為何屬於傾向時段的概述。 根據因素，您可以得到數字、分類或布爾值。 以下範例依地區顯示類別值。

![詳細說明螢幕擷取](../images/insights/drilldown.png)

此外，使用深入分析，您可以比較在兩個或更多傾向區間中出現的分配系數，並使用這些值建立更特定的區段。 以下範例說明第一個使用案例：

![](../images/insights/drilldown-compare.png)

您可以看到，轉換傾向低的個人檔案較不可能最近造訪adobe.com網頁。 「上次網路瀏覽後間隔天數」因子的涵蓋率僅為8%，而中等傾向個人檔案的涵蓋率為26%。 使用這些數字，您可以比較每個時段內系數的分配。 這些資訊可用來推測，在低傾向時段中，網站瀏覽的時近程度沒有中等傾向時段的影響。

### 建立區段

在任何區段中，針對低、中和高傾向選取&#x200B;**[!UICONTROL Create Segment]**&#x200B;按鈕，會將您重新導向至區段產生器。

>[!NOTE]
>
>**[!UICONTROL Create Segment]**&#x200B;按鈕僅在資料集啟用即時客戶設定檔時可用。 有關如何啟用即時客戶配置檔案的詳細資訊，請訪問[即時客戶配置檔案概述](../../../rtcdp/overview.md)。

![按一下建立區段](../images/insights/influential-factors-create-segment.png)

![建立區段](../images/insights/create-segment.png)

區段產生器可用來定義區段。 從「前瞻分析」頁面選取&#x200B;**[!UICONTROL Create Segment]**&#x200B;時，客戶AI會自動將選取的區間資訊新增至區段。 若要完成區段的建立，只需填入位於區段產生器使用者介面右側導軌的&#x200B;*Name*&#x200B;和&#x200B;*Description*&#x200B;容器。 為區段指定名稱和說明後，按一下右上角的&#x200B;**[!UICONTROL Save]**。

>[!NOTE]
>
>由於傾向分數會寫入個別描述檔，因此在「區段產生器」中可使用這些分數，就像任何其他描述檔屬性一樣。 當您導覽至區段產生器以建立新區段時，可在您的命名空間「客戶人工智慧」下查看所有不同的傾向分數。

![區段填入](../images/insights/segment-saving.png)

若要在平台UI中檢視新區段，請按一下左側導覽中的&#x200B;**[!UICONTROL Segments]**。 此時會顯示&#x200B;**[!UICONTROL Browse]**&#x200B;頁面，並顯示所有可用區段。

![您的所有區段](../images/insights/Segments-dashboard.png)

## 效能摘要量度{#performance-metrics}

**[!UICONTROL Performance summary]**&#x200B;標籤會顯示實際流失率或轉換率，並分為客戶AI評分的每個傾向區間。

![「效能摘要」頁籤](../images/insights/summary_tab.png)

最初只顯示預期比率（虛線）。 當未執行計分執行且資料尚未可用時，會顯示預期比率。 但是，一旦結果窗口通過，預期費率將替換為實際費率（實線）。

將滑鼠指標暫留在行上，會顯示該時段中該日的日期和實際／預期比率。

![貯體範例](../images/insights/churn_tab.png)

您可以篩選顯示之預期和實際費率的時間範圍。 選擇&#x200B;**日曆表徵圖** ![表徵圖](../images/insights/calendar_icon.png)，然後選擇新的日期範圍。 每個時段的結果都會更新，以顯示在新的日期範圍內。

![日期選擇器](../images/insights/date_selector.png)

### 個別計分執行率

**[!UICONTROL Performance summary]**&#x200B;標籤的下半部會顯示每個個別計分執行的結果。 在右上角選取下拉式日期，以顯示不同計分執行的結果。

根據您是否預測流失或轉換，[!UICONTROL Distribution of Scores]圖表會顯示每個增量中已轉換／轉換且未轉換／轉換的描述檔分佈。

![個別計分](../images/insights/scoring_tab.png)

## 後續步驟

本檔案概述了客戶AI服務實例提供的見解。 您現在可以繼續[教學課程，下載客戶AI](./download-scores.md)中的分數，或瀏覽其他提供的[Adobe智慧服務](../../home.md)指南。

## 其他資源

以下視訊概述如何使用客戶人工智慧來檢視模型輸出及影響因素。

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
