---
title: 檢視更多
description: 瞭解您SQL分析資料的不同檢視選項。 從您的自訂儀表板，您可以檢視分析的清單結果或下載CSV格式的已處理資料。
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 87675263b817a2026741d6bdd094010831d6ea28
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 檢視更多 {#view-more}

使用[query pro模式](./overview.md#query-pro-mode)建立[自訂insight](./overview.md)後，您可以檢視多種格式的圖表資料。 您可以檢視結果的表格形式，或以CSV格式或透過電子郵件匯出資料。

## 清單化結果 {#tabulated-results}

對於透過SQL以查詢專業模式編寫的每個圖表，您可以在Experience Platform UI中檢視分析的清單結果。

從您的自訂儀表板，選取任何Widget上的省略符號(`...`)以存取[!UICONTROL 檢視更多]和[!UICONTROL 檢視SQL]選項。

![自訂儀表板，包含insight的省略符號下拉式功能表，以及反白顯示的[檢視更多]和[檢視SQL]選項。](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## 轉存 {#export}

從&#x200B;**[!UICONTROL 檢視更多]**&#x200B;對話方塊中，直接下載CSV檔案或傳送連結至您的電子郵件以供稍後安全下載，以匯出表格資料。

>[!IMPORTANT]
>
>若要存取匯出選項，您的管理員必須授與您匯出儀表板資料&#x200B;**[!UICONTROL 的許可權。]**&#x200B;如果[!UICONTROL 匯出]按鈕呈現灰色，請連絡您的管理員。 如需儀表板許可權的詳細資訊，請參閱[存取控制總覽](../../access-control/home.md)。

>[!NOTE]
>
>僅限視覺效果的匯出不需要[!UICONTROL 匯出儀表板資料]許可權。 例如，從PDF格式的[自訂儀表板深入分析](./export-pdf.md)或[Platform UI儀表板深入分析](../download.md)匯出已處理的資料。

### 下載 CSV {#download-csv}

在「[!UICONTROL 檢視更多]」對話方塊中，選取「**[!UICONTROL 匯出]**」，然後選擇「**[!UICONTROL 下載CSV]**」，以CSV格式下載圖表資料。

>[!NOTE]
>
>CSV下載僅限於前500筆記錄。

![顯示insight預覽和產生insight之SQL的表格化結果的對話方塊。](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

### 以電子郵件傳送 {#send-as-email}

若要匯出500筆以上的記錄，請選取&#x200B;**[!UICONTROL 匯出]**，然後從[!UICONTROL 匯出檔案]對話方塊中選擇&#x200B;**[!UICONTROL 以電子郵件傳送]**。 此選項會將下載連結安全地傳送至您與Adobe相關的電子郵件地址。 收件者的名稱與註冊的Adobe電子郵件地址會出現在對話方塊的[!UICONTROL 收件者]區段中。

![檢視更多圖表資料，並反白顯示[匯出和以電子郵件傳送]選項。](../images/sql-insights-query-pro-mode/send-as-email.png)

選取[!UICONTROL 以電子郵件傳送]後，Adobe會產生報表，並傳送電子郵件至您註冊的Adobe地址。 電子郵件內含的安全下載連結需要透過Experience Platform驗證。

>[!NOTE]
>
>您必須在產生連結後24小時內下載報表；之後，檔案就會過期。

![顯示包含下載報表選項且檔案產生成功對話方塊的Experience Platform UI。](../images/sql-insights-query-pro-mode/download-report.png)

為了保護您的資料，Adobe會安全地託管匯出的檔案，而非將其傳送為附件。 存取需要透過Experience Platform UI進行驗證，而Adobe會驗證檔案是否僅由預期的收件者下載。

此方法可讓您匯出最多&#x200B;**10,000筆記錄**，並確保安全存取敏感資料。

## 依欄排序 {#sort-column}

檢視清單化結果時，您可以使用排序功能以遞增或遞減順序依欄排序。 從您的自訂儀表板，選取任何資料表上的省略符號(`...`)以存取[!UICONTROL 檢視更多]選項。

![自訂儀表板，包含表格的省略符號下拉式功能表，且[檢視更多]選項反白顯示。](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

您可以選取欄名稱旁邊的下拉式功能表，然後選取&#x200B;**[!UICONTROL 遞增排序]**&#x200B;或&#x200B;**[!UICONTROL 遞減排序]**，來排序欄。

>[!NOTE]
>
>[!UICONTROL 遞增排序]和[!UICONTROL 遞減排序]選項只會出現在已設定[排序功能](./overview.md#advanced-attributes)的資料行。

![顯示[遞增排序]和[遞減排序]選項的資料表資料行下拉式清單。](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## 調整欄大小 {#resize-column}

您可以調整表格結果中的欄大小，以改善資料可讀性。 從您的自訂儀表板，選取表格的省略符號(`...`)以存取[!UICONTROL 檢視更多]選項。 使用欄名稱旁邊的下拉式功能表來調整欄大小，然後選取&#x200B;**[!UICONTROL 調整欄大小]**。

![顯示[調整資料行大小]選項的資料表資料行下拉式清單。](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

選取滑桿並向左或向右拖移，視需要調整欄大小。

![顯示反白顯示資料行調整列的資料表。](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## 表格分頁 {#table-pagination}

分頁會自動套用至[!UICONTROL 檢視更多]功能的表格，讓您不必手動修改SQL查詢。 此功能可確保以更易於管理的格式呈現您的資料，方便導覽大型資料集的程式。

每頁最多可檢視500筆記錄。 若要瀏覽記錄，請使用頁面底部的&#x200B;**[!UICONTROL >]**。

![結果及分頁標示的表格結果。](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## 後續步驟

閱讀本檔案後，您現在知道如何從自訂圖表的SQL分析檢視清單化結果，以及如何安全地匯出該資料。 請參閱檢視SQL檔案，瞭解如何[檢視自訂深入分析背後的SQL](./view-sql.md)。

您也可以瞭解如何使用[引導式設計模式指南](../standard-dashboards.md)，從Adobe Experience Platform UI中的現有資料模型產生圖表。
