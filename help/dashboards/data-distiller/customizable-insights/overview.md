---
title: 延伸應用程式報表的可自訂分析
description: 瞭解如何使用SQL查詢產生自訂儀表板的深入分析。
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 延伸應用程式報表的可自訂分析

使用自訂SQL查詢，從多樣的結構化資料集中有效擷取深入分析。 技術人員可以使用查詢專業模式來執行複雜的SQL分析，然後透過自訂儀表板上的圖表與非技術使用者共用此分析，或將其匯出為CSV檔案。 這種建立深入分析的方法非常適合具有明確關係的表格，並可讓您在深入分析和篩選器中更大程度的自訂，以適合利基使用案例。

>[!IMPORTANT]
>
>查詢專業模式僅適用於已購買[Data Distiller SKU](../../../query-service/data-distiller/overview.md)的使用者。

若要從SQL產生深入分析，您必須先建立儀表板。

## 建立自訂儀表板 {#create-custom-dashboard}

若要建立自訂儀表板，請從左側導覽面板選取&#x200B;**[!UICONTROL 儀表板]**&#x200B;以開啟儀表板工作區。 接著，選取&#x200B;**[!UICONTROL 建立儀表板]**。

![反白顯示[建立儀表板]的儀表板詳細目錄。](../../images/customizable-insights/create-dashboard.png)

**[!UICONTROL 建立儀表板]**&#x200B;對話方塊就會顯示。 有兩個選項可供您選擇您的儀表板建立方法。 若要建立您的深入分析，您可以使用具有[[!UICONTROL 引導式設計模式]](../../user-defined-dashboards.md)的現有資料模型，或您自己的SQL具有[!UICONTROL Query pro模式]。

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

使用現有的資料模型，其優點在於提供結構化、有效率、可擴充的架構，因應您的特定業務需求而量身打造。 若要瞭解如何[從現有資料模型](../../user-defined-dashboards.md#create-widget)建立深入分析，請參閱自訂儀表板指南。

從SQL查詢產生的深入分析提供更大的彈性和自訂性。 技術人員可以使用查詢專家模式對SQL執行複雜的分析，然後透過此儀表板功能與非技術使用者共用此分析。 選取&#x200B;**[!UICONTROL Query pro mode]**，然後選取&#x200B;**[!UICONTROL 儲存]**。

>[!NOTE]
>
>選取後，就無法在該控制面板中變更此選取專案。 相反地，您必須使用不同的儀表板建立方法來建立新的儀表板。

![以Query pro模式和[儲存]反白顯示的[!UICONTROL 建立儀表板]對話方塊。](../../images/customizable-insights/query-pro-mode.png)

## 建立圖表 {#create-a-chart}

如需使用SQL建立圖表的逐步指示，請參閱[query pro mode guide](./query-pro-mode.md)。
