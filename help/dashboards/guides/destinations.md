---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: 目標控制面板
description: Adobe Experience Platform提供儀表板，您可以透過儀表板檢視有關組織活動目標的重要資訊。
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# （測試版）[!UICONTROL 目標]控制面板

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過此控制面板檢視有關您組織的作用中目的地的重要資訊，如每日快照中所擷取。 本指南概述如何存取和使用UI中的目標控制面板，並提供有關控制面板中顯示之度量的詳細資訊。

有關Experience Platform中所有可用目的地的概觀及目錄，請造訪[目標概觀](../../destinations/home.md)。

## [!UICONTROL 目] 標sdashboard資料  {#destinations-dashboard-data}

[!UICONTROL 目標]控制面板會顯示您組織在體驗設定檔中啟用之目標的快照。 快照中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而目的地控制面板也不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索目的地控制面板

若要導覽至平台UI中的目標控制面板，請在左側導軌中選取&#x200B;**[!UICONTROL 目標]**，然後選取&#x200B;**[!UICONTROL 概述]**&#x200B;標籤以顯示控制面板。

![](../images/destinations/dashboard-overview.png)

## 可用的Widget

Experience Platform提供多個Widget，您可使用這些Widget來視覺化與目標相關的不同量度。 選取下方介面工具集的名稱，以瞭解更多：

* [[!UICONTROL 最常用的目的地]](#most-used-destinations)
* [[!UICONTROL 最近建立的目標]](#recently-created-destinations)
* [[!UICONTROL 最近啟動的區段]](#recently-activated-segments)

### [!UICONTROL 最常用的目的地] {#most-used-destinations}

**[!UICONTROL 最常使用的目標]**&#x200B;介面工具集按映射的段數顯示您組織的頂級目標，截至最後一個快照。 此排名可讓您深入瞭解哪些目標正在被利用，同時可能還顯示哪些目標未得到充分利用。

例如，如果您昨天配置了目標，但未將任何段映射到該目標，則您將能夠看到該目標當前未充分利用。

區段計數欄中顯示的已映射區段數目，自上次每日快照起是正確的。 將新區段對應至目標時，將不會更新計數，直到建立下一個快照。

從介面工具集上顯示的清單中選擇目標名稱，將帶您訪問從&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤連結的目標詳細資訊。 您也可以選擇&#x200B;**[!UICONTROL 查看所有]**&#x200B;以導航至&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤，然後選擇目標名稱以查看其詳細資訊。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近建立的目標] {#recently-created-destinations}

**[!UICONTROL 最近建立的目標]**&#x200B;介面工具集可讓您查看組織最近配置的目標的清單。

顯示的建立日期正確到最後一個每日快照。 換言之，如果您建立新目標，則直到建立下一個快照後，新目標才會出現在清單中。

從介面工具集上顯示的清單中選擇目標名稱，將帶您進入從&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤連結的目標詳細資訊。 您也可以選擇&#x200B;**[!UICONTROL 查看所有]**&#x200B;以導航至&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤，然後選擇目標名稱以查看其詳細資訊。

若要進一步瞭解如何設定特定類型的目的地，請造訪[目的地檔案](../../destinations/home.md)。

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近啟動的區段] {#recently-activated-segments}

**[!UICONTROL 最近啟動的區段]**&#x200B;介面工具集提供最近映射至目的地的區段清單。 此清單提供系統中哪些段和目標活動使用的快照，並有助於排除任何錯誤映射。

顯示的更新日期會顯示區段上次啟動至目的地的時間，並正確至最後一個每日快照。 換言之，如果您將區段啟動至目標，則更新的日期將不會變更，直到建立下一個快照為止。

從介面工具集上顯示的清單中選取區段名稱，會帶您前往區段詳細資訊。 您也可以選擇&#x200B;**[!UICONTROL 檢視全部]**&#x200B;來導覽至區段瀏覽標籤，然後選取區段名稱以檢視其詳細資訊。

如需在Experience Platform中使用區段的詳細資訊，請先閱讀[區段服務概觀](../../segmentation/home.md)開始。

![](../images/destinations/recently-activated-segments.png)

## 後續步驟

遵循本檔案，您現在應該可以找到目標控制面板並瞭解可用Widget中顯示的量度。 若要進一步瞭解如何在Experience Platform中使用目標，請參閱[目標檔案](../../destinations/home.md)。