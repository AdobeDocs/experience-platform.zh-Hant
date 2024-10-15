---
title: Query Pro模式鑽研
description: 瞭解如何從任何圖表導覽至新儀表板，以使用鑽研來探索您的資料。
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 鑽研 {#drill-through}

鑽研可讓您輕鬆地從任何圖表導覽至新儀表板，以利進行多層資料分析。 此功能可讓您在研究趨勢、客戶行為、營運指標等時，輕鬆從高階概覽轉換為深入報告，確保您一律具備所需的情境。

系統會自動將全域篩選器和日期範圍篩選器從來源儀表板傳至目標儀表板，確保您開始的分析在整個鑽研體驗中順暢地持續進行。 為便於在研究的不同層級之間導覽，系統允許多層級鑽研。

## 建立鑽研 {#create-drill-through}

若要建立鑽研，請先從您的儀表板檢視中選取&#x200B;**[!UICONTROL 編輯]**。

![醒目提示編輯的自訂儀表板。](../images/sql-insights-query-pro-mode/drill-through.png)

在圖表中選取您要鑽研的省略符號，然後選取&#x200B;**[!UICONTROL 編輯]**。

![顯示「編輯」反白顯示省略符號選單的圖表。](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

在[!UICONTROL 屬性]面板中，使用切換來啟用&#x200B;**[!UICONTROL 啟用鑽研]**，然後使用下拉式清單來選取&#x200B;**[!UICONTROL 目標儀表板]**。 確定已啟用&#x200B;**[!UICONTROL 篩選通過]**&#x200B;的切換，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。

![啟用鑽研、目標儀表板和篩選通過的圖表屬性面板反白顯示。](../images/sql-insights-query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>針對目標圖示板重複上述步驟，以設定多層次鑽研。

## 檢視鑽研 {#view-drill-through}

若要檢視鑽研，請從您的儀表板檢視中選取圖表中的省略符號，然後選取&#x200B;**[!UICONTROL 鑽研]**。

![圖表顯示省略符號選單，並反白顯示[鑽研]。](../images/sql-insights-query-pro-mode/drill-through-chart-view.png)

顯示鑽研目標儀表板。 如果您有多層鑽研，可以重複此步驟。

![以鑽研反白顯示的目標儀表板。](../images/sql-insights-query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>套用至來源控制面板的任何篩選器都會傳遞至目標控制面板。 但是，會在子控制面板上停用日期篩選器和全域篩選。

## 移除鑽研 {#remove-drill-through}

若要移除鑽研，請先從您的儀表板檢視中選取&#x200B;**[!UICONTROL 編輯]**。

![醒目提示編輯的自訂儀表板。](../images/sql-insights-query-pro-mode/drill-through.png)

在圖表中選取您要移除鑽研的省略符號，然後選取&#x200B;**[!UICONTROL 編輯]**。

![顯示「編輯」反白顯示省略符號選單的圖表。](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

在[!UICONTROL 屬性]面板中，選取切換以停用&#x200B;**[!UICONTROL 啟用鑽研]**，然後選取&#x200B;**[!UICONTROL 儲存並關閉]**。

![圖表屬性面板已停用[!UICONTROL 啟用鑽研]的切換功能並反白顯示。](../images/sql-insights-query-pro-mode/drill-through-disable.png)

## 後續步驟

閱讀本檔案後，您現在知道如何為儀表板建立鑽研。 您也可以瞭解如何使用[引導式設計模式指南](../standard-dashboards.md)，從Adobe Experience Platform UI中的現有資料模型產生圖表。
