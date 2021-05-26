---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用
title: 修改UI中的Platform控制面板
description: '本指南提供逐步指示，自訂組織的Adobe Experience Platform資料在控制面板中的顯示方式。 '
exl-id: 75e4aea7-b521-434d-9cd5-32a00d00550d
source-git-commit: 63f855d7dd3c3591da76a23ca8d673477378c1c3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 修改控制面板{#modify-dashboards}

在Adobe Experience Platform使用者介面(UI)中，您可以使用多個控制面板來檢視及與組織的資料互動。 控制面板中顯示的預設介面工具集和量度可在個別使用者層級進行調整，以顯示偏好的資料，且介面工具集可在相同組織中的使用者間建立和共用。

本指南提供逐步指示，自訂Platform UI中[!UICONTROL Profiles]、[!UICONTROL Segments]和[!UICONTROL Destinations]控制面板中控制面板資料顯示方式。

>[!NOTE]
>
>無法自訂授權使用控制面板中顯示的介面工具集。 請參閱[授權使用控制面板檔案](guides/license-usage.md)以深入了解此唯一的控制面板。

## 快速入門

從任何控制面板（例如[!UICONTROL Profiles]控制面板），可以選擇&#x200B;**[!UICONTROL Modify dashboard]**&#x200B;以調整現有小部件的大小並重新排序。

![](images/customization/modify-dashboard.png)

## 重新排序小部件

選擇修改控制面板後，您可以通過選擇介面工具集標題，並將介面工具集拖放到所需順序來重新排序介面工具集。 在此範例中，**[!UICONTROL 描述檔計數趨勢]**&#x200B;介面工具集會移至最上方列，而[!UICONTROL 描述檔計數]介面工具集現在會顯示在第二列。

![](images/customization/move-widget.png)

## 調整小工具的大小

您也可以通過在介面工具集的右下角選取角度符號(`⌟`)，並將介面工具集拖動到所需大小來調整介面工具集的大小。 在此示例中，**[!UICONTROL 按標識]**&#x200B;配置檔案小部件調整大小以填充整個頂行，自動將其他小部件移動到第二行。 請注意，水準軸會如何調整，以隨著介面工具集變大提供更詳細的增量。

>[!NOTE]
>
>隨著小工具的大小調整，周圍小工具會動態重新定位。 這可能會導致某些小工具被移動到其他行，需要您滾動才能查看所有小工具。

![](images/customization/resize-widget.png)

## 儲存控制面板更新

完成移動和調整小部件大小後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改並返回到主儀表板視圖。 如果您不想保留變更，請選取&#x200B;**[!UICONTROL 取消]**&#x200B;以重設控制面板並返回主控制面板檢視。

![](images/customization/save-changes.png)

## 介面工具集程式庫

除了調整小工具的大小和重新排列小工具外，在[!UICONTROL Profiles]、[!UICONTROL Segments]和[!UICONTROL Destinations]控制面板中選擇&#x200B;**[!UICONTROL Modify dashboard]**，您還可以訪問&#x200B;**[!UICONTROL Widget庫]**，在其中可以找到更多小工具來顯示或為組織建立自定義小工具。

有關如何訪問和使用[!UICONTROL Widget庫]的逐步說明，請參閱[widget庫指南](widget-library.md)。

![](images/customization/widget-library.png)

## 後續步驟

閱讀本檔案後，您學習了如何使用修改控制面板功能來重新排序小工具並調整其大小，以自訂控制面板檢視。 若要了解如何建立介面工具集並將其新增至控制面板，請參閱[介面工具集程式庫指南](widget-library.md)。
