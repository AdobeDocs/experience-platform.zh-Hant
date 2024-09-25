---
title: 檢視更多
description: 瞭解您SQL分析資料的不同檢視選項。 從您的自訂儀表板，您可以檢視分析的清單結果或下載CSV格式的已處理資料。
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: ed1565fad1c539d69b85fb644d4bc16d4a262673
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# 檢視更多資訊 {#view-more}

使用[query pro mode](./overview.md)建立[自訂分析](../sql-insights/overview.md)後，您就可以檢視不同格式的圖表資料。 您可以檢視以表格形式呈現的結果，或是以CSV檔案格式下載資料，以便在試算表中檢視。

## 清單化結果 {#tabulated-results}

對於透過SQL使用查詢專業模式編寫的每個圖表，您可以在Experience PlatformUI中檢視分析的清單結果。

從您的自訂儀表板，選取任何Widget上的省略符號(`...`)以存取[!UICONTROL 檢視更多]和[!UICONTROL 檢視SQL]選項。

![包含深入分析之省略符號下拉式功能表及[檢視更多]和[檢視SQL]選項的自訂儀表板。](../../images/sql-insights/ellipses-dropdown.png)

## 下載 CSV {#download-csv}

[!UICONTROL 檢視更多]功能會以表格形式顯示圖表的特定資料點。 若要簡化資料共用和操控的程式，您可以從此對話方塊下載CSV格式的已處理資料。 選取「**[!UICONTROL 下載CSV]**」以下載您的資料。

>[!NOTE]
>
>CSV下載僅限於前500筆記錄。

![顯示深入分析預覽的對話方塊，以及產生深入分析之SQL的表格化結果。](../../images/query-pro-mode/view-more-download-csv.png)

## 依欄排序 {#sort-column}

檢視清單化結果時，您可以使用排序功能以遞增或遞減順序依欄排序。 從您的自訂儀表板，選取任何資料表上的省略符號(`...`)以存取[!UICONTROL 檢視更多]選項。

![自訂儀表板，包含表格的省略符號下拉式功能表，且[檢視更多]選項反白顯示。](../../images/query-pro-mode/advanced-ellipses-dropdown.png)

您可以選取欄名稱旁邊的下拉式功能表，然後選取&#x200B;**[!UICONTROL 遞增排序]**&#x200B;或&#x200B;**[!UICONTROL 遞減排序]**，來排序欄。

>[!NOTE]
>
>[!UICONTROL 遞增排序]和[!UICONTROL 遞減排序]選項只會出現在已設定[排序功能](../overview.md/#advanced-attributes)的資料行。

![顯示[遞增排序]和[遞減排序]選項的資料表資料行下拉式清單。](../../images/query-pro-mode/advanced-sort-dropdown.png)

## 調整欄大小 {#resize-column}

您可以調整表格結果中的欄大小，以改善資料可讀性。 從您的自訂儀表板，選取表格的省略符號(`...`)以存取[!UICONTROL 檢視更多]選項。 使用欄名稱旁邊的下拉式功能表來調整欄大小，然後選取&#x200B;**[!UICONTROL 調整欄大小]**。

![顯示[調整資料行大小]選項的資料表資料行下拉式清單。](../../images/query-pro-mode/advanced-resize-dropdown.png)

選取滑桿，並向左或向右拖曳，以視需要調整欄大小。

![顯示反白顯示資料行調整列的資料表。](../../images/query-pro-mode/advanced-resize-column.png)

## 表格分頁 {#table-pagination}

分頁會自動套用至[!UICONTROL 檢視更多]功能的表格，讓您不必手動修改SQL查詢。 此功能可確保以更易於管理的格式呈現您的資料，方便導覽大型資料集的程式。

每頁最多可檢視500筆記錄。 若要瀏覽記錄，請使用頁面底部的&#x200B;**[!UICONTROL >]**。

![結果及分頁標示的表格結果。](../../images/query-pro-mode/advanced-table-pagination.png)

## 後續步驟

閱讀本檔案後，您現在知道如何檢視自訂圖表的SQL分析清單結果，以及將資料下載為CSV檔案。 請參閱檢視SQL檔案，瞭解如何[檢視自訂深入分析背後的SQL](./view-more.md)。

您也可以瞭解如何使用[引導式設計模式指南](../../user-defined-dashboards.md)，從Adobe Experience Platform UI中的現有資料模型產生圖表。
