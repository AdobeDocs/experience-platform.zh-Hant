---
keywords: Experience Platform；用戶介面；UI；儀表板；概要檔案；段；目標；許可證使用
title: 在UI中修改平台控制面板
description: '本指南提供逐步指示，以自訂組織的Adobe Experience Platform資料在控制面板中的顯示方式。 '
topic-legacy: guide
exl-id: 75e4aea7-b521-434d-9cd5-32a00d00550d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# （測試版）修改控制面板{#modify-dashboards}

>[!IMPORTANT]
>
>儀表板功能目前處於測試階段，並非所有使用者都能使用。 文件和功能可能會有所變更。

在Adobe Experience Platform使用者介面(UI)中，您可以使用多個控制面板來檢視組織的資料並與之互動。 控制面板中顯示的預設介面工具集和量度可在個別使用者層級進行調整，以顯示偏好的資料，而且可建立介面工具集並在同一組織的使用者之間共用。

本指南提供逐步指示，以自訂平台UI中[!UICONTROL Profiles]、[!UICONTROL Segments]和[!UICONTROL Destinations]控制面板中控制面板資料的顯示方式。

>[!NOTE]
>
>無法自訂授權使用控制面板中顯示的Widget。 請參閱[授權使用資料板檔案](guides/license-usage.md)以進一步瞭解此唯一資料板。

## 快速入門

從任何控制面板（例如[!UICONTROL Profiles]控制面板）中，您可以選取&#x200B;**[!UICONTROL Modify dashboard]**，以調整現有Widget的大小並重新排序。

![](images/customization/modify-dashboard.png)

## 重新排序介面工具集

在選擇修改控制面板後，您可以選取介面工具集標題，並將介面工具集拖放至所要的順序，以重新排序介面工具集。 在此範例中，**[!UICONTROL Profiles by identity namespace]**&#x200B;介面工具集會移至最上方的列，而[!UICONTROL Profile Count]介面工具集現在會顯示在第二列。

![](images/customization/move-widget.png)

## 調整Widget大小

您也可以選取介面工具集右下角的角度符號(`⌟`)，並將介面工具集拖曳至所需的大小，以調整介面工具集的大小。 在此範例中，**[!UICONTROL Profiles by identity namespace]**&#x200B;介面工具集會調整大小以填滿整個頂端列，並自動將其他介面工具集移至第二列。 請注意，當介面工具集變大時，水準軸會如何調整以提供更詳細的增量。

>[!NOTE]
>
>隨著Widget的大小調整，周圍的Widget會動態重新定位。 這可能會導致某些Widget移至其他列，因此您必須捲動才能查看所有Widget。

![](images/customization/resize-widget.png)

## 儲存控制面板更新

移動完介面工具集並調整大小後，請選取&#x200B;**[!UICONTROL Save]**&#x200B;以儲存變更並返回主控制面板檢視。 如果您不想保留變更，請選取&#x200B;**[!UICONTROL Cancel]**&#x200B;以重設控制面板並返回主控制面板檢視。

![](images/customization/save-changes.png)

## 介面工具集程式庫

除了調整Widget的大小和重新排序外，您還可在[!UICONTROL Profiles]和[!UICONTROL Segments]控制面板中選取更多Widget，以使用&#x200B;**[!UICONTROL Widget library]**&#x200B;來顯示或建立Widget。

有關如何訪問和使用[!UICONTROL Widget library]的逐步說明，請參閱[widget庫指南](widget-library.md)。

## 後續步驟

閱讀本檔案後，您已學習如何使用修改控制面板功能來重新排序和調整Widget大小，以自訂控制面板檢視。 若要瞭解如何建立介面工具集並新增介面工具集至您的控制面板，請閱讀[介面工具集資料庫指南](widget-library.md)。
