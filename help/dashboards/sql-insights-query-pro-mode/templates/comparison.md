---
title: 客群比較
description: 瞭解如何使用「對象比較」儀表板來比較不同對象群組之間的關鍵量度。 設定對象篩選器、分析趨勢，並匯出資料導向決策的深入分析
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# 客群比較

[!UICONTROL 對象比較]儀表板會以並排檢視方式比較和比較關鍵對象量度。 您可以從此儀表板執行各種動作，以比較兩個對象群組並分析它們之間的關鍵量度。 然後，您可以針對對象細分和目標定位策略進行資料導向式決策。

## 設定對象比較 {#set-audience-comparisons}

為了提供更有意義的分析和比較，請使用系統篩選器來精準鎖定對象區段，以及您有興趣分析的時間範圍。 選取篩選圖示(![篩選圖示。](../../../images/icons/filter-icon-white.png))以選擇兩個不同的對象（[!UICONTROL 對象A]和[!UICONTROL 對象B]），並設定比較的特定引數。

![對象比較控制面板上的「篩選器」對話方塊。](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters.png)

[!UICONTROL 篩選器]對話方塊就會顯示。 若要選擇第一個要分析的對象，請選取&#x200B;**[!UICONTROL 選取對象A]**&#x200B;下拉式清單。 在此範例中，已選取`California Patients`作為對象A。套用篩選器後，此對象會顯示在比較的左側。

接著，從&#x200B;**[!UICONTROL 選取對象B]**&#x200B;下拉式清單中選擇要與[!UICONTROL 對象A]比較的第二個對象。 在此影像中，[!UICONTROL 同意使用電子郵件的使用者]已選取為[!UICONTROL 對象B]。 套用篩選器後，此對象會顯示在[!UICONTROL 對象比較]儀表板的右側。

### 調整日期範圍 {#adjust-date-ranges}

您也可以依特定時段篩選資料，以瞭解這些對象在自訂日期範圍內的表現或變更。 若要設定時間範圍以依特定期間篩選對象資料，請從日曆欄位中選取開始和結束日期。

此對話方塊也會指出已套用多少篩選器（在下方熒幕擷圖中，使用了兩個篩選器：對象A和對象B，以及今天作為日期範圍）。 若要移除所有套用的篩選器，請選取&#x200B;**[!UICONTROL 全部清除]**。

設定對象和日期範圍後，選取&#x200B;**[!UICONTROL 套用]**&#x200B;以重新整理[!UICONTROL 對象比較]儀表板。

![套用的對象比較控制面板上的「篩選器」對話方塊反白顯示。](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters-apply.png)

儀表板現在會為每個對象並排顯示比較圖表。

![對象比較儀表板，內含數個圖表比較每個對象的量度。](../../images/sql-insights-query-pro-mode/templates/audience-comparison-dashboard.png)

## 可用的受眾比較圖表 {#available-charts}

<!-- Potentially could expand this section to include images of each widget.  -->

儀表板提供數個圖表，用來比較深入分析：

- [[!UICONTROL 對象大小]](../../guides/audiences.md#audience-size)：根據每個對象包含的設定檔數目，輕鬆追蹤每個對象的大小。 此量度可協助您瞭解要比較的兩個對象的規模。
- [!UICONTROL 對象身分劃分]：圓形圖提供每個對象中身分的相對構成劃分。 您可以檢視身分總數的數量，並檢查不同的識別碼（例如電子郵件或CRM ID）對該總數的貢獻度。 此圖表可協助您根據身分型別瞭解每個對象的組成。 將滑鼠停留在圓形圖的某個區段上，即可檢視身分的確切數量。
- [[!UICONTROL 對象人數趨勢]](../../guides/audiences.md#audience-size-trend)：此圖表代表所選對象在一段時間內的人數趨勢。 使用這些圖表以視覺效果呈現每個對象在選定時段內的大小變化，高峰期和谷期表示個人檔案數量的增長或減少。
- [[!UICONTROL 對象人數變更趨勢]](../../guides/audiences.md#audience-size-change-trend)：此圖表顯示所選對象人數變更趨勢。 它可視覺化隨著時間增加或減少的受眾人數，並讓您識別受眾群體中的重大轉變或趨勢。

>[!NOTE]
>
>[!UICONTROL 對象人數趨勢]和[!UICONTROL 對象人數變化趨勢]圖表可協助您追蹤並比較兩個對象在指定期間之間的絕對人數和人數波動。 此資訊可讓您更容易瞭解影響受眾變更的模式和因素。

## 匯出深入分析 {#export-insights}

套用篩選器並分析對象後，您可以匯出資料以供進一步的離線分析或報告用途。 若要匯出您的深入分析，請選取表格右上角的&#x200B;**[!UICONTROL 匯出]**。 列印PDF對話方塊隨即顯示。 在此對話方塊中，您可以儲存為PDF或列印表格中顯示的資料。

選取&#x200B;**[!UICONTROL 範本]**&#x200B;以返回[!UICONTROL 範本]總覽。

![進階對象與反白的範本重疊檢視。](../../images/sql-insights-query-pro-mode/templates/navigation.png)

## 後續步驟

閱讀本檔案後，您已瞭解如何使用&#x200B;**對象比較**&#x200B;儀表板，比較不同對象群組之間的關鍵量度。 若要繼續改善您的對象細分和目標定位策略，請探索其他提供額外深入分析的Data Distiller範本。 請參閱[對象趨勢](./trends.md)、[對象身分重疊](./identity-overlaps.md)和[進階對象重疊](./overlaps.md)使用者介面指南，以進一步增強您的決策並最佳化參與工作。

