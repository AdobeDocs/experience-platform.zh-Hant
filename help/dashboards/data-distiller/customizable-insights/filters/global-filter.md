---
title: 建立全域篩選器
description: 瞭解如何使用自訂全域套用的篩選器來篩選您的資料深入分析。
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 建立全域篩選器 {#create-global-filter}

若要建立全域篩選器，請先從您的儀表板檢視中選取&#x200B;**[!UICONTROL 新增篩選器]**，然後從下拉式選單中選取&#x200B;**[!UICONTROL 全域篩選器]**。

>[!IMPORTANT]
>
>確定您將全域篩選器對應至所有圖表。 這不是自動程式。 若要使用全域篩選，您必須在圖表的SQL中加入[查詢引數](../../../../query-service/ui/parameterized-queries.md)、在Widget撰寫器中啟用全域篩選](#enable-global-filter)，以及在全域篩選對話方塊中為引數選取執行階段值](#select-global-filter)。 [[如需瞭解如何編輯SQL （如果需要合併查詢引數），請參閱查詢專家指南。

![自訂儀表板，其新增篩選器及其下拉式功能表已反白顯示。](../../../images/customizable-insights/add-filter.png)

您可以使用自訂的全域篩選器，快速變更SQL提供的深入分析。

[!UICONTROL 建立全域篩選器]對話方塊開啟。 建立全域篩選會遵循與使用SQL建立深入分析相同的程式。 首先，選取要查詢的資料庫（見解資料模型），然後在查詢編輯器中輸入自訂SQL，最後選取執行圖示（![執行圖示。](/help/images/icons/play.png)）。

>[!IMPORTANT]
>
>建立全域篩選時，您必須包含ID和值。 範例值可讓您執行SQL陳述式並建立圖表。 請注意，構成陳述式時提供的範例值，會由您在執行階段為日期或全域篩選選取的實際值取代。

成功執行查詢後，「結果」索引標籤會顯示結果。 選取&#x200B;**[!UICONTROL 下一步]**。

![此[!UICONTROL 建立全域篩選對話方塊]包含資料集下拉式功能表、執行圖示和「下一步」反白顯示。](../../../images/customizable-insights/global-filter.png)

全域篩選器建立工作流程的最後一步需要您為篩選器新增標籤。 將標籤新增至&#x200B;**[!UICONTROL 篩選標籤]**&#x200B;文字欄位，並從下拉式方塊中選取篩選型別。

>[!NOTE]
>
>目前僅支援[!UICONTROL 組合方塊]篩選型別選項。

最後，選取&#x200B;**[!UICONTROL 選取]**&#x200B;以返回您的儀表板檢視。

![ [!UICONTROL 建立全域篩選對話方塊]，其中的Select和篩選標籤文字輸入反白顯示。](../../../images/customizable-insights/global-filter-label.png)

## 為每個深入分析啟用全域篩選器 {#enable-global-filter}

>[!TIP]
>
>在您建立的每個圖表中啟用全域篩選器。 這可確保您選擇作為全域篩選器的值會反映在所有圖表中。

為您的儀表板建立全域篩選器後，該全域篩選器的切換開關會成為Widget Composer的一部分。

![具有全域篩選器切換的Widget Composer已反白顯示。](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>確定每個分析的SQL中都包含全域篩選引數。

## 選取全域篩選器 {#select-global-filter}

若要開啟列出所有自訂篩選器的[!UICONTROL 篩選器]對話方塊，請選取篩選器圖示（![篩選器圖示）。](/help/images/icons/filter.png))。 接下來，若要套用您的儀表板深入分析上的效果，請從全域篩選器的下拉式選單中選擇一個選項，然後選取&#x200B;**[!UICONTROL 套用]**。

![反白顯示篩選對話方塊的自訂儀表板。](../../../images/customizable-insights/custom-filters.png)
