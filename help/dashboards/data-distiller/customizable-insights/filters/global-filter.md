---
title: 建立全域篩選器
description: 瞭解如何使用自訂全域套用的篩選器來篩選您的資料深入分析。
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 建立全域篩選器 {#create-global-filter}

若要建立全域篩選，請先選取 **[!UICONTROL 新增篩選器]** 從您的儀表板檢視，然後 **[!UICONTROL 全域篩選器]** 下拉式選單中的。

>[!IMPORTANT]
>
>確定您將全域篩選器對應至所有圖表。 這不是自動程式。 若要使用全域篩選，您必須包含 [查詢引數](../../../../query-service/ui/parameterized-queries.md) 在圖表的SQL中， [啟用全域篩選](#enable-global-filter) 在Widget Composer中，以及 [選取執行階段值](#select-global-filter) ，以取得全域篩選對話方塊中的引數。 如需瞭解如何編輯SQL （如果需要合併查詢引數），請參閱查詢專家指南。

![自訂儀表板，其新增篩選器及其下拉式功能表已反白顯示。](../../../images/customizable-insights/add-filter.png)

您可以使用自訂的全域篩選器，快速變更SQL提供的深入分析。

此 [!UICONTROL 建立全域篩選器] 對話方塊開啟。 建立全域篩選會遵循與使用SQL建立深入分析相同的程式。 首先，選取要查詢的資料庫（見解資料模型），然後在查詢編輯器中輸入自訂SQL，最後選取執行圖示(![執行圖示。](../../../images/customizable-insights/run-icon.png))。

>[!IMPORTANT]
>
>建立全域篩選時，您必須包含ID和值。 範例值可讓您執行SQL陳述式並建立圖表。 請注意，構成陳述式時提供的範例值，會由您在執行階段為日期或全域篩選選取的實際值取代。

成功執行查詢後，「結果」索引標籤會顯示結果。 選取&#x200B;**[!UICONTROL 「下一步」]**。

![此 [!UICONTROL 建立全域篩選對話方塊] 在資料集下拉式功能表中，執行圖示和下一個會醒目提示。](../../../images/customizable-insights/global-filter.png)

全域篩選器建立工作流程的最後一步需要您為篩選器新增標籤。 將標籤新增至 **[!UICONTROL 篩選標籤]** 文字欄位，並從下拉式方塊中選取篩選型別。

>[!NOTE]
>
>僅限 [!UICONTROL 下拉式方塊] 目前支援篩選器型別選項。

最後，選取 **[!UICONTROL 選取]** 以返回您的儀表板檢視。

![此 [!UICONTROL 建立全域篩選對話方塊] 選取「 」並反白顯示「濾鏡」標籤文字輸入。](../../../images/customizable-insights/global-filter-label.png)

## 為每個深入分析啟用全域篩選器 {#enable-global-filter}

>[!TIP]
>
>在您建立的每個圖表中啟用全域篩選器。 這可確保您選擇作為全域篩選器的值會反映在所有圖表中。

為您的儀表板建立全域篩選器後，該全域篩選器的切換開關會成為Widget Composer的一部分。

![具有全域篩選器切換的Widget Composer會反白顯示。](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>確定每個分析的SQL中都包含全域篩選引數。

## 選取全域篩選器 {#select-global-filter}

若要開啟 [!UICONTROL 篩選器] 列出所有自訂篩選的對話方塊，選取篩選圖示(![篩選器圖示。](../../../images/customizable-insights/filter.png))。 接下來，若要將效果套用至您的儀表板深入分析，請從全域篩選器的下拉式選單中選擇一個選項，然後選取 **[!UICONTROL 套用]**.

![反白顯示篩選對話方塊的自訂儀表板。](../../../images/customizable-insights/custom-filters.png)
