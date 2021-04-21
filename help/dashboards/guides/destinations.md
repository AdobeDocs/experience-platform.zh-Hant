---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；用戶介面；UI；自定義；配置檔案儀表板；儀表板
title: 目標控制面板
description: Adobe Experience Platform提供儀表板，您可以透過儀表板查看有關組織活動目標的重要資訊。
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# （測試版）[!UICONTROL Destinations]控制面板

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform用戶介面(UI)提供一個儀表板，通過該儀表板可以查看有關組織活動目標的重要資訊（在每日快照中捕獲）。 本指南概述如何存取和使用UI中的目標控制面板，並提供有關控制面板中顯示之度量的詳細資訊。

有關目標的概述以及Experience Platform內所有可用目標的目錄，請訪問[目標概述](../../destinations/home.md)。

## [!UICONTROL Destinations] 控制面板資料  {#destinations-dashboard-data}

[!UICONTROL Destinations]控制面板會顯示您組織在「體驗設定檔」中啟用之目標的快照。 快照中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而目的地控制面板也不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索目的地控制面板

若要導覽至平台UI中的目標控制面板，請在左側導軌中選取&#x200B;**[!UICONTROL Destinations]**，然後選取&#x200B;**[!UICONTROL Overview]**&#x200B;標籤以顯示控制面板。

![](../images/destinations/dashboard-overview.png)

## 可用的Widget

Experience Platform提供多個Widget，您可使用這些Widget來視覺化與目標相關的不同量度。 選取下方介面工具集的名稱，以瞭解更多：

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

**[!UICONTROL Most used destinations]**&#x200B;介面工具集會依映射的區段數顯示您組織的最上層目標，直到最後一個快照為止。 此排名可讓您深入瞭解哪些目標正在被利用，同時可能還顯示哪些目標未得到充分利用。

例如，如果您昨天配置了目標，但未將任何段映射到該目標，則您將能夠看到該目標當前未充分利用。

區段計數欄中顯示的已映射區段數目，自上次每日快照起是正確的。 將新區段對應至目標時，將不會更新計數，直到建立下一個快照。

從介面工具集上顯示的清單中選擇目標名稱，將帶您進入從&#x200B;**[!UICONTROL Browse]**&#x200B;頁籤連結的目標詳細資訊。 您也可以選擇&#x200B;**[!UICONTROL View All]**&#x200B;以導覽至&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，然後選擇目標名稱以檢視其詳細資訊。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

**[!UICONTROL Recently created destinations]**&#x200B;介面工具集可讓您查看組織最近配置的目標清單。

顯示的建立日期正確到最後一個每日快照。 換言之，如果您建立新目標，則直到建立下一個快照後，新目標才會出現在清單中。

從介面工具集上顯示的清單中選擇目標名稱，將帶您進入從&#x200B;**[!UICONTROL Browse]**&#x200B;頁籤連結的目標詳細資訊。 您也可以選擇&#x200B;**[!UICONTROL View All]**&#x200B;以導覽至&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，然後選擇目標名稱以檢視其詳細資訊。

若要進一步瞭解如何設定特定類型的目的地，請造訪[目的地檔案](../../destinations/home.md)。

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

**[!UICONTROL Recently activated segments]**&#x200B;介面工具集提供最近映射至目標的區段清單。 此清單提供系統中哪些段和目標活動使用的快照，並有助於排除任何錯誤映射。

顯示的更新日期會顯示區段上次啟動至目的地的時間，並正確至最後一個每日快照。 換言之，如果您將區段啟動至目標，則更新的日期將不會變更，直到建立下一個快照為止。

從介面工具集上顯示的清單中選取區段名稱，會帶您前往區段詳細資訊。 您也可以選取&#x200B;**[!UICONTROL View All]**&#x200B;來導覽至區段瀏覽標籤，然後選取區段名稱以檢視其詳細資訊。

有關在Experience Platform中使用區段的詳細資訊，請先閱讀[區段服務概觀](../../segmentation/home.md)。

![](../images/destinations/recently-activated-segments.png)

## 後續步驟

遵循本檔案，您現在應該可以找到目標控制面板並瞭解可用Widget中顯示的量度。 要瞭解有關在Experience Platform中使用目標的更多資訊，請參閱[目標文檔](../../destinations/home.md)。
